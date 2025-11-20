# /implement – Execute the plan for a specific bead using Subagents

Use this to start coding based on the approved plan, keeping the main context clean.

Usage: `/implement <bead-id>`

Pre-requisites:
- `.beads/artifacts/<bead-id>/plan.md` should exist and be approved.

Workflow:

1. **Manager Mode (Main Thread)**
   - Load `plan.md`.
   - Identify the next uncompleted step.
   - For each step:
     - Clarify objective.
     - **Spawn a Subagent (Task tool)** to do the work.
     - Update Bead status to `in_progress`.

2. **Subagent Execution (Task Tool)**
   - Each subagent handles a single unit of work (e.g., "Implement API handler").
   - Subagents can:
     - Search codebase (use `finder` for broad searches, `Grep` for specifics).
     - Edit files (use `edit_file` or `create_file`).
     - Run relevant tests/linters.
     - **Visualize**: If changes are complex, generate a **Mermaid diagram** to confirm understanding before editing.
   - Subagent Output: A concise summary of files changed, decisions made, and test results.

3. **Reflect Reality & Cleanup**
   - If subagents discover new work:
     - **STOP**. Ask to file a new Bead (`bd create ... --deps discovered-from:<bead-id>`).
   - If a step is harder than expected:
     - Update `plan.md`.
   - **Cleanup**:
     - Remove any `console.log` or debugging code.
     - Check for leftover `TODO` comments (file new beads for them if needed).
     - **Visualize**: If changes were complex, ask to run `/architect` to update diagrams.

   4. **Completion**
   - When all steps are done and verified:
     - Update Bead status to `ready_for_review`.
     - Run `/land-plane` for final checks.
