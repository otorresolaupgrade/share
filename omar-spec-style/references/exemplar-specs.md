# Omar's Exemplar Specs - Full Text Reference

This file contains full-text exports of Omar's specs from Confluence, used as style references.

---

## Spec 1: PRD: Workflow Automation: Complaints and Surveys
**Created:** 2024-05-10 | **Type:** System integration / workflow automation

| **Targeted for** | Q3 2024 |
| --- | --- |
| **TL;DR** | Transfer complaints triggered in Genesys to a Jira case, to automate Oversight workflow tasks and dispositions. Transfer negative CSAT scores submitted in surveys from vendor CentraCX |
| --- | --- |
| **Tickets** | CA-639 |
| --- | --- |
| **Contributors** | @Melissa Luther, @Sierra Madden |
| --- | --- |
| **Roadmap** | Presented to Execs by: @Omar Torresola / Aligned with Product: @Srini Veerapaneni / Added to: [roadmap link] / Presented for Design to Engineering: @Nii Dodoo / SME: @Melissa Luther, @Rahul Khakurel, @Trenton Hagen |
| --- | --- |
| **Slack** | |
| --- | --- |

# Problem Alignment

Because the existing methods is still manual and meant to be a temporary solution. The lack of this integration leads to a time-consuming and error-prone process, impacting operational efficiency and costs:

* Automates manual effort (DB queries and adhoc scripting)
* Automates system to system integration consistent with similar requests done previously

### Current State for Complaints:

1. Agent dispositions a complaint in Genesys by selecting relevant wrap up code ("COMPLAINT")
2. Wrap Up Code is currently pulled from DB
3. Joined to some VQ data
4. Cleaned up via python
5. Uploaded to CMT Jira board

### Current State for Negative CSAT (surveys):

1. Customer submits "negative" review on a survey presented through voice/chat/email
2. CentraCX data is pulled from the database
3. Cleaned up via python
4. Uploaded to CMT Jira board

---

# Solution Alignment

**Automate existing process**: Design or leverage existing service(s) that allows these systems to pass the relevant attributes.

Because:

* There is no seamless integration between Genesys or CentraCX and Jira.
* Oversight team uses Jira for other existing case handling, and intends to keeps this system for the foreseeable future.

| **Requirement** | **Description** | **Acceptance Criteria** | **Notes / Tasks** |
| --- | --- | --- | --- |
| **Genesys Disposition** | Target all dispositions that are the triggering indicator of a complaint, whenever a call, chat or email is completed. | To capture ensure all variants of `wrap_up_code` relevant to complaints are captured, include either a LIKE 'complaint' in the WHERE clause or add wildcard to the text ('%complaint%') | Email is not used in Genesys today but for the purposes of this requirement, it's irrelevant. |
| **No CentraCX API** | Target any mechanism Data Engineering team has provided to capture this data | | (Eng: please provide an approach to make this work without APIs exposed by vendor) |
| **Fetch CRM Data** | Enrich the complaint case by providing customer and account attributes to the ticket. | | VQ data pending from Melissa Luther |
| **Jira Intake** | Land Complaints tickets in Jira | Project Key: CMT / IssueType: Complaint / StatusCategory: Open / Status: To Do / Title: "MONTH_LOAN_ID_GENESYS_VOICE"; "MONTH_LOAN_ID_GENESYS_CHAT" / Description: include: Conversation Date and Time, Conversation Transcript, Agent Name, Interaction ID, Product Type, DPD (Days Past Delinquent) | |
| **Jira Intake** | Land Negative CSATs tickets in Jira | Project Key: CMT / IssueType: CSAT / StatusCategory: Open / Status: To Do / Title: "MONTH_LOAN_ID_CENTRACX_VOICE"; "MONTH_LOAN_ID_CENTRACX_CHAT"; "MONTH_LOAN_ID_CENTRACX_EMAIL" | |

---

# Questions

| **Topic** | **Question** | **Reference** | **Answer** |
| --- | --- | --- | --- |
| Complaint <> customer matching | How do we identify to a borrower? | @Melissa Luther | Probably some fuzzy logic exists today for the DE pipeline that Rahul built today |

---

## Spec 2: PRD: Unified List for OB Servicing Campaigns
**Created:** 2023-11-16 | **Type:** Data engineering / operations enablement

| **TL;DR** | Product list of Servicing accounts so that Genesys Admins can better support outbound strategy. |
| --- | --- |
| **Roadmap** | Aligned with Execs / Aligned with Product: Aaron / Aligned with Engineering: Servicing / Added to: [roadmap link] |
| --- | --- |
| **Tickets** | IS-4113 |
| --- | --- |
| **Slack** | `#tech_genesys` |
| --- | --- |

# Problem Alignment

Because delinquency trends are increasing, causing our investors to scrutinize our collection performance. This initiative will empower Operations to accelerate implementation changes on strategic outbound decisions, with minimal code change requests.

Due to historic Genesys limitations, Operations requires Servicing Engineering team to maintain lists for Collection, Welcome Calls, and other purposes. In December 2023, Genesys delivered a feature called Contact List Builder that will allow administrators to:

1. Create necessary filters to create sub lists that meet different set of requirements.
2. Implement change management without dependency on Engineering.

---

# Phase 1 Solution

The list will be maintained daily by Servicing Engineering and will product desired customer and account attributes that can be passed to Genesys Contact List APIs.

Because of these reasons:

* We are not moving away from Genesys as our tool for outbound campaigns.
* Unlocks one list for a separate outbound channel: SMS
* Email will also be supported by Genesys after Zendesk goes away

| **REQ #** | **Requirement** | **Acceptance Criteria** | **Notes** |
| --- | --- | --- | --- |
| REQ-01 | Evaluate Constraints | Genesys contact lists have the following constraints: A list can't include more than 5mm records at a time. A list can't exceed 50 columns. An org list can't exceed more than 20mm at a time. 20 filter limit per campaign; 10 limit currently. | |
| REQ-02 | Segment by Product | I can have one comprehensive list for each of the products below: PL, PCL, HI, IA, Flex Pay and Secured Auto | |
| REQ-03 | Apply List Exclusions | Exclusion tab: [Google Sheet link] | |
| REQ-04 | Apply Servicing Attributes | Input/Output tabs: [Google Sheet link] | |
| REQ-05 | Create Contact list | See relevant Genesys API documentation | |
| REQ-07 | Tests | Ensure columns that are not meant to be cleared have tests before the list is refreshed. This is important because some of those columns are related to Regulation F and we had an incident. | SI-7119 |

# Phase 2 Solution

| **REQ #** | **Requirement** | **Acceptance Criteria** | **Notes** |
| --- | --- | --- | --- |
| REQ-01 | Produce More Attributes | [Link to attribute list] | Omar to bring up custom columns discussion 1-2 3-8 |
| REQ-02 | Purge of Sublists | Today we have to manually delete old lists because Genesys caps the total amount. Every day a snapshot is taken from a list with prefix: "UnifiedYYYMMDD_". Delete once snapshot occurs. | Discuss with Engineering: Is there a way to detect these limits at any moment in time? |

---

## Spec 3: PRD: Activity Log UI Improvements - Phase 3 (Tag functionality)
**Created:** 2024-09-25 | **Type:** CRM UI feature

Delivered MVP on Q1 2025.

| **TL;DR** | Add tag-based grouping, centralized tag management, and immutability with audit trails, to reducing search time, increasing user satisfaction, and ensuring scalability. |
| --- | --- |
| **Roadmap** | Reviewed by Execs / Aligned with Product: @Srini Veerapaneni / Aligned with Design: @Vicky Choy / Aligned with Engineering: @Marcela Pedrini Duarte, @Sumant Kumar (CORE) |
| --- | --- |
| **Tickets** | CORE-6294, UXD-3158 |
| --- | --- |

### Why Should We Do This?

1. Grouping activities by tags will make it easier for users to find relevant updates.
2. Centralized tag management will prevent duplication and ensure consistency in categorizing activities.
3. As data volume grows, the functionality should scale without sacrificing performance or effectiveness.

* Deposit is advocating for this work: [link]
* Fraud is another domain blocked: [link]

---

### What Are We Doing?

| **Key Feature** | **User Story** | **Design Req** | **Notes** |
| --- | --- | --- | --- |
| Grouping of System Events and Comments | *As a CRM user, I want to search for customer updates using a tag so that I can quickly find relevant activities.* | Design a filter/toggle UI to group events by tag and allow for quick searching and sorting. | ✅ MVP is create tag functionality in the backend in a 1:M relationship with activities. Filter/Search functionality will be different phase. |
| Tag Activity relationship | *As a CRM user, I want to search for multiple tags for 1 activity so that I have multiple ways to review a common property on multiple activities.* | A tag is always related to an activity. A tag is **not** exclusive to 1 activity. UI shows only 1 tag for MVP | ✅ Sumant: we will deliver a superset of tags. |
| Configuring Tags | *As a Product Manager, I want to submit requests for new tags or categories, ensuring that the Activity View remains organized without duplicates.* *As the tag owner, I want to review and approve or deny tag requests to maintain consistency and avoid unnecessary tag proliferation.* | Create a UI (Google Form?) for submitting and managing tag requests. | ✅ [Google Sheet link] |

---

### Design

UXD-3158

---

## Spec 4: PRD: Banner and Tag Alerts in Upgrade CRM
**Created:** 2024-06-25 | **Type:** CRM UI / agent experience

| **TL;DR** | Actor and account special status alerts that are highly visible on Upgrade CRM pages. |
| --- | --- |
| **Roadmap** | Presented to Execs by: @Omar Torresola / Aligned with Product & Design: / Added to: / Presented to Engineering: |
| --- | --- |
| **Tickets** | |
| --- | --- |

### As an agent, I want to be reminded about critical status alerts so that I'm guided through special and uncommon procedures.

| **Category** | **Requirement** | **Reference** | **Notes** |
| --- | --- | --- | --- |
| Banner alert | Prompt a banner that persist throughout _Actor_-level pages: AC: Cease and Desist, Deceased, SCRA, OFAC / PEP, Fraudster, Power of Attorney | Verbiage: Cease and Desist - @Alex Lizarraga to provide requirements | NEEDS FIGMA from Design |
| Banner alert | Prompt a banner that persist throughout _Account_-level pages: AC: Past Due (0-30), Delinquency (31+), Charge Off (120+), Debt Sold, Bankruptcy | Verbiage: Charge Off - This account has been charged off. | NEEDS FIGMA from Design |
| Navigational Hyperlinks | Enable URL whenever appropriate for re-directs | Scope: Charge Offs | |
| Special status tags | Enable a tag next to the account information on Account-level pages | Tags: Delinquent, Charged Off | NEEDS FIGMA from Design |
| Out of scope | No changes are to be made towards pre-issuance (application) pages | | |

---

## Spec 5: Debit Card Payments in IVR & Sierra for Delinquent PL/HI
**Created:** 2025-11-25 | **Type:** Payment rails / omnichannel

| **Problem Statement** | Delinquent PL/HI callers can't pay via debit in IVR/Sierra, causing friction and missed recoveries. |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: @Aaron Spargo / Engineering: Servicing / Added to: |
| --- | --- |
| **Tickets** | |
| --- | --- |

* Expand self-serve payment rails to PL/HI delinquency to increase right-party contacts that convert to payments and accelerate cash flow.
* Close parity gaps with FlexPay, centralize analytics/controls, and strengthen compliance posture in one consistent, omnichannel experience.

---

### Detailed Table Requirements

* **User:** Delinquent customer (PL/HI) calling IVR or interacting with Sierra.
* **Preconditions:** Customer/account identified (ANI match + KBA or equivalent), product context known, account is eligible.

| Name | User Stories | Description | Team |
| --- | --- | --- | --- |
| Product & delinquency eligibility | Delinquent Customer: "I need to make a payment on my PL/HI now." | The system must determine PL vs. HI and delinquency window; block if legal/fraud/BNK holds apply | Genesys |
| Offer debit as method | Delinquent Customer: "Give me a quick debit option." | The system must present debit payment option when eligible. | Genesys |
| Existing card on file | Delinquent Customer: "Use my saved card ending ••••1234." | The system must surface last-4/brand and let user select it; never voice PAN. | Genesys + Servicing |
| New card entry (secure) | Delinquent Customer: "Use a different debit card." | The system must pause/stop recording and collect PAN/expiry/CVV/ZIP (DTMF for IVR). For Sierra, immediately tokenize and discard PAN/CVV, or transfer to Genesys IVR Secure Line. | Genesys + Servicing |
| Amount options | Delinquent Customer: "I want the past-due or a custom amount." | The system must offer past-due, minimum to cure, or custom within configurable min/max; confirm amount. | Genesys + Servicing |
| Confirmation | Delinquent Customer: "Give me a confirmation that payment has been scheduled." | The system must return a "scheduled payment" message and send receipt via email on file. | Genesys + Servicing |
| Decline handling | Delinquent Customer: "Let me try again." | The system must allow 2 retries with guidance for soft declines; then offer agent transfer. | Genesys |
| Analytics & events | Ops Lead: "Show me the funnel and KPIs." | The system must emit events for eligibility→offer→path→amount option→tokenized→auth result→post result; include decline codes, retries, step time, abandon, agent-escalation. | Genesys + OAT |

### Edge Case Handling

* **Amount Options.** Default options: **past-due amount**, **minimum to cure**, **custom** within min/max per product.
* **Amount Limits.** Enforce configurable **min** (e.g., $1) and **max** (e.g., outstanding balance or policy cap given by API).

---

## Open Questions

(empty — new spec, questions to be filled in)

---

## Spec 6: Upgrade Assist Intake Automation (Phase 1)
**Created:** 2026-03-06 | **Type:** Conversational AI / compliance automation

| **Problem Statement** | Human agents are burdened with manually collecting structured intake data for high-volume requests (SCRA, Bankruptcy, PII), resulting in excessive handling times and inconsistent data capture. |
| --- | --- |
| **Objective** | Deploying conversational AI forms will automate end-to-end data collection and routing, significantly reducing agent handle time while ensuring high compliance. |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: Ops / Engineering: Core, Mobile, DevOps, Platform / Added to: [roadmap link] |
| --- | --- |
| **Tickets** | IS? |
| --- | --- |
| **Slack(s)** | `#tmp-conv-forms` |
| --- | --- |

* **Cost Reduction:** Automating intake for ~14,400 monthly interactions frees human agents to focus on complex servicing.
* **Compliance enforcement:** SCRA and Bankruptcy intakes carry strict compliance requirements. An AI agent follows the script perfectly every time, eliminating human error.
* **Data quality & speed:** Structured forms with validation ensure complete, correctly formatted data on first capture.
* **24/7 availability:** Customers can initiate SCRA requests, report bankruptcy filings, or update personal information at any time.

## Narrative

Today, when a servicemember calls about an SCRA interest rate reduction, a customer reports a bankruptcy filing, or someone needs to update their name or date of birth, a human agent walks through a multi-step procedure—authenticating the caller, asking a series of scripted questions, collecting documentation details, updating internal systems, notating accounts, and routing to specialist teams. Each of these interactions follows a well-defined decision tree with predictable branching, making them ideal candidates for AI agent automation.

#### Out Of Scope

* The AI agent will not perform the back-office processing itself. It handles intake and routing only.
* Real-time document verification (OCR/classification) is out of scope.

| **Requirement** | **Description** | **Notes** |
| --- | --- | --- |
| **SCRA Flow** 200–300/mo | As a **service-member**, I want the AI to collect my service dates so I don't have to wait for a human. | [Use Case link] |
| **Bankruptcy Flow** 2,600/mo | As a **debtor**, I want Upgrade to stop asking for payments once I mention bankruptcy. | [Use Case link] |
| **Name/DOB update** 11,500/mo* | As a **customer**, I want to update my name or DOB without talking to a CCP. | Need to validate volume. Suspect it's actually Address Change |
| **Logic Branching** | As a **customer**, I want the bot to only ask questions relevant to my specific situation. | |
| **System Routing** | As a **back-office** CCP, I want to receive structured data in my queue so that I can disposition it. | |
| **Escalation & Handoff** | If the AI agent cannot complete intake, it must warm-transfer to a human agent with full context of what has been collected so far. | Sierra related changes |

### Service Integration Architecture

1. AI agent completes intake form and calls createActorFormTodo(form_type, external_id, account_id)
2. Actor To Do appears on customer dashboard with document type and submission instructions.
3. Actor To Do status: OPEN. ActorTodoRequest status: PENDING.
4. Activity Service posts notation.
5. Service Request Service creates work item for back-office team.
6. Customer uploads document via dashboard. Doc Management Service appends to actor profile.
7. Back-office team reviews document quality and submits fulfillment.
8. If 45 days elapse without upload, Service Request may be closed.

#### Phase 2:
1. CRM Compliance UI Tab: Bankruptcy intake must write directly to the Compliance tab.
2. Jira: SCRA tickets, Flex Pay Legacy BK tickets require Jira ticket creation.

---

## Spec 7: Don't Call Now – TCPA-Compliant Calling Indicator
**Created:** 2025-05-27 | **Type:** Compliance / CRM UI

| **TL;DR** | ~233 Q4-2024 outbound calls violated the TCPA AM-PM local-time rule, exposing Upgrade to fines. Fix: Add indicator next to every phone number in the CRM that has a hyperlink to Genesys. Icon status is decided at click-time by a Time-Zone Resolution Service that checks the customer's ZIP and phone area code. |
| --- | --- |
| **Reviewed** | Execs & Stakeholders: @Robert Rose, @Melissa Legendre, @Chris Carter, @Srini Veerapaneni / Design: @Vicky Choy / Engineering: Core |
| --- | --- |
| **Slack** | `#tmp_tcpa_button` |
| --- | --- |

### Narrative

Imagine a contact center rep, eager to help a borrower resolve an issue, clicks on a customer's number only to unknowingly ring the customer at 6 AM. These honest mistakes result in regulatory violations.

1. **Prevent Regulatory Risk**: Each infraction can carry legal and reputational consequences.
2. **Empower CCPs**: Gives frontline teams clarity without second-guessing time zones or policy.
3. **Minimize Engineering Debt**: Establish an AWS infrastructure with low-latency, high-availability logic.

Success metrics:
4. 90% reduction in TCPA violations, measured monthly by Compliance team audit logs.
5. 95% correct mappings from area code, zip code or address geocoding, audited quarterly.

## Detailed Requirements Table

| **Name** | User Stories | Description | Notes |
| --- | --- | --- | --- |
| **Compliant Call Window (FE)** | CCP: "I want to know if it's OK to call this customer right now." | Show indicator with next-callable tooltip. | See Design section. |
| **"Are You Sure?" Modal (FE)** | CCP: "I accidentally clicked call on a blocked number. Can I cancel?" | If call click happens during restricted hours, show confirmation modal before allowing override. | |
| **Supervisor Override (FE)** | Supervisor: "Sometimes we must call." | Input reason, log override with timestamp and user ID. | |
| **DST Accuracy (BE)** | Compliance: "I need to know this won't fail during daylight changes." | Stay current on DST changes | |
| **Tech Req: Caching (BE)** | SRE: "I want to avoid repeated external API hits." | ?-day cache for (actor_id, phone, zip) | |
| **Analytics** | Compliance: "We need to report on this quarterly." | BI support for reporting | **Not** CORE team |

#### Out of Scope
* International based calls.
* Email or SMS Timing rules.

## Questions

1. Is there a service on the transactional side that contains compliance call windows today?
   1. **Omar**: Genesys restricts CCPs from calling but it only leverages area of the phone number.
2. How do we manage state-specific calling windows?
   1. **Omar**: accommodate state-specific request; see Edge Cases.

---

## Spec 8: Secure SMS Authentication & other channels
**Created:** 2026-01-14 | **Type:** Authentication / Voice AI

| **TL;DR** | Deploy a "Scope Down Step Up on Voice" framework using secure SMS "Instant Link" technology. This initiative streamlines identity verification, and seamlessly bridges voice interactions with mobile-web workflows. |
| --- | --- |
| **Problem Statement** | Current voice authentication does not have a mechanism for extra layer of security whenever extra authentication is required. |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: @Christopher Griffith / Engineering: @Jean-Lou Hallee, @Pierre-Olivier Roy |
| --- | --- |
| **Tickets** | UXD-4398, IAM-3191, IS-6103, IS-6087 |
| --- | --- |
| **Slack(s)** | `#tech-sierra` |
| --- | --- |

### Detailed Requirements Table

| **Feature (Req Name)** | **User Stories** | **Description and/or Acceptance Criteria** | **Notes** |
| --- | --- | --- | --- |
| **Instant Link Delivery** | **Customer:** I want a secure link sent via SMS, so I can verify my identity with one tap. | The system sends a branded SMS containing a Prove "Instant Link" to the confirmed mobile number on file. AC: Link expires after session timeout (~5 mins). | |
| **Mobile Web Verification** | **Customer:** I want to see a visual confirmation that I am safe, so I trust the process. | Upon clicking the link, the mobile browser validates the network/token and displays a branded success screen. AC: Page loads with Upgrade Logo. Green Checkmark + "Identity Verified" text. No manual data entry required. | |
| **Voice Channel Continuity** | **Customer:** I want the voice bot to know immediately when I've clicked the link, so I don't have to say anything. | Bot says: "Thank you, I see you've verified your identity." AC: Latency < 2 seconds from Browser Success to Voice confirmation. | |

### Error Handling & Edge Cases

| **Scenario** | **Requirement** | **Notes** |
| --- | --- | --- |
| **Landline / Delivery Failure** | Bot states: "It looks like I can't send text messages to this number. Let me get someone on the line to help you." Auto-transfer. | |
| **Wrong Number** | If customer says "That's not my number," bot informs them a human agent must update contact info. | |
| **Refusal to use SMS** | Bot explains: "I understand. However, to complete this request securely, I do need to verify via SMS. Would you like me to transfer you to someone who can help?" | |
| **Verification Failure** | Browser shows error. Voice agent triggers auto-transfer. | |

### High-Risk Use Cases Requiring SMS Authentication

| **Use Case** | **Description** | **IS approved?** |
| --- | --- | --- |
| Add External Bank Account | Linking a new external bank account for payments. | Yes |
| Replace Debit Card | Requesting a new physical card be shipped. | Yes |
| Report Account Takeover (ATO) | Urgent reporting of compromised account access. | Yes |
| Transfer Funds Between Accounts | Moving money between checking/savings. | Yes |
| Update Mailing Address | Change physical mailing address. | No |
| Update My Email Address | Change primary email. | No |

---

## Spec 9: Connie (CCP Assistant) in Upgrade's CRM - MVP
**Created:** 2023-12-17 | **Type:** Internal AI tooling / CRM

Rollout on May 20th, 2025

| **Problem Statement** | Customer Care Professionals (CCPs) optimize to understand the customer's inquiry or request in a fast, reliable way. They are under pressure to resolve accurately (first resolution rate, QA score) and scored on their performance (hold and handle time, CSAT), often juggling multiple inbound interactions, systems, and product lines. |
| --- | --- |
| **Reviewed** | Execs, Stakeholders, Compliance & Legal: ✅ (@Chris Carter, @Karel Raba) / Design: @Vicky Choy, @Shivani Birajdar / Engineering: @Pierre-Alexandre Lacerte, @Eric Veilleux |
| --- | --- |
| **Slack** | `#internal_bot_discussion`; `#tmp_connie_crm_integration` |
| --- | --- |

### Why Connie?

Just like Microsoft Word's "Clippy" (sorry Gen Zers, google it), our primary goal is provide real-time support surfacing the correct procedures, offering contextual / specific customer recommendations during live calls, and integrating seamlessly with the CRM's limited screen space.

An assistant can lead to reduced wasted time, potential errors, and inconsistent customer experiences. An incredible second benefit of unifying knowledge and simplifying complicated steps, is it can also shorten new CCP onboarding time by ~25%.

Fun fact: Connie is named after Confluence.

#### Success Criteria

1. **Efficiency**: Reduce Average Handle Time (AHT) by at least 15% within 6 months.
2. **Cost & Quality**: Decrease cost per call/chat/email and Increase FCR rates by 10% in the first year.
3. **Adoption**: Achieve 80% usage rate among CCPs within 3 months.
4. **Accuracy**: Less than 10% inconsistencies found in audit reports.
* **Response**: Completes <5 seconds for 95% of requests.
* **Uptime**: 99.5% availability during business hours.

### What Are We Doing?

| **Requirement + User Stories** | **Description** | **Notes** |
| --- | --- | --- |
| **Widget Interface** | | |
| I want to have a header button called "Assist" so that I don't have to navigate away from the CRM | MVP: implement Gradio-UI | LVQ-6479 |
| **Quick Access to Procedures** | | |
| I want to instantly find the correct procedure. | Connie surfaces relevant procedures in real time by querying a centralized database. AC: I can read the sources and quickly navigate to them. | |
| **Feedback** | | |
| I want to improve Connie by adding my thoughts whether positive or negative. | Thumbs up/down + text feedback | Figma link |

---

## Spec 10: Subpoena Automation - Application Data
**Created:** 2025-09-09 | **Type:** Compliance / legal automation

| **Problem Statement** | Subpoena/exam fulfillment is manual and fragmented, requiring hours per matter across multiple systems. No unified, permissioned way to search by SSN, or retrieve critical PII data through a database. |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: Karel Raba, @Douglas Neeld / Engineering: Nii, IT |
| --- | --- |
| **Tickets** | CA-1078 |
| --- | --- |
| **Slack(s)** | `#tmp_subpoena_automation` |
| --- | --- |
| **InfoSec** | IS-6148 |
| --- | --- |

### Why Should We Do This?

**1** subpoena is received **every day**. An Upgrade paralegal receives a subpoena requesting "any and all applications" for a consumer with multiple unfunded attempts and one funded loan. Today, they hunt through VQ, Spectrum, and other tools, screenshotting, redacting, and assembling evidence by hand. This portal lets them enter an SSN, see every related application and account in one view, and check only what the language requires.

* **Reduce manual work, risk:** Eliminate screenshotting so Legal can redeploy **2 FTE** effectively
  * Bypass the lookup apps process
  * Bypass the screenshot process
  * Bypass the screenshot download to your local (laptop) for redaction
  * Bypass uploading to file sharing service (today One Hub is used)

### Requirements

1. Allow user to search by last 4 of SSN (also support: full SSN, FN, LN, DOB)
2. Fetch all application data for all related applications under SSN (including Uplift and BNPL)
3. Generate an **Application Packet** with specific data points (18 items listed)
4. Deliver information to secure folder structure in .pdf format
5. Generate and provide a shareable link for external parties

**Constraints**
* Avoid generation of composite "new work product" summaries. Return existing records/links.

### Open Questions

1. ~~**InfoSec destination:** Final approved export destinations~~ One Hub ✅
2. **Roadmap sequencing:** After delivery of this spec, which artifacts next?

---

## Spec 11: Sierra Live Assist + Genesys Integration
**Created:** 2026-03-06 | **Type:** AI agent / CCP tooling / vendor integration

| **Problem Statement** | CCPs face cognitive overload, forced to navigate fragmented workflows and systems, while the organization fails to learn from every conversation to identify and fix hidden knowledge gaps. |
| --- | --- |
| **Objective** | Integrating Live Assist into Genesys will surface real-time guidance - step-by-step AI assistance - and a continuous feedback loop of the transferred conversation. |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: Ops / Engineering: DevOps, Platform |
| --- | --- |
| **Tickets** | VM IS? |
| --- | --- |
| **Slack(s)** | `#tech_sierra` |
| --- | --- |

**Business Metrics**
* Reduce Average Handling Time (AHT) by 15% by Q4 2026.
* Reduce critical compliance errors by 10% by Q4 2026.
* Decrease onboarding CCP or re-training time-to-proficiency by 20% by Q4 2026.

**Technical Metrics**
* Maintain Live Assist iframe load performance under 1 second.
* Achieve 99.9% Uptime for the Sierra post-conversation webhook.

### Design

| **Feature (Req Name)** | **User Stories** | **Description and/or Acceptance Criteria** |
| --- | --- | --- |
| **Integration** | **CCP**: I want Live Assist embedded in my main screen, so I avoid multiple browser tabs. | Deploy Live Assist as a lightweight iframe natively within the Genesys Cloud CX desktop. |
| **Contextual Handoff** | **CCP**: I want to see what the AI already discussed, so I don't repeat questions. | ✅ Vendor deliverable |
| **Real-Time Guidance** | **CCP**: I want a dynamic checklist of next steps, so I can accurately process complex requests. | ✅ Vendor deliverable |
| **Post-Call Summary** | **PM**: I want the system to generate a summary after a call. Utilize `summarizeConversation` in the Sierra `onPostConversation` hook. | [Includes inline code sample of Sierra SDK usage] |
| **Feedback Loop** | **PM**: I want to learn from what happens after the customer gets transferred. | ✅ Vendor Deliverable |

## Open Questions

#### Product
* (empty)

#### Engineering
* What is the optimal `postConversationDelaySeconds` to ensure all metadata is synced?
* Will the generated summaries be pushed directly into the Upgrade CRM via API, or...?

---

## Spec 12: Voice Bot for Inbound Calls - MVP
**Created:** 2025-01-12 | **Type:** Voice AI / Sierra / IVR

| **Objective** | Enable 24/7 support for common use cases and reduce call center load. |
| --- | --- |
| **Roadmap** | [roadmap links] |
| --- | --- |
| **Slack** | `#tech_sierra` |
| --- | --- |
| **Tickets** | Dominic & team: UA-64 / InfoSec: IS-6111, IS-6141 / Compliance & Legal: CAR-4534 |
| --- | --- |

#### Why Should We Do This?

* Cost of a call is about $2.80 (2025 avg using BPO numbers) for $828k monthly costs in account servicing
* Cost of a _contained_ call using Sierra is $1.07

| Metric | Target | Definition | Tracking Method |
| --- | --- | --- | --- |
| Containment Rate | **30%** reduction of human-handled calls by EOY | % of engaged sessions resolved without human escalation | Bot-only sessions / total sessions |
| CSATs | **4/5** average | post-call IVR survey | BAU |
| Response Time | **< 2s** for 90% | Avg time to first bot message | Bot log timestamps |
| Recover Costs | Achieve **100%** cost recovery on voice bot investment | Avoid wasting pre-purchased resolutions | Sierra billing reports |

### Out of Scope

* Will not authenticate customers (Use existing Neustar integration)
* Will not add new payment methods
* Will not handle backend actions requiring complex workflows
* Will not support languages other than English

### Detailed Requirements Table

| Name | User Story | Description | Notes |
| --- | --- | --- | --- |
| Smart Routing | I want to get to the right team quickly. | Identify routes based on existing chat parameters. AC: Agent should prompt for account selection prior to transfer. | Genesys work needs to be validated. |
| Latency | I want a response pretty quickly. | < 2 secs for 90% of responses. AC: < 3 secs would provide additional instructions. > 3 secs, trigger a check in. On tool calls, inform customer "please hold while I...." | Big body of work / challenge |
| Interruptibility | I want to interrupt when the bot just rambles. | Acceptable to interrupt. AC: Payment disclosure cannot be interrupted. | Omar tested this in PreProd and accepted. |
| Inactivity | I want to be reminded that I'm still connected. | Check in logic + disconnect after 300 seconds. | @Omar to ask Sierra for guidance |
| High Risk (upstream) | I am in the middle of bankruptcy status. | Actor must skip Sierra if: deceased date, active bankruptcy, cease & desist, active SCRA | Compliance check is MVP. Different approach long term. |
| ~~Sentiment Escalation~~ | ~~"You are useless!!!!"~~ | ~~Bot detects negative sentiment and escalates~~ | ✅ Between abuse indicators and transfer logic this is delivered. |

### TBD or Fast Follow

| Name | User Story | Description | Notes |
| --- | --- | --- | --- |
| Make a Payment | I want to make a payment from a saved account. | For MVP: we must allow customers to make a payment in the IVR or Sierra. | Enable when Servicing is ready. |
| Voice Persona | I want to talk to a bot that sounds human | See Design section. | @Huyen Le to deliver details |
| Further Authentication (Step Up) | I want to INSERT SENSITIVE USE CASE. | Spec: [SMS Auth link] | |

---

## Spec 13: Post-Call Summary Automation (Activity)
**Created:** 2025-05-28 | **Type:** AI automation / CCP tooling

Delayed until this POC is complete: [link]

| **TL;DR** | CCPs spend valuable time documenting calls, adding inefficiencies and inconsistencies. Our objective is to automate post-call summaries and wrap-up code suggestions to reduce handle time and enhance compliance. |
| --- | --- |
| **Reviewed** | Execs & Stakeholders / Compliance & Legal: @Yajayra Carlos Ibarra / Engineering: / IS: Needs a ticket |
| --- | --- |
| **Slack** | `#internal_bot_discussion` |
| --- | --- |

* **Improve Operational Efficiency**: Reduce average call wrap-up time by 50%.
* **Drive Consistency in Dispositions**: Standardized wrap-up codes reduce reporting noise.
* This is part of our **AI strategy** during customers interactions with the CCP
  * IVR Spec is here → [link]
  * Real Time Spec is here → [link]

Imagine a Contact Center Professional (CCP) wrapping up a complex customer call, only to spend an extra minute documenting it manually. Across thousands of calls, this adds up to hours of lost time and uneven data quality.

### Design (Mockup)

***Post-Call Summary***
🕒 May 28, 2025 | 11:42 AM MST · Duration: 6 min 12 sec
📲 Call Type: IB ; [Conversation ID]
👤 CCP: Jamie A.    📇 Customer: Allen M.
✅ Suggested Disposition: **Servicing - Loan Detail Inquiry**
🔍 Summary: [bullets]
🟡 Sentiment: Mild Concern / Neutral
**📥 [Post to CRM Log]   🖊️ [Edit Note]**

* Reduce average post-call documentation time from ~60 seconds to <30 seconds
* 90%+ accuracy in wrap-up code suggestions
* <20% manual override rate
* 85% of eligible calls have the summary widget reviewed and posted

### Detailed Requirements Table

Out Of Scope: ❌ PL, PCL, BNPL (Spectrum) / ❌ Multilingual transcription / ❌ Supervisor editing

| **Requirement + User Stories** | **Description** | **Notes** |
| --- | --- | --- |
| **Summary Generation** | | |
| **CCP**: "I want an auto-generated summary after a call." | AC: I can see a summary for voice, chat, and email. | Needs format review |
| **Wrap-Up Code Generation** | | |
| **CCP**: "I want suggested wrap-up codes so that I can review them fast." | Suggest top relevant codes from standard set. | |
| **Sentiment Tagging** | | |
| **Oversight**: "I want to identify frustrated customers." | Flag summaries with sentiment tags for QA visibility. | |
| **Integration** | | |
| **PM**: "I want each of these to show up in the Activity Log". | Send to `activity-srvc` as `account_comment_added`. | |
| **Analyst**: "I want reports to stay valid, such as dispositions". | Send to `dw_genesys` schema, add new column under Participants table. | |

### FAQs

* What fallback options are available if transcription services fail?
  * **Answer:** CCPs will manually enter the disposition from a list.
* What thresholds should trigger QA alerts for sentiment or low-confidence notes?
  * **Answer:** Implementation team will recommend thresholds based on model confidence and QA needs.
