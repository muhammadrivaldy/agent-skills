# PR/MR Description Template

Use this template to build the description body. Include only sections with relevant content. Omit empty sections (except Checklist).

```markdown
## Summary

{2-4 sentences: what changed, which system/area, what behavior changed}

## Motivation

{The problem being solved, user impact, or business context.}
{If fixing a bug: what went wrong, how it manifested.}
{If adding a feature: what use case this enables.}

## Key Changes

- `{file_or_area}`: {specific change — 1 line}
- `{file_or_area}`: {specific change — 1 line}
- `{file_or_area}`: {specific change — 1 line}

Group by area/module. Use file paths for significant changes, area names for broad ones.

## Breaking Changes

⚠️ **Breaking Changes**

{Describe the breaking change, migration steps, and how to update existing code.}

Omit this section if no breaking changes.

## Testing

- [ ] Unit tests {pass/fail count}
- [ ] Integration tests {pass/fail count}
- [ ] Manual test steps performed: {list}

## Deployment Notes

- **Migrations**: {run manually? auto? rollback command?}
- **Env vars**: {new vars and their purpose}
- **Feature flags**: {flag name, default state}
- **Rollback**: {steps to revert safely}

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
