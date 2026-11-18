# Agent dev skills

The skills I use with coding agents (Claude Code, Codex) for everyday software work: understand what to build, change it in small tested steps, check it before it ships, and see how a codebase is built. Three are mine; the rest are other people's skills that I use every day and ship here as one bundle, with their licences.

Security has its own repository: [agent-security-skills](https://github.com/Hilmernator/agent-security-skills).

## How I work with agents

- **Evidence decides the next step.** A failing test, a reproduced bug, a working prototype or an exercised user flow, not a confident paragraph. Reviews say what was checked and what was not.
- **The smallest change that fully works.** Reuse what the codebase and the platform already have; no speculative abstractions or dependencies. Small still means tested, with errors handled and nothing unsafe.
- **The agent is a colleague, not a typist.** It reads the repository and the conversation, makes routine reversible decisions itself, and asks only when the answer changes the outcome or a wrong guess is costly.
- **Report-only means report-only.** The review and QA skills change nothing; fixing is a separate, explicit step.

## My skills

| Skill | Use it for |
| --- | --- |
| [blueprint](skills/blueprint/SKILL.md) | Draw the architecture of a codebase, or of one feature, as one HTML page where every box cites the code behind it. Also sketches and compares proposed architectures, and shows what a branch changes. |
| [code-validation](skills/code-validation/SKILL.md) | Review the uncommitted diff before a commit, for defects with a concrete failure scenario, without editing anything. |
| [qa-only](skills/qa-only/SKILL.md) | Exercise a feature through its real entry point (browser, API, CLI or job) and report reproducible failures without fixing code. Inspired by gstack's report-only QA; no gstack code. |

Blueprint needs Node 22.12+ and its npm dependencies (`npm ci --prefix skills/blueprint/scripts`); its pages use my design system. When the asd-ste100 skill is installed beside it, Blueprint checks every text on a page against its rules.

## Other skills I use

Written by other people, shipped in this bundle so that one install gives the whole toolset. Each folder keeps its author's licence. "Adapted" means I changed it; the changes are listed in [SOURCES.md](SOURCES.md).

| Skill | Author | What I use it for |
| --- | --- | --- |
| [tdd](skills/tdd/SKILL.md) | [Matt Pocock](https://github.com/mattpocock/skills), adapted | One behaviour and one failing test at a time, red, green, refactor |
| [diagnosing-bugs](skills/diagnosing-bugs/SKILL.md) | [Matt Pocock](https://github.com/mattpocock/skills) | Reproduce, isolate, fix and verify a hard bug or a slowdown |
| [prototype](skills/prototype/SKILL.md) | [Matt Pocock](https://github.com/mattpocock/skills), adapted | A throwaway prototype that answers one design question |
| [interview-me](skills/interview-me/SKILL.md) | [Addy Osmani](https://github.com/addyosmani/agent-skills), adapted | A short product interview that ends in a living brief and the next experiment |
| [doubt-driven-development](skills/doubt-driven-development/SKILL.md) | [Addy Osmani](https://github.com/addyosmani/agent-skills), adapted | An independent fresh-context review of one difficult claim |
| [ponytail](skills/ponytail/SKILL.md) | [Dietrich Gebert](https://github.com/DietrichGebert/ponytail) | The laziest solution that actually works: stdlib and platform before code, one line before fifty |
| [asd-ste100](skills/asd-ste100/SKILL.md) | [danyuchn](https://github.com/danyuchn/asd-ste100-skill) | Simplified Technical English for text an agent or a reader must not misread, with a structural linter |

## How they fit together

Interview-me when the direction is unclear. Then tdd for each behaviour, diagnosing-bugs when something fails, and a prototype when an experiment can settle a question faster than an argument. Ponytail is the coding style throughout. Before a commit, code-validation; when runtime behaviour matters, qa-only. Doubt-driven development for the one claim a decision rests on, not for every edit. Blueprint whenever a picture of the system helps a decision.

## Install

Copy the skill folders you want into your agent's skill directory (`~/.claude/skills/<name>` for Claude Code, `~/.agents/skills/<name>` for Codex), or enable the repository as a plugin. Each skill is self-contained.

## Verification

```sh
python3 scripts/validate_package.py
python3 skills/asd-ste100/scripts/ste-lint.py --selftest
npm ci --prefix skills/blueprint/scripts && npm test --prefix skills/blueprint/scripts
```

## Licence

My code and text are MIT-licensed ([LICENSE](LICENSE)). The skills under "Other skills I use" keep their own licences, in their folders. The AWS Architecture Icons in Blueprint fall under AWS's terms for those icons; see [SOURCES.md](SOURCES.md).
