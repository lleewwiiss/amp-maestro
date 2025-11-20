# /split – Break a plan into child beads

Use this when a plan is too big for a single Bead and needs to be broken down.

Usage: `/split <bead-id>`

Pre-requisites:
- `.beads/artifacts/<bead-id>/plan.md` exists.

Workflow:

1. **Analyze Plan**
   - Read `plan.md`.
   - Identify distinct, separable units of work (e.g., "Backend API", "Frontend UI", "DB Migration").

2. **Propose Child Beads**
   - For each unit, propose a new Bead:
     - **Title**: Action-verb oriented (e.g., "Create...", "Refactor...").
     - **Dependency**: `blocks` <bead-id> (to prevent parent completion).
     - **Description**:
       ```markdown
       **Goal**: <One sentence summary>
       **Context**: Child of <bead-id>. See plan at `.beads/artifacts/<bead-id>/plan.md` (Step X).
       **Inputs**: <Required files/data>
       **Outputs**: <Expected code/tests>
       ```

3. **HUMAN-IN-THE-LOOP**
   - "I propose creating these X child beads to track the work. Approve?"
   - Show list.

4. **Execute**
   - Run `bd create ... --deps ... --json` for each.
   - Update `plan.md` to reference these new bead IDs instead of raw text steps.
   - Update parent Bead status to `blocked` (if waiting on children) or leave as `in_progress`.

5. **Summarize**
   - List new beads created.
