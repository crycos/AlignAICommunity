# AI Governance Toolkit: NIST AI RMF Implementation

## Overview

This toolkit provides a complete, operationalized framework for organizations to assess, classify, approve, and monitor artificial intelligence (AI) tools and use cases according to the **NIST AI Risk Management Framework (AI RMF) 1.0**.

The toolkit enables organizations to move from ad-hoc AI tool adoption to a structured, auditable governance program that:
- **Governs** AI deployments through defined policies and approval gates
- **Maps** AI capabilities to organizational risk profiles
- **Measures** compliance through systematic reviews and assessments
- **Manages** ongoing risk through monitoring, reassessment, and incident response

Whether you're just beginning AI governance or refining an existing program, this toolkit provides production-ready templates, procedures, and calculation models that can be deployed immediately or adapted to your organization's specific needs.

---

## What's Included

### 📋 **File 1: AI Governance Procedure** 
*AI_Governance_Procedure_SANITIZED.md*

**What it is:** A complete, step-by-step governance procedure aligned to NIST AI RMF 1.0 that defines the mandatory process for evaluating and approving any AI tool used in your organization.

**What it covers:**
- **Scope:** All AI tool types — Generative AI, Agentic AI, Embedded AI, API integrations, and internal deployments
- **Process flow:** From initial intake through risk assessment, approval, registration, monitoring, and annual review
- **Governance roles:** Responsibilities for IT Security, Business Owners, Technical Owners, Privacy, Legal, Procurement, and ITGC
- **Risk definitions:** Clear classification for Sensitive, Confidential, and Internal data
- **Five AI capability categories:** Definitions, risk profiles, and escalation rules for each
- **Control requirements:** Security, privacy, legal, and compliance standards
- **Approval gates:** How tools move from intake to production use
- **Monitoring cadence:** Reassessment frequencies based on risk tier
- **Incident response:** Categories and escalation for AI-specific incidents
- **20 risk profiles:** Pre-defined governance expectations for common AI use cases

**Key sections:**
- Appendix A: End-to-end review and approval process flow (visual)
- Appendix B: NIST AI RMF alignment mapping
- Appendix C: 20 AI RMF Profiles with oversight models
- Appendix D: Sample data from an authorized AI systems catalog
- Appendix E: Control evidence and security requirements
- Appendix F: Sample risk treatment documentation
- Appendix G: Incident categories requiring escalation
- Appendix H: Risk classification and escalation logic (technical reference)

**How to use it:** This is your **governance policy document**. Use it to:
- Define the mandatory process for your organization
- Train stakeholders on their roles and responsibilities
- Establish the criteria for AI tool approval
- Create supporting policies and procedures
- Brief leadership and compliance teams

---

### 📊 **File 2: AI Inventory & Risk Assessment Workbook**
*AI_Inventory___Risk_Assessment_Workbook_SANITIZED.xlsx*

**What it is:** A production-ready Excel workbook that implements the governance procedure in operational form. This is the day-to-day system of record for tracking every AI tool your organization uses.

**What it does:**
- **Intake & classification:** Register new AI tools and assign them to one of 20 governance profiles
- **Risk assessment:** Automatically calculate inherent, validated, and overall risk tiers based on data classification, AI capability, and harm assessment
- **Domain reviews:** Parallel tracks for security, privacy, legal, and compliance domain expertise
- **Approval workflow:** Track approvals through required gates and escalations to IT Governance Committee
- **Monitoring:** Schedule reassessments and track compliance status
- **Executive reporting:** Dashboard with KPIs, charts, and risk summaries

**The 12 sheets:**

| Sheet | Purpose |
|-------|---------|
| **Dashboard** | Executive summary: KPIs, system counts, risk distribution charts, profile usage |
| **AI Inventory** | System of record for all AI tools: intake data, classification, assigned profile, current risk tier |
| **Profiles** | Reference table: 20 pre-defined AI RMF profiles with oversight models and approval authorities |
| **Profile Selection** | Logic rules for automatically assigning the right profile based on AI capability and data classification |
| **Risk Assessment** | Calculates Validated Risk Tier by escalating Inherent Risk based on harm assessment and AI capability |
| **Risk & Harm Assessment** | Domain review: Scores 13 risk categories and 6 harm types to determine escalation triggers |
| **Data & Privacy** | Domain review: Evaluates data classification, PII handling, residency, retention, and DPA status |
| **Vendor & Security** | Domain review: Validates security controls (SOC 2, MFA, encryption, logging, etc.) and vendor posture |
| **Legal & Compliance** | Domain review: Reviews IP ownership, training data rights, liability, audit rights, and deletion rights |
| **Approval Workflow** | Tracks approvals from Business Owner → IT Security → ITGC; mirrors review status from domain sheets |
| **Monitoring** | Schedules next reassessment; tracks overdue reviews; calculates effective review cadence |
| **Reference Lists** | Lookup tables: Risk tiers, data classifications, AI capabilities, control types, harm categories |

**Key design features:**
- **No manual risk calculations:** Every risk rating is a live formula keyed to the tool's AI ID
- **Parallel domain reviews:** Security, Privacy, Legal, and Compliance are independent gates; no bottlenecks
- **Escalation rules:** Built-in logic for when Generative AI, Agentic AI, or sensitive data combinations require higher oversight
- **Profile defaults:** Profiles pre-populate expected Risk Tier, Approval Authority, and reassessment frequency
- **Risk drivers:** Overall Risk Rating identifies which domain is the current constraint (e.g., "Critical due to Privacy Risk")
- **Audit trail:** Every approval decision and review status is captured; Excel recalculation ensures consistency

**How to use it:** This is your **operational tool**. Use it to:
- Register every AI tool your organization uses
- Assign each tool to the appropriate governance profile
- Guide domain experts through their reviews
- Automatically calculate risk ratings and escalation needs
- Track approval status and identify bottlenecks
- Generate dashboards for leadership reporting
- Monitor reassessment schedules
- Maintain an auditable history of all decisions

---

### 📖 **File 3: AI Inventory Workbook Technical Reference Guide**
*AI_Inventory_Workbook___Technical_Reference_Guide_SANITIZED.md*

**What it is:** A detailed technical specification document that explains, cell-by-cell, how the workbook functions. This is the reference manual for spreadsheet maintainers, auditors, and anyone who needs to understand why calculations work the way they do.

**What it covers:**

**Architecture & Data Flow (Section 2):**
- The 6-layer pipeline: Reference & Lookup → Intake → Domain Reviews → Reconcile → Workflow → Monitoring
- How data flows from static reference tables through intake to parallel domain reviews, then to a single reconciliation point
- Why this architecture prevents bottlenecks and ensures consistency

**Operational Guidance (Section 3):**
- Day-to-day workbook usage from the perspective of each role
- Input fields vs. calculated fields
- Common workflows: Registering a tool, responding to a domain review, handling escalations
- How to resolve disputes between a domain review and a profile default

**Governance Roles (Section 4):**
- Business Owner: Defines use case and data classification
- IT Security: Leads review and risk validation
- Privacy, Legal, Technical Owner: Run parallel domain reviews
- ITGC: Final approval authority for High/Critical tools

**Sheet Specifications (Section 5):**
- One-page purpose statement for each of the 12 sheets
- What data flows in and what it produces
- How each sheet connects to others

**Formula Explanations (Section 6):**
- Every formula in the workbook, organized sheet-by-sheet
- Plain-language description of what each formula does
- Why it was designed that way
- Examples of when it produces different results

**Deep Dives (Section 7):**

Three of the most complex risk-rating formulas are explained in detail with test scenario matrices:

1. **Legal Risk Rating Formula**
   - How to score IP ownership, training data rights, liability, audit rights, data-use restrictions, and deletion rights
   - Why any single "No" forces the rating to High
   - Test matrix: 15 scenarios showing how different combinations resolve

2. **Privacy Risk Rating Formula**
   - How data classification, PII flags, vendor data sharing, and DPA status combine
   - Why classification escalates the rating (Sensitive is riskier than Confidential)
   - Why Internal data has special handling
   - Test matrix: 18 scenarios covering all classification + PII combinations

3. **Validated Risk Tier & AI Capability Floor Logic**
   - How Inherent Risk escalates based on harm findings
   - Why Generative AI tools have a "floor" (never rated below Moderate, even with Low data classification)
   - Why Agentic AI escalates when combined with Third-party risk or Data poisoning
   - Why "AI APIs and Integrations" does not have its own escalation floor
   - Test matrix: 11 scenarios showing how different AI capabilities and harm triggers resolve

**Known Gaps & Design Decisions (Section 8):**
- What was consciously decided vs. what remains pending
- Why some fields are informational but not used in calculations
- Why the AI Governance Committee is "Not Established" (organizational gap, not workbook gap)
- Why ITGC Approval is semi-automated (needs manual update when actual sign-off occurs)

**How to use it:** This is your **technical reference**. Use it to:
- Understand why formulas are structured the way they are
- Debug or modify calculations when needed
- Train auditors or compliance staff on calculation logic
- Document risk-rating decisions for regulators
- Adapt the formulas to your organization's specific requirements
- Resolve disputes over how a risk tier was calculated

---

## Quick Start Guide

### For your first week:

**Day 1-2: Understand the Framework**
1. Read the **Governance Procedure** executive summary (pages 1-5)
2. Review the NIST AI RMF alignment (Appendix B in Procedure)
3. Familiarize yourself with the 5 AI capabilities and 20 profiles

**Day 3-4: Set Up the Workbook**
1. Create a copy of the **Workbook** for your organization
2. Update sheet headers if needed (organization name, contact info)
3. Load your existing AI tools into the AI Inventory sheet
4. Assign each tool to a Profile based on AI Capability and Data Classification

**Day 5: First Risk Assessment**
1. Select one AI tool to use as a pilot
2. Have the Technical Owner fill in the Intake fields on AI Inventory
3. Have domain experts complete Risk & Harm, Data & Privacy, and Vendor & Security reviews
4. Observe the Validated Risk Tier calculation on Risk Assessment
5. Process the approval decision on Approval Workflow

**Ongoing:**
- Add new tools as they're proposed for use
- Schedule domain reviews for high-risk tools quarterly
- Run annual profile reassessment
- Use Dashboard for status reporting to leadership

### Recommended Roles & Responsibilities

| Role | Workbook Responsibility | Key Sheets |
|------|------------------------|-----------|
| **Program Manager** | Owns overall workflow; tracks status; schedules reviews | Dashboard, Monitoring |
| **Business Owner** | Defines tool use case and data classification | AI Inventory (Columns B-E) |
| **Technical Owner** | Documents architecture, integrations, logging | AI Inventory (Columns F-H) |
| **IT Security Lead** | Oversees review process; validates risk tier; recommends approval | All sheets; Risk Assessment |
| **Privacy Officer** | Reviews data handling and DPA status | Data & Privacy |
| **Legal / Compliance** | Reviews contractual terms and governance obligations | Legal & Compliance |
| **ITGC Chair** | Final approval for High/Critical risk tools | Approval Workflow |
| **Security Analyst** | Evaluates vendor security controls | Vendor & Security |

---

## Key Concepts

### The Five AI Capabilities

Your governance approach depends on what the AI system *does*:

| Capability | What It Is | Risk Profile | Example |
|------------|-----------|--------------|---------|
| **Generative AI** | Creates new content (text, code, images) from prompts | Medium-High | ChatGPT, Claude, DALL-E, code generation |
| **Agentic AI** | Takes actions: calls tools, executes workflows, triggers processes | High | AI that automatically sends emails, updates records, or modifies systems |
| **Embedded AI** | AI feature built into an existing SaaS application | Medium | Copilot in Microsoft 365, AI in Slack, Salesforce Einstein |
| **AI APIs & Integrations** | Your system calls an AI model API as a component | Medium | Integrating OpenAI API into your workflow; RAG systems; AI connectors |
| **Internal Deployments** | Your organization hosts the model internally | Medium | Custom ML models, internal chatbots, data science pipelines |

**Why it matters:** Agentic AI is riskier than Generative AI (because actions have consequences). Embedded AI is less risky (because the host app already went through vetting). This determines your oversight model.

### The Four Risk Ratings

The workbook calculates risk in layers:

1. **Inherent Risk Tier** (from AI Inventory)
   - Determined by: Data Classification (Public/Internal/Confidential/Sensitive) + PII/IP flags
   - This is what's knowable at intake before any controls are evaluated
   - Example: "This tool processes Sensitive data → Inherent Risk = High"

2. **Validated Risk Tier** (from Risk Assessment)
   - Inherent Risk, potentially escalated based on harm assessment + AI capability
   - Never downgrades, only escalates
   - Escalation rules: Safety harm = Critical; Agentic + Third-party risk = High; Generative AI floor = Moderate minimum
   - Example: "Inherent Risk is High, but the tool was flagged for Data Poisoning and is Agentic → Validated Risk = Critical"

3. **Domain Risk Ratings** (from Security, Privacy, Legal, Compliance sheets)
   - Each domain evaluates independently based on its own evidence
   - Vendor Risk Rating = function of security control evidence
   - Privacy Risk Rating = function of data handling + DPA status
   - Legal Risk Rating = function of IP/contract terms
   - Example: "Vendor looks good (Vendor Risk = Low), Privacy looks good (Privacy Risk = Moderate), but Legal found missing IP terms (Legal Risk = High)"

4. **Overall Risk Rating** (from Risk Assessment)
   - The highest of: Validated Risk Tier, Vendor Risk Rating, Privacy Risk Rating, Legal Risk Rating
   - This is the "real" risk after all domain evidence is in
   - Example: "Overall Risk Rating = Critical (driven by Legal)" — meaning Legal governance is the current bottleneck

**Key insight:** Inherent Risk and Overall Risk Rating can diverge significantly. That's by design. If a tool's Overall Risk Rating is High while Inherent Risk is Low, one of the domain reviews is pulling it up. The workbook identifies which one (Risk Drivers field), so you know where to focus remediation.

### The 20 AI RMF Profiles

Profiles pre-package governance expectations for recurring categories of AI use. They define:
- Expected Risk Tier
- Oversight model (who reviews)
- Approval Authority (who approves)
- Reassessment frequency

**Sample profiles (see Governance Procedure Appendix C for all 20):**

| Profile | Use Case | Oversight Model | Approval Authority | Reassessment |
|---------|----------|-----------------|-------------------|--------------|
| **P1** | Foundation models (GPT, Claude, etc.) for general productivity | IT Security, Privacy, Legal | ITGC | Quarterly |
| **P3** | Internal training data, limited audience, non-production | IT Security | IT Security | Annually |
| **P5** | Customer-facing systems, external commitments | IT Security, Privacy, Legal, Business Owner | ITGC | Quarterly |
| **P10** | Data science, analytics, models with no live action | IT Security, Privacy | IT Security | Annually |
| **P19** | Synthetic/generated media (not real people) | IT Security, Privacy, Legal | ITGC | Quarterly |
| **P20** | Synthetic/generated media (real people) | IT Security, Privacy, Legal, Comms | ITGC | Monthly |

**How they work:** When you assign a tool to a profile, the workbook automatically populates that tool's Risk Tier, Approval Authority, and Reassessment Frequency from the profile. If your domain reviews disagree with the profile's tier, that gap is flagged (*Review vs Profile* column), and you investigate.

---

## How to Use These Files Together

### The Workflow

```
1. GOVERNANCE DESIGN (Procedure)
   ↓
   Business and IT leadership define the AI governance policy, 
   roles, and approval gates using the Governance Procedure.
   
2. TOOL REGISTRATION (Workbook - AI Inventory)
   ↓
   Business Owner proposes an AI tool. 
   Technical Owner documents how it works.
   System auto-assigns a Profile and calculates Inherent Risk.

3. PARALLEL DOMAIN REVIEWS (Workbook - 4 sheets)
   ↓
   Privacy, Security, Legal, Risk & Harm teams evaluate independently:
   - Does Privacy approve data handling?
   - Does Security approve vendor controls?
   - Does Legal approve IP/liability terms?
   - Are there unacceptable harm risks?

4. RISK RECONCILIATION (Workbook - Risk Assessment)
   ↓
   System escalates Inherent Risk based on harm + AI capability.
   System compares Validated Risk Tier against each domain rating.
   Overall Risk Rating = highest of all four.

5. APPROVAL DECISION (Workbook - Approval Workflow)
   ↓
   IT Security leads the decision.
   If Inherent Risk is High/Critical, must go to ITGC.
   Once approved: tool is registered in Authorized AI Systems Catalog.

6. ONGOING MONITORING (Workbook - Monitoring)
   ↓
   Reassessment scheduled based on Profile + Risk Tier.
   Overdue reviews flagged on Dashboard.
   Incidents reported; escalated if AI-specific.

7. ANNUAL REVIEW (Procedure + Workbook)
   ↓
   Profiles, risk thresholds, and escalation rules reviewed.
   High-risk tools re-validated.
   Program metrics reported to leadership.
```

### Adapting for Your Organization

**The Governance Procedure is your policy template.** Customize it by:
- Replacing "[the Organization]" placeholders with your actual organization name
- Adjusting the 20 profiles to match your actual use cases (you may use only 5-10)
- Adding your own approval authorities and ITGC structure
- Tailoring incident escalation categories to your incident response process
- Adding specific data retention or compliance requirements (e.g., regulated data handling)

**The Workbook is your operational system.** Customize it by:
- Renaming/reordering profiles to match your final list
- Adding domain-specific columns if needed (e.g., "Regulatory Standard" for legal)
- Adjusting the threshold at which tools escalate to ITGC (default is High/Critical)
- Modifying the escalation logic if your harm taxonomy is different

**The Technical Reference is your maintenance manual.** Use it to:
- Understand any formula before modifying it
- Document your customizations for future maintainers
- Test changes before deploying to production

---

## Requirements & Prerequisites

### To Implement

**Minimum Requirements:**
- Excel 2016 or later (or Google Sheets equivalent)
- Markdown editor or viewer (for Procedure and Reference Guide)
- Cross-functional team: IT Security lead, Privacy officer, Legal counsel, Technical leads, Business owners
- Executive sponsor (ITGC chair or CIO)

**Recommended Setup:**
- SharePoint or OneDrive for centralized workbook access with version control
- Slack/Teams integration for approval notifications
- Monthly governance committee meetings
- Quarterly dashboard review with leadership

### Skills Needed

**To operate the workbook:**
- Basic Excel: sorting, filtering, understanding formulas
- Ability to read and apply governance rules
- Domain expertise: Security, Privacy, Legal, or Risk Assessment

**To customize/maintain:**
- Advanced Excel: INDEX/MATCH, SEARCH, nested IF statements
- Understanding of risk frameworks (NIST, ISO 42001, etc.)
- Governance process design

### Time Investment

**First deployment:** 2-4 weeks
- Week 1: Leadership alignment on Procedure
- Week 2: Customize workbook to your profiles
- Week 3: Train stakeholders and intake first tools
- Week 4: Complete first round of domain reviews and approvals

**Ongoing:** 5-10 hours/month
- Monthly intake of new tools
- Coordination of domain reviews
- Dashboard updates and status reporting
- Reassessment scheduling and follow-up

---

## What's Included in This Toolkit

| File | Type | Purpose | Audience |
|------|------|---------|----------|
| **Governance Procedure** | Markdown (88 KB) | Policy document; mandatory review process; role definitions; risk definitions | Leadership, IT Security, Compliance, Domain Experts |
| **Risk Assessment Workbook** | Excel (92 KB) | Operational system of record; intake, review, approval, monitoring | Day-to-day users: Business Owners, Technical Owners, Domain Experts, Program Managers |
| **Technical Reference** | Markdown (66 KB) | Formula specifications; architecture explanation; test scenarios | Spreadsheet maintainers, Auditors, Advanced users |

**All files sanitized:** References to specific organizations and individuals have been replaced with generic placeholders. Files are ready to share, template, and adapt.

---

## Common Questions

### "Can I just use the workbook without the procedure?"
Not recommended. The workbook implements the Procedure—they're designed together. Use the Procedure to define your governance policy, then operationalize it through the workbook. If you skip the Procedure, you lose the governance framework that makes the workbook meaningful.

### "Do I need to use all 20 profiles?"
No. The toolkit includes 20 profiles as reference. Most organizations use 5-10. Review Appendix C, select the ones that match your use cases, delete the rest. The Profile Selection logic will still work.

### "What if our organization's risk tolerance is different?"
The escalation logic (when tools move from Low → Moderate → High → Critical) is configurable. See Section 7 of the Technical Reference for how the formulas work, then customize the thresholds to match your risk tolerance. Document your changes.

### "Can we integrate this with our existing IT risk management system?"
The workbook is self-contained and can operate independently. But the Overall Risk Rating can feed into a broader IT risk register if you export it. The Risk Assessment sheet provides all the data needed for integration.

### "How do we handle AI tools that are already in use?"
Import them into the AI Inventory and process them through the normal review workflow retroactively. This is a "shadow AI" remediation. High/Critical tools should be reviewed and approved within 30 days; Medium tools within 60 days.

### "What if a domain expert doesn't approve?"
The tool is not approved. It's either remediated (controls added, evidence provided) and re-reviewed, or a risk treatment decision is made (accept, mitigate, transfer, avoid). Document the decision on the Risk Treatment form (Appendix F in Procedure).

---

## Next Steps

### 1. **Immediate (This Week)**
   - [ ] Read the Governance Procedure (pages 1-20)
   - [ ] Review the 5 AI capabilities and 20 profiles (Appendix C)
   - [ ] Identify your governance leads (IT Security, Privacy, Legal)

### 2. **Short Term (Weeks 2-4)**
   - [ ] Customize the Procedure for your organization
   - [ ] Adapt the workbook profiles to your actual use cases
   - [ ] Define your ITGC structure and approval authorities
   - [ ] Identify all AI tools currently in use (inventory effort)

### 3. **Implementation (Month 2)**
   - [ ] Train your governance committee on the procedure and workbook
   - [ ] Load existing tools into AI Inventory
   - [ ] Assign each to a Profile
   - [ ] Process through domain reviews and approvals

### 4. **Operational (Ongoing)**
   - [ ] Establish monthly intake process for new tools
   - [ ] Schedule domain reviews based on risk tier and profile
   - [ ] Monthly governance committee meetings to review status
   - [ ] Quarterly dashboard review with leadership
   - [ ] Annual profile review and risk threshold reassessment

---

## Support & Further Reading

### References
- **NIST AI Risk Management Framework (AI RMF) 1.0**: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf
- **NIST AI RMF Playbook**: https://airc.nist.gov/AI_RMF_Knowledge_Base/Playbook
- **ISO/IEC 42001** (AI Management Systems): https://www.iso.org/standard/81230.html
- **NIST Cybersecurity Framework 2.0**: https://nvlpubs.nist.gov/nistpubs/cswp/NIST.CSWP.29.pdf

### How to Modify the Workbook
The Technical Reference Guide (File 3) provides cell-level documentation of every formula. To modify:
1. Identify the sheet and cell in question
2. Read Section 6 of the Technical Reference for that sheet
3. Understand the formula logic and its dependencies
4. Test your change using the test scenario matrix (Section 7)
5. Document your modification with a date and reason

### Troubleshooting
If formulas look wrong or inconsistent:
1. Check that all tools have an AI ID (AI Inventory column A)
2. Verify that domain review sheets use the correct AI ID to look up data
3. Ensure no calculated cells were manually overwritten
4. Compare your result against the test scenario matrix in Section 7 of the Technical Reference

---

## Version History

| Version | Date | Summary |
|---------|------|---------|
| **1.0** | Aug 2026 | Initial release: NIST AI RMF 1.0 aligned governance procedure, Excel workbook (12 sheets), and technical reference guide. All core functionality complete: 5 AI capabilities, 20 profiles, 4 parallel domain reviews, escalation logic for Generative/Agentic AI, Dashboard reporting. |
| **1.1** (Future) | TBD | Planned: (1) Integration with IT risk register, CMDB, and procurement database. (2) An AI Agent built in Copilot Studio to help with all steps under a single interface.

---

## License & Usage

These materials are provided as a template for implementing AI governance. You are free to:
- ✅ Use, customize, and deploy in your organization
- ✅ Adapt to your governance structure and risk tolerance
- ✅ Share with your governance committee and stakeholders
- ✅ Version-control and modify as your program matures

You are asked to:
- ℹ️ Retain attribution to the original design (see Document Provenance section in Technical Reference)
- ℹ️ Maintain the NIST AI RMF 1.0 alignment as you customize
- ℹ️ Document your modifications for future maintainers

---

## Questions or Feedback?
Toolkit developed by a cyber security leader with extensive experience in AI, compliance engineering, IT, and governance.

If you have questions:
1. **On governance procedure:** Review Appendices A-C in the Governance Procedure and Section 3 of the Technical Reference
2. **On workbook operation:** See Section 5 (Sheet Specifications) and Section 6 (Formula Explanations) in the Technical Reference
3. **On risk calculations:** See Section 7 (Deep Dives) in the Technical Reference; cross-reference to the test scenario matrix
4. **On customization:** Document your changes and maintain the Technical Reference alongside your customizations

---

## Getting Started Checklist

- [ ] All team members have access to the three files
- [ ] Leadership has reviewed and approved the Procedure
- [ ] Roles and responsibilities have been assigned (see Governance Procedure, page X)
- [ ] Profiles have been selected/customized (Governance Procedure, Appendix C)
- [ ] Approval authorities have been defined (Governance Procedure, page X)
- [ ] ITGC structure and escalation paths are clear
- [ ] First set of AI tools to assess has been identified
- [ ] Domain experts are trained on their review responsibilities
- [ ] Workbook has been loaded with baseline tool inventory
- [ ] First tool has been taken through the complete review-to-approval workflow
- [ ] Dashboard has been configured for leadership reporting
- [ ] Monthly intake process has been scheduled
- [ ] Quarterly ITGC reviews are on the calendar

---

**You're ready to implement AI governance aligned to NIST AI RMF 1.0. Start with the Governance Procedure, operationalize through the Workbook, and use the Technical Reference as your ongoing guide.**

Good luck! 🚀
