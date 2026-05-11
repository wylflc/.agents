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

2. Create the smallest useful structure:

   ```text
   skill-name/
   ├── SKILL.md              # required
   ├── agents/openai.yaml    # recommended UI metadata
   ├── scripts/              # optional executable helpers
   ├── references/           # optional docs loaded only when needed
   └── assets/               # optional templates or output resources
   ```

3. Write `SKILL.md` with YAML frontmatter and concise instructions.

   ```md
   ---
   name: skill-name
   description: Clear capability summary. Use when [specific triggers].
   ---

   # Skill Name

   [Essential workflow and resource guidance.]
   ```

4. Add bundled resources only when they directly support the skill:
   - `scripts/` for deterministic or repeated operations.
   - `references/` for longer guidance that should load only when relevant.
   - `assets/` for files used in outputs, such as templates or images.

5. Validate the skill:

   ```sh
   python3 /Users/yaleiwang/.codex/skills/.system/skill-creator/scripts/quick_validate.py path/to/skill
   ```

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
