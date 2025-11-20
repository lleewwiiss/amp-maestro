# /bd-next – Choose the next Beads issue to work on

You are Amp, selecting the next task using the Beads (`bd`) issue tracker instead of intuition.

Goal:
- Use Beads’ notion of “ready work” to propose 1–3 good candidates.
- Ask the human to select or adjust the choice.
- Once selected, optionally start a Branchlet-style short-lived branch for that bead.

Follow this workflow:

1. **Query ready work**

   - Prefer JSON output so you can reason programmatically:
     - `bd ready --json`
   - If the `bd next` command is available in this repo (check help or docs), you may also try:
     - `bd next --json`
   - Parse the results and shortlist the **top 1–3 candidate beads**, prioritizing:
     - Higher priority (0, 1).
     - Clear, actionable descriptions.
     - Issues that match any constraints the user already mentioned (e.g., “backend only”, “small tasks”).

2. **Propose candidates to the human**

   - Present a concise table/list for each candidate:
     - `id`, `title`, `priority`, `status`, and a short summary of dependencies.
   - **HUMAN-IN-THE-LOOP CHECK:**

     Ask explicitly:

     > “Which bead should we pick next? For example:  
     > 1) bd-… – …  
     > 2) bd-… – …  
     > 3) bd-… – …  
     > Or specify a different bead id/title.”

   - Wait for the human to choose or override. Do **not** proceed until they confirm.

3. **Propose Environment (Branch vs Worktree)**
   - Ask: "Create a dedicated **Worktree** (Branchlet) or a standard **Feature Branch**?"
   - **Worktree** (Recommended for deep/parallel work):
     - Run `/branchlet-from-bead <ID>`.
   - **Feature Branch** (Simpler for quick fixes):
     - Run `git switch -c feature/<ID>-<slug>`.
     - Ensure working directory is clean first.

4. **Start Work**
   - If Worktree: Agent opens new window.
   - If Branch: Agent stays here.
   - Next step: `/research <ID>`.
