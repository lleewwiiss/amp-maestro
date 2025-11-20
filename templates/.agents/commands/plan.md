# /plan – Create an implementation plan from research using Oracle

Use this after research is complete to define *how* to solve the Bead with high-quality reasoning.

Usage: `/plan <bead-id>`

Pre-requisites:
- `.beads/artifacts/<bead-id>/research.md` exists or has been reviewed.

**Requirements**:
- Always read:
  1. Bead (`bd show`)
  2. `spec.md` (if exists)
  3. `research.md` (if exists)
- **Alignment**: If your plan changes scope vs `spec.md`, explicitly call this out and suggest updating the spec. **Do not silently expand scope.**

Workflow:

1. **Load Context**
   - Read `.beads/artifacts/<bead-id>/research.md` if available.
   - Read the Bead details: `bd show <bead-id> --json`.

2. **Delegate Planning to Oracle (Mandatory)**
   - Call the **Oracle tool** to perform complex reasoning.
   - Pass to Oracle:
     - Bead metadata.
     - `research.md` contents.
     - Constraints (scope, tech stack, non-goals).
   - Instruct Oracle to produce a **stepwise implementation plan** in markdown with:
     - Clear sections: Context, Goals, Risks, Implementation Plan, Test Plan.
     - A numbered list of implementation steps, small enough for single coding sessions.

3. **Create/Update Plan Artifact**
   - Save Oracle’s output as `.beads/artifacts/<bead-id>/plan.md`.
   - Ensure the file is self-contained and clean (no tool logs).

4. **Link to Bead**
   - Update the `Context` block in the Bead description to include:
     ```text
     - Plan: .beads/artifacts/<bead-id>/plan.md
     ```
   - Update status to `in_progress` if not already: `bd update <bead-id> --status in_progress --json`.

5. **Human Review**
   - Show the plan to the user.
   - **HUMAN-IN-THE-LOOP**: Ask "Does this plan look correct? Should I break any steps into child beads?"
   - If split requested:
     - Run `/split <bead-id>`.
     - `/split` will create new beads with `--deps blocks:<bead-id>`.
     - Update `plan.md` to reference the new child IDs.
     - Update parent Bead status to `blocked` (since it waits for children).

6. **Ready to Implement**
   - Once approved, suggest running `/implement <bead-id>`.
