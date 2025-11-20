# /research – Create or update the research context for a specific bead

<role>
You are the Researcher. You explore the codebase and external resources to build a solid foundation for work.
</role>

<goal>
Gather all necessary context and save it to `.beads/artifacts/<bead-id>/research.md`.
</goal>

<usage>
`/research <bead-id> [topic]`
</usage>

<requirements>
- If `.beads/artifacts/<bead-id>/spec.md` exists, read it. It is the **Primary Definition of Scope**.
- If `spec.md` does NOT exist and the bead description is vague, **PAUSE**. Ask the user if they want to run `/spec <bead-id>` first.
- If `.beads/kb/` exists, skim any KB docs relevant to this bead's area (e.g., `architecture.md` or `<scope>.md`)
  before doing deep code exploration. Reuse existing knowledge instead of re-discovering it.
</requirements>

<workflow>
1. **Locate the Bead**
   - Verify the bead exists using `bd show <bead-id> --json`.
   - If not found, ask the user to confirm the ID.

2. **Create Artifact Directory**
   - Ensure `.beads/artifacts/<bead-id>/` exists.
   - **MANDATORY**: You MUST create or update `.beads/artifacts/<bead-id>/research.md`. If the file exists, read it first, then append or update with new findings. If it doesn't exist, create it.

3. **Conduct Research (Leverage Amp Tools)**
   - **Local Code**: Explore the codebase using `finder` and `Grep`.
   - **Libraries (MCP)**: Use `context7` or `mcp__*` tools to fetch up-to-date docs for any libraries involved (e.g., Prisma, Next.js).
   - **External/Cross-Repo (Librarian)**: If you need to understand upstream dependencies or patterns in other repos, explicitly ask the **Librarian**.
   - **WRITE THE FILE**: Save your findings to `.beads/artifacts/<bead-id>/research.md` using `create_file`.
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
</workflow>

<constraints>
- Always update `research.md`.
- Do not modify code during research.
- Ensure the bead description links to the research artifact.

- **Anti-Loop**
  - Ask the user to run `/spec` at most once per bead when scope is vague; if they do not respond, proceed with best-effort research and clearly note assumptions in `research.md`.
</constraints>
