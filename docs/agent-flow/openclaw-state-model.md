# OpenClaw State Model

OpenClaw should own workflow state instead of scraping Codex's interactive session picker.

## Work Item Key

Use:

`<repositoryFullName>#<issueNumber>`

Also store the human display key:

`<projectName>-issue-<issueNumber>`

## Suggested Record

```json
{
  "projectName": "example",
  "repository": "owner/example",
  "issueNumber": 123,
  "sessionName": "example-issue-123",
  "codexSessionId": "019e0c09-a4ee-7d00-9afd-0d484da0780f",
  "repoPath": "/srv/repos/example",
  "worktreePath": "/srv/worktrees/example/issue-123",
  "branch": "issue-123-short-title",
  "mode": "code",
  "status": "ready-for-review",
  "lastRunAt": "2026-05-09T12:00:00Z",
  "lastRunSummary": "Branch pushed and PR updated."
}
```

## Status Values

- `idle`
- `starting`
- `running`
- `initialized`
- `planned`
- `pushed`
- `blocked`
- `ready-for-review`
- `failed`
- `merged`

## Resume Rule

If `codexSessionId` exists, use:

```bash
codex exec resume <codexSessionId> --json "<prompt>"
```

If it does not exist, use:

```bash
codex exec -C <repoPath> --json "<prompt>"
```

After a new session starts, capture and store the Codex session id.
If the JSON output does not expose it cleanly, OpenClaw may use Codex local state as a fallback, but the OpenClaw mapping remains authoritative.

