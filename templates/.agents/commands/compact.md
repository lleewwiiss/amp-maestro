# /compact – Summarize session and sync state

Use this at the end of a session to "save game" and clean up context.

Usage: `/compact <bead-id>`

Workflow:

1. **Summarize Session**
   - Create a session artifact: `.beads/artifacts/<bead-id>/sessions/session-<ISO8601>.md`.
   - Content should include:
     - **Summary**: What was accomplished.
     - **Changes**: Key code changes (files touched).
     - **Decisions**: Why certain paths were taken.
     - **Next Steps**: What is left to do.

2. **Update Bead Description (Lightweight)**
   - Append a *one-line* summary to the Bead's description under a `Session History` section (create if missing).
   - Example format:
     ```text
     Session History
     - 2025-11-20: Implemented auth middleware, added tests. Next: integrate with router.
     ```
   - Ensure `Context` block points to `sessions/` dir:
     ```text
     - Sessions: .beads/artifacts/<bead-id>/sessions/
     ```
   - Use `bd update <bead-id> --description "..." --json`.

3. **Git Hygiene**
   - Check `git status`.
   - **HUMAN-IN-THE-LOOP**: "I propose to commit these changes with message '...'. Approve?"
   - If approved, commit.
   - **HUMAN-IN-THE-LOOP**: "Push to remote? (git push)"
   - If approved, push.

4. **Beads Sync**
   - **HUMAN-IN-THE-LOOP**: "Run `bd sync` to synchronize issue state? (Recommended)"
   - If approved, run `bd sync`.

5. **Clear Context**
   - Explicitly state: "Session compacted. You can now safely clear this thread context or start a new one."
