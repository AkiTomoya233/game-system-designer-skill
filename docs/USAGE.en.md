# Game System Designer Usage Guide

## Intended use

This skill supports game-feature requirement analysis, system rules, player flows, UX/UI states, configuration changes, planning documents, design review, QA, and playtest design. It is not intended for pure copywriting, standalone art creation, or unsolicited low-level engineering design.

## Installation

The steps below are specific to OpenAI Codex. For DeepSeek Harness, Claude, Gemini CLI, Cursor, GitHub Copilot, and other hosts, see the [multi-agent compatibility guide](AI-COMPATIBILITY.en.md).

### Manual installation

1. Download or clone this repository.
2. Copy the repository folder into your Codex skills directory.
3. The default Windows location is:

   ```text
   %USERPROFILE%\.codex\skills\game-system-designer
   ```

4. Start a new Codex task and invoke `$game-system-designer`.

You may also ask a Codex client with skill-installation support to install the skill from this GitHub repository.

Successful installation only means that the host can read the skill. Spreadsheet, diagram, UI-image, Figma, and native-preview work still requires matching tools in that host.

## Prepare a project material library first

This skill contains no project's proprietary rules, configuration, UI, or art. The first use in every project requires the absolute path to that project's own material library.

Recommended contents:

- planning templates: approved planning documents and spreadsheet templates;
- configuration: real project tables, field notes, type dictionaries, and valid examples;
- project UI: shipped or approved full-page screenshots;
- UI components: buttons, tabs, frames, icons, state components, and variants;
- concept art: approved characters, creatures, environments, and event art;
- generated UI: versioned full-page UI produced later with this skill;
- generated components: versioned reusable components produced later with this skill.

Folder names may differ, but their purpose should be clear. Confirm a new library whenever the project, workspace, or material root changes. Never reuse another project's binding automatically.

## Standard workflow

1. Provide the absolute project-library path.
2. The skill performs a read-only review of requirements, templates, configuration, and UI assets.
3. It asks every currently identifiable player-result question in one complete batch.
4. If the answers expose new contradictions or dependencies, it asks the next complete batch.
5. When no blocking questions remain, it summarizes the full scope and confirmed behavior for final approval.
6. Formal planning documents, UI, diagrams, or configuration deliverables begin only after approval.

If you explicitly request an unconfirmed draft, the skill may continue, but every unresolved item must remain visibly marked `TBD` and must not be presented as a formal conclusion.

## Example prompts

```text
$game-system-designer Create a formal feature plan from this requirement document.
```

```text
$game-system-designer Review this design and ask all questions that could change a player's result in one batch.
```

```text
$game-system-designer Improve the UI operation specification using this project's material library and create the key states.
```

## Important boundaries

- Requirement documents, competitor screenshots, and legacy-project materials are references, not current-project rules.
- The skill does not invent rewards, values, purchase conditions, limits, timing, or exception behavior.
- Existing generic configuration capability is not repeated in the planning document merely to make it look complete.
- The main body is the single source of truth for review and testing; duplicate UI, flow, or acceptance tabs are not created by default.
- UI work prioritizes approved project components and art. External references, generated assets, and placeholders must be identified honestly.
- Source files and earlier versions are preserved unless overwrite or deletion is explicitly authorized.

## Privacy and distribution

Before publishing requirement documents, configuration, UI, art, or planning documents, confirm that you have permission to distribute them. Keep project libraries out of this public, generic skill repository. Teams should share project materials through a separate private repository or controlled storage.

## Capability differences

Diagram, spreadsheet, Figma, image-generation, and native-application preview capabilities depend on the tools and connections installed in the user's Codex environment. When a tool is unavailable, the skill should disclose the limitation and provide a verifiable fallback instead of claiming that validation was completed.

On other AI hosts, do not copy Codex paths, `$game-system-designer`, or Codex-specific tool names blindly. Follow the [compatibility guide](AI-COMPATIBILITY.en.md). Hosts without native Agent Skills support require `SKILL.md` and the references needed for the current task to be supplied manually.

