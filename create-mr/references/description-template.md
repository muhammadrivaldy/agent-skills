# PR/MR Description Template

Use this template to build the description body. Include only sections with relevant content. Omit empty sections (except Checklist).

**IMPORTANT:** All file names (`auth.go`, `db.ts`) and function/identifier names (`validateInput`, `handleLogin`) in the generated description must be wrapped in backticks so they render as highlighted code in GitHub/GitLab markdown.

```markdown
## Summary

{2-4 sentences: what changed, which system/area, what behavior changed — backtick all file/function names}

## Motivation

{The problem being solved, user impact, or business context. Backtick all file/function names.}
{If fixing a bug: what went wrong, how it manifested — backtick all file/function names.}
{If adding a feature: what use case this enables — backtick all file/function names.}

## Key Changes

- `{file_or_area}`: `{specific change — backtick all file/function names}`
- `{file_or_area}`: `{specific change — backtick all file/function names}`
- `{file_or_area}`: `{specific change — backtick all file/function names}`

Group by area/module. Use file paths for significant changes, area names for broad ones.

## Breaking Changes

⚠️ **Breaking Changes**

{Describe the breaking change, migration steps, and how to update existing code — backtick all file/function names.}

Omit this section if no breaking changes.

## Testing

- [ ] Unit tests {pass/fail count — backtick test file/function names}
- [ ] Integration tests {pass/fail count — backtick test file/function names}
- [ ] Manual test steps performed: {list — backtick script/tool names}

## Deployment Notes

- **Migrations**: {run manually? auto? rollback command? — backtick migration file names}
- **Env vars**: {new vars and their purpose — backtick var names}
- **Feature flags**: {flag name, default state — backtick flag name}
- **Rollback**: {steps to revert safely — backtick script/command names}

Omit this section if nothing special is needed.
```

## Section Inclusion Rules

| Section | Include when |
| --- | --- |
| Summary | Always |
| Motivation | Always |
| Key Changes | Always |
| Breaking Changes | Diff contains API signature changes, DB schema changes, removed exports, or `BREAKING CHANGE` in commit messages |
| Testing | Always |
| Deployment Notes | Only if diff contains migrations, env var changes, or config changes |

## Title Format

```text
<type>(<scope>): <description>
```

Examples:

- `feat(auth): add JWT token refresh endpoint`
- `fix(api): handle null user in profile endpoint`
- `refactor(db): extract connection pool into shared module`
- `chore(deps): upgrade express to v5`
