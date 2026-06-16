---
name: create-mr
description: Analyze code changes and create GitHub PRs or GitLab MRs with auto-generated title and structured description. Detects platform from remote URL, analyzes git diff against target branch, determines change type/scope/breaking changes. Generates description covering: summary, motivation, key changes, breaking changes, testing, related issues, deployment notes, and checklist. Use when user asks to create a PR, MR, pull request, or merge request.
---

# Create MR/PR

Analyze git diff against a target branch, generate a structured PR/MR with auto-title and detailed description, then submit via `gh` or `glab` CLI.

## When to use

User says: "create a PR", "create an MR", "open a pull request", "make a merge request", "submit changes".

## Workflow

### 1. Ask target branch

"Which branch should this merge into?" Default: `main` or `master`.

### 2. Check diff

```bash
git diff <target_branch>...HEAD --stat
git diff <target_branch>...HEAD
```

If no diff, abort with error.
If uncommitted changes exist (`git status --porcelain`), show them and say:
"Uncommitted changes detected. Please commit first or use `/commit`."

### 3. Detect platform

```bash
git remote get-url origin
```

- `github.com` → use `gh`
- `gitlab.com` → use `glab`
- Else → ask user which platform

Verify CLI is installed (`gh --version` or `glab --version`). If missing, error with install instructions.

### 4. Analyze diff

From the diff output, determine:

| Property | How |
|---|---|
| **Type** | feat/fix/refactor/chore/docs/test/style/perf |
| **Scope** | Module/directory name from changed files |
| **Breaking** | `BREAKING CHANGE` in commit msgs or removed public APIs |
| **Migration** | Presence of migration/DDL files |
| **New env vars** | `.env.example` or `process.env` additions |
| **New deps** | `package.json`, `requirements.txt`, `go.mod` changes |

### 5. Generate title

Format: `<type>(<scope>): <description>`

Rules:
- Imperative present tense ("add" not "added")
- Under 72 chars
- Lowercase after colon

### 6. Generate description

Pull from the template at `references/description-template.md`. Include only sections with relevant content. Omit empty sections (except Checklist).

### 7. Create PR/MR

```bash
# GitHub
gh pr create --title "<title>" \
  --body "$(cat << 'PRBODY'
<description>
PRBODY
)" \
  --base <target_branch>

# GitLab
glab mr create --title "<title>" \
  --description "$(cat << 'MRBODY'
<description>
MRBODY
)" \
  --target-branch <target_branch>
```

### 8. Return result

Show the URL and a summary:

```
Created PR: https://github.com/owner/repo/pull/123
Type: feat(auth) — implement JWT login
Target: main
```

## Template

See `references/description-template.md` for the full description template.

## Platform CLI Installation

- **GitHub (`gh`)**: `brew install gh` or https://cli.github.com
- **GitLab (`glab`)**: `brew install glab` or https://gitlab.com/gitlab-org/cli
