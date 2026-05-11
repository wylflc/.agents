# Global Agent Configuration

This repository stores global skill files and the agent configuration used by
Codex.

## Directory Structure

- `AGENTS.md`: Global instructions used by Codex agents.
- `skills/`: Global skill files available to agents.

## Skills

Codex always sees each skill's `name` and `description`. The full `SKILL.md`
body is loaded only after the user explicitly names the skill or the user's
request matches the trigger conditions in the description.

| Skill | Purpose | Trigger conditions |
| --- | --- | --- |
| `caveman` | Ultra-compressed response mode for reducing token usage. | User says "caveman mode", "talk like caveman", "use caveman", "less tokens", "be brief", or invokes `/caveman`. Once triggered, it stays active until the user says "stop caveman" or "normal mode". |
| `diagnose` | Structured debugging loop for bugs and performance regressions. | User says "diagnose this" or "debug this", reports a bug, says something is broken, throwing, or failing, or describes a performance regression. |
| `find-skills` | Discover and install additional agent skills. | User asks questions like "how do I do X", "find a skill for X", "is there a skill that can...", or otherwise asks about extending agent capabilities with installable skills. |
| `grill-with-docs` | Stress-test plans against project language and ADRs. | User wants to challenge or refine a plan against the project's domain model, terminology, `CONTEXT.md`, or ADRs. |
| `improve-codebase-architecture` | Find architecture and refactoring opportunities that improve module depth, locality, and testability. | User wants to improve architecture, find refactoring opportunities, consolidate tightly-coupled modules, or make a codebase more testable and AI-navigable. |
| `tdd` | Guide test-first work with a red-green-refactor loop. | User wants to build features or fix bugs using TDD, mentions "red-green-refactor", wants integration tests, or asks for test-first development. |
| `write-a-skill` | Create or update Codex skills using current skill structure and validation practices. | User wants to create, write, update, or build a Codex skill. |
| `zoom-out` | Explain unfamiliar code from a higher-level module and caller map. | User says to "zoom out" or asks for broader context, higher-level perspective, or help understanding how unfamiliar code fits into the bigger picture. |

## Usage

After cloning this repository on a server, link Codex's global
`~/.codex/AGENTS.md` file to the `AGENTS.md` file in this repository.

Run the following commands from the repository root:

```sh
mkdir -p ~/.codex
ln -sf "$(pwd)/AGENTS.md" ~/.codex/AGENTS.md
```
