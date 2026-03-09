---
name: omar-spec-style
description: Write product specs (PRDs) in Omar's writing style for Upgrade, Inc. Use this skill whenever Omar asks to create a spec, PRD, product requirements document, product specification, feature spec, or requirements doc. Also trigger when he says "write a spec for", "draft a PRD", "help me spec out", "create requirements for", or any variation of writing a product document for a feature or initiative. This skill captures Omar's distinct spec-writing patterns gathered from 14 deeply-analyzed real Confluence specs (out of 109 total pages) spanning 2023-2026, covering migrations, voice AI, CRM tooling, compliance automation, conversational AI (Sierra/Upgrade Assist), and CCP tooling.
---

# Omar's Spec Writing Style

This skill enables Claude to write product specs (PRDs) that match Omar's established writing style at Upgrade, Inc. The style was extracted from 109 Confluence pages authored by Omar across domains including IVR, chat migration, CRM tooling, workflow automation, vendor integrations, conversational AI (Sierra/Upgrade Assist), compliance automation, real-time coaching, and internal AI tooling (Connie). Full content was analyzed from 11 representative specs spanning 2023-2026, with patterns verified across the broader corpus.

## Before Writing

Before writing, Claude should ask Omar for the following inputs (if not already provided):
1. **Feature/initiative name** — What are we calling this?
2. **TL;DR** — 1-2 sentence summary of what we're doing
3. **Why** — Business rationale / problem statement
4. **What** — Key requirements or user stories
5. **Who** — Stakeholders, engineering teams, contributors
6. **Target quarter or date** — When is this planned for?
7. **Any related Jira tickets, Slack channels, or design links?**

If Omar provides a rough brain dump, Claude should organize it into spec format without requiring all fields upfront.

---

## Spec Structure (in order)

Omar's specs follow a consistent structure. Not every section appears in every spec — use judgment based on scope and complexity.

### 1. Title
- Format: `PRD: [Feature Name]` for formal specs
- Or just a descriptive title for lighter specs (e.g., "Debit Card Payments in IVR & Sierra for Delinquent PL/HI")
- Include phase number if applicable: `PRD: [Feature] - Phase 1`

### 2. Status Line (if applicable)
- A single line at the very top if the spec has been delivered, has a go-live date, or is blocked
- Examples: `Delivered`, `Delivered MVP on Q1 2025.`, `Go Live: 2024-05-01`, `Rollout on May 20th, 2025`
- Delayed/blocked: `Delayed until this POC is complete: [link]` or `Deprioritized until further notice after speaking with [Name].`

### 3. Header Metadata Table
Always the first structural element. A **2-column key-value table** with bolded keys. Include only the rows relevant to the spec:

| Key | Usage |
|-----|-------|
| **TL;DR** | Always include. 1-2 concise sentences. Action-oriented. |
| **Go Live** | Include if date is known |
| **Targeted for** | Include if planned for a specific quarter |
| **Problem Statement** | Sometimes used instead of TL;DR for newer specs. More descriptive than TL;DR — describes the pain point in one sentence. |
| **Objective** | Sometimes paired with Problem Statement (newer pattern). States what we're going to do about it. |
| **Roadmap** | Stakeholder alignment tracking. Format: "Presented to Execs by: @Name / Aligned with Product: @Name / Aligned with Design: @Name / Aligned with Engineering: @Name / Added to: [roadmap link]" |
| **Reviewed** | Alternative to Roadmap (used more in 2025+). "Execs / Stakeholders: @Name / Engineering: [Team] / Added to: [roadmap link]" |
| **Tickets** | Jira issue links |
| **Contributors** | @mentions of key collaborators |
| **Slack** or **Slack(s)** | Channel name in backtick code format, e.g., `#channel_name` with link |
| **InfoSec** | InfoSec ticket link when applicable (newer specs) |
| **Slack** | Channel name in backtick code format, e.g., `#channel_name` with link |

### 4. Problem Alignment (or "Why Should We Do This?" or "Why are we doing this?" or "Why [Feature Name]?")
This section explains the business rationale. Omar's patterns have evolved over time:

#### Pattern A: "Because..." framing (2023-2024 specs)
- Often starts sentences with "Because" to tie problems to business impact
  - Example: *"Because delinquency trends are increasing, causing our investors to scrutinize our collection performance."*
  - Example: *"Because the existing method is still manual and meant to be a temporary solution."*

#### Pattern B: Narrative paragraph (2025-2026 specs)
- A short vivid scenario (2-4 sentences) that makes the reader *feel* the problem before listing the requirements
  - Example: *"Imagine a contact center rep, eager to help a borrower resolve an issue, clicks on a customer's number only to unknowingly ring the customer at 6 AM. These honest mistakes result in regulatory violations."*
  - Example: *"Today, when a servicemember calls about an SCRA interest rate reduction... a human agent walks through a multi-step procedure—authenticating the caller, asking a series of scripted questions, collecting documentation details..."*

#### Pattern C: Problem Statement + Objective (newest specs)
- Header metadata contains "Problem Statement" and "Objective" rows
- Followed by bullet points on value: cost reduction, compliance, data quality, availability

#### Consistent sub-patterns across all eras:
- **Current State walkthrough**: Numbered steps showing the existing manual/broken process
  - Example: "1. Agent dispositions a complaint in Genesys... 2. Wrap Up Code is currently pulled from DB... 3. Cleaned up via python... 4. Uploaded to CMT Jira board"
- **Bullet points for pain points**: Short, punchy bullets
  - "Automates manual effort (DB queries and adhoc scripting)"
  - "Reduce costs."
  - "Eliminate screenshotting so Legal can redeploy **2 FTE** effectively"
- **Volume/data context**: Include relevant numbers, stats, top drivers
  - "Avg 2023 - 30K calls/month"
  - "1 subpoena is received every day"
  - "~233 Q4-2024 outbound calls violated the TCPA AM-PM local-time rule"
- **Success Criteria / Success Metrics** (often in newer specs):
  - Numbered list of specific, measurable targets
  - Example: "90% reduction in TCPA violations, measured monthly by Compliance team audit logs."
  - Example: "Reduce Average Handle Time (AHT) by at least 15% within 6 months."
- **Cost comparison** (for cost-driven specs):
  - Direct dollar comparison: "Cost of a call is about $2.80... Cost of a contained call using Sierra is $1.07"
  - Links to supporting spreadsheets
- **Metrics table** (for KPI-driven specs, especially Voice/AI):

| Metric | Target | Definition | Tracking Method |
|--------|--------|------------|-----------------|

  - Example rows: Containment Rate → 30% reduction, CSATs → 4/5 average, Response Time → <2s for 90%
- **Business Metrics + Technical Metrics** (newer Sierra specs):
  - Separate labeled bullet sections under these headers
  - Business: AHT reduction, compliance errors, onboarding time
  - Technical: iframe load time, uptime SLAs
- **AI strategy cross-references**: "This is part of our AI strategy during customer interactions with the CCP" with links to related specs (IVR, Real-Time, PostCall)
- **Outcome and Satisfaction** (occasionally):
  - "**Outcome**: decrease IVR wait times, increase frictionless experiences"
  - "**Satisfaction**: NPS Survey"
- **Fun facts or cultural references** (Omar's personality):
  - "Just like Microsoft Word's 'Clippy' (sorry Gen Zers, google it)..."
  - "Fun fact: Connie is named after Confluence."

### 5. Solution Alignment (or "What Are We Doing?")
The core requirements section. Omar uses **structured tables** extensively rather than prose.

#### Requirements Table Formats (pick the one that fits):

**Simple feature table:**
| Key Feature | User Story | Design Req | Notes |
|-------------|-----------|------------|-------|

**Detailed requirements table:**
| REQ # | Requirement | Acceptance Criteria | Notes | Epic |
|-------|-------------|-------------------|-------|------|

**Detailed with description:**
| Requirement | Description | Acceptance Criteria | Notes / Tasks |
|-------------|-------------|-------------------|---------------|

**User story + team table (for newer specs):**
| Name | User Stories | Description | Team |
|------|-------------|-------------|------|

#### User Story Format
Omar uses multiple user story styles depending on context:

**Formal (2023-2024):** Italicized traditional format
- *"As a CRM user, I want to search for customer updates using a tag so that I can quickly find relevant activities."*

**Conversational (2025-2026):** Role + quoted statement
- CCP: "I want to know if it's OK to call this customer right now."
- Customer: "Give me a quick debit option."
- PM: "I want to detect when the customer is getting upset so that I can include in summarization."
- Supervisor: "Sometimes we must call."

**Volume annotations next to requirement names** (newer pattern):
- **SCRA Flow** 200–300/mo
- **Bankruptcy Flow** 2,600/mo
- **Name/DOB update** 11,500/mo*

#### Requirement Writing Style
- Concise and direct
- Use "I can..." or "Allow..." for capability requirements
- Reference specific APIs, endpoints, or system names
- Include SQL-like details when relevant: "include either a LIKE 'complaint' in the WHERE clause or add wildcard"
- Strikethrough (~~text~~) for removed or changed requirements
- Status emojis: ✅ for completed/delivered, ⚠️ for warnings, ❗ for critical, ❌ for out-of-scope items
- **✅ Vendor deliverable** — mark requirements that are vendor-owned (e.g., Sierra features)
- **Category header rows** — bold text in the first column acting as section dividers within the table (e.g., "**Summary Generation**", "**Integration**", "**InfoSec Review**")
- **Inline code samples** — when an SDK or API is involved, Omar includes actual code snippets directly in the requirements table (e.g., Sierra `onPostConversation` hook code)
- **Inline action items** — "Omar to test simulations", "@Omar to ask Sierra for guidance", "Body of work / challenge"

### 6. Design
- Section header, then links to Figma, Lucidchart, or embedded images
- Keep it minimal — link out rather than describe designs inline
- Sometimes includes before/after comparison tables
- Newer specs include low-fidelity mockups/Google Sites links alongside high-fidelity Figma links
- Sometimes a flow chart image is embedded with a caption like "Assume customer is eligible"
- **Text/emoji mockups** (newer pattern): When a UI is being proposed but Figma doesn't exist yet, Omar writes a formatted text mockup using emojis and markdown to convey the concept. Example: "🕒 May 28, 2025 | 11:42 AM MST · Duration: 6 min 12 sec / 📲 Call Type: IB / ✅ Suggested Disposition: **Servicing - Loan Detail Inquiry** / 🔍 Summary: [bullets] / 🟡 Sentiment: Mild Concern"

### 7. Service Integration Architecture (for complex specs)
- A newer pattern (2025-2026) for specs involving multiple services
- Describes end-to-end flow as a **numbered list** of system interactions
- References specific service names (Actor To Do Service, Doc Management, Activity Service, etc.)
- Example: "1. AI agent completes intake form and calls createActorFormTodo(...) → 2. Actor To Do appears on dashboard → ... → 12. If 45 days elapse, Service Request may be closed."
- Includes Phase 2 notes at the bottom of the architecture section

### 8. Implementation Details (for complex specs)
- Architecture diagrams or flow references
- Integration details (API endpoints, data elements)
- Pricing tables for vendor integrations
- **Technical Implementation Notes** subsection (sometimes marked "AI Suggested")
- **References** subsection with API documentation links, vendor docs, EDW table names, etc.

### 9. Error Handling & Edge Cases (newer pattern)
- Table format for edge cases:

| Scenario | Requirement | Notes |
|----------|-------------|-------|

- Examples: Landline/Delivery Failure, Wrong Number, Refusal to use SMS, Verification Failure
- Each row includes the bot's exact scripted response in italics
- Sometimes in a separate child page (e.g., "Edge Cases & Error Handling – [Feature]")

### 10. Launch Readiness (for larger initiatives)
Table format:

| Area | Description | Stakeholder(s) | Notes | Status (ETA) |
|------|-------------|----------------|-------|--------------|

Categories: Kick off, Analytics, InfoSec, Dev complete, Test complete, Go Live, Internal Comms

### 12. Questions
Multiple formats:

**Table format (formal specs):**
| Topic | Question | Reference | Answer |
|-------|----------|-----------|--------|

**Numbered list format (newer specs):**
- Numbered questions with indented answers prefixed by "Omar:" when self-answered
- Example: "1. How will this impact CCP procedures? → Omar: I don't know. Will discuss with compliance, fraud and ops."

**Category-split format (newest specs):**
- "Open Questions" header, with sub-headers like "#### Product" and "#### Engineering"
- Keeps questions organized by audience

Include meeting notes and in-progress answers. It's OK for answers to be informal/incomplete. "I don't know" is acceptable.

### 13. TBD or Fast Follow (newer pattern)
- A table of features that are acknowledged but not in current scope
- Uses same requirements table format but explicitly labeled "TBD or Fast Follow"
- Strikethrough requirements that were considered and cut

### 14. Constraints (newer pattern)
- Short bullet list under a "Constraints" header
- Example: "Avoid generation of composite 'new work product' summaries."

### 15. Out of Scope
- Bullet list of explicitly excluded items
- Sometimes marked with ⚠️ emoji or ❌ emoji prefix
- Brief rationale when helpful
- Can appear inline within a section (not always its own section), especially in newer specs
- Example with ❌: "❌ PL, PCL, BNPL (Spectrum) / ❌ Multilingual transcription"

### 16. FAQs (newer pattern)
- Short Q&A pairs at the bottom of the spec
- Format: Question as bullet, answer indented below with "Answer:" prefix
- Used when common stakeholder questions are predictable

### 17. Other References / Related Specs
- Links to related specs, Google Sheets, external docs
- "Child pages:" or "Go Back To Parent Page" for page hierarchy

---

## Phasing Pattern
Omar frequently breaks work into phases:
- Phase 1: MVP or core functionality
- Phase 2: Enhancements, additional attributes, scale
- Each phase gets its own requirements table
- Clearly label what's in each phase

---

## Voice & Tone Characteristics

1. **Concise and telegraphic** — Omar doesn't write long paragraphs. Sentences are short and direct. Tables do the heavy lifting.
2. **Action-oriented TL;DRs** — Start with a verb: "Migrate...", "Integrate...", "Add...", "Transfer...", "Automate...", "Deploy..."
3. **Narrative hooks (newer specs)** — 2-4 sentence scenarios that make the reader feel the problem before diving into requirements
4. **Practical over theoretical** — References real systems (Genesys, Spectrum, Zendesk, Jira, Sierra, VQ, Prove), real APIs, real data pipelines
5. **Stakeholder-aware** — Always names who reviewed, who owns what, who to talk to
6. **Cross-functional** — Addresses Engineering, Ops, Compliance, Legal, InfoSec, Design concerns in one doc
7. **Living document** — Includes meeting notes, Q&A, status updates, strikethroughs of changed decisions
8. **Link-heavy** — Points to Jira tickets, Google Sheets, Slack channels, Figma, Lucidchart, Google Sites prototypes rather than duplicating content
9. **Domain-specific vocabulary** — Uses Upgrade terminology naturally: CCP (Contact Center Professional), Spectrum, VQ, CRM, Activity Service, containment, wrap up codes, ANI, IVR, PCI DSS, Actor To Do, TCPA, DNC
10. **Honest about unknowns** — "I don't know", "TBD", "Omar: come back to this", "Need to validate volume"
11. **Personality shows through** — Fun facts, cultural references (Clippy), creative naming (Connie), inline commentary
12. **Volume-conscious** — Always quantifies the problem: monthly volumes, FTE impact, cost savings, percentage targets
13. **Conversational user stories in newer specs** — Moves from formal "As a..." to direct quoted voice: CCP: "I want..."

---

## Anti-Patterns (What NOT to Do)

- ❌ Don't write long narrative prose paragraphs — use tables and bullets
- ❌ Don't use vague language — be specific about systems, APIs, teams
- ❌ Don't skip the metadata table — it's always first
- ❌ Don't omit the "Why" — always explain the business rationale
- ❌ Don't write user stories in non-italic format
- ❌ Don't forget to include Jira ticket placeholders even if tickets don't exist yet
- ❌ Don't use generic PM jargon — use Upgrade-specific terminology
- ❌ Don't write overly polished marketing language — this is a working doc

---

## Template (Quick Start)

When Omar asks for a spec, start with this skeleton and fill in based on the inputs:

```markdown
| **Problem Statement** | [1 sentence describing the pain point] |
| --- | --- |
| **Objective** | [1 sentence describing what we're doing about it] |
| --- | --- |
| **Reviewed** | Execs / Stakeholders: / Engineering: / Added to: |
| --- | --- |
| **Tickets** | [Jira links or "TBD"] |
| --- | --- |
| **Slack(s)** | `#channel_name` |
| --- | --- |

* **[Value prop 1]:** [Quantified impact]
* **[Value prop 2]:** [Quantified impact]

## Narrative

[2-4 sentences painting a vivid scenario of the problem. Make the reader feel it.]

#### Out Of Scope

* [Explicitly excluded item 1]
* [Explicitly excluded item 2]

---

| **Requirement** | **Description** | **Notes** |
| --- | --- | --- |
| **[Feature Name]** [volume/mo] | [User story or description] | [Context, links, team] |
| **[Feature Name]** | [User story or description] | [Context, links, team] |

---

### Design

[Link to Figma or design artifacts]

---

### Questions

1. [Question]?
   1. **Omar**: [Answer or "TBD"]
```

**Alternative header (for specs that use TL;DR):**

```markdown
| **TL;DR** | [1-2 sentence action-oriented summary starting with a verb] |
| --- | --- |
| **Reviewed** | Execs & Stakeholders: / Design: / Engineering: / Added to: |
| --- | --- |
| **Slack** | `#channel_name` |
| --- | --- |
```

---

## Reference Specs

For detailed examples, see the `references/` directory which contains full-text exports of Omar's specs from Confluence. Key exemplar specs:

- `references/exemplar-specs.md` — Contains 13 full specs showing the range of Omar's writing style across different types of initiatives (migrations, vendor integrations, UI improvements, workflow automation, conversational AI, compliance automation, internal AI tooling, authentication, voice AI, CCP tooling, post-call automation)

Additionally, Omar's formalized templates are available at the repo root:

- `../../Template-PRD.md` — Omar's latest PRD template with structured sections: Overview table, Narrative, Why, Success Metrics (Business/User-Centric/Technical), Non-Goals, Design References, Requirements, Appendices, Open Questions
- `../../Template-Use-Case-Without-PRD.md` — Use Case Specification (UCS) template for detailed use case documentation with Main Flow, Alternate Flows, Postconditions, and Success Criteria
- `../../Template-Use-Cases.md` — Use Cases template for PRD-attached use cases

When writing a new spec, prefer the patterns in SKILL.md (extracted from real specs) over the templates. The templates represent Omar's aspirational structure; the SKILL.md represents how he actually writes in practice. Use both together for the best result.
