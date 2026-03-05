# [AI Agent / System] — Use Case Requirements

**[Use Case 1 Name] | [Use Case 2 Name] | [Use Case 3 Name]**

Author: [Name], [Title] | [Month Year] | v[X.X] Draft

---

## Overview

| | |
|---|---|
| **Problem Statement** | - [Describe the manual process agents currently follow and the resulting inefficiency — high handle times, inconsistent data, etc.] |
| | - [Quantify the opportunity — combined monthly volume, estimated time savings, error reduction potential.] |
| **Objective** | - [What the system will do — e.g., "Enable the AI agent to fully handle intake for [use cases] without human involvement."] |
| | - [Quantified targets — e.g., "Reduce intake handle time by 40–60%, increase data completeness to >95%."] |
| **Volume** | **[Use Case 1]:** [X]/mo \| **[Use Case 2]:** [X]/mo \| **[Use Case 3]:** [X]/mo* |
| | *\* [Any caveats about volume data — e.g., suspected outliers, data quality issues]* |
| **Reviewed** | ☐ Execs ☐ Stakeholders ☐ Design ☐ Engineering ☐ Compliance ☐ Legal |
| **Slack** | **#[channel-name]** |

---

## Narrative

[Single paragraph describing the current manual process across all use cases, why the work is repetitive/predictable, and how encoding it as structured flows enables end-to-end automation. Mention the key outcome: structured data capture, compliance enforcement, system updates, and routing — all without a human agent.]

---

## Why should we do this?

- **[Value lever 1 — e.g., Agent capacity]:** [How automating these interactions frees human agents for complex work.]
- **[Value lever 2 — e.g., Compliance enforcement]:** [How automation eliminates human error on compliance-sensitive interactions.]
- **[Value lever 3 — e.g., Data quality & speed]:** [How structured forms with validation ensure complete data on first capture.]
- **[Value lever 4 — e.g., 24/7 availability]:** [How customers benefit from always-on access.]

---

## Success Metrics

### Business Metrics

| Metric | Target | Measurement | Tooling | Cadence |
|---|---|---|---|---|
| [e.g., AI intake containment] | [e.g., >80% handled without human agent] | [How measured] | [Tool] | [Cadence] |
| [e.g., AHT reduction] | [e.g., −40–60%] | [How measured] | [Tool] | [Cadence] |
| [e.g., Data completeness] | [e.g., >95% fully complete] | [How measured] | [Tool] | [Cadence] |

### User-Centric Metrics

| Metric | Target | Measurement | Tooling | Cadence |
|---|---|---|---|---|
| [e.g., Customer CSAT] | [e.g., ≥4.0/5.0] | [How measured] | [Tool] | [Cadence] |
| [e.g., Completion rate] | [e.g., >75% of started flows] | [How measured] | [Tool] | [Cadence] |
| [e.g., Escalation rate] | [e.g., <15% require human handoff] | [How measured] | [Tool] | [Cadence] |

### Non-Goals

- [What the system will NOT do — e.g., "Will not perform back-office processing itself. Handles intake and routing only."]
- [Deferred capabilities — e.g., "Real-time document verification (OCR) is out of scope for initial release."]
- [Language/channel limitations — e.g., "Spanish voice support deferred to future phase."]

---

## Use Case [N]: [Use Case Name]

**Volume: [X]/mo | Channel: [Chat & Voice / Chat only] | Compliance: [High / Critical / Standard]**

### Current State (Human Agent)

[Paragraph describing the current manual process: what the agent does step by step — authentication, data collection, system updates, notations, routing. Be specific about tools, systems, and handoff points.]

### AI Agent Flow

[Paragraph describing how the AI agent handles the same process conversationally. Mention: intent detection, data collection sequence, system actions on submission, and routing.]

### Form Fields

| Field | Type | Required | Validation / Notes |
|---|---|---|---|
| [Field name] | [Text / Choice / Yes/No / Date / Phone / SSN / Auto] | [Yes / Optional / Conditional] | [Validation rules, acceptable values, conditional logic] |
| [Field name] | [Type] | [Required?] | [Notes] |
| [Field name] | [Type] | [Required?] | [Notes] |

### Decision Logic

| Condition | Agent Action | System Outcome |
|---|---|---|
| [If condition X] | [What the AI agent does/says] | [What the system does — tickets, updates, routing] |
| [If condition Y] | [Agent action] | [System outcome] |
| [If condition Z] | [Agent action] | [System outcome] |

### Compliance Guardrails

[Only include this section for use cases with compliance requirements. Use bold + red-emphasis patterns for critical rules.]

- **[CRITICAL RULE in caps]** [Explanation of why and what to do instead.]
- **[CRITICAL RULE in caps]** [Explanation.]
- [Standard guardrail — e.g., "All name variations must be confirmed and recorded."]
- [Standard guardrail — e.g., "Customer has X days to submit documentation."]

### System Actions on Submit

- **[Service/System 1]:** [What happens — API call, status change, customer-facing action.]
- **[Service/System 2]:** [What happens.]
- **[Service/System 3]:** [What happens.]
- **[Service/System 4]:** [What happens.]
- **[Fallback]:** [What happens if the primary path isn't available.]
- **[Expiration]:** [What happens after a timeout — e.g., 45 days without document upload.]

---

*[Repeat the "Use Case [N]" section above for each additional use case. Use sub-sections (e.g., "3A: Name Change", "3B: DOB Change") for use cases with distinct sub-flows under one umbrella.]*

---

## Cross-Cutting Requirements

### Authentication & Verification

- [List authentication requirements per use case — e.g., "All use cases require full customer authentication before intake begins."]
- [Use Case 1: Any special auth — e.g., "Accepts authorized third parties."]
- [Use Case 2: Auth level — e.g., "Standard authentication. No additional MFA required."]
- [Use Case 3: Auth level — e.g., "Standard authentication + Genesys MFA required."]

### Bilingual Support

- [Current state of multilingual scripting.]
- [What the AI agent will support — e.g., "Chat should support Spanish if the underlying model supports it."]
- [What is deferred — e.g., "Voice-based Spanish support deferred to future phase."]

### Escalation & Handoff

- [General rule: When the AI agent cannot complete intake, it must warm-transfer with full context.]
- [Use case–specific escalation rules — e.g., "For Bankruptcy: If customer mentions dismissal, escalate to Team Lead."]
- [Use case–specific dead ends — e.g., "For DOB: If MFA fails for non-phone reasons, flow cannot continue."]

### Service Integration Architecture

[Paragraph describing the unified end-to-end flow across all use cases — which services are involved and how they replace the previous manual/email-based processes.]

#### End-to-End Flow

1. [Step 1: AI agent completes intake and triggers initial service call — e.g., createActorFormTodo(form_type, external_id, account_id)]
   - [Sub-step: form_type A → Customer uploads X]
   - [Sub-step: form_type B → Customer uploads Y]

2. [Step 2: What appears on the customer's dashboard.]
3. [Step 3: Initial statuses set.]
4. [Step 4: Activity Service notation.]
5. [Step 5: Service Request created.]

6. [Step 6: Customer uploads document. Doc Management appends to profile.]
7. [Step 7: Activity notation on upload.]
8. [Step 8: Back-office reviews.]

9. [Step 9: Fulfillment — back-office marks complete.]
   - [Sub-step: Request status → COMPLETED]
   - [Sub-step: If all requests done → overall status → FULFILLED]
10. [Step 10: Activity notation on fulfillment.]

11. [Step 11: Customer receives confirmation.]
12. [Step 12: Expiration path — what happens after X days without action.]
    - [Sub-step: Status → EXPIRED]
    - [Sub-step: New request created]
    - [Sub-step: Activity notation]

#### Fallback for Email/Mail Submission

- [Describe how traditional submission methods (email, physical mail) are handled as fallbacks.]
  - [Email details]
  - [Mail details]
  - [Both methods trigger the same fulfillment flow once received.]

### Integration Requirements

- **1. [Service Name]:** [What it does. List endpoints/methods.]
  - [Endpoint 1 → What it does]
  - [Endpoint 2 → What it does]
  - [Endpoint 3 → What it does]
  - [Configuration: form types, status flows, events]

- **2. [Service Name]:** [What it does. When triggered.]

- **3. [Service Name]:** [What it does. Routing rules per use case.]
  - [Use Case 1: Route to X queue]
  - [Use Case 2: Route to Y queue]
  - [Use Case 3: Route to Z queue]

- **4. [Service Name]:** [What it does. When notations are posted.]
  - [Event 1]
  - [Event 2]
  - [Event 3]

- **[Additional integrations]:** [CRM tabs, Jira, Spectrum, etc.]

---

## Phasing

### Phase 1: [Use Case Name] ([Rationale — e.g., "Highest Volume"])

- [Capability 1 included in this phase.]
- [Capability 2.]
- [Capability 3.]
- [Capability 4.]

**Target: [X] interactions/mo fully automated.**

### Phase 2: [Use Case Name]

- [Capability 1.]
- [Capability 2.]
- [Capability 3.]

**Target: [X] interactions/mo fully automated.**

### Phase 3: [Use Case Name]

- [Capability 1.]
- [Capability 2.]
- [Capability 3.]

**Target: [X] interactions/mo (after [any analysis needed]).**

### Phase 4: [Channel Expansion / Future Scope]

- [Capability 1 — e.g., "Extend all use cases to voice."]
- [Capability 2 — e.g., "Multi-language support."]
- [Capability 3 — e.g., "Real-time document classification (OCR)."]

---

## Open Questions

The following items require further input before or during implementation:

- **[Topic 1]:** [Specific question. Who needs to answer it. What it blocks.]
- **[Topic 2]:** [Question.]
- **[Topic 3]:** [Question.]
- **[Topic 4]:** [Question.]
- **[Topic 5]:** [Question.]
- **[Topic 6]:** [Question.]

---

### Formatting Notes

This use cases template follows the Upgrade Assist document style:

- **Overview table** at top with Problem Statement, Objective, Volume, Review status, Slack
- **Each use case** follows a consistent structure: Current State → AI Agent Flow → Form Fields table → Decision Logic table → Compliance Guardrails → System Actions on Submit
- **Form Fields tables** use 4 columns: Field, Type, Required, Validation/Notes
- **Decision Logic tables** use 3 columns: Condition, Agent Action, System Outcome
- **Compliance Guardrails** use bold red-emphasis for critical rules (NEVER/IMMEDIATELY patterns)
- **Cross-Cutting Requirements** cover auth, bilingual, escalation, and service integration architecture
- **Service Integration Architecture** describes the full end-to-end flow with numbered steps
- **Phasing** prioritized by volume/impact with explicit automation targets per phase

When generating the docx version, the document uses:
- Color palette: Green (#059669), Dark (#1F2937), Medium (#4B5563), Light Green (#ECFDF5), Amber (#D97706), Red (#DC2626)
- Font: Arial throughout
- Headers/Footers with page numbers and "Confidential — Upgrade, Inc." branding
- Compliance-critical text rendered in red (#DC2626) with bold emphasis
