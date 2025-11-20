# /land-plane – Cleanly land the session using Beads + Branchlet conventions

Use this when the human wants to “land the plane” on the current work session. The goal is to leave:
- Beads in sync with reality.
- Git in a clean state.
- A clear next step for the next session.

Follow this checklist:

1. **Inventory current work**
   - Summarize:
     - Which bead(s) you’ve been working on.
     - What changes you’ve made (code, config, tests, docs).
   - Ask the human to confirm or correct this list.

2. **File beads for remaining work (if any)**

   - For any discovered-but-not-tracked work:
     - Propose `bd create "…" -t task|bug -p <priority> --deps discovered-from:<parent-id> --json`.
   - **HUMAN-IN-THE-LOOP CHECK:**
     - Show each proposed new bead (title, type, priority, parent) and ask for approval before creating it.

3. **Update and/or close beads for work done**

   - For the bead(s) you’ve worked on:
     - Propose appropriate status changes, e.g.:
       - `bd update <ID> --status blocked|in_progress|open --json`
       - `bd close <ID> --reason "Implemented and verified" --json`
   - Again, ask the human to approve each change before executing it.

4. **Run quality gates (tests/linters) if code changed**

   - If you’ve made code changes, propose a short list of relevant commands, e.g.:
     - `go test ./...` or project-specific test commands.
     - Lint/format commands.
   - **HUMAN-IN-THE-LOOP CHECK:**

     Say:

     > “I propose to run these checks before we finish:  
     > - …  
     > Approve / modify / skip?”

   - Only run the commands the human approves.
   - If any tests or linters fail:
     - Summarize failures.
     - Decide together whether to file new beads (with `bd create …`) or fix immediately.

5. **Sync Beads carefully**

   - Propose running `bd sync` to flush/export/commit/pull/import/push the issue database.
   - Explain what it does in this context.
   - **HUMAN-IN-THE-LOOP CHECK:**

     > “I propose to run `bd sync` now to ensure all beads are safely synced via git. Approve / decline?”

   - Only if approved:
     - Run `bd sync`.
     - If there are any conflicts or errors (especially around `.beads/` files), explain them clearly and ask how they’d like to resolve them.

6. **Git Hygiene & Conventional Commits**
   - Show a succinct `git status` summary.
   - **Commit Message Rules**:
     - Format: `<type>: <subject>` (e.g., `feat: add user login`, `fix: resolve race condition`).
     - Types: `feat`, `fix`, `chore`, `refactor`, `docs`, `test`, `perf`.
     - Body: Must include `Refs <bead-id>` or `Fixes <bead-id>`.
   - **HUMAN-IN-THE-LOOP**: "I propose commit message: '...'. Approve?"
   - If approved, commit.
   - **HUMAN-IN-THE-LOOP**: "Push to remote? (git push)"
   - If approved, push.

7. **Suggest the next bead / next prompt**

   - Use `bd ready --json` and/or `bd stats` to suggest:
     - A specific bead id + title as the next task.
     - A short “next session prompt” the human can paste into Amp later, e.g.:

       > “Continue work on `<ID>` – ‘<title>’.  
       > Context: <1–3 sentences of what’s been done and what’s next>.”

8. **Final recap**

   - Provide a brief recap:
     - Which beads were created / updated / closed.
     - Which tests/quality gates ran and their status.
     - Whether `bd sync` and git push were performed.
   - Stop after this recap unless the human asks for more.
