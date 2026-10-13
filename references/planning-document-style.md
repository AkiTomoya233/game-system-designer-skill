# Planning Document Style

## Authority and structure

Use the user's current template when supplied. Otherwise use this default body:

1. Design purpose
2. Feature overview
3. Reference video, if needed
4. UI reference, if needed
5. System rules
6. Interface flow
7. Configuration changes
8. UI operation specification

The body is the authoritative review and test source. Do not duplicate the same rules across summary, UI, flow, and acceptance tabs.

## Rule writing

- Organize rules as feature group, scenario/rule group, and independent condition/result.
- Keep each level on its own spreadsheet row.
- State the subject, precondition, player-visible result, and boundary in the relevant group.
- Describe runtime outcomes in rules; place included and excluded scope in the scope section.
- Unknown player-visible behavior remains `TBD` until confirmed.

## Interface flow

When the feature has entry, navigation, back/close behavior, operations, or state branches, include:

- numbered text steps;
- the editable diagram source filename;
- an embedded preview near the corresponding section.

Lines must meet node edges, preserve clear branch direction, and avoid crossing nodes, labels, arrows, or unrelated branches. Verify the editable source, exported image, and embedded result.

## Configuration section

For review documents, summarize feature-specific configuration changes using columns equivalent to:

| Configuration group | Required fields or parameters | Purpose | Status |
|---|---|---|---|

This summary is not a substitute for a real project configuration workbook. If the user requests actual configuration data, preserve the project's schema, metadata rows, separators, types, validation rules, and existing conventions.

## UI operation specification

Put each image beside its component notes. Each note starts with component name and purpose, then adds:

- composition, if relevant;
- state;
- operation and feedback;
- difference from the baseline state, when relevant.

For multiple states of one page, document common components once in the baseline state. Difference states describe only changed components.

## Spreadsheet visibility

- Give wrapped text enough explicit row height, especially in merged cells.
- Do not rely only on automatic row height for merged regions.
- Keep heading, body, note, and status styles consistent within the document.
- Check that embedded media and top-layer markers remain visible after export.
- Reopen the actual delivery in the native spreadsheet application when available.

