---
name: jira-ticket
description: "Create well-structured Jira tickets using a consistent User Story template with Acceptance Criteria, Technical Notes, Definition of Done, and Links/References sections. Use when user asks to create a Jira issue, ticket, task, story, or file a bug."
---

# Jira Ticket

Create Jira tickets following a consistent team template. User Story format with optional sections.

## When to Use

User says: "create a ticket", "file a Jira issue", "make a new task", "write a Jira story", "create a new issue", "file a bug".

## Template

```
As a <role>, I want <capability> so that <benefit>.

### Acceptance Criteria
- Each bullet must be independently verifiable pass/fail

### Technical Notes
- Implementation details, gotchas, file paths, patterns to follow

### Definition of Done
- [ ] go test ./... passes
- [ ] go vet ./... passes
- [ ] MR created against <branch>

### Links / References
- Related issues: #
- MR: #
```

## Section Rules

| Section | Required | Purpose |
|---------|----------|---------|
| User Story | Yes | Single line: role + capability + concrete benefit |
| Acceptance Criteria | Yes | Clear pass/fail conditions, no ambiguity |
| Technical Notes | No | Tribal knowledge, gotchas, file paths, reference patterns |
| Definition of Done | Yes | Verification checklist. Update commands and branch per project |
| Links / References | No | Cross-references to issues, MRs, designs, docs |

## Formatting Rules

- `### ` for section headings (Markdown h3)
- `- [ ]` for DoD checklist items
- `- ` for bullet lists in AC and Technical Notes
- Plain intro paragraph before sections — no heading, serves as Jira description preview
- Omit empty sections entirely — never include blank sections

## Workflow

### 1. Gather requirements

Ask user for:
- User story (role + capability + benefit)
- Acceptance criteria
- Technical notes (if any)
- Parent Epic key (default: SPPI-19)
- Issue type (Task / Bug / Story — default Task)
- Priority (default Medium)
- Target branch for DoD MR item

### 2. Resolve cloud ID

Use `atlassian_getAccessibleAtlassianResources` to discover cloud ID.

### 3. Create issue

Use `atlassian_createJiraIssue`:
- `projectKey`: "SPPI"
- `issueTypeName`: as determined
- `summary`: short descriptive title
- `description`: full template body as plain text with Markdown
- `assignee_account_id`: reporter's account ID (or ask user)
- `additional_fields`: `{"parent":{"key":"<EPIC_KEY>"}}`

### 4. Return result

Show URL: `https://<domain>.atlassian.net/browse/<KEY>`
