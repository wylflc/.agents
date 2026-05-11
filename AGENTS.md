# Global Agent Preferences

## General
- Be accurate and explicit about uncertainty.
- Prefer practical progress over unnecessary caution.
- Keep responses concise unless the task is complex.
- If a reasonable assumption allows progress, state it briefly and proceed.
- Do not re-ask for goals or permissions that were already clear unless something materially changed.

## Working Style
- Use available skills when they clearly apply, but do not duplicate their workflows here.
- When providing a modification plan for any project, present two options:
  1. Minimal-change plan: the smallest practical change that solves the request.
  2. Cleanest-thorough plan: the cleanest, most elegant, and most complete change that addresses the root shape of the problem.
- For complex tasks, first produce a short plan with those two options, then execute after the user chooses or after stating a reasonable assumption.

## File Writing
- Write new files and substantial new content in English by default, unless the user explicitly asks for another language or the existing file clearly uses another language.
- For structured documents, Markdown, notebooks, and long-form generated content, use numbered section headings by default: `1.`, `1.1`, `1.1.1`, etc.
- In `.ipynb` notebooks, number Markdown section headings so later discussion can refer to exact sections.
- Do not force section numbering into source code or small config files where it would be unnatural.

## Git Workflow
- Before making file changes in any project, check whether the current directory is inside a Git repository.
- If it is not a Git repository, tell the user and recommend creating one with `git init`. Do not initialize Git without explicit user approval.
- When creating a new Git repository, also create or update `.gitignore` and include `.agents/` and `.codex/` by default.
- If it is a Git repository, inspect `git status --short` before editing so existing user changes are known.
- After completing requested modifications and validation, automatically create a Git commit for the agent's own changes.
- Group commits by change type. Even within one conversation, commit unrelated or different-type changes separately.
- Do not stage unrelated files or user changes.
- Do not commit when the user explicitly asks not to commit, when the task was read-only, or when validation failed and the user has not approved committing anyway.
- Never push, deploy, reset history, or discard changes without explicit approval.

## Changes
- Read the relevant files before changing them.
- Match existing style unless there is a strong reason not to.
- Keep implementation scope aligned with the selected plan.
- Do not expand from a minimal-change plan into a thorough refactor, or from a thorough plan into unrelated cleanup, without making that scope change explicit.
- Do not add new dependencies without a clear reason.
- Do not delete code, comments, files, or user work unless explicitly asked or directly required by the requested change.
- After key codebase changes, update related README, CONTEXT, ADR, or other project documentation if they are affected.

## Validation
- After code changes, run the most targeted useful check available: test, lint, typecheck, build, or minimal repro.
- Add or update tests for new behavior or bug fixes when the project has a relevant test pattern.
- Do not claim a fix works unless it was verified.
- If something could not be verified, say so clearly.

## Safety
- Do not run destructive commands, delete data, reset history, deploy, push, publish, or expose secrets without explicit approval.
