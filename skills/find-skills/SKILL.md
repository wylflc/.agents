---
name: find-skills
description: Discover, evaluate, and install agent skills from the skills ecosystem. Use only when the user explicitly asks to find, list, compare, install, or update skills, asks whether an installable skill exists, or wants to extend Codex with reusable skill capabilities. Do not trigger for general "how do I do X" questions unless the user asks for a skill.
---

# Find Skills

This skill helps discover and install skills from the open agent skills
ecosystem. It is not a replacement for answering ordinary how-to questions.

## What is the Skills CLI?

The Skills CLI (`npx skills`) is the package manager for the open agent skills ecosystem. Skills are modular packages that extend agent capabilities with specialized knowledge, workflows, and tools.

**Key commands:**

- `npx skills find [query]` - Search for skills interactively or by keyword
- `npx skills add <package>` - Install a skill from GitHub or other sources
- `npx skills check` - Check for skill updates
- `npx skills update` - Update all installed skills

**Browse skills at:** https://skills.sh/

These commands use network access. Request approval before running them in
sandboxed environments, and do not install anything without explicit user
confirmation.

## How to Help Users Find Skills

### Step 1: Understand What They Need

When the user asks for installable skill help, identify:

1. The domain (e.g., React, testing, design, deployment)
2. The specific task (e.g., writing tests, creating animations, reviewing PRs)
3. Whether this is a common enough repeated workflow that a skill likely exists

### Step 2: Check the Leaderboard First

Before running a CLI search, check the [skills.sh leaderboard](https://skills.sh/) to see if a well-known skill already exists for the domain. The leaderboard is dynamic; treat all counts, rankings, and repository metadata as current only after checking them.

### Step 3: Search for Skills

If the leaderboard doesn't cover the user's need, run the find command:

```bash
npx skills find [query]
```

For example:

- User asks "how do I make my React app faster?" → `npx skills find react performance`
- User asks "can you help me with PR reviews?" → `npx skills find pr review`
- User asks "I need to create a changelog" → `npx skills find changelog`

### Step 4: Verify Quality Before Recommending

**Do not recommend a skill based solely on search results.** Verify current
metadata before recommending:

1. **Install count** - use it as one signal, not a hard threshold.
2. **Source reputation** - prefer known maintainers, but verify the specific repo.
3. **Repository health** - check recent activity, README quality, issues, and license when available.
4. **Fit** - read the skill description or source before recommending it.

### Step 5: Present Options to the User

When you find relevant skills, present them to the user with:

1. The skill name and what it does
2. The install count and source
3. The install command they can run if they choose to proceed
4. A link to learn more at skills.sh

Example response:

```
I found a skill that might help: "<skill-name>".
It provides <short capability summary>. Current metadata: <install count>,
<source>, <repository health notes>.

To install it:
npx skills add <owner/repo@skill>

Learn more: <skills.sh or repository URL>
```

### Step 6: Offer to Install

If the user explicitly wants to proceed, install the skill for them:

```bash
npx skills add <owner/repo@skill> -g -y
```

The `-g` flag installs globally (user-level) and `-y` skips CLI confirmation
prompts. Do not use `-y` as a substitute for user approval in the conversation.

## Common Skill Categories

When searching, consider these common categories:

| Category        | Example Queries                          |
| --------------- | ---------------------------------------- |
| Web Development | react, nextjs, typescript, css, tailwind |
| Testing         | testing, jest, playwright, e2e           |
| DevOps          | deploy, docker, kubernetes, ci-cd        |
| Documentation   | docs, readme, changelog, api-docs        |
| Code Quality    | review, lint, refactor, best-practices   |
| Design          | ui, ux, design-system, accessibility     |
| Productivity    | workflow, automation, git                |

## Tips for Effective Searches

1. **Use specific keywords**: "react testing" is better than just "testing"
2. **Try alternative terms**: If "deploy" doesn't work, try "deployment" or "ci-cd"
3. **Check known sources**: known repositories can be useful starting points,
   but verify current metadata before recommending anything.

## When No Skills Are Found

If no relevant skills exist:

1. Acknowledge that no existing skill was found
2. Offer to help with the task directly using your general capabilities
3. Suggest the user could create their own skill with `npx skills init`

Example:

```
I searched for skills related to "xyz" but didn't find any matches.
I can still help you with this task directly! Would you like me to proceed?

If this is something you do often, you could create your own skill:
npx skills init my-xyz-skill
```
