# /context – Load full context for a bead

Use this at the start of a thread to "boot up" the agent with all relevant history for a bead.

Usage: `/context <bead-id>`

Workflow:

1. **Fetch Bead Details**
   - Run `bd show <bead-id> --json`.
   - Display ID, Title, Status, Priority, Dependencies.

2. **Load Artifacts**
   - Check `.beads/artifacts/<bead-id>/`.
   - If `research.md` exists, read it (or the first 50 lines + summary).
   - If `plan.md` exists, read it.
   - If `sessions/` exists, read the *most recent* session file to see where we left off.

3. **Synthesize State**
   - "We are working on <Title>."
   - "The plan is <Plan Summary>."
   - "Last session ended with <Last Session Summary>."
   - "Immediate next step appears to be <Next Step>."

4. **Ready**
   - Ask user: "Ready to continue implementation? (Run /implement <bead-id>)"
