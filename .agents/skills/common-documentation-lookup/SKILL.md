---
name: common-documentation-lookup
description: Find and read the repository guidance needed before planning or editing. Use when Codex needs to understand project docs, AGENTS.md files, architecture notes, PRD material, or local conventions before acting.
---

# Common Documentation Lookup

Use this skill before planning or implementation when the task depends on repository context.

## Read Order

1. Root `AGENTS.md`.
2. The nearest child `AGENTS.md` for each touched area.
3. The GitHub issue body and latest comments when the task is issue-driven.
4. Relevant docs under `docs/`.
5. Relevant README files near the touched code.

## Lookup Rules

- Prefer local repository docs over assumptions.
- Prefer the most specific `AGENTS.md` that applies to the files being changed.
- If docs conflict, call out the conflict and use the most local guidance unless a root workflow rule applies.
- If required docs are missing, continue with existing code patterns and note the documentation gap.
- Do not bulk-read unrelated docs; read enough to make the current task safe.

## Output Expectations

When this skill is used for issue work, summarize:

- relevant project rules
- relevant area-specific rules
- docs that were read
- missing or ambiguous guidance

Keep the summary short enough to fit naturally in an issue comment, PR body, or final handoff.

