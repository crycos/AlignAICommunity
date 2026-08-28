# AI Governance Procedure: Agentic & Generative AI Tool Review

*Aligned to NIST AI RMF 1.0 | Govern - Map - Measure - Manage*

## **Purpose**

This procedure is used to evaluate, classify, approve, register, monitor, and govern AI tools to ensure security, compliance, and responsible use within the Organization. It applies to all AI tools regardless of deployment type and defines the mandatory governance steps required before any AI tool may be used for the organization business purposes.

The procedure is aligned to the NIST AI Risk Management Framework 1.0, which is intended to help organizations incorporate trustworthiness considerations into the design, development, use, and evaluation of AI systems. This procedure operationalizes the AI RMF Govern, Map, Measure, and Manage functions through required intake, classification, assessment, control evaluation, approval, registration, monitoring, enforcement, reporting, and annual review activities.

## **Scope**

It applies to all Agentic and Generative AI tools, including internal deployments, SaaS-based tools, embedded AI features, and API-based integrations, used for any the organization business purpose.

### ** Key Requirements**

- Only approved AI tools may be used for the organization business purposes.

- All approved tools must be recorded in the Authorized AI Systems Catalog prior to production use.

- Tools processing Sensitive, Confidential, or regulated data require mandatory ITGC approval.

- High and Critical risk AI tools require an IT Security recommendation, a documented risk treatment decision, and formal risk acceptance where residual risk remains.

### **In-Scope AI Capabilities**

|  |  |
| --- | --- |
| **AI Capability** | **Examples** |
| Generative AI | Text generation, summarization, document analysis, code generation, image generation |
| Agentic AI | Systems that take actions, call tools, orchestrate workflows, or execute multi-step tasks |
| Embedded AI | AI features inside existing SaaS, productivity, security, analytics, HR, legal, engineering, or laboratory applications |
| AI APIs and Integrations | External model APIs, plugins, connectors, retrieval augmented generation, AI copilots |
| Internal AI Deployments | Internally hosted models, custom AI workflows, internal chatbots, data science models |

## **Governance and Roles**

The following roles and responsibilities govern the AI tool review and approval process. Responsibilities are mapped to the AI RMF function they primarily support.

| **Role** | **Responsibility** | **AI RMF Function** |
| --- | --- | --- |
| IT Security | Leads the review process, performs risk classification, validates controls, documents risk, and recommends the approval disposition. | Govern, Measure, Manage |
| Business Owner | Defines the intended use case, provides data classification input, and owns ongoing compliance with the approved scope. | Govern, Map, Manage |
| Technical Owner | Documents architecture, integrations, access model, logging, and system dependencies. | Map, Measure |
| Legal / Compliance | Reviews regulatory obligations, contractual terms, records requirements, and legal exposure. | Govern, Map, Manage |
| Privacy | Reviews PII and Sensitive data handling, retention, residency, consent, and data protection terms. | Map, Measure, Manage |
| Procurement | Executes the IT Data Risk Assessment (ITDRA) for third-party AI tools. | Govern, Measure |
| IT Governance Committee (ITGC) | Provides mandatory approval for all High and Critical risk AI tools and reviews formal risk acceptance. | Govern, Manage |
| AI Governance Committee (where established) | Reviews enterprise AI posture, exceptions, metrics, and program maturity. | Govern, Manage |

## **Definitions and Acronyms**

The following terms are used throughout this procedure. Where a term is also defined in the the organization AI Policy or IT Risk Assessment Standard, that definition prevails.

|  |  |
| --- | --- |
| **Term** | **Definition** |
| AI System | Any system that uses machine learning, statistical models, or generative models to produce outputs such as predictions, recommendations, content, or actions. |
| Generative AI | An AI system that produces new content such as text, code, images, or audio in response to a prompt. |
| Agentic AI | An AI system that plans and executes multi-step tasks, calls tools or APIs, and can take actions on other systems. |
| Shadow AI | Any AI tool used for the organization business purposes that has not been reviewed and registered through this procedure. |
| Hallucination | Output that is fabricated or unsupported by the underlying data yet presented as factual. |
| Prompt Injection | An attack in which crafted input causes an AI system to ignore its instructions, disclose data, or take unintended action. |
| Inherent Risk | Risk before the application of controls. |
| Residual Risk | Risk remaining after controls are applied and validated. |
| Risk Treatment | The decision to mitigate, accept, transfer, or avoid an identified risk. |
| Human Oversight | The degree of human review or intervention applied to AI output before action is taken. |
| Authorized AI Systems Catalog | The live register of AI tools approved for the organization business use. |
| AI RMF Profile | A pre-defined implementation of the AI RMF functions for a recurring category of AI use, as defined in **AI RMF Profiles** section. |
| ITDRA | IT Data Risk Assessment, the vendor and data risk evaluation executed with Procurement. |
| ITGC | IT Governance Committee, the approval authority for High and Critical risk AI tools. |
| DPA | Data Processing Agreement executed with a vendor that processes the organization data. |
| PII | Personally identifiable information. |
| PCN | Process Control Network supporting plant and operational technology environments. |



## **NIST AI RMF Lifecycle Alignment**

All AI systems are reviewed using the four AI RMF functions. Each function is embedded in the procedure steps rather than executed as a separate exercise.

|  |  |  |
| --- | --- | --- |
| **AI RMF Function** | **Purpose in This Procedure** | **Procedure Steps** |
| Govern | Establish accountability, ownership, policy compliance, risk tolerance, approval authority, and oversight. | Governance and Roles, Step 1 - Intake and Scoping, Step 5 - Decision and Approval, Step 8 - Enforcement, Step 9 - AI Governance Reporting, Step 10 - Annual Program Review |
| Map | Document context, use case, stakeholders, data, lifecycle status, integrations, oversight model, and potential impacts. | Step 1 - Intake and Scoping, Step 2 - Risk Classification (Mandatory Logic), Step 3 - Risk Assessment, Step 6 - Registration |
| Measure | Evaluate AI risks, controls, trustworthiness characteristics, evidence, and residual risk. | Step 3 - Risk Assessment, Step 4 - Control and Trustworthiness Evaluation, Step 7 - Monitoring and Reassessment |
| Manage | Treat risks, decide approval, set conditions, monitor, reassess, enforce, report, and improve. | Step 5 - Decision and Approval, Step 6 - Registration, Step 7 - Monitoring and Reassessment, Step 8 - Enforcement, Step 9 - AI Governance Reporting, Step 10 - Annual Program Review |

## **End-to-End Review Process**

The review process consists of ten sequential steps. Each step must be completed before proceeding to the next.

|  |  |  |  |
| --- | --- | --- | --- |
| **#** | **Step** | **Owner** | **Key Output** |
| 1 | Intake and Scoping | Requester / Business Owner / IT Security | Request logged; impact assessment completed; inventory entry created with status Pending Review |
| 2 | Risk Classification | IT Security | Final risk tier: Low, Moderate, High, or Critical |
| 3 | Risk Assessment | IT Security / Procurement / Privacy / Legal | Risk assessment report; harms documented; mitigations defined |
| 4 | Control and Trustworthiness Evaluation | IT Security / Technical Owner | Control gaps identified; trustworthiness characteristics evidenced |
| 5 | Decision and Approval | IT Security / ITGC | Approval outcome, conditions, risk treatment, and risk acceptance documented |
| 6 | Registration | IT Security / Business Owner | Tool entered in the Authorized AI Systems Catalog |
| 7 | Monitoring and Reassessment | IT Security / Business Owner | Ongoing compliance; reassessment as triggered |
| 8 | Enforcement | IT Security / Management | Unapproved use addressed; exceptions governed |
| 9 | AI Governance Reporting | IT Security / AI Governance | Quarterly AI governance metrics reported |
| 10 | Annual Program Review | IT Security / ITGC | Annual program review and procedure updates |



### **Step 1 - Intake and Scoping**

The requesting business unit or individual submits a formal AI tool request. Intake establishes the factual record required for AI RMF Map activities and for all downstream classification, assessment, approval, and monitoring steps.

#### **Required Inputs**

|  |  |
| --- | --- |
| **Required Input** | **Requirement** |
| Business use case and purpose | Intended business purpose, expected benefit, and the specific use case for which approval is sought. |
| Requester and owners | Named requester, Business Owner, Technical Owner, and accountable risk owner. |
| User scope | Enterprise-wide, limited pilot group, function, site, region, or named users. |
| AI system type | LLM, Agentic, predictive, classification, computer vision, NLP, embedded AI, or AI-assisted automation. |
| Lifecycle status | Proposed, Pilot, Production, Suspended, or Retired. |
| Data classification | Highest classification the tool will access or process: Public, Internal, Confidential, or Sensitive. |
| Data processed | Specific data categories, including prompts, uploaded documents, source code, engineering and laboratory data, financial, HR, legal, customer, supplier, and intellectual property. |
| PII and protected data | Whether PII, employee data, customer data, or other regulated or protected information may be processed. |
| Integration details | Internal systems, APIs, plugins, repositories, identity providers, external connections, and automation capabilities. |
| Vendor information | Vendor name, hosting model, retention and data use terms, subprocessors, DPA status, and available assurance reports. |
| Human oversight model | Human-In-The-Loop, Human-On-The-Loop, or Human-Out-Of-The-Loop. |
| Known limitations | Failure modes, hallucination risk, prohibited uses, and situations where output must not be relied upon without validation. |



#### **AI Impact Assessment**

The requester must complete the following assessment. An affirmative response does not automatically reject a tool, but it informs risk classification and may require additional review or evidence.

|  |  |  |
| --- | --- | --- |
| **Impact Area** | **Required Question** | **Response** |
| Stakeholders | Who are the intended users and which groups may be affected by the outputs? | Narrative |
| People impact | Could outputs affect employees, candidates, customers, suppliers, or contractors? | Yes / No / N/A |
| Decision impact | Could the system recommend, prioritize, or automate decisions affecting operations, finance, legal matters, employment, access, or eligibility? | Yes / No / N/A |
| Operational impact | Could inaccurate or unavailable outputs disrupt manufacturing, laboratory, IT, OT, security, finance, or compliance activities? | Yes / No / N/A |
| Safety impact | Could the system influence physical or process safety, environmental controls, OT and PCN operations, or emergency response? | Yes / No / N/A |
| Regulatory impact | Could the tool create obligations under GDPR, NIS2, SOX, privacy law, export control, or contractual commitments? | Yes / No / N/A |
| Confidentiality and IP | Could prompts, outputs, uploads, or logs expose Confidential or Sensitive data, source code, formulations, or trade secrets? | Yes / No / N/A |
| Bias and fairness | Could the system produce biased, unfair, misleading, or harmful outputs where people are evaluated or prioritized? | Yes / No / N/A |
| Misuse potential | Could the tool be misused for unauthorized automation, data extraction, or policy violations? | Yes / No / N/A |
| Third-party reliance | Does the organization rely on an external model, API, subprocessor, or hosting environment outside the organization control? | Yes / No / N/A |



#### **Outputs**

- AI tool request formally logged in the IT intake system.

- Tool added to the AI inventory with status Pending Review.

- Candidate AI RMF Profile assigned per **AI RMF Profiles: Profile Summary** to establish default controls and oversight expectations.

- Preliminary risk triggers identified, including PII, Sensitive or Confidential data, autonomy, safety, and regulatory exposure.

- Required review path identified, including Legal, Privacy, Procurement, Compliance, or ITGC involvement.

### **Step 2 - Risk Classification (Mandatory Logic)**

Risk classification follows deterministic logic applied in sequence. If a trigger is identified at any stage, classification is finalized at that level and the tool is escalated accordingly.

#### **Automatic Escalation (First Gate)**

|  |  |  |
| --- | --- | --- |
| **Condition** | **Result** | **Required Action** |
| Processes PII or Sensitive data by default | Critical | ITGC approval, Privacy review, and formal risk acceptance |
| Handles Confidential or regulated data, including financial, employee, legal data, or intellectual property | High | ITGC approval and formal risk acceptance |
| Performs automated decisions affecting individuals or operations | Critical | ITGC approval and Legal review |
| Influences safety, laboratory, manufacturing, environmental, or OT and PCN operations | Critical | ITGC approval and operational safety review |
| Performs autonomous or agentic actions without human approval | High or Critical | Human oversight classification and ITGC approval |
| External AI with unclear data handling or retention practices | High | ITGC approval and vendor controls assessment |
| Regulatory exposure present, including GDPR, NIS2, or SOX | High | ITGC approval and compliance validation |
| Customer-facing, supplier-facing, or externally exposed | High | Security, Privacy, Legal, and business review |



*Rule: if any condition above is met, classification is set at the indicated tier or higher. Stop and escalate. No further scoring is required to establish the minimum tier.*

#### **Base Classification (If No Automatic Triggers Apply)**

|  |  |  |
| --- | --- | --- |
| **Risk Tier** | **Data Profile** | **Use Case Profile** |
| Low | Public or non-sensitive data only | No system integration and no decision impact |
| Moderate | Internal data only, no PII and no Confidential data | Supports business processes but not critical decisions |
| High | Confidential or regulated data, or intellectual property | Influences operations, decisions, or individuals |
| Critical | Sensitive data, or high-impact decision authority | Affects people, safety, regulated outcomes, or acts autonomously |



#### **Impact and Control Validation (Final Adjustment)**

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **Factor** | **Low** | **Moderate** | **High** | **Critical** |
| Business impact | Minimal or negligible | Operational or financial impact | Significant financial, regulatory, or reputational damage | Enterprise, safety, or material legal impact |
| Data exposure risk | Non-sensitive, limited exposure | Internal exposure possible | Confidential, IP, or regulated data exposure | Sensitive data or significant PII exposure |
| Control effectiveness | Strong and proven controls | Moderate controls, gaps exist | Weak, unverified, or absent controls | Controls absent or bypassable |
| Likelihood of misuse | Low | Possible | High or difficult to prevent | Likely, with broad exposure |
| Autonomy | No action capability | Advisory only | Triggers workflows with human review | Acts without prior human approval |
| Human impact | None | Limited and indirect | Affects employees, customers, or suppliers | Affects employment, safety, access, or legal rights |



*Rule: if any factor trends High or Critical, escalate the classification accordingly regardless of the base result, unless IT Security documents verified controls and residual risk supporting a lower tier.*

#### **Final Risk Decision**

|  |  |  |
| --- | --- | --- |
| **Risk Tier** | **Approval Authority** | **Additional Requirement** |
| Low | IT Security | Catalog registration and approved use case |
| Moderate | IT Security and Business Owner | Risk assessment and monitoring expectations documented |
| High | Mandatory ITGC approval | IT Security recommendation, treatment plan, and documented residual risk |
| Critical | Mandatory ITGC approval with Legal, Privacy, and Compliance review | Formal risk acceptance, human oversight controls, and enhanced monitoring |



Step 2 Process Flow

### **Step 3 - Risk Assessment**

Following risk classification, a formal risk assessment is performed in alignment with the the organization IT Risk Assessment Standard, including likelihood and impact evaluation per the the organization risk scoring methodology.

#### **Required Risk Categories**

|  |  |  |
| --- | --- | --- |
| **Risk Category** | **Description** | **Minimum Evidence** |
| Data leakage and disclosure | Prompts, uploads, outputs, logs, or vendor systems expose company data. | Data flow, classification, retention and deletion terms |
| Prompt injection and adversarial input | Crafted inputs manipulate behavior, bypass controls, or cause unintended action. | Guardrails, abuse testing, monitoring |
| Hallucination and incorrect output | AI generates inaccurate or fabricated information that users rely upon. | Validation process, user guidance, review requirements |
| Unauthorized data retention | Vendor retains, trains on, or reuses the organization data. | Contract terms, DPA, vendor documentation |
| Model drift and degradation | Behavior or quality changes over time. | Change notification, monitoring approach, review cadence |
| Data poisoning | Training, retrieval, or reference data is manipulated. | Source validation, access control, change control |
| Model theft or extraction | Model, prompts, embeddings, or proprietary logic are extracted. | Access control, rate limiting, contractual protection |
| Overreliance and automation bias | Users accept output without adequate review. | Human oversight model, training, disclaimers |
| Bias and harmful output | Unfair, skewed, or discriminatory results. | Bias assessment, human review, prohibited uses |
| Third-party and value chain risk | Vendor hosting, APIs, subprocessors, and components. | ITDRA, SOC 2 or ISO evidence, subprocessor review |
| Information security risk | Unauthorized access, insecure integration, or privilege misuse. | Architecture review, MFA, RBAC, logging, patching |
| Privacy risk | Improper processing, retention, or exposure of PII or Sensitive data. | Privacy review, DPA, retention controls |
| Regulatory and legal risk | Noncompliance with law, contract, or records obligations. | Legal and Compliance review, regulatory mapping |



#### **Harm Assessment**

|  |  |
| --- | --- |
| **Harm Type** | **Assessment Requirement** |
| Individual harm | Whether outputs could affect a person, employee, candidate, customer, supplier, or contractor. |
| Organizational harm | Financial, operational, security, legal, compliance, and reputational impact. |
| Safety harm | Whether outputs could affect physical or process safety, environmental controls, or emergency response. |
| Regulatory harm | Whether the tool could create noncompliance or reporting obligations. |
| Confidentiality harm | Whether Confidential or Sensitive information, IP, formulations, or source code could be exposed. |
| Information integrity harm | Whether misleading outputs could enter records, reports, or business decisions. |



#### **Outputs**

- Completed risk assessment report with inherent risk, controls, residual risk, and named risk owner.

- Defined list of mitigation controls and remediation actions required prior to approval.

- Determination of whether a risk register entry and formal risk acceptance are required.

- IT Security recommendation for approval, conditional approval, rejection, or deferral.

### **Step 4 - Control and Trustworthiness Evaluation**

Controls must be evaluated and validated across the domains below before a recommendation can be made. The original control domains are retained and mapped to the AI RMF trustworthiness characteristics.

#### **Control Domains**

|  |  |  |
| --- | --- | --- |
| **Domain** | **Control Objective** | **AI RMF Characteristic** |
| Transparency | Documentation of model behavior, explainability, and data and model provenance. | Accountable and Transparent; Explainable and Interpretable |
| Bias and Fairness | Bias detection mechanisms and fairness testing in place. | Fair with Harmful Bias Managed |
| Accountability | Defined ownership, usage logging, and full auditability. | Accountable and Transparent |
| Privacy | Encryption at rest and in transit, anonymization, retention, and consent management. | Privacy Enhanced |
| Security | Vulnerability management, RBAC, adversarial testing, and access controls. | Secure and Resilient |
| Compliance | Alignment with GDPR, NIS2, SOX, and NIST CSF. | Accountable and Transparent |
| Ethical Use | Defined and limited purpose with safeguards against misuse or harm. | Safe |
| Reliability | Accuracy, expected performance, and documented limitations. | Valid and Reliable |
| Human Oversight | Documented oversight model appropriate to the impact of the use case. | Safe; Accountable and Transparent |



#### **Trustworthiness Assessment**

|  |  |  |
| --- | --- | --- |
| **Characteristic** | **Evidence Expected** | **Result** |
| Valid and Reliable | Testing results, pilot feedback, accuracy review, documented limitations | Met / Gap / N/A |
| Safe | Safety and operational impact review, prohibited uses, oversight model | Met / Gap / N/A |
| Secure and Resilient | MFA, RBAC, encryption, logging, vulnerability and adversarial testing | Met / Gap / N/A |
| Accountable and Transparent | Named owners, approval record, usage logging, catalog entry | Met / Gap / N/A |
| Explainable and Interpretable | Model or system documentation, user guidance, output disclaimers | Met / Gap / N/A |
| Privacy Enhanced | DPA, retention terms, minimization, residency, deletion rights | Met / Gap / N/A |
| Fair with Harmful Bias Managed | Bias assessment, human review requirements, restricted use cases | Met / Gap / N/A |



#### **Minimum Evidence by Risk Tier**

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **Evidence Area** | **Low** | **Moderate** | **High** | **Critical** |
| Security review | Basic | Standard | Enhanced | Enhanced with ITGC review |
| Privacy review | If PII possible | If PII possible | Required | Required |
| Legal and Compliance review | If applicable | If applicable | Required | Required |
| Vendor review (ITDRA) | If third party | Required if third party | Enhanced | Enhanced with conditions |
| Trustworthiness assessment | Abbreviated | Required | Required with evidence | Required with evidence and monitoring |
| Human oversight documentation | If applicable | Required if decision support | Required | Required with action controls |
| Risk acceptance | Not required | If residual risk exceeds tolerance | Required for High residual risk | Required |



### **Step 5 - Decision and Approval**

Following completion of the risk assessment and control evaluation, a formal decision must be made and documented.

|  |  |
| --- | --- |
| **Outcome** | **Description** |
| Approved | Tool meets all security, compliance, privacy, and control requirements for the approved use case. |
| Approved with Conditions | Tool is approved subject to completion of specified remediation actions or control enhancements within a defined timeframe. |
| Rejected | Tool presents unacceptable risk that cannot be mitigated to an acceptable level. |
| Deferred | Review cannot proceed because required intake, vendor, privacy, or control evidence is missing. Status remains Pending Review. |

#### **Mandatory Approval Rules**

- High and Critical risk tools require a formal IT Security recommendation and mandatory ITGC approval.

- Risk acceptance must be formally documented for all High and Critical risk tools, regardless of approval outcome.

- Conditional approvals must specify remediation timelines and responsible owners.

- No approval is effective until the tool is registered in the Authorized AI Systems Catalog.

#### **Risk Treatment Decision**

|  |  |  |
| --- | --- | --- |
| **Treatment** | **Description** | **When Used** |
| Mitigate | Implement controls that reduce likelihood or impact. | Risk can be reduced to an acceptable residual level. |
| Accept | Business and approval authority formally accept residual risk. | Residual risk is within tolerance and justified. |
| Transfer | Shift or share risk through contract, insurance, or vendor obligations. | Contractual protections meaningfully reduce exposure. |
| Avoid | Do not use the tool or prohibit a specific use case. | Risk cannot be reduced or accepted. |



Step 5 Process Flow

### **Step 6 - Registration (Mandatory Control)**

Registration in the Authorized AI Systems Catalog is a mandatory control. No AI tool may enter production use prior to registration. Production use before registration constitutes a policy violation.

|  |  |
| --- | --- |
| **Catalog Field** | **Description** |
| Provider | Organization that developed the tool, for example Microsoft. |
| Name | Official name of the AI tool or system, for example Copilot. |
| Purpose | What the tool is used for. |
| Scope | Users approved for the tool, for example global or limited pilot. |
| LLM or Agentic | Type of AI capability. |
| Data processed | Data the tool accesses, processes, or generates. |
| Approved Use Case | Specific documented purpose for which the tool is approved. |
| Approved Data Classification | Public, Internal, Confidential, or Sensitive. |
| Intellectual Property | Yes or No indicator for IP and trade secrets. |
| PII | Yes or No indicator for personal information. |
| Risk Level | Low, Moderate, High, or Critical. |
| Requested By | Named individual accountable for the request. |
| Reviewed By | Person or function that performed the assessment. |
| Approval Date | Date of IT Security or ITGC approval. |
| AI System ID | Unique inventory identifier. |
| Lifecycle Status | Proposed, Pilot, Production, Suspended, or Retired. |
| Business Owner | Accountable business owner. |
| Technical Owner | System or support owner. |
| Assigned Profile | AI RMF Profile assigned per Section **AI RMF Profiles**. |
| Human Oversight | Human-In-The-Loop, Human-On-The-Loop, or Human-Out-Of-The-Loop. |
| Approval Status | Pending Review, Approved, Approved with Conditions, Rejected, Suspended, or Retired. |
| Next Reassessment Date | Next required review based on risk tier. |
| Monitoring Required | Monitoring scope and frequency. |
| Vendor Risk Rating | Outcome of the vendor assessment. |
| Data Residency | Hosting or processing location where applicable. |
| Third-Party Sharing | Whether data is shared beyond the vendor. |
| Incident History | AI-related incidents or none reported. |



### **Step 7 - Monitoring and Reassessment**

All approved AI tools are subject to ongoing monitoring and periodic reassessment proportional to data classification, risk tier, autonomy, and vendor dependency.

#### **Continuous Monitoring**

|  |  |
| --- | --- |
| **Monitoring Area** | **Requirement** |
| Usage and access | Usage tracking and access logging within approved scope. |
| Data exposure | Data exposure monitoring and anomaly detection. |
| Output validation | Output validation and model behavior review. |
| Security events | Alerts for unauthorized access, abuse, and suspicious integrations. |
| Bias and fairness | Monitoring where outputs affect individuals or groups. |
| Drift and change | Vendor model updates, feature changes, and behavior changes. |
| Vendor posture | Contract, DPA, subprocessor, and assurance report changes. |
| Incidents | Incidents, near misses, corrective actions, and lessons learned. |



#### **Review Frequency**

|  |  |
| --- | --- |
| **Risk Tier** | **Minimum Review Frequency** |
| Low | Annual |
| Moderate | Annual |
| High | Semiannual |
| Critical | Quarterly |



#### **Reassessment Triggers**

- Model or vendor changes that may affect the risk profile.

- New regulatory requirements applicable to the tool or its data.

- Security or privacy incidents involving the tool.

- Significant changes to the approved use case or data scope.

- Expansion from pilot to production, or a material increase in user scope.

- Processing of data at a higher classification than previously approved.

#### **Incident Handling**

All AI-related incidents must be reported and handled in accordance with the standard the organization Incident Response process. Categories requiring escalation include the following.

|  |  |  |
| --- | --- | --- |
| **Category** | **Examples** | **Required Action** |
| Data leakage or unauthorized exposure | Sensitive or Confidential data uploaded, PII exposure, unapproved sharing | Incident response, privacy review, containment, reassessment |
| Harmful, biased, or inappropriate outputs | Discriminatory, unsafe, or misleading output | Business Owner review, Legal and Privacy involvement, control update |
| Security compromise or unauthorized access | Account compromise, prompt injection, malicious integration | Incident response, security review, corrective action |
| Unauthorized use | Shadow AI or unapproved data processing | Suspend use, review, register or remove, user communication |



### **Step 8 - Enforcement**

According to the Organization’s AI Policy

- The use of unapproved AI tools for the organization business purposes is strictly prohibited.

- AI tools must not be used to process Sensitive, Confidential, or regulated data unless explicitly approved through the process.

- All approved tools must remain registered in the Authorized AI Systems Catalog.

#### **Shadow AI Handling**

AI tools, applications, or models used outside approved governance and oversight processes are considered **shadow AI**. When such are discovered, the following must take place:

1. Identify and document the tool, users, purpose, and data processed.

1. Stop processing of Sensitive, Confidential, or regulated data pending review.

1. Create an inventory entry with status Pending Review.

1. Perform expedited classification and determine whether to approve, restrict, remediate, or block.

1. Document corrective action, user communication, and lessons learned.

#### **Exception Management**

|  |  |
| --- | --- |
| **Exception Field** | **Requirement** |
| Business justification | Why the exception is needed and the impact if denied. |
| Scope | Tool, users, data, use case, and timeframe covered. |
| Risk owner | Business owner accountable for residual risk. |
| Compensating controls | Controls that reduce risk during the exception period. |
| Expiration date | Exceptions may not be open ended. |
| Approval authority | ITGC approval required where High or Critical risk exists. |



### **Step 9 - AI Governance Reporting**

Given its involvement in review of AI tools and third party data risk assessments (TPDSA), IT Security is capable to maintain AI tools metrics and can report them to ITGC or AI governance stakeholders on a quarterly basis. Reporting provides visibility into AI adoption, risk posture, and remediation progress.

|  |  |
| --- | --- |
| **Metric** | **Purpose** |
| Total AI systems in inventory | Inventory completeness and adoption trend |
| Approved and pending review systems | Governance throughput and backlog |
| High and Critical risk systems | Elevated risk portfolio visibility |
| Systems processing PII or Sensitive data | Privacy and regulatory exposure |
| Systems processing Confidential data | Business sensitivity exposure |
| Vendor-hosted AI systems | Third-party dependency |
| Open remediation actions and conditional approvals | Control gap closure |
| Overdue reassessments | Governance hygiene |
| AI-related incidents | Operational risk and lessons learned |
| Shadow AI discoveries | Unauthorized adoption and training needs |



### **Step 10 - Annual Program Review**

At least annually, IT Security conducts a program level review of AI governance effectiveness and recommends updates to this procedure.

- Inventory completeness and catalog accuracy.

- Effectiveness of classification, assessment, approval, and monitoring controls.

- AI incidents, exceptions, shadow AI discoveries, and remediation trends.

- Changes to NIST AI RMF, the Generative AI Profile, NIST CSF, NIS2, SOX, and privacy requirements.

- Recommended procedure updates, control enhancements, training, and dashboard improvements.

## **Process Summary**

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **#** | **Step** | **Owner** | **Key Output** | **AI RMF Function** |
| 1 | Intake and Scoping | IT Security / Requester | Request logged; tool added to inventory | Map |
| 2 | Risk Classification | IT Security | Risk tier determined | Map |
| 3 | Risk Assessment | IT Security / Procurement | Risk assessment report; mitigations defined | Measure |
| 4 | Control and Trustworthiness Evaluation | IT Security | Control gaps identified; remediation required | Measure |
| 5 | Decision and Approval | IT Security / ITGC | Approval outcome and treatment documented | Manage |
| 6 | Registration | IT Security | Tool entered in Authorized AI Systems Catalog | Govern |
| 7 | Monitoring and Reassessment | IT Security / Business Owner | Ongoing compliance; reassessment as triggered | Manage |
| 8 | Enforcement | IT Security | Policy violations addressed | Govern |
| 9 | AI Governance Reporting | IT Security | Quarterly metrics reported | Govern |
| 10 | Annual Program Review | IT Security / ITGC | Program review and procedure updates | Govern |

*A swimlane view of the process flow*

## **AI RMF Profiles**

An AI RMF Profile is an implementation of the framework functions for a specific setting, application, or use case. The profiles below establish pre-defined expectations for recurring categories of AI use at the organization.

A profile is assigned at intake, under **Step 1 - Intake and Scoping: Outputs**, and sets the starting position for the review: default classification, default risk tier, oversight model, and the control set the reviewer should expect to see evidenced. It does not replace **Step 2 - Risk Classification**; the final risk tier is always confirmed through the classification logic. A profile may be escalated during review but must not be silently downgraded; any reduction requires documented, verified controls and residual risk. Where a tool spans two profiles, the more restrictive profile applies. Where a tool matches no profile, it is reviewed without one, and IT Security determines whether a new profile is warranted.

### Profile Selection

Profile selection is deterministic and uses information already captured in **Step 1 - Intake and Scoping: Required Inputs **and** AI Impact Assessmen**t. Apply the rules in order and stop at the first match. Record the assigned profile and the rule number that produced the match in the intake record and the Authorized AI Systems Catalog.

|  |  |  |  |
| --- | --- | --- | --- |
| **Rule** | **If the intake record shows** | **Source Intake Field** | **Profile** |
| Rule 1 | The system evaluates, ranks, screens, or prioritizes people | Impact Assessment - People impact | P7 |
| Rule 2 | The system clones or replicates a real, identifiable person's voice or likeness | AI system type; Impact Assessment - People impact | P20 |
| Rule 3 | The system supports plant, PCN, process, or laboratory activity | Impact Assessment - Safety impact | P8 |
| Rule 4 | The system acts on other systems, calls tools, or executes workflows | AI system type - Agentic | P5 |
| Rule 5 | Output reaches customers, suppliers, or the public | User scope; Impact Assessment - Stakeholders | P6 |
| Rule 6 | The tool is owned by a specialist function: R&D, Legal, Finance, Security Operations, Procurement, or Marketing | Business Owner function | P9, P10, P11, P12, P15, P14 respectively |
| Rule 7 | The tool is defined by a capability: code assistance, meeting capture, dataset querying, policy question answering, or video/audio generation | Business use case and purpose | P4, P16, P13, P17, P19 respectively |
| Rule 8 | AI is being enabled inside an application that is already approved | Vendor and integration details | P18 |
| Rule 9 | The tool is a time-boxed pilot: Internal data only, no PII or Confidential data, and no production dependency | User scope; Lifecycle = Pilot | P2 |
| Rule 10 | The tool is deployed enterprise-wide within the existing data boundary | User scope - enterprise-wide | P1 |
| Rule 11 | The tool serves a narrow group, one tool or dataset, with no decision impact | User scope and data scope | P3 |
| Rule 12 | No rule above matches | Not applicable | No profile; IT Security determines whether a new profile is warranted |


### Profile Definitions

**P1 Enterprise Productivity Assistant**

A general-purpose assistant deployed broadly and embedded in the tools employees already use daily. Risk comes from breadth of access rather than from a single sensitive use case — the tool inherits whatever the user can already reach.

***How it is used: **Apply when the user population is enterprise-wide and the tool operates inside the existing data boundary. Reviewer focus is on permission hygiene, oversharing, and user guidance rather than on a narrow use case.*

**P2 Evaluation and Proof of Concept**

A time-boxed trial to determine whether a tool has business value, before any production commitment. Risk is contained by keeping scope small and data classification low.

***How it is used: **Apply to any pilot or trial. The reviewer must confirm a defined end date and named participants. When the evaluation concludes, the tool is either re-reviewed under a production profile or retired — a PoC never becomes production by default.*

**P3 Domain and Technical Assistant**

A narrow assistant supporting one tool, dataset, or technical discipline, typically deployed to a small group with specific expertise.

***How it is used: **Apply when both the user group and the data scope are limited and the tool does not make or influence decisions. Reviewer focus is scope creep — verifying the tool is not quietly expanded beyond its approved subject area.*

**P4 Developer and Code Assistant**

AI that generates, reviews, or explains code. Two distinct risks: proprietary source code leaving the environment, and insecure or licensed code entering it.

***How it is used: **Apply to any software development use. Reviewer confirms code review before merge, secret scanning, and license review. Generated code is treated as untrusted input, not as reviewed work product.*

**P5 Agentic Automation**

AI that plans and executes multi-step work, calls tools or APIs, and takes action on systems rather than only producing text. Risk shifts from disclosure to unintended action.

***How it is used: **Apply whenever the system can act, not just advise. Reviewer confirms the action allow list, service identity privilege, logging, and rollback. Privileged or irreversible actions require an explicit human approval gate.*

**P6 Customer or Supplier Facing**

AI whose output reaches parties outside the organization, either directly through interaction or indirectly through generated external content. Errors become external commitments or reputational events.

***How it is used: **Apply when any output leaves the company. Reviewer confirms content boundaries, escalation to a human, and disclosure of AI use where required. Legal review is not optional.*

**P7 People and HR Decision Support**

AI that informs decisions about individuals — recruiting, evaluation, or workforce actions. The highest-consequence category because outcomes affect people's employment.

***How it is used: **Apply whenever a person is evaluated, ranked, screened, or prioritized. Reviewer confirms that a named human holds decision authority, that bias assessment is complete, and that notice obligations are met. Autonomous decisions are prohibited.*

**P8 Operational Technology and Laboratory**

AI supporting plant, process, or laboratory activity, where incorrect output can affect physical or process safety rather than only data.

***How it is used: **Apply to any plant, PCN, or lab use. The tool is advisory only — no write access to control systems, enforced by network segmentation. Engineering validates outputs before they are acted upon.*

**P9 Research and Formulation Support**

AI supporting R&D work, including literature review, experimental design, and formulation activity. Prompts and uploads may contain the company's most valuable intellectual property.

***How it is used: **Apply to R&D and technical research use. Reviewer confirms restrictions on uploading formulations or compositions, IP and export control review, and technical validation of outputs before they inform research direction.*

**P10 Legal and Contract Analysis**

AI that reads contracts and legal material to compare clauses, extract obligations, or support research. Documents are frequently privileged or third-party confidential.

***How it is used: **Apply to Legal and contract workflows. Reviewer confirms privilege protection, that the vendor does not train on submitted documents, and retention limits. All conclusions are reviewed by an attorney or the contract owner.*

**P11 Finance and Reporting Support**

AI touching financial data, close activities, or reporting inputs. May fall inside SOX scope depending on how output is used.

***How it is used: **Apply to Finance workflows. Reviewer confirms no autonomous postings, evidence retention sufficient for audit, and segregation of duties. Where output feeds a SOX-relevant control, the control mapping is documented.*

**P12 Security Operations Assistant**

AI supporting the security team with triage, investigation, log summarization, and detection work. High-volume, and the tool has access to privileged security data.

***How it is used: **Apply to SOC and IR workflows. Triage runs Human-On-The-Loop because per-item approval is impractical at volume; containment escalates to Human-In-The-Loop. Analyst validation is required before any action is taken.*

**P13 Data Analytics and Business Intelligence**

Natural language querying and report generation over business datasets. Risk is that AI-mediated access bypasses established data permissions.

***How it is used: **Apply to BI and analytics use. Reviewer confirms access is aligned to existing data permissions, the data owner has approved, and sources are documented. Results are validated before informing decisions.*

**P14 Marketing and Communications Content**

AI drafting internal or external content, campaigns, and communications. Risk concentrates at the moment of publication.

***How it is used: **Apply to content generation. Reviewer confirms brand and legal review before external release, that no material nonpublic information is used, and that AI-use disclosure and IP or likeness requirements are addressed.*

**P15 Procurement and Vendor Analysis**

AI supporting supplier research, RFP work, spend analysis, and vendor document review. Frequently involves third-party confidential material under NDA.

***How it is used: **Apply to Procurement workflows. Reviewer confirms that NDA or vendor-confidential material is not submitted without approval, and that sourcing conclusions are validated by the buyer with assumptions documented.*

**P16 Meeting Transcription and Summarization**

AI that records, transcribes, and summarizes meetings. Captures unstructured, unfiltered discussion and creates a durable record that did not previously exist.

***How it is used: **Apply to any recording or transcription tool. Reviewer confirms participant notice and consent where required, distribution restrictions, and retention limits. Privileged and HR-sensitive meetings require explicit approval.*

**P17 Training and Knowledge Assistant**

AI answering questions about internal policy, procedure, onboarding, and knowledge base content. The lowest-risk category, but answers carry implied authority.

***How it is used: **Apply to internal knowledge use. The tool must draw only from authoritative sources and cite them, and must not interpret policy beyond the documented text. Reviewer monitors answer accuracy and source drift.*

**P18 Embedded AI Feature in Existing SaaS**

An AI capability switched on inside an application that was already approved. These arrive without a procurement event and would otherwise bypass intake entirely.

***How it is used: **Apply when a vendor enables AI in an existing tool. The feature inherits the host application's classification, with a Moderate minimum. Reviewer confirms the data boundary and tenant configuration before enablement, and re-reviews if classification or scope increases.*

**P19 Synthetic Media Generation**

AI that generates new video or audio — text-to-video, AI presenters, stock avatars, and synthetic (non-real) voiceover. The tool produces polished media from a human's script or source material; the human drives every step. Risk sits in rights and disclosure, not autonomy.

***How it is used: **Apply to video and audio generation that uses synthetic or stock presenters and voices. Reviewer confirms licensing and rights to avatars, faces, and music; that no real identifiable person is reproduced (which escalates to P20); disclosure of AI-generated media where required; and that scripts carry no material nonpublic information.*

**P20 Identity Cloning & Impersonation**

AI that clones or replicates the voice or likeness of a specific, identifiable real person — a cloned voice, a digital twin, or a custom avatar. Because a voiceprint or faceprint is biometric data, this is the most tightly regulated media use and carries consent, right-of-publicity, and deepfake/impersonation risk.

***How it is used: **Apply whenever a tool reproduces a real person. Reviewer confirms written, revocable consent from the individual on file; biometric handling under GDPR and Illinois BIPA with a retention and destruction schedule; restricted, logged, revocable access to the cloned asset; AI-use disclosure or provenance watermark; and prohibited uses (no approvals, financial, legal, or safety instructions issued via a cloned voice). No autonomous generation.*

### Profile Summary 

|  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Profile** | **Typical Use** | **Default Classification** | **Default Risk Tier** | **Human Oversight** | **Approval Authority** |
| **P1 Enterprise Productivity Assistant** | Broadly deployed assistant embedded in enterprise productivity tools | Confidential | High | Human-In-The-Loop for business decisions and external communication | ITGC |
| **P2 Evaluation and Proof of Concept** | Time-boxed evaluation with a limited user group | Internal | Moderate | Human-In-The-Loop | IT Security and Business Owner |
| **P3 Domain and Technical Assistant** | Support for a specific tool, dataset, or technical discipline | Internal | Moderate | Human-In-The-Loop | IT Security and Business Owner |
| **P4 Developer and Code Assistant** | Code generation, review, and software development support | Confidential | High | Human-In-The-Loop with code review | ITGC |
| **P5 Agentic Automation** | AI that executes multi-step tasks, calls tools, or acts on systems | Confidential | High to Critical | Human-In-The-Loop for privileged or irreversible actions | ITGC |
| **P6 Customer or Supplier Facing** | AI that interacts with external parties or generates external content | Confidential | High | Human-In-The-Loop with approved response boundaries | ITGC with Legal review |
| **P7 People and HR Decision Support** | AI supporting recruiting, evaluation, or workforce decisions | Sensitive | Critical | Human-In-The-Loop with documented decision authority | ITGC with Legal and Privacy review |
| **P8 Operational Technology and Laboratory** | AI supporting plant, process, or laboratory activities | Confidential to Sensitive | Critical | Human-In-The-Loop with no autonomous control actions | ITGC with operational safety review |
| **P9 Research and Formulation Support** | R&D support, scientific literature review, experimental design, formulation work | Confidential to Sensitive | High to Critical | Human-In-The-Loop with technical validation of all outputs | ITGC with R&D leadership review |
| **P10 Legal and Contract Analysis** | Contract review, clause comparison, obligation extraction, legal research | Confidential | High | Human-In-The-Loop with attorney or contract owner review | ITGC with Legal review |
| **P11 Finance and Reporting Support** | Financial data analysis, close support, reporting inputs | Confidential | High to Critical | Human-In-The-Loop with reviewer independent of preparer | ITGC with Finance and SOX review |
| **P12 Security Operations Assistant** | Alert triage, investigation support, log summarization, detection engineering | Confidential | High | Human-On-The-Loop for triage; Human-In-The-Loop for containment | IT Security leadership with ITGC notification |
| **P13 Data Analytics and Business Intelligence** | Natural language querying, report generation, analysis over business datasets | Internal to Confidential | Moderate to High | Human-In-The-Loop before results inform decisions | IT Security with data owner approval |
| **P14 Marketing and Communications Content** | Drafting internal or external content, campaigns, communications | Internal to Confidential | Moderate to High | Human-In-The-Loop with brand and legal review before publication | IT Security; ITGC where external facing |
| **P15 Procurement and Vendor Analysis** | Supplier research, RFP support, spend analysis, vendor document review | Confidential | High | Human-In-The-Loop with buyer and Legal review | IT Security with Procurement approval |
| **P16 Meeting Transcription and Summarization** | Recording, transcription, notes, action item generation | Confidential to Sensitive | High | Human-In-The-Loop for accuracy and distribution control | ITGC with Privacy and Legal review |
| **P17 Training and Knowledge Assistant** | Policy, procedure, onboarding, and knowledge base question answering | Internal | Moderate | Human-On-The-Loop with authoritative source citation | IT Security and Business Owner |
| **P18 Embedded AI Feature in Existing SaaS** | AI capability activated inside an already approved application | Inherits host application classification | Inherits, minimum Moderate | Human-In-The-Loop where outputs affect records or decisions | IT Security; ITGC if classification or scope increases |
| **P19 Synthetic Media Generation** | Text-to-video, AI presenters and stock avatars, synthetic voiceover, training and promotional video | Confidential | High | Human-In-The-Loop with brand and legal review before publication | ITGC with Legal review (external-facing); IT Security and Business Owner (internal only) |
| **P20 Identity Cloning & Impersonation** | Cloned voice or likeness of a named real person, digital twins, custom personal avatars, in-voice dubbing | Sensitive | Critical | Human-In-The-Loop with every output reviewed; no autonomous generation | ITGC with Legal and Privacy review; documented consent of the individual on file |



### **Profile Control Expectations**

|  |  |  |  |
| --- | --- | --- | --- |
| **Profile** | **Mandatory Controls** | **Monitoring Focus** | **Review Frequency** |
| **P1 Enterprise Productivity Assistant** | Tenant data boundary, access aligned to existing permissions, audit logging, acceptable use guidance, user training | Data exposure, oversharing, output reliance | Semiannual |
| **P2 Evaluation and Proof of Concept** | Defined end date, named participants, Internal data only, no PII or Confidential data, no production dependency | Scope and classification adherence | At conclusion, or annually |
| **P3 Domain and Technical Assistant** | Restricted user group, limited data scope, documented limitations, no automated decisions | Scope creep, output accuracy | Annual |
| **P4 Developer and Code Assistant** | No Sensitive data in prompts, code review before merge, secret scanning, license and IP review | Source code exposure, insecure suggestions | Semiannual |
| **P5 Agentic Automation** | Least privilege identity, action allow list, approval gate for privileged actions, full action logging, rollback capability | Action logs, privilege use, unexpected actions | Quarterly |
| **P6 Customer or Supplier Facing** | Approved content boundaries, disclosure of AI use where required, escalation path to a human, brand and legal review | Output accuracy, complaints, external disclosure | Quarterly |
| **P7 People and HR Decision Support** | Documented human decision authority, bias assessment, privacy review, retention, notice where required | Bias indicators, overrides, complaints | Quarterly |
| **P8 Operational Technology and Laboratory** | Advisory only, no control system write access, network segmentation, engineering validation of outputs | Output validation, attempted integrations, safety impact | Quarterly |
| **P9 Research and Formulation Support** | No unapproved upload of formulations or compositions; IP and export control review; technical validation before use; restricted user group | Formulation and IP exposure, output accuracy, scope adherence | Quarterly |
| **P10 Legal and Contract Analysis** | Privilege protection; no vendor training on submitted documents; retention limits; attorney or contract owner review of all conclusions | Privileged content exposure, extraction accuracy | Semiannual |
| **P11 Finance and Reporting Support** | No autonomous journal or system postings; evidence retention for audit; segregation of duties; SOX control mapping where in scope | Output accuracy, reliance within controls, audit evidence completeness | Quarterly |
| **P12 Security Operations Assistant** | Least privilege access to logs and cases; no autonomous containment; analyst validation before action; full action logging | Analyst overrides, incorrect conclusions, privileged data access | Quarterly |
| **P13 Data Analytics and Business Intelligence** | Access aligned to existing data permissions; data owner approval; documented data sources; no unapproved dataset uploads | Query scope, data access alignment, output accuracy | Semiannual |
| **P14 Marketing and Communications Content** | Brand and legal review before external release; no material nonpublic information; disclosure of AI use where required; IP and likeness review | External accuracy, disclosure compliance, brand consistency | Semiannual |
| **P15 Procurement and Vendor Analysis** | No vendor confidential or NDA material without approval; sourcing conclusions validated by buyer; documented assumptions | Confidential vendor data exposure, decision quality | Semiannual |
| **P16 Meeting Transcription and Summarization** | Participant notice and consent where required; restricted distribution; retention limits; no recording of privileged or HR-sensitive meetings without approval | Recording scope, distribution, retention, privacy complaints | Quarterly |
| **P17 Training and Knowledge Assistant** | Authoritative source restriction; citation of source policy or procedure; no interpretation beyond documented text | Answer accuracy, source drift, user feedback | Annual |
| **P18 Embedded AI Feature in Existing SaaS** | Feature-level review before enablement; confirmation of data boundary; tenant configuration review; inherits host controls and monitoring | Feature changes, data boundary changes, scope expansion | Aligned to host application, minimum annual |
| **P19 Synthetic Media Generation** | Licensing and rights to stock avatars, faces, and music confirmed; no real identifiable person's voice or likeness (escalate to P20); disclosure of AI-generated media where required; no material nonpublic information in scripts; retention limits on uploaded source material; brand and legal review before external release | Disclosure compliance, unauthorized likeness use, external accuracy, brand consistency, source-material retention | Semiannual; Quarterly if external-facing |
| **P20 Identity Cloning & Impersonation** | Written, revocable consent from the person cloned, held on file (for employees, decoupled from any condition of employment); biometric handling under GDPR and Illinois BIPA with a documented retention and destruction schedule; restricted, logged access to the cloned asset with revoke or delete on demand; AI-use disclosure or provenance watermark on output; prohibited uses defined (no approvals, financial, legal, or safety instructions issued via a cloned voice; anti-vishing safeguards); right-of-publicity review by Legal; defined incident path for misuse or deepfake | Consent status and expiry, access to and use of the cloned asset, misuse or deepfake attempts, disclosure compliance, biometric retention compliance | Quarterly |



### **Example of Profile Assignment for Current Catalog Entries**

|  |  |  |
| --- | --- | --- |
| **AI System** | **Assigned Profile** | **Rationale** |
| Microsoft Copilot | P1 Enterprise Productivity Assistant | Deployed to all employees and approved for Confidential data, with IP and PII processing indicated. |
| Anthropic Claude AI | P2 Evaluation and Proof of Concept | Limited proof of concept group for AI evaluation, approved for Internal data only. |
| <http://CustomGPT.ai>  JMP Learnbot | P3 Domain and Technical Assistant | Limited group using the tool for JMP Pro navigation questions, approved for Internal data only. |



## **References**

- *NIST AI Risk Management Framework 1.0 (NIST AI 100-1)*- Primary AI risk management framework and trustworthiness characteristics
- *NIST AI 600-1 Generative AI Profile*- Generative AI specific risk considerations and actions
- *the organization IT Risk Assessment Standard *- Risk evaluation methodology and likelihood and impact scoring model
- *the Organization AI Policy*- Authorized AI usage definitions and data handling requirements
- *Authorized AI Systems Catalog* - Live register of approved AI tools

### **Appendix A - Risk Classification Table**

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **Risk Tier** | **Definition** | **Key Criteria** | **Impact** | **Governance Requirement** |
| Low | Minimal risk exposure | Public data, no integration, no decision impact | Negligible | IT Security approval |
| Moderate | Moderate risk exposure | Internal data, limited integration, process influence | Operational or reputational impact | IT Security and Business Owner approval |
| High | Significant risk exposure | Confidential or regulated data, IP, vendor uncertainty, decision influence | Financial, regulatory, or reputational damage | Mandatory ITGC approval and formal risk acceptance |
| Critical | Severe or high impact exposure | Sensitive data, PII by default, employment, safety, or autonomous action | Material legal, safety, human, or enterprise impact | ITGC approval with Legal and Privacy review, formal risk acceptance, enhanced monitoring |



### **Appendix B - Review Checklist (ITDRA-Aligned)**

The following checklist summarizes the key control objectives reviewed during the AI tool assessment. The official review artifact is the IT Data Risk Assessment (ITDRA) worksheet.

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| **Domain** | **Control** | **Description** | **Score** | **Evidence** |
| General | AI tool catalog entry required | All approved tools must be entered into the Authorized AI Systems Catalog | Yes / No |  |
| General | Business use case defined | Documented and approved business purpose | Yes / No |  |
| General | Profile assigned | An AI RMF Profile is assigned per Section **AI RMF Profiles** | Yes / No |  |
| Risk | Data classification identified | Public, Internal, Confidential, or Sensitive clearly defined | Yes / No |  |
| Risk | Sensitive or PII processing | If yes, High or Critical risk and ITGC approval required | Yes / No |  |
| Risk | ITGC approval | Required for all High and Critical risk AI tools | Yes / No |  |
| Risk | Impact assessment completed | Stakeholder, decision, safety, and regulatory impact documented | Yes / No |  |
| Transparency | Documentation available | Model or system documentation exists | Yes / No |  |
| Transparency | Explainability | Outputs understandable to business users | Yes / No |  |
| Transparency | Data provenance | Training or source data clearly defined | Yes / No |  |
| Bias and Fairness | Bias assessment | Bias testing or review performed | Yes / No |  |
| Bias and Fairness | Fairness metrics | Use of fairness metrics defined where applicable | Yes / No |  |
| Accountability | Ownership defined | Business Owner, Technical Owner, and risk owner documented | Yes / No |  |
| Accountability | Logging | Prompt and output logging enabled where available | Yes / No |  |
| Privacy | Data protection | Encryption and access controls implemented | Yes / No |  |
| Privacy | Anonymization | Sensitive data anonymization in place where applicable | Yes / No |  |
| Privacy | Consent and notice | Consent or notice mechanisms defined where required | Yes / No |  |
| Security | Vulnerability management | Regular scanning and patching | Yes / No |  |
| Security | Access control | RBAC and MFA enforced | Yes / No |  |
| Security | Adversarial testing | Prompt injection and abuse testing performed | Yes / No |  |
| Compliance | Regulatory alignment | GDPR, NIS2, and SOX considered | Yes / No |  |
| Compliance | Standards alignment | NIST AI RMF and NIST CSF alignment confirmed | Yes / No |  |
| Ethical Use | Purpose limitation | Approved purpose enforced and misuse safeguards documented | Yes / No |  |
| Human Oversight | Oversight model | Oversight model documented and appropriate to impact | Yes / No |  |
| Monitoring | Monitoring defined | Monitoring scope and reassessment date established | Yes / No |  |



### **Appendix C - Process Flow Summary**

|  |  |  |
| --- | --- | --- |
| **#** | **Action** | **Decision / Output** |
| 1 | Submit AI tool request with use case, data classification, impact assessment, and integration details | Request logged; inventory updated |
| 2 | Assign an AI RMF Profile using the ordered rules in **AI RMF Profiles: Profile Selection** | Profile and selection rule recorded; default controls and oversight expectations established |
| 3 | Apply automatic escalation rules for PII, Sensitive data, safety, autonomy, and regulated exposure | If triggered, classification is set at the indicated tier and escalated to ITGC |
| 4 | Apply base classification and impact and control validation | Final risk tier confirmed |
| 5 | Perform formal risk assessment (ITDRA-aligned) and harm assessment | Risk assessment report completed |
| 6 | Evaluate controls and trustworthiness characteristics | Control gaps identified; remediation actions defined |
| 7 | Determine risk treatment and obtain approval | Approval outcome and conditions documented |
| 8 | Register tool in the** Authorized AI Systems Catalog** | Registration complete; production use authorized |
| 9 | Implement monitoring and trigger reassessment as needed | Ongoing compliance maintained |
| 10 | Report governance metrics and perform annual program review | Program oversight and continuous improvement |

### **Appendix D - **Authorized AI Systems Catalog/Inventory Workbook (Operating Guide)

Companion to Step 6 – Registration and to the Authorized AI Systems Catalog above. The catalog is maintained in the workbook AI Inventory & Risk Assessment Workbook.xlsx. Registration under Step 6 is complete only when the AI system has a fully populated row in the AI Inventory sheet, including an assigned AI RMF Profile. The workbook is the operational companion to the catalog field definitions in Step 6, and is aligned to the same NIST AI RMF functions (Govern, Map, Measure, Manage) as this procedure.

*This section and Appendix H describe what the workbook computes and why, at the level a reviewer needs to operate it correctly. The complete, cell-level formula reference, field-matching tables, and validated test-scenario matrices for each risk-rating formula are maintained separately, in the workbook's own technical system documentation — not reproduced in full here — so that this procedure remains a stable governance document even as formula implementation details are refined.*

**Workbook Sheets**

1. **Dashboard – **Read-only KPIs and charts, including AI RMF Profile coverage and distribution, and company-wide frequency counts across the 13 risk categories and 6 harm types scored on Risk & Harm Assessment. Recalculates automatically; not edited directly.
2. **AI Inventory – **The master register. One row per AI system. This is the only sheet reviewers routinely type into.
3. **Profiles – **Reference definitions for Profiles P1–P20 (default classification and tier, oversight, authority, mandatory controls, monitoring focus, review frequency). Do not edit during a review.
4. **Profile Selection – **The ordered rules and tie-breaks used to choose the correct profile at intake.
5. **Risk & Harm Assessment – **Reviewer-scored risk categories and harm types for the tool. A defined subset feeds the Validated Risk Tier escalation on Risk Assessment (see Appendix H); the sheet is intentionally not wired into Data & Privacy, Vendor & Security, or Legal & Compliance. 
6. **Risk Assessment, Data & Privacy, Vendor & Security, Legal & Compliance, Approval Workflow, Monitoring – **Supporting detail keyed to each AI ID. Several fields look up the assigned profile automatically (review cadence, approval authority, assessment context).
7. **Reference Lists – **Dropdown source values, including the profile, human-oversight, and AI Capability pick lists, plus an AI Capability Description reference column (see Appendix H).xt).

**How to add or update an entry**

1. **Create the row.** In the AI Inventory sheet, add a new row and assign the next AI ID (AI-00n).
2. **Complete intake fields. **Provider, Name, Purpose, Scope, AI Capability, Data Processed, Data Classification, Intellectual Property, PII, and Requested By.
3. **Assign the profile. **Use the Profile Selection sheet - apply the rules in order (start with Rule 1) and stop at the first match. Enter the result in Assigned Profile and the rule in Profile Selection Rule.
4. **Confirm the risk tier (Step 2).** If the Tier vs Profile Check shows "Review vs profile default", the confirmed tier is below the profile default - resolve it before approval, since a profile may be escalated but not silently downgraded.
5. **Leave derived fields as-is**. Default Risk Tier, Human Oversight, Approval Authority, and Review Frequency. These fields populate automatically from the Profiles sheet according to the selected Assigned Profile.
6. **Record approval evidence.** Reviewed By, Approved Date, and Approval Status. Approval authority is the higher of the risk-tier authority and the profile authority.
7. **Verify on the Dashboard.** Confirm Missing Profile = 0 and that the entry appears under Systems by Assigned Profile.


**Authorized AI Systems Catalog**

This catalog is a live record and must be updated upon each new approval, modification, or decommission.

AI Inventory & Risk Assessment Workbook.xlsx

|  |  |  |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Provider** | **Name** | **Purpose** | **Scope** | **LLM or Agentic** | **Data Processed** | **Approved Classification** | **IP** | **PII** | **Requested By** | **Reviewed By** | **Approved Date** | **Profile** |
| Microsoft | Copilot | Productivity assistance | All employees | LLM and Agentic | the organization confidential data | Confidential | Yes | Yes | Not provided | Not provided | Not provided | P1 |
| Anthropic | Claude AI | AI evaluation | Limited PoC group | LLM | Custom software code, uploaded documents, and user provided data | Internal | No | No | Not provided | Not provided | Not provided | P2 |
| <http://CustomGPT.ai>  | JMP Learnbot | AI used with JMP Learnbot | Limited group with chemical composition access | LLM | User questions specific to JMP Pro tool navigation | Internal | No | No | <[Contact-1]@organization.local> | IT Security and ITGC | 2026-06-04 | P3 |



*Legend: IP indicates intellectual property processed. PII indicates personally identifiable information processed. Profile refers to the **AI RMF Profile** assigned in  ***AI RMF Profiles*** section. Original classification values of Internal Use and Internal Use Only have been normalized to Internal. Entries marked Not provided require completion of the requester, reviewer, and approval date fields.*


### **Appendix E - Human Oversight Classification**

|  |  |  |
| --- | --- | --- |
| **Classification** | **Description** | **Minimum Requirement** |
| Human-In-The-Loop | A person reviews and approves the output before action is taken. | Required for employment, legal, financial, safety, and external communication use cases. |
| Human-On-The-Loop | A person supervises operation and can intervene or halt the system. | Permitted where outputs assist but do not determine high impact outcomes. |
| Human-Out-Of-The-Loop | The system acts without prior human review. | Requires High or Critical review and is prohibited for high impact actions unless explicitly approved by ITGC. |



### **Appendix F - AI Threat and Harm Catalog**

|  |  |  |
| --- | --- | --- |
| **Threat** | **Description** | **Primary Harm** |
| Prompt injection | Crafted input overrides instructions or extracts data | Confidentiality, integrity |
| Data poisoning | Manipulated training, retrieval, or reference data | Integrity, reliability |
| Model theft or extraction | Model, prompts, or embeddings extracted or replicated | Intellectual property |
| Training data leakage | Company data retained or reused by the provider | Confidentiality, privacy |
| Hallucination | Fabricated or unsupported output presented as fact | Information integrity, decision quality |
| Overreliance and automation bias | Output accepted without adequate review | Decision quality, operational |
| Model drift | Behavior or quality changes over time | Reliability |
| Shadow AI | Unapproved tools used for business purposes | Confidentiality, compliance |
| Bias and discrimination | Unfair or skewed outputs affecting people | Individual harm, legal |
| Adversarial input | Inputs crafted to force unsafe or incorrect behavior | Safety, integrity |
| Insecure plugins and agent actions | Excessive privilege or unvalidated tool execution | Security, operational |
| Third-party and value chain risk | Vendor, subprocessor, or component weakness | Confidentiality, availability |
| Unsafe code or automation generation | Insecure code or harmful automation produced | Security, safety |



### **Appendix G - Governance Metrics and Dashboard**

|  |  |  |
| --- | --- | --- |
| **Metric** | **Definition** | **Cadence** |
| Total AI systems | Count of all entries in the AI inventory | Quarterly |
| Approved systems | Entries with approval status Approved or Approved with Conditions | Quarterly |
| Pending review systems | Entries awaiting classification, evidence, or approval | Quarterly |
| High and Critical risk systems | Entries with risk tier High or Critical | Quarterly |
| Systems processing PII | Entries with PII indicator Yes | Quarterly |
| Systems processing Sensitive data | Entries with approved classification Sensitive | Quarterly |
| Systems processing Confidential data | Entries with approved classification Confidential | Quarterly |
| Vendor-hosted systems | Entries hosted or operated by a third party | Quarterly |
| Open remediation actions | Outstanding conditions from conditional approvals | Quarterly |
| Overdue reassessments | Entries past the next reassessment date | Quarterly |
| AI-related incidents | Incidents involving an AI system in the period | Quarterly |
| Shadow AI discoveries | Unapproved AI use identified in the period | Quarterly |

### Appendix H - AI Inventory

#### How the Inventory Workbook Calculates

The Authorized AI Systems Catalog is designed so that reviewers **enter a small number of facts** and the workbook **derives everything else**. This keeps the catalog consistent: the same input always produces the same classification, and every dependent sheet reads from a single source of truth. Reviewers should understand which cells they control and which are calculated, and must not overtype a calculated cell — doing so breaks the link that keeps the workbook internally consistent.

There are three kinds of calculation in the workbook:

- **Decision formulas** convert inputs into a status or a tier using nested IF logic.
- **Lookups** copy a value from the Profiles reference table based on the tool's assigned profile.
- **Roll-ups** count rows across the inventory to produce the Dashboard metrics.

The **AI Inventory** sheet is the hub. It derives each tool's Approval Status and Risk Tier, and it pulls the profile defaults. Those results then flow outward to the Risk Assessment, Data & Privacy, Vendor & Security, Approval Workflow, and Monitoring sheets, and are finally counted on the Dashboard.

**What the Reviewer Enters vs. What the Workbook Calculates**

| **Reviewer enters (inputs)** | **Workbook calculates (derived)** |
| --- | --- |
| Data Classification | Approval Status |
| Intellectual Property and PII flags | Risk Tier |
| Requested By, Reviewed By, Approved Date | Profile Default Risk Tier |
| Assigned Profile and Selection Rule | Tier vs Profile Check |
| Approval decisions on the Approval sheet | Human Oversight, Approval Authority, Review Frequency |
| Last Reassessment date | Next Reassessment, Reassessment Status, Effective Cadence |

#### Core Calculations

##### Approval Status

**What it does.** Records where a tool stands in the review lifecycle.

**How it works.** This is now a **fully manual field**, set by the reviewer from a seven-value dropdown: *Not Submitted, Pending / Needs Documentation, Under Review, Approved, Approved with Conditions, Rejected, Retired*.

**Reviewer note.** This changed from how it used to work. Approval Status was originally a formula that inferred status from an Approved Date and a Reviewer name — but that formula could only ever reach three of the seven states, leaving no way to record *Approved with Conditions*, *Rejected*, or *Retired* without overtyping the formula. That gap has been closed: the field is now entirely reviewer-controlled, so every one of the seven states is available directly, every time. **Set it deliberately whenever a decision is made** — nothing derives it for you anymore.

##### Risk Tier

**What it does.** Assigns the tool's base risk tier from its data sensitivity and what it processes.

**How it works.** If the tool processes Sensitive data, or processes PII, the tier is *High*. If it processes Confidential data, or processes Intellectual Property, the tier is *High*. If it processes Internal data, the tier is *Moderate*. Otherwise the tier is *Low*.

**Reviewer note.** This is the base tier, and it is still the single most reused value in the workbook. It was found, at one point, hardcoded as static text rather than a live formula — a rebuild had copied the displayed value without regenerating the formula behind it. It has since been restored as a formula and the field no longer accepts manual dropdown entry, so this cannot silently drift out of sync with Data Classification, IP, and PII again. Accurate entry of those three inputs remains essential — this tier now feeds not just five other sheets, but the fully cross-domain Overall Risk Rating described below.

##### Profile Selection Rule *(new)*

**What it does.** Records which rule in the Profile Selection sheet justifies the tool's Assigned Profile.

**How it works.** This is no longer a manual entry. It automatically looks up the Assigned Profile in the Profiles reference table and returns that profile's Primary Selection Rule.

**Reviewer note.** Previously, a reviewer chose the rule from a dropdown by hand after applying the Profile Selection logic themselves. That created a real risk of mismatch — a reviewer could assign one profile but record a different rule number. Now the field derives directly from whichever profile is assigned, so the two can never disagree. The reviewer's only job is still to apply the Profile Selection rules correctly when choosing the Assigned Profile in the first place; this field just guarantees the record reflects that choice accurately.

##### Profile Default Risk Tier, Human Oversight, Approval Authority, Review Frequency

**What they do.** Copy the assigned profile's defaults onto the tool so every sheet can use them without re-deriving.

**How they work.** Each field looks up the Assigned Profile in the Profiles reference table and returns the matching attribute — the profile's default tier, its oversight model, its approval authority, or its review cadence. If no profile is assigned, the field stays blank.

**Reviewer note.** Unchanged. These values change only by changing the Assigned Profile. To adjust a default, update the Profiles sheet through the Annual Program Review, not the individual tool row.

##### Tier vs Profile Check — the guardrail

**What it does.** Compares the confirmed Risk Tier against the profile's default tier and flags any attempt to classify a tool below what its profile expects.

**How it works.** If the confirmed tier matches the profile default, it reads *Matches profile*. If the confirmed tier is High or Critical, it reads *Above profile (OK)*, because escalation is always permitted. If the confirmed tier is lower than the profile default, it reads *Review vs profile default*.

**Reviewer note.** Unchanged. This is the control that enforces the principle *escalate, never silently downgrade*. A *Review vs profile default* flag must be resolved, with documented justification, before the tool is approved.

##### Overall Risk Rating (reference)

**What it does.** Surfaces the tool's fully synthesized risk score directly in the Inventory, without requiring a trip to the Risk Assessment sheet.

**How it works.** It pulls in the Overall Risk Rating computed on Risk Assessment — the higher of the tool's Validated Risk Tier, its Vendor Risk Rating, its Privacy Risk Rating, and its Legal Risk Rating.

**Reviewer note.** This value is **deliberately not the same field as Risk Tier**, and the two are expected to diverge. Risk Tier is what's knowable at intake, from three facts. Overall Risk Rating reflects everything known once vendor security evidence, privacy exposure, and legal governance answers exist. When the two disagree — for example, Risk Tier reads High but this column reads Critical — that gap is the signal, not an error: it means a downstream domain (most often Privacy or Legal) is currently the binding constraint on this tool's real risk.

#### How the Other Sheets Derive Their Values

Each supporting sheet is keyed to the tool's AI ID and reads back from the AI Inventory or the Profiles table, so it always agrees with the hub.

**Risk Assessment.** The tool's Inherent Risk is pulled from the AI Inventory Risk Tier. That base tier can then be **escalated** — never downgraded — into a Validated Risk Tier, based on findings from the Risk & Harm Assessment sheet (for example, a flagged Safety harm on Sensitive data always escalates to Critical). The *Risk Register Entry Required* and *Risk Acceptance Required* flags now read *Yes* whenever the **Validated** Risk Tier is High or Critical — not the raw base tier — so an escalation is never missed by these two governance triggers. Risk Assessment additionally computes an **Overall Risk Rating**, the higher of the Validated Tier and the ratings from Vendor & Security, Data & Privacy, and Legal & Compliance, plus a **Risk Drivers** field naming which domain is responsible whenever that rating is High or Critical.

**Data & Privacy.** The single Data Classification value is expanded into four Yes/No flags — Public, Internal, Confidential, Sensitive — so classification becomes countable. Because controls are cumulative, a higher classification also sets the lower flags: a Confidential tool is also flagged Internal. This sheet also computes a **Privacy Risk Rating**, evaluated independently from its own evidence — data classification, PII, whether data is shared with a vendor, and whether a DPA is on file — rather than being copied from the tool's Risk Tier.

**Vendor & Security.** The Vendor Risk Rating is no longer a starting point seeded from the tool's Risk Tier. It is computed directly from the sheet's own control evidence: the proportion of the ten security controls (SOC 2, MFA, encryption, and so on) confirmed as "Yes", provided the Security Review itself is Approved. If the Security Review hasn't concluded favorably, the rating defaults to High regardless of how many individual controls look good.

**Legal & Compliance.** *(new sheet)* Tracks Legal Review status and six AI-specific governance questions — IP ownership of AI output, training data rights, liability for hallucination, audit rights, data-use restriction, and exit/deletion rights. The **Legal Risk Rating** is computed from the proportion of those six questions confirmed "Yes"; any single confirmed "No" forces the rating to High immediately, and a Rejected Legal Review forces it to Critical.

**Risk & Harm Assessment.** *(new sheet)* Where the reviewer scores 13 risk categories and 6 harm types per tool (Yes/No/N-A). This scoring is what actually drives the escalation from Inherent Risk to Validated Risk Tier on Risk Assessment — for example, a flagged Safety harm is what pushes a tool to Critical regardless of its base data classification.

**Approval Workflow.** IT Security, Privacy, and Legal Approval no longer read from an approval date. Each now mirrors the corresponding review status on its owning sheet — Vendor & Security's Security Review, Data & Privacy's Privacy Review, and Legal & Compliance's Legal Review respectively. *ITGC Required* still reads *Yes* when the tool's Risk Tier is High or Critical, and *ITGC Approval* is now **guarded**: whenever ITGC Required is No, ITGC Approval is forced to *Not Required*, so a tool can never show a decision value implying ITGC reviewed something that was never routed to them. The Approval Decision still mirrors the Approval Status from the hub, and a reference column shows the approval authority the assigned profile expects. (The separate *Compliance Approval* column has been retired — there was never a supporting sheet behind it, and an unfillable manual gate was judged worse than not having it.)

**Monitoring.** Unchanged. The Next Reassessment date is the Last Reassessment plus twelve months. The Reassessment Status reads *Overdue* automatically once that date passes, *Current* before it, or *Not Scheduled* if no date is set. The Effective Review Cadence takes the more frequent of the sheet's own frequency and the profile's cadence, so a profile can tighten a review schedule but never loosen it.

#### How the Dashboard Rolls Up

The Dashboard holds no source data. Every figure is a count of the AI Inventory or Risk Assessment, so it updates automatically whenever an inventory row changes.

**KPI counts** total the systems and count those meeting a single condition, such as tier equal to High or PII equal to Yes. The *Missing Profile* metric counts rows that have an AI ID but no assigned profile, and must remain at zero. A newer KPI, *Overall Critical/High Systems*, counts tools whose Overall Risk Rating (not just Risk Tier) is High or Critical — this number can be higher than the Risk Tier count alone, precisely because of the escalation behavior described above.

**Distinct Profiles In Use** counts how many of the twenty profiles appear at least once in the inventory.

**Systems by Assigned Profile** lists all twenty profiles with a live count of the tools carrying each.

**Chart helpers** count the inventory by Capability, Risk Tier, Data Classification, and Approval Status — and now also by **Overall Risk Rating**, as a fifth chart, precisely because that composite figure can diverge from the plain Risk Tier chart next to it. The capability count uses a partial-match so that a tool listing several capabilities is counted in each; for this reason the capability figures intentionally sum to more than the number of tools.

#### Reference Lists – AI Capability Description

As of this revision, Reference Lists includes an AI Capability Description column defining what each of the five AI Capability values means for a reviewer assigning one at intake, and why it carries the risk profile it does:

**Generative AI – **Creates new content — text, images, video, audio, or code — from a prompt or input. Output is novel each time, which is what creates hallucination, IP/likeness, and output-reliance risk. This capability now triggers the Generative AI floor on Risk Assessment (see above).

**Agentic AI – **Takes actions on other systems: calling tools, executing multi-step workflows, or triggering downstream processes without a human performing the action directly. Risk is about consequence and reversibility, not just content. Already escalates the Validated Risk Tier when combined with Third-party risk or Data poisoning.

**Embedded AI – **An AI feature activated inside an application already approved and onboarded. The vendor was not independently selected or vetted; it inherits the host application's data boundary and security posture. No dedicated escalation trigger.

**AI APIs and Integrations – **The organization calls a vendor's AI model or service programmatically as one structured component of a larger internal workflow. Considered for a dedicated escalation floor this revision and explicitly not given one (see above).

**Internal AI Deployments – **The model runs inside the organization's own infrastructure rather than being sent to an external vendor at inference time. No third-party data exposure at the model layer. No dedicated escalation trigger.

A relative risk ordering for these five capabilities, lowest to highest, was established this revision: Internal AI Deployments \< Embedded AI \< AI APIs and Integrations \< Generative AI \< Agentic AI. This ordering is reflected in which two capabilities received a dedicated escalation rule (Generative AI, Agentic AI) versus which three continue to rely solely on classification/PII-driven escalation.

#### Reviewer Responsibilities

1. Enter only the input fields; never overtype a calculated cell.
2. Ensure Data Classification, IP, and PII are accurate — they drive the Risk Tier that both Risk Assessment and the Overall Risk Rating depend on.
3. Resolve any *Review vs profile default* flag before approval.
4. **Set Approval Status directly from the dropdown whenever a review decision is made** — this field is fully manual now, so nothing will set it for you.
5. Where Overall Risk Rating diverges from Risk Tier, check the Risk Drivers field on Risk Assessment before treating the tool as fully assessed — a High or Critical driven by Legal or Privacy needs that domain's evidence resolved, not just the base classification.
6. Allow the workbook to recalculate before relying on the Dashboard; if figures look stale, trigger a recalculation.
7. Change profile defaults only on the Profiles sheet, through the Annual Program Review.

## **Document Provenance and Attribution**

**Design and content ownership:** Every review step, risk classification rule, control requirement, approval gate, and governance workflow described in this procedure was designed, tested, and iteratively refined by **[IT Security Lead]**, IT Security Senior Manager at the Organization. The underlying process design — including the end-to-end review sequence (Business → IT Security → ITGC, with Privacy and Legal as separate gates), the risk classification and escalation logic summarized in Appendix H, and the AI Capability floor/escalation decisions (including the deliberate choice to leave "AI APIs and Integrations" un-escalated) — reflects their analysis and decisions, not an AI-generated design.

**Drafting assistance:** This procedure was drafted, structured, and formatted with the assistance of **Microsoft 365 Copilot**, an enterprise AI assistant built on an Anthropic Claude large language model, working from [IT Security Lead]'s prior procedure drafts, the companion Authorized AI Systems Catalog workbook, and related design discussions. AI assistance was used for writing, organizing, and reconciling this document — not for originating the review process or risk logic itself. This procedure is maintained separately from the AI Inventory workbook's technical system documentation; it references the workbook (Appendix D, Appendix H) only at a summary level.
