# OpenClaw Codex Workflow

## Goal

Use GitHub issues as the durable task source, OpenClaw as the coordinator, and Codex as the implementation agent.

## Roles

- Dev: lead, issue author, reviewer, final merge authority.
- OpenClaw: Discord-facing coordinator, session mapping owner, notification center.
- Codex: issue reader, planner, coder, branch/PR author.
- GitHub: durable task log through issues, comments, branches, and PRs.

## Session Key

Use this human-readable key:

`<projectName>-issue-<issueNumber>`

OpenClaw should store the Codex UUID for that key.
The UUID is the reliable resume identifier.

## Modes

- `init`: refine the issue, update issue body/comments, do not code.
- `reinit`: re-read issue comments and update understanding, do not code by default.
- `plan`: post an implementation plan to the issue, do not code.
- `code`: create or continue the issue branch, implement, validate, push.
- `merge`: create/update/merge PR only when explicit maintainer approval is present.

## New Session Command Shape

```bash
codex exec -C <repo-path> --json "<prompt>"
```

The prompt should include:

- project name
- repository
- issue number
- session display name
- mode
- branch name
- instruction to read `AGENTS.md` and relevant skills

## Resume Command Shape

```bash
codex exec resume <codex-session-id> --json "<prompt>"
```

Do not use `codex resume --all` in automation.
It is an interactive picker for humans.

## Status Contract

Codex should write durable status to GitHub:

- issue comment when work starts
- issue comment when blocked
- issue comment when ready for review
- PR summary and validation when a PR is created or updated

OpenClaw should send short Discord updates:

- started
- initialized
- planned
- pushed
- blocked
- ready for review
- failed
- merged

GitHub contains the details.

