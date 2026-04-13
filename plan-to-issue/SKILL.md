---
name: plan-to-issue
description: Convert high-level AI-generated plans into detailed, production-grade GitHub issues. Use this when the user has an existing plan (from any agent or conversation) and wants a very clear, deeply detailed explanation and requirements captured as an active GitHub issue via the gh CLI.
---

# plan-to-issue

This skill turns a rough or high-level plan into a **production-ready GitHub issue** with:

- A strong, action-oriented title
- Clear context and problem framing
- Explicit goals and non-goals
- A deeply detailed explanation of the plan ("super detailed" narrative)
- Structured requirements and sub-tasks
- Acceptance criteria that can be checked off

The input is **any plan text** (often written by another AI agent in "plan mode"). The output is a GitHub issue created via the `gh` CLI.

## When to use this skill

Trigger this skill when:

- The user says they have a "plan" from another agent and wants it **turned into a GitHub issue**.
- The user asks: "Create an issue from this plan", "/plan-to-issue", or similar.
- There is already a reasonably complete plan (phases/steps/ideas) and the missing piece is **clarity, structure, and detail**, not more brainstorming.

Do **not** use this skill when:

- The user is still exploring options and not ready to commit to a concrete plan.
- There is no clear project or task yet.

## Required assumptions

Because plans can come in many formats, follow these assumptions:

- The plan may be bullets, numbered steps, or free prose.
- Treat all content as **raw material** for the issue: extract goals, constraints, phases, tasks.
- If the plan is extremely short, you must **expand it heavily** with your own structure and reasonable assumptions, but keep them clearly written and practical.

## GitHub usage

Assume:

- `gh` is installed and already authenticated.
- The issue should be created in the **current repository** by default.

### Command to create the issue

Use `gh issue create` and pass title and body. Prefer here-docs for clarity and to avoid shell escaping issues.

Example pattern:

```bash
gh issue create \
  --title "<ISSUE_TITLE>" \
  --body "$(cat << 'EOF'
<ISSUE_BODY_MD>
EOF
)"
```

Replace `<ISSUE_TITLE>` and `<ISSUE_BODY_MD>` with the generated content.

If a specific repository is required, add:

```bash
  --repo owner/repo
```

but only when the user explicitly specifies it.

## Issue structure (standard template)

Always structure the issue body with these sections, in this order, using Markdown headings:

1. **Context**
2. **Problem / Motivation**
3. **Goals**
4. **Non-goals** (if any)
5. **Detailed Plan & Explanation**
6. **Requirements**
7. **Implementation Notes** (optional, include when helpful)
8. **Risks & Open Questions** (optional)
9. **Acceptance Criteria**

### 1. Context

Summarize in 3–6 sentences:

- What this plan is about
- Where it came from (e.g. "Derived from AI planning discussion")
- Any relevant background from the original plan

### 2. Problem / Motivation

Answer:

- What user or system problem are we solving?
- Why is this important now?

Use bullets or short paragraphs. Be explicit and concrete.

### 3. Goals

A bullet list of **clear outcomes**, for example:

- "Provide a documented workflow for X"
- "Enable Y so that Z"

Each goal should be testable or observable.

### 4. Non-goals

Optional, but recommended when the plan could easily creep in scope.

Examples:

- "Not a full redesign of the dashboard"
- "Does not include mobile app implementation"

If there are no obvious non-goals, you can write:

- "None explicitly identified at this time."

### 5. Detailed Plan & Explanation

This is where you produce the **"very clear & super detailed"** explanation.

Guidelines:

- Organize by phases or sections, for example:

  ```markdown
  #### Phase 1: Discovery & design
  - ...

  #### Phase 2: Implementation
  - ...

  #### Phase 3: QA & rollout
  - ...
  ```

- For each phase, explain:
  - What will be done
  - Why it is done in this order
  - Key decisions or tradeoffs

- Expand high-level bullets into detailed steps. For each major step:
  - Provide a short explanation
  - Include any relevant edge cases or notes

- Prefer concrete language over vague phrases. Avoid "do it nicely" and instead explain what "nicely" means in this context.

### 6. Requirements

Translate the plan into **explicit requirements**. Use a combination of bullet points and sub-lists. For example:

```markdown
- Functional
  - User can X
  - System should Y

- Non-functional
  - Performance: ...
  - Security: ...
```

If the plan implies data structures, APIs, or UX decisions, capture them here as requirements.

### 7. Implementation Notes (optional)

Include this section when the plan mentions technical details, tech stacks, or integration points. Capture:

- Suggested technologies or libraries
- Existing modules to reuse
- Migration or compatibility considerations

### 8. Risks & Open Questions (optional)

If the plan hints at uncertainties, note them explicitly:

- Unknowns that require clarification
- Risks that might affect timeline or scope

### 9. Acceptance Criteria

This should be a **checklist** of conditions that must be true for the issue to be considered done.

Example pattern:

```markdown
- [ ] Scenario A is supported (details...)
- [ ] Scenario B is supported (details...)
- [ ] Documentation updated at <location>
- [ ] Basic monitoring/alerting configured (if applicable)
```

Make the criteria specific enough that a reviewer can objectively say "yes" or "no" for each item.

## Workflow to follow when using this skill

1. **Collect the plan**
   - Take the entire plan text as input.

2. **Extract structure**
   - Identify: context, goals, constraints, steps, phases, and any implied requirements.

3. **Design the issue title**
   - Short, imperative, and focused on the main outcome.
   - Examples:
     - "Implement AI plan for user onboarding flow redesign"
     - "Turn X planning document into executable rollout plan"

4. **Draft the full issue body**
   - Use the template above.
   - Expand sparsely described parts into clear, detailed explanations.

5. **Run `gh issue create`**
   - Use the title and body from steps 3 and 4.
   - Default repo is the current directory’s repo unless user specified otherwise.

6. **Return a summary to the user**
   - Include:
     - The created issue URL (from `gh issue create` output)
     - The final title
     - A very short recap of what the issue covers.

## Tone & style for generated issues

- Professional but direct.
- Optimized for **engineers and reviewers**.
- Avoid marketing fluff.
- Prefer clarity over brevity: it is okay for the issue to be long if it is organized and skimmable.

This skill’s job is to take any rough plan and turn it into a **single, high-quality source of truth** in GitHub that someone can immediately work from.