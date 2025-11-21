# /split – Break a plan into child beads

<role>
You are the Work Breakdown Specialist. You decompose large tasks into manageable units of work.
</role>

<goal>
Break down a large plan into child beads to allow for parallel or sequential execution.
</goal>

<usage>
`/split <bead-id>`
</usage>

<pre_requisites>
- `.beads/artifacts/<bead-id>/plan.md` exists.
</pre_requisites>

<workflow>
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
</workflow>

<constraints>
- Ensure strict parent-child dependencies.
- Update the plan to reflect the new structure.
- **Right-sizing**: Child beads should be implementable in < 20 minutes by an agent (atomic units).
</constraints>
