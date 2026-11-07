---
name: create-workstation
description: "Create a new agent workstation with persona.md and memory.md files following the Atlas workspace conventions, and register it in global_memory.md and the root_persona.md routing map. Use when the user wants a new workstation, project workspace or agent folder, or says 'create workstation', 'new workspace', 'add a project folder', 'set up files for X'."
---

# Create Workstation

Creates a workstation folder with templated `<name>_persona.md` and `<name>_memory.md`, then updates the root index files so the new workstation is discoverable.

## Workspace root

The folder that contains `root_persona.md` and `global_memory.md` (your `agent_workspace/`).

## Information to gather

1. **Name** — short lowercase slug (`cooking`, `thesis`, `linkedin`)
2. **Parent directory** — root level, or nested (`projects/<group>/`)
3. **Identity** — one paragraph on what the agent does
4. **Workflow** — 2–4 numbered steps, starting with the Notion sync
5. **Initial tasks or decisions** — optional

If the context already answers these, proceed without asking. Otherwise ask briefly.

## Steps

1. Create `<parent>/<name>/`.
2. Write `<name>_persona.md` from `templates/workstation_persona.md`, filling Identity, Workflow and domain rules. Keep the two fixed rules: *append-only Key Decisions* and *Task Planning Inquiry*.
3. Write `<name>_memory.md` from `templates/workstation_memory.md` with empty sections (or the initial tasks).
4. Fix the relative links in the Navigation lines for the folder depth.
5. Add a line to the **Memory Index** in `global_memory.md`.
6. **Ask before** adding a row to the **Routing Map** in `root_persona.md`, then add it.
7. Confirm what was created, with paths.

## Checks

- Both files under 100 lines
- No secrets, tokens or personal data copied from other workstations
- The new agent appears in the Agent Network table if other agents should route to it
