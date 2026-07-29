---
plan_id: 2026-07-29-11-00-58_document-downstream-workflow-retirement-migration
title: Document Downstream Workflow-Retirement Migration
summary: Give downstream submodule consumers explicit migration instructions for the retired workflow, user TODO contract, and automatic journal updates.
status: past
created_at: 2026-07-29-11-00-58
---

# Document Downstream Workflow-Retirement Migration

Key: `[ ]` pending task, `[x]` completed task, `[?]` needs validation, `[-]` closed task

- [x] 1. Define a downstream breaking-change migration procedure.
  - [x] 1.1 Update the submodule-update playbook with an explicit host-side inventory, synthesis, migration, verification, and rollback sequence.
    - [x] 1.1.1 Specify the retired workflow artifacts and unused shims that hosts must remove when present.
    - [x] 1.1.2 Specify creation and ownership of root `TODO.md`, automatic journal-update policy, and the required host agent-instruction wording.
  - [x] 1.2 Update the synthesis-report template so hosts record decisions, actions, and evidence for this migration.

- [x] 2. Update downstream documentation and policy for migration discoverability.
  - [x] 2.1 Add an explicit migration section to `README.md` that routes maintainers and agents to the detailed playbook.
  - [x] 2.2 Add a governing-policy requirement to apply the documented migration during downstream updates.

- [x] 3. Verify and close the documentation migration.
  - [x] 3.1 Review the migration instructions for complete coverage of removal, new-file, policy, verification, and rollback actions.
  - [x] 3.2 Update today's journal automatically with completed-work details.
  - [x] 3.3 Update this plan, regenerate indexes, review the diff/status, and archive the plan.
