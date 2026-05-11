---
name: write-a-skill
description: Create new agent skills with proper structure, progressive disclosure, and bundled resources. Use when user wants to create, write, update, or build a new Codex skill.
---

# Writing Skills

## Process

1. Gather requirements:
   - What task or domain does the skill cover?
   - What user requests should trigger it?
   - Does it need scripts, references, assets, or only instructions?
   - Are there source materials or examples to include?
   - Should it be user-level or project-level?

2. Choose the destination:
   - User-level skills default to `~/.agents/skills/<skill-name>`.
   - Project-level skills default to `./.agents/skills/<skill-name>` from the
     project root.
   - If the user does not specify scope, use user-level for reusable personal
     workflows and project-level for repo-specific domain knowledge.

3. Create the smallest useful structure:

   ```text
   skill-name/
   ├── SKILL.md              # required
   ├── agents/openai.yaml    # recommended UI metadata
   ├── scripts/              # optional executable helpers
   ├── references/           # optional docs loaded only when needed
   └── assets/               # optional templates or output resources
   ```

4. Write `SKILL.md` with YAML frontmatter and concise instructions.

   ```md
   ---
   name: skill-name
   description: Clear capability summary. Use when [specific triggers].
   ---

   # Skill Name

   [Essential workflow and resource guidance.]
   ```

5. Add bundled resources only when they directly support the skill:
   - `scripts/` for deterministic or repeated operations.
   - `references/` for longer guidance that should load only when relevant.
   - `assets/` for files used in outputs, such as templates or images.

6. Validate the skill:

   ```sh
   python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" path/to/skill
   ```

   If the validator is unavailable or missing Python dependencies, perform an
   equivalent check: `SKILL.md` exists, frontmatter is valid YAML, only allowed
   frontmatter keys are used, `name` is lowercase hyphen-case, and
   `description` is a non-empty string under 1024 characters.

## Standards

- Use lowercase hyphen-case for the skill name.
- Put trigger guidance in `description`; it is the primary loading signal.
- Keep `SKILL.md` lean. Move long or rarely needed details into directly linked
  reference files.
- Keep references one level deep from `SKILL.md`.
- Do not add unrelated files such as README, changelog, installation guide, or
  quick reference documents inside a skill folder.
- Test any added scripts by running them.

## Review Checklist

- [ ] `SKILL.md` exists and starts with YAML frontmatter.
- [ ] Frontmatter includes `name` and `description`.
- [ ] Description explains what the skill does and when to use it.
- [ ] Body contains procedural guidance, not duplicate trigger rules.
- [ ] Bundled files are directly useful and referenced where needed.
- [ ] Validation passes.
