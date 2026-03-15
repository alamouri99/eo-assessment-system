# TASK-002: Create spec template and sample task spec
## Status: done
## Assigned: openclaw
## Risk Tier: low

## Objective
Create a reusable agent task spec template and a self-referencing sample task spec to establish the spec-driven workflow for all future agent work.

## Declared Files
- specs/tasks/SPEC-TEMPLATE.md
- specs/tasks/TASK-002.md

## Hard Constraints
- Do NOT touch any files outside Declared Files
- Do NOT modify .github/, prompts/, infra/, or product/

## Acceptance Criteria
- [ ] specs/tasks/SPEC-TEMPLATE.md exists and is valid markdown
- [ ] specs/tasks/TASK-002.md exists and references itself in Declared Files
- [ ] No files outside declared scope were touched

## Notes
This is the first agent-executed task in the SMOrchestra AI-Native Git Architecture.
Spec template follows the format defined in the AI-Native Git Architecture v2 doc.
Self-referencing spec demonstrates that the workflow is operational end-to-end.
