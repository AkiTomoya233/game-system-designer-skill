# Project Library

## First-use requirement

The first formal task in each project requires an explicitly confirmed absolute material-library path. A library binding belongs only to that project or workspace.

If the path is missing, ask for it and explain the expected content in one message. Do not create formal documents, UI, diagrams, or configuration before completing the read-only inventory.

## Recommended structure

```text
project-library/
├─ planning-templates/     Approved planning documents and spreadsheet templates
├─ configuration/         Real project tables, schemas, type notes, and examples
├─ project-ui/             Screenshots and approved full-page UI references
├─ ui-components/         Reusable controls, frames, buttons, icons, and variants
├─ concept-art/            Approved characters, creatures, environments, and key art
├─ generated-ui/           Versioned formal UI outputs produced for the project
└─ generated-components/   Versioned reusable components produced for the project
```

Folder names may differ. Resolve the project's actual directories by purpose rather than requiring these exact English names.

## Read-only inventory

Record:

- the confirmed absolute root;
- which categories exist or are missing;
- the newest approved planning templates;
- the actual configuration tables relevant to the feature;
- likely same-system UI and reusable components;
- known project profiles or style guides;
- files that are examples only, inherited from another project, deprecated, or unverified.

File presence does not prove runtime use. Do not claim a field, asset, component, or table is active without supporting project evidence.

## Missing library content

Missing content does not authorize inventing it.

- Missing template: request a representative approved document or use a neutral structure with an explicit note.
- Missing configuration: describe rules and mark configuration mapping as unverified.
- Missing UI reference: make only a low-fidelity structure unless the user authorizes a new visual direction.
- Missing components or art: mark them as placeholders or proposed new assets.

## Archiving

Keep new full-page UI and new reusable components in separate, versioned locations. Preserve originals and earlier approved versions unless deletion or overwrite is explicitly requested.

