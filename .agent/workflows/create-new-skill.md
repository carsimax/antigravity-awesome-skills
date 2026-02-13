---
description: Create a new Antigravity skill following official standards
---

# Create New Antigravity Skill

This workflow guides the creation of a new skill, ensuring compliance with Antigravity standards.

1. **Analyze Request**
    - Identify the skill's **Purpose** (what problem it solves), **Scope** (Workspace vs Global), and **Type** (Convention, Workflow, Tool, Generator).

2. **Check Existing Skills (MANDATORY)**
    - Open and read `CATALOG.md` to search for similar or related skills.
    - Check the `skills/` directory to see examples of existing skill implementations.
    - *Goal*: Use an existing skill as a baseline references to ensure consistency.

3. **Consult Documentation (MANDATORY)**
    - **CRITICAL**: Do not rely on internal training data for skill structure.
    - **Source of Truth**: [https://antigravity.google/docs/skills](https://antigravity.google/docs/skills)
    - **Verify**:
        - Naming conventions (must be `kebab-case`).
        - Directory structure (must strictly follow the docs).
        - `SKILL.md` format (Frontmatter + Markdown body).

4. **Create Skill Structure**
    - Create the directory: `.agent/skills/<skill-slug>/` (for workspace skills).
    - Create `SKILL.md`.
    - (Optional) Create `scripts/`, `resources/`, `examples/` folders if required.

5. **Write SKILL.md**
    - **Frontmatter**: Include `name` and a clear `description` for agent triggering.
    - **Body**: Use imperative instructions, clear sections, and **always include examples**.

6. **Validate**
    - Verify `SKILL.md` format against the official docs.
    - Ensure the skill name is a valid slug.
