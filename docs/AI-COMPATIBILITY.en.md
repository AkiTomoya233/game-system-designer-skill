# Multi-agent compatibility and setup

> Verified on 2026-10-15. Agent clients evolve quickly; check the linked official documentation before installation.

## Three separate compatibility questions

1. **Can the model understand it?** Most models can follow `SKILL.md` when the required files are supplied.
2. **Can the host discover it?** Automatic discovery requires native Agent Skills support or explicit skill registration.
3. **Can the host execute it?** Spreadsheet, image, Figma, diagram, web, and native-preview work requires matching tools. Loading instructions does not create those tools.

This repository follows the portable `SKILL.md` directory structure. `agents/openai.yaml` is optional OpenAI/Codex interface metadata and may be ignored by other hosts.

## Before installation

- Clone or download the complete repository; `SKILL.md` references files under `references/`.
- The final layout should be `<skills-root>/game-system-designer/SKILL.md`.
- Confirm an absolute project material-library path on first use in every project.
- Keep proprietary configuration, UI, art, requirements, credentials, and private paths outside this public repository.
- Run a small end-to-end test before formal production: discovery, reference loading, file access, and every required output tool.
- If a tool is unavailable, disclose the limitation and produce only a verifiable fallback.

## Host matrix

| Host | Discovery/install | Invocation | Notes |
|---|---|---|---|
| OpenAI Codex | `%CODEX_HOME%/skills/game-system-designer` or `.codex/skills/game-system-designer` | `$game-system-designer` or automatic matching | OpenAI metadata applies; deliverable tools depend on the current Codex environment |
| DeepSeek Harness | `%DSH_HOME%/skills`, `.dsh/skills`, or `.agents/skills` | `/game-system-designer` or automatic matching | Mount `dsh-skill`, `dsh-skill-filesystem`, and `dsh-tool-skill` |
| Claude Code | `~/.claude/skills/game-system-designer` or `.claude/skills/game-system-designer` | `/game-system-designer` or automatic matching | Translate host-specific tool names and permission flows |
| claude.ai | Upload the complete skill as a ZIP in Settings > Features | Automatic matching | Requires a plan with custom Skills and code execution; separate from Claude Code and API |
| Claude API | Upload through the Skills API and reference the returned skill ID | API configuration | Requires code execution; hosted runtime restrictions apply |
| Gemini CLI | `gemini skills install <repo-url>`, `.gemini/skills`, or `.agents/skills` | Automatic matching; inspect with `/skills list` | Skill activation requires consent; reload with `/skills reload` |
| Cursor | `.cursor/skills`, `.agents/skills`, and compatible `.codex/skills` or `.claude/skills` | `/game-system-designer` or `@game-system-designer` | Local and cloud skill availability differ |
| GitHub Copilot | `.github/skills`, `.claude/skills`, `.agents/skills`, or `~/.copilot/skills` | Automatic matching or SDK registration | SDK sessions configure parent directories through `skillDirectories` |
| OpenAI API / Agents API | Upload the bundle or register an absolute local skill path | Request configuration | Hosted and local-shell attachment methods differ |
| Other chat/model hosts | Usually manual only | Attach instructions explicitly | No automatic discovery, progressive loading, or guaranteed tools |

## Official references

- OpenAI Skills: <https://developers.openai.com/api/docs/guides/tools-skills>
- DeepSeek Harness filesystem skills: <https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/skill/skill-filesystem/README.md>
- Claude Agent Skills: <https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview>
- Gemini CLI Skills: <https://github.com/google-gemini/gemini-cli/blob/main/docs/cli/using-agent-skills.md>
- Cursor Skills: <https://cursor.com/help/customization/skills>
- GitHub Copilot customization: <https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/customization-cheat-sheet>

## Manual fallback for unsupported hosts

1. Attach `SKILL.md`.
2. Attach only the references required by the current task.
3. Instruct the model to read the skill first, request a project library, and resolve all player-result blockers in complete batches before formal production.
4. Repeat the attachment in new conversations unless the host provides persistent project context.
5. Treat spreadsheet, image, configuration, and native-preview claims as drafts unless the host exposes and actually runs those tools.

## Capability checklist

Before requesting a complete delivery, verify the host has the capabilities the task needs:

- filesystem read/write access;
- XLSX editing, formula checks, and media/shape preservation;
- native Microsoft Excel or equivalent preview;
- editable diagram output;
- image generation/editing and alpha handling;
- Figma access;
- web research and citations;
- project-library access;
- Chinese path, font, and encoding support.

Missing capabilities should produce an explicit downgrade, not an unverified completion claim.
