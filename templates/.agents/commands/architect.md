# /architect – Visualize and Document System Architecture

Use this to create or update architecture diagrams and decision records.

Usage: `/architect <bead-id> [topic]`

Workflow:

1. **Visualize State**
   - Ask: "What system or flow are we visualizing?"
   - Generate a **Mermaid Diagram** (Sequence, Class, or Entity Relationship).
   - **HUMAN-IN-THE-LOOP**: "Does this diagram accurately reflect the system? What should I change?"

2. **Decision Records (ADR)**
   - If a major architectural decision was made (e.g., "Switch to Redis"), create an ADR.
   - Path: `.beads/artifacts/<bead-id>/adr-<topic>.md`.
   - Sections: Context, Decision, Consequences.

3. **Update Context**
   - Add diagram/ADR link to `research.md` or `plan.md`.
