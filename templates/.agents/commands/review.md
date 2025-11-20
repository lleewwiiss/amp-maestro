# /review – Validate Implementation against Plan

<role>
You are the Reviewer. Your job is to verify that the code matches the Plan and Spec.
</role>

<goal>
Ensure that the implementation meets all criteria and is high quality.
</goal>

<usage>
`/review <bead-id>`
</usage>

<inputs>
- Bead: `bd show <bead-id> --json`
- Spec: `.beads/artifacts/<bead-id>/spec.md`
- Plan: `.beads/artifacts/<bead-id>/plan.md`
</inputs>

<constraints>
- **YOU MUST NOT** Edit code.
- **YOU MUST NOT** Change plans/specs.
</constraints>

<workflow>
1. **Inspect Changes**
   - `git diff main...HEAD --stat` (summary)
   - `git diff main...HEAD` (detailed check of key files)

2. **Verify Acceptance Criteria**
   - For each criterion in `spec.md` and step in `plan.md`:
     - Mark as **Met**, **Not Met**, or **Changed**.
   - Verify that tests have been run (ask user if unsure).

3. **Identify Deviations**
   - List unplanned changes or missing work.
   - Flag any leftover `console.log`, `TODO`, or `FIXME` markers.

4. **Create Review Artifact**
   - Write to `.beads/artifacts/<bead-id>/review.md`:
     - **Summary**: High-level overview.
     - **Plan Alignment**: Table of Plan Steps vs Status.
     - **Deviations**: Unplanned work or scope creep.
     - **Quality Check**:
       - [ ] No console.logs?
       - [ ] Tests passed?
       - [ ] Types strict?
       - [ ] **Deep Modules**: Are interfaces simple vs. implementation? (APoSD)
       - [ ] **No Clutter**: Is the code free of unnecessary defensive checks?
     - **Recommendation**: "Ready to Merge" OR "Needs Work".

5. **Output**
   - Summarize the review. If blocking issues exist, state them clearly.
</workflow>
