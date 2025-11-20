# /bd-create – Interactively create a new Beads issue or epic

Use this when the user wants to file a new issue but needs guidance on structure, type, and dependencies.

Usage: `/bd-create`

Workflow:

1. **Interview Phase (Problem Understanding)**
   - Ask the user: "What problem are we solving? Or what feature are we building?"
   - Ask probing questions to clarify scope (e.g., "Is this frontend only?", "Does this affect the DB?", "Is this a bug or a new capability?").
   - **Goal**: Understand the *Work*, not just the name.

2. **Structure & Classification**
   - **Type**: Suggest `bug`, `feature`, `task`, `epic`, or `chore` based on the interview.
   - **Priority**: Suggest `0`-`4` based on urgency/impact.
   - **Title Generation**:
     - Generate a concise, action-oriented title (e.g., "Implement robust retry logic for API client").
     - **Do not ask the user for a title**—propose the best one.

3. **Dependency & Lineage (Crucial)**
   - Search: `bd list --json`.
   - Identify relationships:
     - "Does this belong to Epic X?" -> `blocks:bd-X`
     - "Is this blocking Bead Y?" -> `blocks:bd-Y`
     - "Was this found while working on Bead Z?" -> `discovered-from:bd-Z`
   - Explain the proposed lineage graph.

4. **Create Bead**
   - Construct: `bd create "<Generated Title>" ...`
   - **HUMAN-IN-THE-LOOP**: "I propose creating this bead with title '...' and deps '...'. Approve?"
   - Execute.

5. **Post-Creation Actions**
   - Display the new Bead ID.
   - Ask: "Do you want to start research on this now? (/research <id>)"
