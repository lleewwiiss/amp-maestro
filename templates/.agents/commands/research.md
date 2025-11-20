# /research – Create or update the research context for a specific bead

Use this when starting work on a Bead to build context before planning or coding.

Usage: `/research <bead-id> [topic]`

**Requirements**:
- If `.beads/artifacts/<bead-id>/spec.md` exists, read it. It is the **Primary Definition of Scope**.
- If `spec.md` does NOT exist and the bead description is vague, **PAUSE**. Ask the user if they want to run `/spec <bead-id>` first.

Workflow:

1. **Locate the Bead**
   - Verify the bead exists using `bd show <bead-id> --json`.
   - If not found, ask the user to confirm the ID.

2. **Create Artifact Directory**
   - Ensure `.beads/artifacts/<bead-id>/` exists.
   - Create `.beads/artifacts/<bead-id>/research.md` if it doesn't exist.

3. **Conduct Research (Leverage Amp Tools)**
   - **Local Code**: Explore the codebase using `finder` and `Grep`.
   - **Libraries (MCP)**: Use `context7` or `mcp__*` tools to fetch up-to-date docs for any libraries involved (e.g., Prisma, Next.js).
   - **External/Cross-Repo (Librarian)**: If you need to understand upstream dependencies or patterns in other repos, explicitly ask the **Librarian**.
   - **Document findings** in `research.md`:
     - Problem statement / Goals.
     - Relevant files and code paths.
     - Potential approaches and trade-offs.
     - Links to external docs or related beads.
   - **Do NOT** create a task list here (use `plan.md` or new Beads for that).

4. **Link to Bead**
   - Read the current bead description: `bd show <bead-id> --json`.
   - Check for a `Context` block. If missing, create one at the bottom:
     ```text
     Context
     - Research: .beads/artifacts/<bead-id>/research.md
     ```
   - If present, ensure the `Research:` line points to the correct file.
   - Use `bd update <bead-id> --description "..." --json` to save changes.

5. **Summarize**
   - Report what was researched and where the artifact is saved.
   - Prompt the user to review `research.md` or proceed to `/plan`.
