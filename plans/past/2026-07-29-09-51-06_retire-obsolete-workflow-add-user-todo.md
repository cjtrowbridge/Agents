---
plan_id: 2026-07-29-09-51-06_retire-obsolete-workflow-add-user-todo
title: Retire Obsolete Workflow and Unused Shims; Add User-Owned TODO
summary: Retire the obsolete board workflow and unused harness shims with all references, then add a root TODO.md reserved for user brainstorming.
status: past
created_at: 2026-07-29-09-51-06
---

# Retire Obsolete Workflow and Unused Shims; Add User-Owned TODO

Key: `[ ]` pending task, `[x]` completed task, `[?]` needs validation, `[-]` closed task

- [x] 1. Retire the obsolete board workflow from the repository.
  - [x] 1.1 Delete its workspace directory and five board files.
    - [x] 1.1.1 Remove the five former horizon- and theme-specific board files.
  - [x] 1.2 Delete dedicated workflow artifacts.
    - [x] 1.2.1 Remove the movement playbook, handling reference, and board template.
  - [x] 1.3 Remove workflow language from active policies, workflows, templates, bootstrap guidance, checkpoint guidance, and the existing journal artifact.
    - [x] 1.3.1 Update `RULES.md`, `README.md`, `AGENTS.md`, the daily kickoff, host bootstrap, and journal checkpoint playbooks, the journal template, and checkpoint reference.
  - [x] 1.4 Remove workflow references from historical plan artifacts so a repository-wide search contains no obsolete-workflow references.
    - [x] 1.4.1 Update the two archived plan files that mention the retired workflow.

- [x] 2. Remove unused harness shim files and all references to them.
  - [x] 2.1 Delete the four unused root harness shim files.
  - [x] 2.2 Remove active policy and README references that identify the deleted files as supported shims.
    - [x] 2.2.1 Retain `AGENTS.md` as the sole supported root agent instruction file.
  - [x] 2.3 Remove references to the deleted shim files from archived plan artifacts.

- [x] 3. Add and document the mandatory user-owned TODO file.
  - [x] 3.1 Create root `TODO.md` with an explanation, a checklist key, and an ordered brainstorming checklist.
    - [x] 3.1.1 State that TODO items are not agent tasks and may be inspected or worked only when the user explicitly directs it.
  - [x] 3.2 Update `AGENTS.md` and governing policy to require `TODO.md` while preserving user ownership and the explicit-direction boundary.
    - [x] 3.2.1 Update downstream bootstrap documentation to create and preserve root `TODO.md`.

- [x] 4. Make completed-work journal updates automatic and informative.
  - [x] 4.1 Update governing rules to require an immediate journal update after completed work without asking permission.
    - [x] 4.1.1 Require entries to state what was completed, why it was done, and the next direction or follow-up.
  - [x] 4.2 Update affected playbooks, references, and journal templates to remove journal-update approval gates and use the automatic-update policy.
    - [x] 4.2.1 Preserve approval requirements for commits and pushes.
  - [x] 4.3 Update today's journal entry with the completed-work details required by the new policy.

- [x] 5. Verify the migration and record plan completion.
  - [x] 5.1 Run repository-wide searches confirming no retired-workflow or deleted-shim references remain.
  - [x] 5.2 Confirm `TODO.md` provides the required explanation, key, and ordered checklist, and that agent instructions state the explicit-direction rule.
  - [x] 5.3 Confirm journal policy and documentation require automatic, detailed completed-work entries without permission gates.
  - [x] 5.4 Update this plan, regenerate plan indexes, and review the final diff and repository status.
