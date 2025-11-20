# Agent Guidelines

## Project Overview
<!-- User: Add a brief description of your project here -->

## Build, Lint, Test Commands
<!-- User: specific commands for your project. If empty, Agent should inspect package.json/Makefile. -->
- **Build**: `[Inspect package.json/Makefile]`
- **Test**: `[Inspect package.json/Makefile]`
- **Lint**: `[Inspect package.json/Makefile]`
- **Format**: `[Inspect package.json/Makefile]`

**IMPORTANT**: 
- Always run linting and type-checking commands before reporting a task as complete.
- Do not suppress errors (e.g., `// @ts-ignore`) unless absolutely necessary and explicitly authorized.

## Issue Tracking: bd (beads) ONLY
**CRITICAL**: Use `bd` commands for ALL task tracking. NEVER use TodoWrite, markdown TODOs, or planning files.
- `bd ready --json` — Check unblocked work
- `bd create "Task description" -t bug|feature|task -p 0-4 --json` — Create issues
- `bd create "Found bug" --deps discovered-from:bd-42 -t bug -p 1 --json` — Link discovered issues
- `bd update bd-42 --status in_progress --json` — Claim work
- `bd close bd-42 --reason "Completed" --json` — Mark done
- Always commit `.beads/issues.jsonl` with code changes

**Issue Types**: `bug`, `feature`, `task`, `epic`, `chore`
**Priorities**: `0` (critical: security, data loss, broken builds) → `4` (backlog: future ideas)

## Agentic Workflow
See [AGENTIC_WORKFLOW.md](./AGENTIC_WORKFLOW.md) for the full protocol (Ideation → Research → Plan → Implement → Merge).

**Quick Protocol:**
1. **Start**: `/context <id>`
2. **Research**: `/research <id>`
3. **Plan**: `/plan <id>` (Uses Oracle)
4. **Work**: `/implement <id>` (Uses Subagents)
5. **Finish**: `/land-plane`

**Source of Truth**: `bd` issues for **WHAT**, `.beads/artifacts/` for **HOW**.

### Rules
- **NEVER** put long plans in Bead descriptions.
- **ALWAYS** use slash commands to manage lifecycle.
- **ALWAYS** run `bd sync` before ending.

## Code Style
- **Conventions**: Mimic existing code style, naming conventions, and directory structure.
- **Types**: Avoid `any` or `unknown` where possible. Be explicit.
- **Comments**: Only comment complex logic; code should be self-documenting.
- **Secrets**: NEVER commit secrets or keys.

## Testing & Verification
- Test early and often.
- Verify assumptions with code (e.g., small scripts) before implementing large changes.
- **Libraries**: Never assume you know how to use a library. Use `context7` or search tools to read documentation first.
