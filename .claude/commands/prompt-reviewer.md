---
name: prompt-reviewer
description: Reviews a candidate prompt file for template compliance and duplicate intent; approves with suggestions or rejects with reason
version: 1
---

# prompt-reviewer
Read prompts/_template.md and all existing prompts/*.md files. For the $ARGUMENTS: (1) check structural compliance with the template, (2) check for duplicate intent against existing prompts. Approve with concrete section-level suggestions, or reject citing the duplicate file and overlapping Goal in 1–2 sentences..

## Baseline (weak) — what you started from

```
help me improve prompt $ARGUMENTS
```

## Production — markdown (OpenAI / GPT-5.x dialect)

```markdown
Role: Senior prompt engineer reviewing a $ARGUMENTS file in the `prompts/` folder.
Goal: Verify the $ARGUMENTS follows `prompts/_template.md` structure AND does not duplicate the intent of any existing prompt in `prompts/`.
Context:
- Template: `prompts/_template.md` (read-only)
- Existing prompts: all `*.md` files in `prompts/` (read for duplicate detection)
- Candidate: $ARGUMENTS specified by the user
Constraints:
- Do not edit the candidate file or `prompts/_template.md`.
- Do not invent new template rules; enforce only what `_template.md` defines.
- In case there is no manipulation with .ts files, do not add running tests in verified section.
- No secrets or PII in output.
- Prompt should have ## Production — XML (Anthropic / Claude dialect) or ## Production — markdown (OpenAI / GPT-5.x dialect) without sections
without ## Tool-fit notes and ## Verified sections.
Acceptance criteria:
- Approved: every missing/weak section is listed with a one-sentence reason.
- Rejected: duplicate file path is named and overlapping Goal is quoted.
- "No changes needed" is stated explicitly — never silently do nothing.
Output:
- Approval: bulleted list (section → suggested change → why).
- Rejection: one paragraph with duplicate file path and overlap summary.
Stop rules:
- Do not flag cosmetic issues (spelling, whitespace) if structure and intent are sound.
- Do not approve a prompt whose Goal overlaps an existing one even if the wording differs.

```

## Production — XML (Claude dialect)

```xml
<instructions>
You are a senior prompt engineer. Given $ARGUMENTS as the candidate prompt file:
1. Read prompts/_template.md and check structural compliance.
2. Read all prompts/*.md and check for duplicate intent.
Approve with section-level suggestions, or reject citing the duplicate file and overlapping Goal.
Do not edit any file.
- In case there is no manipulation with .ts files, do not add running tests in verified section.
</instructions>

<context>
- Template: prompts/_template.md (read-only)
- Existing prompts: prompts/*.md (read for duplicate detection)
- Candidate: $ARGUMENTS
</context>

<constraints>
- Do not edit the candidate or prompts/_template.md.
- Enforce only existing template rules; do not invent new ones.
- No secrets or PII in output.
</constraints>

<output_format>
Approval: bulleted list — section → suggested change → why.
Rejection: duplicate file path + 1–2 sentence overlap summary.
"No changes needed" stated explicitly if everything is sound.
</output_format>
```

## Tool-fit notes

| Variant | Best for | Why |
|---------|----------|-----|
| markdown | Copilot / ChatGPT | More verbose and understandable commands for the same task. From a human perspective, more readable. |
| XML | Claude Code | Well structured and shorter format, which can help save redundant reading and costs. But it requires more capable models. |

## Verified

- [x] Run against a real candidate prompt via `/prompt-reviewer prompts/<file>.md`
- [x] Agent stayed in scope (no files edited; only suggestions or rejection displayed)