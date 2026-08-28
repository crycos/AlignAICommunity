# AI Inventory Workbook — Technical Reference Guide

*Aligned to NIST AI RMF 1.0 | Govern - Map - Measure - Manage*

## **Purpose of This Document**

This document is the complete technical and operational reference for the **AI Inventory & Risk Assessment Workbook**, the workbook the Company uses to intake, classify, risk-assess, approve, and monitor artificial intelligence (AI) tools and use cases under its AI governance program. It is written for engineers, workbook maintainers, and governance staff who need to understand — precisely — what every sheet does, how every calculated column is derived, and why the logic was designed the way it was.

The workbook operationalizes the **NIST AI Risk Management Framework (AI RMF) 1.0**, structuring the intake and review process around the four NIST functions: **Govern, Map, Measure, and Manage**. Each AI system that the Company evaluates is carried through the same seven-sheet lifecycle, from initial classification to ongoing monitoring, and every calculated field in the workbook is a live formula — not a manual entry — so that risk ratings stay consistent and auditable as new tools are added.

This document covers, in order:

- The end-to-end workbook architecture and data flow between sheets (Section 2).

- How to use the workbook day-to-day (Section 3).

- The governance roles involved in reviewing and approving AI tools, and how they work together (Section 4).

- A plain-language purpose statement for every sheet in the workbook (Section 5).

- A complete, cell-level explanation of every formula in the workbook, organized sheet by sheet (Section 6).

- A deep-dive on the three most complex, iteratively refined risk-rating formulas in the workbook — Legal & Compliance, Data & Privacy, and the Validated Risk Tier / AI Capability floor logic — including the full set of test scenarios used to validate each one (Section 7).

- Known gaps, deliberate design decisions, and open items still pending a decision (Section 8).

Company-identifying references have been generalized in this document (e.g., "the Company") so that it can be shared, templated, or version-controlled without exposing internal naming.



## **Workbook Architecture and Data Flow**

The workbook is built as a **layered pipeline**, not a flat collection of independent tabs. Data flows in one direction — from static reference tables, through intake, through parallel domain reviews, into a single reconciliation sheet, and out to workflow, monitoring, and executive reporting. Every sheet from AI Inventory onward is keyed to the same **AI ID**, which is what lets every downstream `INDEX`/`MATCH` lookup find the right row automatically. The diagram below shows every sheet, grouped into its architectural layer, with arrows indicating the direction data actually flows (source → destination).



### **Text-Based Version of the Architecture Diagram**

The same six layers and data-flow shown in the diagram above, reproduced in plain text so it can be pasted directly into a markdown file, ticket, or chat message without the image:

```
LAYER 1 - REFERENCE & LOOKUP (static, rarely edited) 
========================================================== 
  [ Profiles ]   [ Profile Selection ]   [ Reference Lists ] 
========================================================== 
                        | 
                        | INDEX/MATCH lookups (Profile defaults, 
                        | dropdown values, Low->Mod->High->Critical order) 
                        v 
========================================================== 
LAYER 2 - INTAKE (system of record) 
========================================================== 
                 [ AI Inventory ] 
   - Assigns AI ID (the key every other sheet is built on) 
   - Calculates Inherent Risk Tier from Data Classification + PII/IP flags 
   - Pulls Profile defaults: Risk Tier, Oversight model, Approval 
     Authority, Review Frequency 
========================================================== 
                        | 
                        | same AI ID feeds all 4 domain sheets in parallel 
        ----------------+----------------+---------------- 
        |               |                |               | 
        v               v                v               v 
========================================================== 
LAYER 3 - DOMAIN REVIEWS (four parallel, independent gates) 
========================================================== 
 [ Risk & Harm ]  [ Data & Privacy ] [ Vendor &   ] [ Legal &      ] 
 [ Assessment  ]  [                ] [ Security   ] [ Compliance   ] 
 - no sequencing dependency between any of the four - 
========================================================== 
        |               |                |               | 
        ----------------+----------------+---------------- 
                        | 
                        | each rating looked up independently 
                        v 
========================================================== 
LAYER 4 - RECONCILE (single convergence point) 
========================================================== 
                [ Risk Assessment ] 
   - Escalates Inherent Risk -> Validated Risk Tier 
     (harm-based + AI Capability floor/escalation rules) 
   - Overall Risk Rating = MAX(Validated Risk Tier, 3 domain ratings) 
   - Risk Drivers field names which input actually drove the result 
========================================================== 
                |                              | 
                v                              v 
========================================================================== 
LAYER 5 - WORKFLOW & MONITORING (both branch off Risk Assessment 
                                  AND AI Inventory directly) 
========================================================================== 
 [ Approval Workflow ]                    [ Monitoring ] 
 - mirrors each domain sheet's           - pulls Profile review 
   approval status directly              frequency from AI Inventory 
 - checks AI Inventory's base Risk       to set reassessment cadence 
   Tier to decide if ITGC sign-off 
   is required 
========================================================================== 
                |                              | 
                --------------+----------------- 
                              v 
========================================================== 
LAYER 6 - EXECUTIVE ROLLUP (read-only, never writes back) 
========================================================== 
                   [ Dashboard ] 
   Live counts/distributions pulled from: 
   AI Inventory + Risk Assessment + Risk & Harm Assessment 
```


### **The Six Architectural Layers**

|  |  |  |
| --- | --- | --- |
| **Layer** | **Sheets** | **Role** |
| 1. Reference & Lookup (static) | Profiles, Profile Selection, Reference Lists | Curated, rarely-edited answer keys. Nothing here is calculated; everything else in the workbook reads from these three sheets via INDEX/MATCH. |
| 1. Intake (system of record) | AI Inventory | The only sheet where a new AI system is actually created. Calculates the base Inherent Risk Tier from data classification and PII/IP flags, and looks up Profile defaults. |
| 1. Domain Reviews (parallel gates) | Risk & Harm Assessment, Data & Privacy, Vendor & Security, Legal & Compliance | Four independent, manually-scored review sheets that run in parallel, each owned by a different function, each producing its own rating or rollup. |
| 1. Reconcile | Risk Assessment | The single point where all four domain outputs and the Inherent Risk are combined into one Validated Risk Tier and one Overall Risk Rating. |
| 1. Workflow & Monitoring | Approval Workflow, Monitoring | Operationalizes the reconciled risk rating: routes approvals across the four gates and schedules ongoing reassessment. |
| 1. Executive Rollup | Dashboard | Aggregates counts and distributions from every layer below it into a single leadership-facing view. |

### **How Data Actually Moves Through the Pipeline**

1. **Reference sheets feed AI Inventory.** When a reviewer assigns a Profile on AI Inventory, that single entry pulls the Profile’s Default Risk Tier, Human Oversight model, Approval Authority, and Review Frequency in from the Profiles sheet — the Profile Selection sheet’s ordered rules determine which Profile gets assigned in the first place, and Reference Lists supplies every dropdown and the Low→Moderate→High→Critical ordering used throughout.

1. **AI Inventory feeds all four domain review sheets.** Every row on Risk & Harm Assessment, Data & Privacy, Vendor & Security, and Legal & Compliance is keyed to the same AI ID from AI Inventory, so a reviewer working any one of those sheets is always scoring the same tool the others are scoring — just from a different angle (harm, privacy, security, legal).

1. **The four domain sheets feed Risk Assessment independently and in parallel.** There is no sequencing dependency between Data & Privacy, Vendor & Security, and Legal & Compliance — each can be completed in any order, or simultaneously by different reviewers, because Risk Assessment simply looks up whatever each one currently shows.

1. **Risk Assessment is the only place where those four inputs converge.** It escalates AI Inventory’s Inherent Risk into a Validated Risk Tier using the harm- and capability-based rules (Section 7.3), then takes the MAX of that Validated Risk Tier with the three domain ratings to produce the Overall Risk Rating — and names which input is actually driving that result.

1. **Approval Workflow and Monitoring both branch off Risk Assessment and AI Inventory**, not off each other. Approval Workflow mirrors each domain sheet’s approval status directly (not through Risk Assessment) and separately checks AI Inventory’s base Risk Tier to decide if ITGC sign-off is required. Monitoring pulls the Profile’s review frequency from AI Inventory to set the reassessment cadence.

1. **Dashboard sits at the very end of the pipeline** and only reads — it never writes back into any other sheet. Every count, distribution, and breakdown on it is a live formula against AI Inventory, Risk Assessment, or Risk & Harm Assessment, so it always reflects the current state of the other six layers without needing to be refreshed manually.

### **Why This Architecture Matters**

- **Separation of duties is structural, not just procedural.** Because Data & Privacy, Vendor & Security, and Legal & Compliance are physically separate sheets owned by separate functions, no single reviewer can complete another gate’s review — the workbook’s layout enforces the same segregation the Company’s governance model requires (see Section 4).

- **One reconciliation point avoids conflicting "final" answers.** Because every domain rating flows into a single Risk Assessment sheet rather than each domain sheet declaring its own overall verdict, there is exactly one Overall Risk Rating per tool, with a Risk Drivers field that always explains which input produced it.

- **The pipeline is a source of truth, not a source of duplication.** Because Approval Workflow, Monitoring, and Dashboard all pull rather than re-enter data, a status change made once on a domain sheet (e.g., Legal Review moving from Pending to Approved) automatically propagates to every downstream sheet without a reviewer needing to update anything else.

- **New tools inherit the full pipeline for free.** Adding a new AI ID to AI Inventory and copying formula rows down through the six other calculated sheets is sufficient to bring a new tool through the entire architecture — there is no separate configuration step required per layer.

## **How to Use The Workbook**

The workbook is designed so that **only a small number of cells are ever typed in by a person** — everything else recalculates automatically. Follow this sequence whenever a new AI tool needs to be reviewed, or when an existing tool changes:

**Step 1 — Add the tool to AI Inventory**

1. Open the **AI Inventory** sheet and add a new row directly beneath the last AI system (the next sequential AI ID, e.g. AI-008).

1. Fill in the manually entered fields: Provider, AI System Name, Purpose, Scope, AI Capability, Data Processed, Original Approved Data Classification, Data Classification, Requested By, Reviewed By, Approved Date, Approval Status, and Notes.

1. Assign a **Profile** using the **Profile Selection** sheet's ordered rules (see Section 5.4) — apply the rules top to bottom and stop at the first match.

1. Once a Profile is entered, Risk Tier, Human Oversight, Profile Approval Authority, and Profile Review Frequency all populate automatically by lookup from the **Profiles** sheet.

**Step 2 — Score risk and harm**

1. On the **Risk & Harm Assessment** sheet, answer Yes/No/N/A for each of the 13 risk categories and 6 harm types for the new AI ID. This is the only sheet where these judgments are entered manually.

1. The sheet automatically rolls up the applicable categories, applicable harms, and their counts, which then feed the **Risk Assessment** sheet's Validated Risk Tier calculation.

**Step 3 — Complete the three domain reviews**

1. **Data & Privacy** — Privacy answers the data-related questions (data sources, classification breakdown, PII/Employee/Customer/Financial/Legal/IP flags, vendor sharing, residency, retention, logging, DPA status).

1. **Vendor & Security** — IT Security completes the security posture questions (SOC 2, ISO 27001, pen testing, MFA, RBAC, encryption, logging, SIEM, prompt-injection testing).

1. **Legal & Compliance** — Legal completes the AI-specific governance questions (IP ownership of output, training data rights, liability for errors/hallucination, right to audit, data-use restriction, termination/deletion rights, regulatory exposure).

Each of these three sheets calculates its own **domain risk rating** (Privacy Risk Rating, Vendor Risk Rating, Legal Risk Rating) automatically from the Yes/No/N/A/To Confirm answers — see Section 7 for the exact logic and validated test scenarios for each.

**Step 4 — Let the Risk Assessment sheet reconcile everything**

The **Risk Assessment** sheet automatically pulls the Inherent Risk from AI Inventory, escalates it into a **Validated Risk Tier** using the harm/capability floor logic, and then computes the **Overall Risk Rating** as the maximum of the Validated Risk Tier, Vendor Risk Rating, Privacy Risk Rating, and Legal Risk Rating. It also tells you, in plain text, which domain is driving the final rating (e.g., "Legal (High)").

**Step 5 — Route for approval**

The **Approval Workflow** sheet automatically mirrors the Business Approval, IT Security Approval (via Vendor & Security), Privacy Approval (via Data & Privacy), and Legal Approval (via Legal & Compliance) statuses, determines whether ITGC sign-off is required (Yes whenever the base Risk Tier is High or Critical), and shows the Profile Approval Authority for reference. See Section 4 for how these roles relate to each other.

**Step 6 — Set up monitoring**

The **Monitoring** sheet calculates the Next Reassessment date (12 months after Last Reassessment) and the effective review cadence (the more frequent of a fixed annual cadence and the Profile's own review frequency), and flags whether a reassessment is Current, Overdue, or Not Scheduled.

**Step 7 — Re-run Profile Selection if the use changes**

If the business use case, data scope, or capability of an already-approved tool changes materially, re-run the Profile Selection rules — this is the designated Step 7 reassessment trigger, and it may change the Profile, the default risk tier, and the required approval authority.

**Adding new rows — keeping formulas consistent**

Every calculated column in every sheet uses row-relative formulas (e.g., row 5 in Risk & Harm Assessment feeds row 5 of Risk Assessment, and so on). When a new AI ID row is inserted:

- Copy an existing formula row (not a blank row) so the formulas, conditional formatting, and dropdown data validations all copy across together.

- Dropdown-menu (data validation) cells do not always carry over with a simple copy in every spreadsheet client — if a pasted cell loses its dropdown, reapply Data Validation from a working cell in the same column, or re-select it from the Reference Lists sheet.

- After adding a row, spot-check the new row's Overall Risk Rating and Approval Workflow row against the Reference Lists and Profiles sheets to confirm the lookups resolved (an unresolved lookup usually shows a blank or an error rather than a wrong value).



## **Governance Roles and How They Work Together**

AI tool review at the Company is a **cross-functional** process. No single function can approve a tool on its own — the workbook is deliberately structured so that Business, IT Security, Privacy, and Legal each own a separate review gate, and ITGC (and, where established, the AI Governance Committee) acts as the escalation and final-authority layer for higher-risk systems. This separation of duties is what the Approval Workflow, Data & Privacy, Vendor & Security, and Legal & Compliance sheets exist to enforce.

### **Business Owner / Requestor**

The Business Owner (also recorded as "Requestor") is the person or function that wants to use the AI tool. They:

- Initiate intake by describing the tool's purpose, scope, and intended users in **AI Inventory**.

- Own the first approval gate — **Business Approval** in the Approval Workflow sheet.

- Are recorded as the **Risk Owner** on every row of the Risk Assessment sheet, meaning they carry accountability for the residual risk once a tool is approved and in use.

- Participate in Profile Approval Authority for lower-risk profiles (e.g., Profile 2 "Evaluation and Proof of Concept" and Profile 3 "Domain and Technical Assistant" both name "IT Security and Business Owner" as the joint approval authority).

### **IT Security**

IT Security owns the technical security posture review and is the most broadly involved reviewer in the workflow. They:

- Complete the **Vendor & Security** sheet — SOC 2/ISO 27001/pen-test evidence, MFA, RBAC, encryption at rest and in transit, audit logging, SIEM integration, and prompt-injection testing — which drives the **Vendor Risk Rating**.

- Own the second approval gate — **IT Security Approval** — which is populated directly from the Vendor & Security review outcome.

- Serve as the sole or joint Profile Approval Authority for the majority of profiles (e.g., Profile 2, 3, 12, 13, 15, 17), and jointly with ITGC or Legal/Privacy on higher-risk profiles.

- Are named jointly with AI Governance on nearly every open Executive Action Item on the Dashboard sheet — including completing owner/approval evidence, validating agentic controls, and validating assigned Profiles.

### **Privacy**

Privacy owns the data-protection review and is a **separate gate from Legal**, even though both sit within Legal & Compliance functions organizationally. Privacy:

- Completes the **Data & Privacy** sheet — data classification, PII/Employee/Customer/Financial/Legal/IP data flags, vendor data sharing, residency, retention, and logging — which drives the **Privacy Risk Rating**.

- Owns the **Privacy Approval** gate in the Approval Workflow sheet, tracked independently of Legal Approval.

- Is named as a required reviewer on higher-sensitivity profiles, such as Profile 7 (People and HR Decision Support), Profile 16 (Meeting Transcription and Summarization), and Profile 20 (Identity Cloning & Impersonation).

### **Legal & Compliance**

Legal owns the contractual and regulatory review and is likewise tracked as its **own gate**, separate from Privacy. Legal:

- Completes the **Legal & Compliance** sheet — IP ownership of AI output, training data rights, liability for errors/hallucination, right to audit AI decisions, data-use restriction for model training, termination/deletion rights on exit, and regulatory exposure (GDPR/NIS2/sector-specific) — which drives the **Legal Risk Rating**.

- Owns the **Legal Approval** gate in the Approval Workflow sheet.

- Is a required reviewer on external-facing or contract-driven profiles, such as Profile 6 (Customer or Supplier Facing), Profile 10 (Legal and Contract Analysis), Profile 19 (Synthetic Media Generation), and Profile 20.

### **ITGC (IT General Controls)**

ITGC is the governance-control layer that sits above the four domain reviews. Its role is defined by the Approval Workflow sheet's **ITGC Required** column, which is automatically set to **Yes** whenever a tool's base Risk Tier (from AI Inventory) is **High or Critical** — meaning ITGC involvement is triggered by risk level, not by choice. ITGC:

- Provides the **ITGC Approval** — the final sign-off recorded once Business, IT Security, Privacy, and Legal gates are satisfied for higher-risk tools.

- Is the sole or primary named **Profile Approval Authority** for the highest-exposure profiles (Profile 1 Enterprise Productivity Assistant, Profile 4 Developer and Code Assistant, Profile 5 Agentic Automation, and others), reflecting that broadly deployed or highly autonomous tools need governance-level sign-off, not just domain-level sign-off.

- Is joined by Legal review specifically for external-facing generative/agentic tools (e.g., Profile 6, Profile 19 when external-facing), and by Privacy and Legal jointly for the most sensitive profiles (Profile 7, Profile 16, Profile 20).

### **AI Governance Committee**

The AI Governance Committee is the intended top-level, cross-functional oversight body for the AI program as a whole — reviewing patterns across tools, setting policy, and resolving conflicts between domain ratings. It is tracked as its own column in the Approval Workflow sheet and currently shows **"Not Established"** for every AI system, reflecting that this body has not yet been formally stood up; this is an open item for the program (see Section 8).

### **How the Gates Fit Together — Sequence and Logic**

the organization’s intended review sequence is: **Business → IT Security → ITGC**, with **Privacy and Legal running as separate, parallel gates** rather than sequential steps in that chain. In practice, across the workbook:

- **Business Approval** happens first, since a tool cannot be scored or reviewed until its purpose and scope are documented.

- **IT Security Approval** follows, informed by the Vendor & Security review, and is a prerequisite for production use regardless of data sensitivity.

- **Privacy Approval** and **Legal Approval** run in parallel to IT Security's review whenever the tool touches data-protection or contractual/regulatory questions — they are not blocked by, or blocking of, each other.

- **ITGC Approval** is the closing gate for any tool whose base Risk Tier is High or Critical, effectively acting as the governance checkpoint that confirms all applicable domain gates (Business, IT Security, and, where relevant, Privacy and Legal) have been satisfied before the tool is considered fully approved.

- The **Overall Risk Rating** (MAX of Validated Risk Tier, Vendor, Privacy, and Legal ratings) is what determines which domain is actually the constraint on a given tool — the Risk Assessment sheet's "Risk Drivers" column names the driving category (e.g., "Legal (High)") so reviewers know which gate to focus remediation on.

This design means a tool can be fully cleared on security and privacy grounds and still be blocked or downgraded by an outstanding Legal question (as is the case for Claude AI, where the Legal Risk Rating of High is the reason the Overall Risk Rating is High despite a Moderate Validated Risk Tier), and vice versa.

## **Workbook Structure — Purpose of Each Sheet**

The workbook has twelve sheets. Ten of them (AI Inventory through Monitoring) form the seven-step review lifecycle described in Section 3; Profiles, Profile Selection, and Reference Lists are supporting lookup sheets; and Dashboard is the executive rollup. This section explains **why each sheet exists** and what it contributes to the overall governance picture. See Section 2 for how these sheets connect architecturally.

### **Dashboard**

The executive rollup. It gives leadership a one-page view of the AI program: total systems, approval status counts, PII/Confidential/IP exposure counts, profile distribution across all 20 NIST AI RMF profiles, risk tier and Overall Risk Rating distributions, capability and data-classification breakdowns, and a running list of open executive action items. Every figure on this sheet is a formula pulling from AI Inventory, Risk Assessment, or Reference Lists — nothing here is typed in — so it always reflects the current state of the inventory.

### **AI Inventory**

The system of record for every AI tool the Company has evaluated. This is the only sheet where a new AI system is actually created (a new AI ID/row). It captures the business facts about the tool (provider, name, purpose, scope, capability, data processed) alongside manually recorded approval facts (requested by, reviewed by, approved date, approval status) and NIST AI RMF function coverage. Once a Profile is assigned here, the sheet automatically looks up that Profile's default risk tier, human oversight model, approval authority, and review frequency, and flags whether the tool's actual Risk Tier matches, exceeds, or falls below the Profile default.

### **Profiles**

The reference catalog of 20 NIST AI RMF-aligned profiles (P1–P20); can expand to match NIST AI RMF Playbook . Each profile defines a \*starting position\* for a newly intaked tool: typical use, default data classification, default risk tier, required human oversight model, approval authority, mandatory controls, monitoring focus, and review frequency. This sheet is never edited row-by-row during normal use — it is a stable lookup table that AI Inventory, Approval Workflow, and Monitoring all reference.

### **Profile Selection**

The decision table that determines \*which\* Profile (P1–P20) applies to a new tool. Twelve ordered rules are applied top to bottom, and the review stops at the **first** rule that matches — this is why rule order matters (e.g., a tool that is both agentic and customer-facing is always classified under the agentic rule, Rule 4, before the customer-facing rule, Rule 5, because Rule 4 comes first and rules run highest-risk-first). If no rule matches, Rule 12 hands the decision to IT Security to determine whether a new profile is warranted. Any material change to a tool's use should trigger a re-run of this sheet.

### **Risk Assessment**

The reconciliation sheet where the four independent domain reviews come together into one number. For each AI ID it: pulls the Inherent Risk from AI Inventory; escalates it into a **Validated Risk Tier** using harm-based and capability-based floor/escalation logic (see Section 7.3); computes the **Overall Risk Rating** as the maximum of the Validated Risk Tier, Vendor Risk Rating, Privacy Risk Rating, and Legal Risk Rating; and names which domain is driving that result. It also rolls up the applicable risk categories and harms (with counts) and lists the required evidence for each applicable category, giving reviewers a checklist of what documentation still needs to be gathered.

### **Risk & Harm Assessment**

The only sheet where risk-category and harm-type judgments are entered manually — a Yes/No/N/A answer for each of 13 risk categories (data leakage, prompt injection, hallucination, unauthorized retention, model drift, data poisoning, model theft, overreliance, bias, third-party risk, information security, privacy, and regulatory/legal risk) and 6 harm types (individual, organizational, safety, regulatory, confidentiality, and information integrity harm). These answers are the primary input to the Validated Risk Tier calculation on the Risk Assessment sheet.

### **Data & Privacy**

Privacy's domain review sheet. It records what data a tool touches (sources, classification, PII and category-specific flags for Employee/Customer/Financial/Legal/IP data), where that data goes (vendor sharing, residency), how long it is kept and whether inputs/outputs are logged, and whether a Data Processing Agreement (DPA) is executed. From these answers it calculates the **Privacy Risk Rating** automatically (see Section 7.2).

### **Vendor & Security**

IT Security's domain review sheet, scoped specifically to **security posture and control evidence** (Privacy Review, Legal Review, and DPA execution are intentionally owned elsewhere, by Data & Privacy and Legal & Compliance respectively, to avoid duplicate ownership). It tracks SOC 2, ISO 27001, penetration testing, MFA, RBAC, encryption at rest and in transit, audit logging, SIEM integration, and prompt-injection testing evidence, and calculates the **Vendor Risk Rating** from the completeness and outcome of that evidence.

### **Legal & Compliance**

Legal's domain review sheet, covering the AI-specific contractual and regulatory questions that a standard vendor contract review does not always capture: IP ownership of AI-generated output, training data rights, liability for AI errors or hallucination, right to audit AI decisions, restriction of Company data use for vendor model training, and termination/data-deletion rights on exit, plus overall regulatory exposure. It calculates the **Legal Risk Rating** automatically (see Section 7.1 for the full, finalized logic and test scenarios).

### **Approval Workflow**

The single place to see where a tool stands across **all four approval gates** at once. Business Approval, IT Security Approval (from Vendor & Security), Privacy Approval (from Data & Privacy), and Legal Approval (from Legal & Compliance) are each pulled in automatically; ITGC Required is calculated from the base Risk Tier; and Profile Approval Authority is shown for reference so reviewers know who needs to sign off next.

### **Monitoring**

The ongoing-oversight sheet. For every approved tool it tracks which monitoring types are required (usage, security, privacy, bias, drift), any incident history or open findings, and calculates the next reassessment date and status (Current, Overdue, or Not Scheduled) by combining a standard annual cadence with the tool's Profile-specific review frequency — always using whichever cadence is more frequent.

### **Reference Lists**

The shared dropdown and lookup catalog behind the entire workbook: valid values for Data Classification, Risk Tier, Approval Status, Lifecycle Status, Yes/No/N/A, Review Frequency, Profile IDs, Human Oversight models, AI Capability (with a description column explaining what each capability means and why it carries the risk profile it does), the 13 Risk Categories (with descriptions and minimum evidence expectations), the 6 Harm Types (with assessment requirements), and Review Status values used across the Security/Privacy/Legal reviews. Every dropdown in every other sheet — and the risk-tier ordering used by every MAX/escalation formula in the workbook — is sourced from this sheet.

## **Cell-Level Formula Reference**

This section documents every calculated (formula-driven) column in the workbook, sheet by sheet. Manually entered columns (free text, dates, or dropdown selections typed in by a reviewer) are noted but not reproduced here since they hold no formula logic. Row numbers below refer to the first data row of each sheet's table (e.g., row 4 or row 5 depending on the sheet) — the same formula pattern repeats down every subsequent row, with only the row number changing.

### **Dashboard**

Every figure on the Dashboard is a `COUNTA`, `COUNTIF`, `COUNTIFS`, `SUMPRODUCT`, or `INDEX/MATCH` formula reading from AI Inventory, Risk Assessment, Risk & Harm Assessment, or Profiles. Representative examples:

|  |  |  |
| --- | --- | --- |
| **Metric** | **Formula (row 1 shown)** | **What it does** |
| Total AI Systems | =COUNTA('AI Inventory'!$A$5:$A$11) | Counts non-blank AI IDs — the total number of tools in the inventory. |
| Approved Systems | =COUNTIF('AI Inventory'!$R$5:$R$11,"Approved") | Counts rows where Approval Status equals “Approved.” |
| Pending / Missing Evidence | =COUNTIF('AI Inventory'!$R$5:$R$11,"Pending / Needs Documentation") | Counts rows still awaiting documentation. |
| High Risk Systems | =COUNTIF('AI Inventory'!$H$5:$H$11,"High") | Counts rows where the Inherent Risk Tier is High. |
| Systems Processing PII | =COUNTIF('AI Inventory'!$N$5:$N$11,"Yes") | Counts rows flagged Yes for PII Processed. |
| Profiles Assigned | =COUNTIFS('AI Inventory'!$A$5:$A$11,"?\*",'AI Inventory'!$T$5:$T$11,"P\*") | Counts inventory rows that have both an AI ID and a Profile beginning with “P.” |
| Distinct Profiles In Use | =SUMPRODUCT(--(COUNTIF('AI Inventory'!$T$5:$T$11,Profiles!$A$4:$A$23)\>0)) | Counts how many of the 20 catalog profiles have at least one tool assigned to them. |
| Overall Critical/High Systems | =COUNTIFS('Risk Assessment'!$A$4:$A$10,"?\*",'Risk Assessment'!$F$4:$F$10,"High")+…"Critical" | Counts tools whose Overall Risk Rating (column F on Risk Assessment) is High or Critical. |
| Systems by Assigned Profile (table) | =COUNTIF('AI Inventory'!$T$5:$T$11,A23) | For each Profile ID listed in column A/E, counts how many inventory rows use that exact Profile. |
| Risk Tier / Overall Rating / Capability / Classification / Approval Status breakdowns | =COUNTIF('AI Inventory'!$H$5:$H$11,A45); =COUNTIF('Risk Assessment'!$F$4:$F$10,A51); =COUNTIF('AI Inventory'!$F$5:$F$11,"\*"&A57&"\*"); =COUNTIF('AI Inventory'!$L$5:$L$11,A65); =COUNTIF('AI Inventory'!$R$5:$R$11,A72) | Each breakdown table counts inventory or Risk Assessment rows matching each reference value (Low/Moderate/High/Critical, each Capability, each Data Classification, each Approval Status). |
| Risk Categories table | =COUNTIF('Risk & Harm Assessment'!C5:C11,"Yes") | For each of the 13 risk categories, counts how many tools were flagged Yes for that category on Risk & Harm Assessment. |

Executive Action Items and the Overall Risk Rating formula note beneath the tables are static text maintained manually, not formulas — they are the one place on the Dashboard meant for a person to update directly as priorities change.

### **AI Inventory**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 5 shown)** | **What it does** |
| H — Risk Tier | =IF(OR(L5="Sensitive",N5="Yes"),"High",IF(OR(L5="Confidential",M5="Yes"),"High",IF(L5="Internal","Moderate","Low"))) | Derives the Inherent Risk Tier purely from what the tool touches: Sensitive data or IP Processed = Yes → High; Confidential data or PII Processed = Yes → High; Internal → Moderate; otherwise Low. This is the "base" risk before any behavior-based escalation happens on the Risk Assessment sheet. |
| I — Profile Default Risk Tier | =IF(T5="","",INDEX(Profiles!$E$4:$E$23,MATCH(T5,Profiles!$A$4:$A$23,0))) | Looks up the Default Risk Tier for the assigned Profile (column T) from the Profiles catalog. |
| J — Tier vs Profile Check | =IF(OR(H5="",T5=""),"",IF(ISNUMBER(SEARCH(H5,I5)),"Matches profile",IF(OR(H5="High",H5="Critical"),"Above profile (OK)","Review vs profile default"))) | Flags whether the calculated Risk Tier matches, exceeds ("Above profile (OK)" — always acceptable since risk was validated upward), or falls short of ("Review vs profile default" — needs a look) what the Profile would normally expect. |
| U — Profile Approval Authority | =IFERROR(INDEX(Profiles!$K$4:$K$23,MATCH(T5,Profiles!$A$4:$A$23,0)),"") | Looks up who must approve this Profile from the Profiles catalog (e.g., ITGC; IT Security and Business Owner). |
| V — Profile Selection Rule (reference) | =IF(T5="","",INDEX(Profiles!$F$4:$F$23,MATCH(T5,Profiles!$A$4:$A$23,0))) | Note: despite the column name, this actually looks up Human Oversight (Profiles column F) for reference alongside the Profile. |
| W — Human Oversight | =IF(T5="","",INDEX(Profiles!$G$4:$G$23,MATCH(T5,Profiles!$A$4:$A$23,0))) | Looks up the required human oversight model for the assigned Profile. |
| X — Profile Review Frequency | =IF(T5="","",INDEX(Profiles!$J$4:$J$23,MATCH(T5,Profiles!$A$4:$A$23,0))) | Looks up how often the Profile requires reassessment. |
| Z — Overall Risk Rating (reference) | =IFERROR(INDEX('Risk Assessment'!$F$4:$F$10,MATCH(A5,'Risk Assessment'!$A$4:$A$10,0)),"") | Pulls the final Overall Risk Rating back from Risk Assessment so it is visible directly on the inventory row without needing to flip sheets. |

All other AI Inventory columns (Provider, AI System Name, Purpose, Scope, AI Capability, Data Processed, Original Approved Data Classification, Data Classification, Requested By, Reviewed By, Approved Date, Approval Status, NIST AI RMF Function Coverage, Assigned Profile, Notes) are manually entered.

### **Risk & Harm Assessment**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 5 shown)** | **What it does** |
| A / B — AI ID / Name | =INDEX('AI Inventory'!$A$5:$A$11,1) and =INDEX('AI Inventory'!$C$5:$C$11,1) | Pulls the AI ID and System Name directly from AI Inventory so this sheet always stays aligned to the same row order. |
| W — Applicable Risk Categories | =TEXTJOIN(", ",TRUE,IF(C5="Yes","Data leakage and disclosure",""), … repeated for all 13 categories) | Builds a comma-separated list of every risk category (of the 13 in columns C–O) answered Yes for this tool. |
| X — Category Count | =COUNTIF(C5:O5,"Yes") | Counts how many of the 13 risk categories are applicable (answered Yes). |
| Y — Applicable Harms | =TEXTJOIN(", ",TRUE,IF(P5="Yes","Individual harm",""), … repeated for all 6 harm types) | Builds a comma-separated list of every harm type (of the 6 in columns P–U) answered Yes. |
| Z — Harm Count | =COUNTIF(P5:U5,"Yes") | Counts how many of the 6 harm types are applicable. |

Columns C through U (the 13 risk-category and 6 harm-type Yes/No/N/A answers) are the manually entered judgment calls this sheet exists to capture; everything else on the sheet is a rollup of those answers.

### **Data & Privacy**

Columns G, H, I, and J (Public / Internal / Confidential / Sensitive Yes-No flags) are derived directly from the manually entered Data Classification (column F), for example `=IF(F4="Public","Yes","No")`. Column D, the **Privacy Risk Rating**, is the most complex formula on this sheet and is covered in full — including its complete test-scenario matrix — in **Section 7.2**.

### **Vendor & Security**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 4 shown)** | **What it does** |
| E — Vendor Risk Rating | =IF(D4="Rejected","Critical", IF(NOT(OR(D4="Approved",D4="Approved with Conditions")),"Moderate", IF(COUNTIF(F4:O4,"Yes\*")/COUNTA(F4:O4)\>=0.8,"Low", IF(COUNTIF(F4:O4,"Yes\*")/COUNTA(F4:O4)\>=0.5,"Moderate","High")))) | If the Security Review was Rejected → Critical. If it was never Approved or Approved with Conditions → Moderate (review incomplete). Otherwise, the rating is driven by what share of the ten security controls (SOC 2 through Prompt Injection Testing) came back as some form of "Yes": 80%+ → Low, 50–80% → Moderate, below 50% → High. The wildcard \`"Yes\*"\` matches answers like "Yes (analyzed)" or "Yes (SSO)," not just a bare "Yes." |

### **Legal & Compliance**

Column D, the **Legal Risk Rating**, is this sheet's core formula and the one most extensively refined during workbook development. It is covered in full — including its complete test-scenario matrix — in **Section 7.1**.

### **Risk Assessment**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 4 shown)** | **What it does** |
| C — Inherent Risk | =IFERROR(INDEX('AI Inventory'!$H$5:$H$11,MATCH(A4,'AI Inventory'!$A$5:$A$11,0)),"") | Pulls the base Risk Tier calculated on AI Inventory (data-classification driven). |
| D — Validated Risk Tier | (Harm- and capability-based escalation logic over C4 — see Section 7.3 for the full formula and scenarios.) | Escalates the Inherent Risk using Risk & Harm Assessment answers and AI Capability, applying whichever escalation rule fires (Safety harm, Agentic + Data poisoning, PII/Privacy + Sensitive or Confidential classification, Agentic + Third-party risk, Bias + PII, Model theft, or the Generative AI floor), never silently downgrading below the Inherent Risk. |
| E — Validation Result | =IF(D4=C4,"Confirmed at "&C4,"Escalate: "&C4&" to "&D4) | Plain-language statement of whether validation confirmed the inherent tier or escalated it, and to what. |
| F — Overall Risk Rating | =INDEX('Reference Lists'!$B$4:$B$7,MAX(MATCH(D4,…),MATCH(Vendor Risk Rating,…),MATCH(Privacy Risk Rating,…),MATCH(Legal Risk Rating,…))) | Takes the single highest rating among the Validated Risk Tier and the three domain ratings (Vendor, Privacy, Legal), using the Low→Moderate→High→Critical order defined on Reference Lists. |
| G — Risk Drivers | =TRIM(TEXTJOIN(", ",TRUE, IF(D4 is the max,"Validated Risk ("&D4&")",""), IF(Vendor is the max,"Vendor ("&…&")",""), IF(Privacy is the max,"Privacy ("&…&")",""), IF(Legal is the max,"Legal ("&…&")",""))) | Names every domain that is tied for the maximum rating, so reviewers know exactly which review(s) to focus remediation on. |
| L / M — IT Risk Register Entry / Risk Acceptance Required | =IF(OR(D4="High",D4="Critical"),"Yes","No") | Both flags trigger automatically whenever the Validated Risk Tier is High or Critical. |
| S — Required Evidence | =TEXTJOIN(", ",TRUE,IF(risk-category="Yes",minimum-evidence-text,"") … for all 13 categories) | Pulls together the "Minimum Evidence" text from Reference Lists for every applicable risk category, producing a ready checklist of what documentation is needed. |

### **Approval Workflow**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 4 shown)** | **What it does** |
| D — IT Security Approval | =IFERROR(IF(INDEX('Vendor & Security'!$D$4:$D$10,MATCH(A4,…))="Rejected","Rejected",IF(…="Approved","Approved",IF(…="Approved with Conditions","Approved with Conditions","Pending"))),"") | Mirrors the Security Review status from Vendor & Security into a normalized approval status. |
| E — Privacy Approval | Same pattern, sourced from Data & Privacy column C (Privacy Review). | Mirrors the Privacy Review status. |
| F — Legal Approval | Same pattern, sourced from Legal & Compliance column C (Legal Review). | Mirrors the Legal Review status. |
| G — ITGC Required | =IFERROR(IF(OR(INDEX('AI Inventory'!$H$5:$H$11,…)="High",…="Critical"),"Yes","No"),"") | Requires ITGC sign-off whenever the base Inherent Risk Tier (not the escalated tier) is High or Critical. |
| H — ITGC Approval | =IF(G4="No","Not Required","Approved") | Placeholder that marks ITGC Approval as satisfied once required (in practice this is updated manually as ITGC actually signs off; see Section 8 for the gap this creates). |
| J — Approval Conditions | =IFERROR(INDEX('AI Inventory'!$R$5:$R$11,…),"") | Reflects any conditions noted against the Approval Status on AI Inventory. |
| O — Profile Approval Authority (reference) | =IFERROR(INDEX(Profiles!$G$4:$G$23,MATCH(INDEX('AI Inventory'!$T$5:$T$11,…),Profiles!$A$4:$A$23,0)),"") | Looks up the Profile’s designated approval authority for quick reference alongside the four gate statuses. |

Business Approval (column C) and the AI Governance Committee column are manually entered/updated, since there is no upstream sheet that tracks Business sign-off or Governance Committee status independently.

### **Monitoring**

|  |  |  |
| --- | --- | --- |
| **Column** | **Formula (row 4 shown)** | **What it does** |
| N — Next Reassessment | =IF(M4\<\>"",EDATE(M4,12),"") | Adds 12 months to the Last Reassessment date. |
| O — Reassessment Status | =IF(N4="","Not Scheduled",IF(N4\<TODAY(),"Overdue","Current")) | Flags whether the next reassessment date has already passed. |
| P — Profile Review Frequency (reference) | =IFERROR(INDEX(Profiles!$J$4:$J$23,MATCH(INDEX('AI Inventory'!$T$5:$T$11,…),Profiles!$A$4:$A$23,0)),"") | Looks up how often the assigned Profile itself requires review. |
| Q — Effective Review Cadence | =IF(P4="",L4,"More frequent of "&L4&" and "&P4) | States the effective cadence, always taking the tighter (more frequent) of the standard annual schedule and the Profile’s own required frequency. |

### **Profiles, Profile Selection, and Reference Lists**

These three sheets are static reference/lookup tables — every cell is manually curated content (profile definitions, ordered selection rules, and dropdown/description lists) with no calculated formulas. They are the "answer key" that every formula elsewhere in the workbook (`INDEX`/`MATCH` lookups) reads from, which is why they should be edited carefully: a typo in a Profile ID or Risk Tier label here will silently break lookups on every other sheet.



## **Deep Dive: The Three Iteratively-Refined Risk Formulas**

Three formulas in this workbook were deliberately reverse-engineered, stress-tested against edge cases, and rebalanced during development: the **Legal Risk Rating**, the **Privacy Risk Rating**, and the **Validated Risk Tier** (including the AI Capability floor/escalation logic). This section documents the finalized logic for each, in plain language and as the literal formula, followed by the **complete matrix of test scenarios** used to validate that the logic produces the intended risk level in every case. Every scenario below has been run against the exact formula currently live in the workbook, so the results are guaranteed to match what the workbook will calculate for an equivalent set of answers.

### **Legal Risk Rating (Legal & Compliance, Column D)**

This is the **finalized, fine-tuned version** of the formula and is the version that must be used going forward — it replaced an earlier, simpler draft that treated the six governance questions too uniformly and did not correctly separate absolute blockers from softer gaps.

Column mapping: **C** = Legal Review status, **E** = IP Ownership of AI Output Clarified, **F** = Training Data Rights Confirmed, **G** = Liability for AI Errors/Hallucination Addressed, **H** = Right to Audit AI Decisions, **I** = Data Use for Model Training Restricted, **J** = Termination/Data Deletion Rights on Exit.

```
=IF(C4="Rejected","Critical", IF(AND(E4="No",I4="No"),"Critical", IF(J4="No","Critical", IF(OR(C4="Not Started", I4="No", COUNTIF(E4:G4,"No")>=1),"High", IF(H4="No","Moderate", IF(OR(J4="To Confirm", I4="To Confirm"),"Moderate", IF(COUNTIF(E4:J4,"To Confirm")=1,"Low", IF(AND(COUNTIF(E4:J4,"Yes")=COUNTA(E4:J4)-COUNTIF(E4:J4,"N/A"), COUNTA(E4:J4)-COUNTIF(E4:J4,"N/A")>0),"Low", IF(COUNTA(E4:J4)-COUNTIF(E4:J4,"N/A")=0,"Low", IF(COUNTIF(E4:J4,"Yes")/(COUNTA(E4:J4)-COUNTIF(E4:J4,"N/A"))>=0.5,"Moderate", "High"))))))))))
```

**Plain-language logic, in the order it actually evaluates**

1. **Rejected legal review is an absolute block.** If Legal Review = Rejected, the rating is Critical no matter what the six questions say.

1. **A compounded double-gap is Critical.** If IP Ownership is No \*and\* Data Use Restriction is No at the same time, that combination alone is treated as Critical — losing ownership of the output while also being unable to restrict the vendor’s use of Company data for training is more severe than either gap alone.

1. **Denied exit/deletion rights is an absolute block, on its own.** If Termination/Data Deletion Rights = No, the rating is Critical even if every other answer is Yes — this was a deliberate correction: "Deletion Rights denied alone = absolute block" is treated as its own top-tier trigger, distinct from (and just as severe as) the double-gap case above, even though both land at Critical.

1. **Any single core gap, or an unreviewed contract, is High.** Legal Review = Not Started, or Data Use Restriction = No (alone), or any one of IP Ownership / Training Data Rights / Liability = No, all escalate to High.

1. **A weak audit right, alone, is only Moderate.** Right to Audit AI Decisions = No does not, by itself, indicate a severe problem — the team specifically determined that the inability to audit AI decisions is a real but secondary concern, so a lone No here caps out at Moderate rather than High.

1. **Open items on the two exit-related questions are Moderate.** If Deletion Rights or Data Use Restriction is "To Confirm" (rather than a hard No), that is treated as an unresolved item worth Moderate attention, not yet an escalation to High.

1. **Exactly one open "To Confirm" elsewhere is still Low.** If precisely one of the six questions is marked "To Confirm" and it isn’t one of the two called out above, the rating stays Low — a single loose end doesn’t outweigh five confirmed protections.

1. **All applicable answers Yes is Low.** If every question that isn’t marked N/A came back Yes, the tool is Low risk.

1. **All six answers N/A is Low, not High.** This was a deliberate fix: if every question is Not Applicable, there is nothing outstanding to flag, so the formula now correctly returns Low instead of defaulting upward.

1. **Otherwise, it comes down to the Yes-ratio.** Count how many of the non-N/A questions are Yes, divide by the number of applicable questions: 50% or more → Moderate; below 50% → High.

**Test Scenario Matrix**

The table below lists every distinct logical path through the formula, the inputs that trigger it, the result, and why. C = Legal Review; E–J = the six governance questions in order (IP Ownership, Training Data Rights, Liability, Right to Audit, Data Use Restricted, Deletion Rights).

|  |  |  |  |
| --- | --- | --- | --- |
| **#** | **Scenario (C, E, F, G, H, I, J)** | **Result** | **Why** |
| 1 | Legal Review = Rejected (all six = Yes) | Critical | Absolute block — a rejected legal review overrides every other answer. |
| 2 | IP Ownership = No AND Data Use Restricted = No (rest Yes) | Critical | Compounded double-gap — losing output ownership and training-data-use control together is a critical exposure. |
| 3 | Deletion Rights on Exit = No (rest Yes) | Critical | Absolute block on its own — no ability to force data deletion at contract end. |
| 4 | Legal Review = Not Started (rest Yes) | High | An unreviewed contract cannot be relied on, regardless of the answers given. |
| 5 | Data Use for Training Restricted = No, alone | High | Single core gap: vendor may retain/train on Company data. |
| 6 | IP Ownership of AI Output = No, alone | High | Single core gap: unclear who owns AI-generated output. |
| 7 | Training Data Rights Confirmed = No, alone | High | Single core gap: unclear rights to the data used to train the model. |
| 8 | Liability for AI Errors/Hallucination = No, alone | High | Single core gap: no addressed liability for AI mistakes. |
| 9 | Four "To Confirm" answers, two Yes (ratio below 50%) | High | Too many unresolved items outweigh the few confirmed protections. |
| 10 | Right to Audit AI Decisions = No, alone | Moderate | A weak audit right is a real but secondary concern — capped at Moderate, not escalated further. |
| 11 | Deletion Rights = To Confirm, alone | Moderate | Open item on an exit-related protection, not yet a hard No. |
| 12 | Data Use Restricted = To Confirm, alone | Moderate | Open item on a training-data protection, not yet a hard No. |
| 13 | Two "To Confirm", four Yes (ratio 100% of applicable) | Moderate | Multiple open items, but confirmed answers still make up the majority. |
| 14 | Three "To Confirm", three Yes (ratio exactly 50%) | Moderate | Boundary case — a 50/50 split still resolves to Moderate, not High. |
| 15 | Exactly one "To Confirm" elsewhere (e.g., IP Ownership), rest Yes | Low | A single loose end does not outweigh five confirmed protections. |
| 16 | All six governance questions = Yes | Low | Fully confirmed contract terms. |
| 17 | All six governance questions = N/A | Low | Nothing applicable is outstanding — corrected so N/A no longer inflates risk. |
| 18 | Three Yes / three N/A (all applicable answers Yes) | Low | N/A items are excluded from the ratio, so a clean set of applicable answers stays Low. |

**Note on the Critical tier:** three independent paths reach Critical (Rejected review; the IP+Data-Use double gap; Deletion Rights alone). These were intentionally kept as separate, equally severe triggers rather than collapsed into one rule, since each represents a distinct real-world failure mode that a reviewer should be able to identify at a glance from the Notes column.

### **Privacy Risk Rating (Data & Privacy, Column D)**

Column mapping: **C** = Privacy Review status, **F** = Data Classification (from which **G**=Public, **H**=Internal, **I**=Confidential/Sensitive, and **J**=Sensitive are each derived as Yes/No), **K–P** = the six sensitive-data-category flags (PII, Employee, Customer, Financial, Legal, IP/Trade Secrets), **Q** = Data Shared With Vendor, **V** = DPA Executed.

```
=IF(C4="Rejected","Critical", IF(OR(J4="Yes", AND(NOT(ISNUMBER(SEARCH("Yes",V4))), I4="Yes", ISNUMBER(SEARCH("Yes",Q4)), COUNTIF(K4:P4,"Yes")>=2)), "Critical", IF(AND(NOT(ISNUMBER(SEARCH("Yes",V4))), ISNUMBER(SEARCH("Yes",Q4)), OR(I4="Yes", COUNTIF(K4:P4,"Yes")>=2)), "High", IF(OR(AND(I4="Yes", ISNUMBER(SEARCH("Yes",V4))), AND(COUNTIF(K4:P4,"Yes")=1, ISNUMBER(SEARCH("Yes",Q4)), NOT(ISNUMBER(SEARCH("Yes",V4)))), AND(I4="Yes", NOT(ISNUMBER(SEARCH("Yes",Q4))))), "Moderate", IF(AND(COUNTIF(K4:P4,"Yes")=0, I4<>"Yes", H4<>"Yes", OR(G4="Yes", NOT(ISNUMBER(SEARCH("Yes",Q4))), ISNUMBER(SEARCH("Yes",V4)))), "Low", "Moderate")))))
```


**Plain-language logic, in the order it actually evaluates**

1. **Rejected privacy review is Critical**, exactly like Legal Review = Rejected on the Legal sheet.

1. **Sensitive data classification is an automatic Critical ceiling**, regardless of every other answer — once data is classified Sensitive, nothing else can pull the rating down.

1. **Confidential data, shared with a vendor, with no DPA on file, touching two or more sensitive-data categories (PII/Employee/Customer/Financial/Legal/IP) is also Critical** — the combination of Confidential classification, external sharing, no contractual protection, and broad category exposure is treated as severe as a Sensitive classification.

1. **The same combination but only one sensitive-data category flagged drops to High** rather than Critical — still no DPA and still vendor-shared, but narrower exposure.

1. **Moderate covers three distinct "contained" situations:** (a) Confidential data where a DPA \*is\* executed; (b) exactly one sensitive-data category shared with a vendor while a DPA is pending; or (c) Confidential data that is \*not\* shared with any vendor at all.

1. **Low requires Public-or-non-sensitive data with zero flagged categories**, and either no vendor sharing or a DPA already in place. Because the Internal flag (H) must not be "Yes" to reach Low, and Internal classification always sets H to Yes, **Internal-classified tools can never reach Low under the current formula** — they resolve to Moderate by the catch-all. This is a known, discussed characteristic of the formula (see Section 8).

1. **Everything else defaults to Moderate** — the catch-all ensures no combination of answers falls through without a rating.

**Test Scenario Matrix**

|  |  |  |  |
| --- | --- | --- | --- |
| **#** | **Scenario** | **Result** | **Why** |
| 1 | Data Classification = Sensitive (all else clean) | Critical | Sensitive classification is an automatic ceiling, independent of vendor sharing or DPA status. |
| 2 | Confidential, vendor-shared, no DPA, 2 categories flagged (e.g., PII + Employee Data) | Critical | Broad sensitive-category exposure leaving the Company with no contractual protection. |
| 3 | Confidential, vendor-shared, no DPA, only 1 category flagged | High | Same unprotected sharing, but narrower data exposure. |
| 4 | Confidential, vendor-shared, DPA executed | Moderate | A DPA on file meaningfully contains the risk of Confidential data sharing. |
| 5 | Confidential, not shared with any vendor | Moderate | No external sharing removes the main driver of risk even without a DPA. |
| 6 | Internal, no PII/category flags, not vendor-shared | Moderate | Internal classification always sets the Internal flag to Yes, which blocks the Low branch — resolves via the catch-all. |
| 7 | Public data, nothing else flagged | Low | Only Public-classified data (Internal flag = No) can satisfy the Low branch’s requirements. |
| 8 | Internal, exactly 1 PII-type field flagged, vendor-shared, no DPA | Moderate | One flagged category with unprotected vendor sharing, but Internal (not Confidential) classification. |

### **Validated Risk Tier — AI Capability Floor and Escalation Logic (Risk Assessment, Column D)**

This formula takes the Inherent Risk (column C, from AI Inventory’s data-classification-driven Risk Tier) and escalates it — **never silently downgrades it** — based on the harm judgments from Risk & Harm Assessment and the tool’s AI Capability. The Generative AI floor logic added here mirrors the pre-existing Agentic AI escalation pattern, using `SEARCH` so it matches any AI Capability value that \*contains\* "Generative" or "Agentic" (allowing for tools with multiple capabilities).

```
=INDEX('Reference Lists'!$B$4:$B$7, MAX( MATCH(C4, 'Reference Lists'!$B$4:$B$7,0), MATCH( IF(Harm!SafetyHarm="Yes","Critical", IF(AND(Harm!DataPoisoning="Yes", SEARCH("Agentic",Inventory!Capability)),"Critical", IF(AND(OR(Harm!PrivacyRisk="Yes",Inventory!PIIProcessed="Yes"), Inventory!DataClassification="Sensitive"),"Critical", IF(AND(OR(Harm!PrivacyRisk="Yes",Inventory!PIIProcessed="Yes"), Inventory!DataClassification="Confidential"),"High", IF(AND(SEARCH("Agentic",Inventory!Capability), Harm!ThirdPartyRisk="Yes"),"High", IF(AND(Harm!BiasHarmfulOutput="Yes", Inventory!PIIProcessed="Yes"),"High", IF(Harm!ModelTheft="Yes","High", IF(AND(SEARCH("Generative",Inventory!Capability), C4="Low"),"Moderate", C4 )))))))), 'Reference Lists'!$B$4:$B$7,0) ))
```

**Plain-language logic, in the order it actually evaluates**

1. **Safety harm = Yes → Critical**, unconditionally — nothing outweighs a flagged safety impact.

1. **Data poisoning = Yes, and the tool is Agentic → Critical** — an agentic tool acting on poisoned data or references is treated as a critical combination.

1. **Privacy risk or PII processing, combined with Sensitive data classification → Critical.**

1. **The same privacy/PII condition, combined with Confidential (not Sensitive) classification → High.**

1. **Agentic capability combined with flagged Third-party/value-chain risk → High** — a tool that acts on other systems is riskier when its vendor chain is also a concern.

1. **Bias and harmful output = Yes, combined with PII processing → High.**

1. **Model theft or extraction = Yes → High**, on its own.

1. **The Generative AI floor: if the tool’s capability contains "Generative" and the Inherent Risk is Low, it is floored up to Moderate.** This mirrors the Agentic escalation pattern and reflects the judgment that Generative AI carries inherent hallucination, IP, and output-reliance risk even when the data it touches is otherwise low-sensitivity.

1. **If none of the above conditions are met, the Validated Risk Tier simply equals the Inherent Risk** — the formula never lowers the rating below what the data classification alone already established.

**Deliberate scope decision — "AI APIs and Integrations" left un-escalated:** a parallel floor for the "AI APIs and Integrations" capability (one step below Generative AI in the ordering) was considered and explicitly **rejected**. That capability continues to rely only on the existing classification- and PII-based escalation rules above, with no dedicated capability floor of its own — it is escalated only if it independently trips one of the harm-based rules.

**Risk & Harm Assessment was intentionally used narrowly here.** Its 13 risk categories and 6 harm types were considered for broader use across the workbook, but the team decided that — like Security, Legal, and Compliance, which each stand on their own — Risk & Harm Assessment should remain purpose-built for the Risk Assessment sheet’s Validated Risk Tier calculation (items 1, 5, and 6 above use it directly) rather than being wired into other sheets’ formulas.

**Test Scenario Matrix**

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **#** | **Scenario** | **Inherent Risk (C4)** | **Validated Risk Tier** | **Why** |
| 1 | Safety harm = Yes | Any | Critical | Unconditional — safety always wins. |
| 2 | Data poisoning = Yes + Agentic capability | Any | Critical | Agentic action on poisoned data/tools is a critical combination. |
| 3 | Privacy risk or PII = Yes + Sensitive classification | Any | Critical | Confirmed privacy exposure on the most sensitive data tier. |
| 4 | Privacy risk or PII = Yes + Confidential classification | Any | High | Same privacy exposure, one tier below Sensitive. |
| 5 | Agentic capability + Third-party/value-chain risk = Yes | Any | High | Vendor-chain concern compounded by autonomous action. |
| 6 | Bias and harmful output = Yes + PII = Yes | Any | High | Biased output affecting personal data. |
| 7 | Model theft or extraction = Yes | Any | High | Stands alone as a High trigger. |
| 8 | Generative AI capability, no other trigger fires | Low | Moderate | The Generative AI floor — mirrors the Agentic escalation pattern. |
| 9 | Generative AI capability, no other trigger fires | Moderate or higher | Unchanged | The floor only lifts a Low; it never lowers an already-higher tier. |
| 10 | AI APIs and Integrations capability, no harm-based trigger fires | Low | Low (unchanged) | Deliberately left un-escalated — no dedicated floor was built for this capability. |
| 11 | Embedded AI or Internal AI Deployments, no trigger fires | C4 value | Unchanged | Falls through to "= C4" — Validated Risk Tier simply equals Inherent Risk. |



## **Known Gaps, Design Decisions, and Pending Items**

This section captures the open questions and deliberate scope decisions surfaced while building and stress-testing the workbook, so future maintainers understand what was consciously decided versus what is genuinely still outstanding.

### **Data & Privacy — reviewer-entered fields not read by the Privacy Risk Rating**

On the Data & Privacy sheet, the Privacy Risk Rating formula (column D) reads columns C (Privacy Review), F (Data Classification, via the derived G/H/I/J flags), K through P (PII, Employee, Customer, Financial, Legal, and IP/Trade Secrets flags), Q (Data Shared With Vendor), and V (DPA Executed). Columns **R (Data Residency), S (Retention Period), T (Inputs Logged), and U (Outputs Logged)** are reviewer-entered and displayed on the sheet, but are **not** factored into the risk-rating calculation itself — they remain informational/documentary fields. Whether residency, retention, or logging posture should ever feed the rating logic is an open question for a future iteration.

### **Data & Privacy — Internal classification can never reach Low**

As documented in Section 7.2, the current formula structurally prevents any Internal-classified tool from reaching a Low Privacy Risk Rating, because the Internal flag (H) is required to be "No" to satisfy the Low branch, and only a Public classification sets H to "No." This was identified and discussed during testing; the decision was to **leave the formula as-is** rather than adjust it further at this time, so Internal-classified tools with no other flags will resolve to Moderate via the catch-all rather than Low. This should be revisited if it produces rating outcomes that don’t match reviewer expectations in practice.

### **AI Capability escalation — "AI APIs and Integrations" intentionally left un-escalated**

A dedicated capability-based floor/escalation rule for the "AI APIs and Integrations" capability (analogous to the Generative AI floor) was proposed and explicitly **rejected**. That capability continues to rely solely on the pre-existing classification- and PII-based escalation rules in the Validated Risk Tier formula — it has no capability-specific floor of its own. If usage patterns for API-integrated AI tools later suggest this capability is being under-rated, this decision should be revisited.

### **ITGC Approval is a semi-automated placeholder**

The Approval Workflow sheet's ITGC Approval column (H) currently auto-populates to "Approved" the moment ITGC Required (G) is Yes, rather than reflecting an actual, independently tracked ITGC sign-off event. In practice this column should be manually corrected once ITGC has genuinely reviewed and signed off — the formula only establishes that ITGC involvement is \*needed\*, not that it has \*happened\*.

### **AI Governance Committee not yet established**

Every row on the Approval Workflow sheet currently shows "Not Established" for the AI Governance Committee column. Standing up this committee — and defining what it actually reviews versus what ITGC already covers — remains an open organizational item outside the scope of the workbook itself.

### **Reference Lists — AI Capability Description column**

The Reference Lists sheet includes a dedicated "AI Capability Description" column (column J) that defines what each of the five AI Capability values means in plain language: Generative AI, Agentic AI, Embedded AI, AI APIs and Integrations, and Internal AI Deployments. These descriptions are the basis for the plain-language capability explanations used throughout this document and should be kept in sync if capability definitions evolve.

### **Vendor & Security — Privacy, Legal, and DPA ownership deliberately excluded**

The Vendor & Security sheet is explicitly scoped to security posture and control evidence only; Privacy Review, Legal Review, and DPA Executed are owned on the Data & Privacy and Legal & Compliance sheets respectively. This is a deliberate separation of duties, not an oversight — it exists so that no single reviewer sheet duplicates another gate's ownership (see Section 2.3 for how this separation is enforced architecturally).

## **Document Provenance and Attribution**

**Design and content ownership:** Every risk-rating formula, workbook layer, escalation rule, and governance workflow described in this document was designed, tested, and iteratively refined by **[IT Security Lead]**, IT Security Lead. The underlying logic — including the Legal Risk Rating formula, the Privacy Risk Rating formula, and the Validated Risk Tier / AI Capability floor and escalation rules — reflects their analysis and decisions, not an AI-generated design.

**Drafting assistance:** This document was drafted, structured, and formatted with the assistance of **Microsoft 365 Copilot**, an enterprise AI assistant built on an Anthropic Claude large language model, working from [IT Security Lead]'s live workbook, formulas, and prior design discussions. AI assistance was used for writing, organizing, and diagramming — not for originating the risk logic itself.
