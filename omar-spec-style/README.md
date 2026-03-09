# Omar's Spec Writing Style — Claude Skill

A Claude skill that writes product specs (PRDs) matching Omar Torresola's established writing style at Upgrade, Inc.

## What This Does

When installed, this skill teaches Claude how to write specs the way Omar writes them — with the right structure, tone, terminology, and formatting. It was built by analyzing 14 real specs from Omar's Confluence space spanning 2023–2026, covering migrations, voice AI, CRM tooling, compliance automation, conversational AI (Sierra/Upgrade Assist), and CCP tooling.

## Key Patterns Captured

- **Header metadata tables** (TL;DR, Problem Statement, Objective, Reviewed, Tickets, Slack)
- **Problem framing evolution**: "Because..." framing → narrative scenario hooks → Problem Statement + Objective
- **Structured requirements tables** with conversational user stories and volume annotations
- **Metrics tables** for KPI-driven specs
- **Service Integration Architecture** sections
- **Error Handling & Edge Cases** tables
- **TBD / Fast Follow** sections
- **Text/emoji design mockups**
- **Living document patterns**: strikethroughs, inline action items, "I don't know" honesty

## How to Install

1. Download `omar-spec-style.skill`
2. In Claude.ai, go to **Settings → Skills**
3. Upload the `.skill` file

Or point Claude at this repo's `SKILL.md` directly.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | The skill definition — patterns, structure, voice, templates |
| `references/exemplar-specs.md` | 13 full spec examples for style reference |
| `omar-spec-style.skill` | Packaged skill file for Claude installation |
| `CHANGELOG.md` | History of updates to the skill |

## Keeping It Updated

This skill is synced weekly from Omar's Confluence space. Each sync pulls new specs, identifies evolved patterns, and updates the skill files.

## Usage

Just ask Claude to write a spec:

> "Write a spec for [feature name]"
> "Help me draft a PRD for [initiative]"
> "Spec out [idea] in my style"

Claude will follow your established patterns automatically.

---

*Built with Claude · Sourced from Confluence · Maintained on GitHub*
