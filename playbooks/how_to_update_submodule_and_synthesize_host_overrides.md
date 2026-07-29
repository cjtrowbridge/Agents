# Playbook: Update Submodule and Synthesize Host Overrides

*Status: Draft*

## Objective

Provide a safe, repeatable workflow for updating the `./agents` submodule in a host repository and synthesizing host-managed framework files (`./playbooks`, `./references`, `./templates`, `./scripts`, shims) with user-approved merge decisions.

## Prerequisites

- Host repository includes this framework as `./agents`.
- Host repository contains managed framework copies and/or customizations.
- User approval available for merge resolutions.

## Step-by-Step Instructions

1. **Capture Update Baseline**
   - Record current submodule commit.
   - Inventory host-managed framework files changed since prior sync.
   - Identify high-risk artifacts (policy files, plan tooling, templates used in active workflows).

2. **Update Submodule**
   - Update submodule pointer to target upstream revision.
   - Record new submodule commit.

3. **Compute Three-Way Inputs**
   - For each managed file:
     - old upstream version from previous submodule commit,
     - new upstream version from updated submodule commit,
     - current host-managed version.

4. **Draft Synthesis Recommendations**
   - Propose merged outputs that:
     - preserve host-specific behavior,
     - integrate new upstream safety/policy/tooling improvements.
   - Use `./templates/submodule_update_synthesis_report.md` to organize proposals.

5. **Ask User Before Final Merge Decisions**
   - Present recommendations and impacted files.
   - Ask explicit approval for final resolution choices.
   - Do not silently apply unresolved merge decisions.

6. **Apply Approved Synthesis Outputs**
   - Write only approved merged content.
   - Keep file-level changes atomic and traceable.

7. **Run Migration/Integration Checks**
   - Check for path changes requiring host updates.
   - Check policy/schema changes requiring host migration.
   - Check script behavior/flags that affect host commands.
   - Run:
     - `python agents/scripts/regenerate_plan_indexes.py --check --repo-root .`

8. **Finalize and Report**
   - Summarize:
     - submodule commit delta,
     - files synthesized,
     - user-approved merge decisions,
     - migration actions and residual risks.
   - Include active plan path and checklist item deltas.

## Required Migration for This Upstream Change

This update retires an operational workflow, removes obsolete root harness shims, introduces a mandatory user-owned `TODO.md`, and makes completed-work journal updates automatic. Treat it as a breaking host-integration change.

1. **Identify the Exact Delta Before Writing**
   - Record the old and new submodule commit IDs.
   - From the host root, inspect the authoritative upstream delta:
     - `git -C agents diff --name-status <old-submodule-commit> <new-submodule-commit>`
     - `git -C agents diff --diff-filter=D --name-only <old-submodule-commit> <new-submodule-commit>`
   - Use those deleted-path results as the authoritative inventory. Do not recreate, retain, or link to retired artifacts in the host.

2. **Remove Host Mirrors of Retired Artifacts**
   - For every deleted upstream artifact that has a host-managed counterpart, remove the counterpart only after confirming it is the matching retired file.
   - Remove obsolete root harness shims when they appear in the deletion inventory; retain the root `AGENTS.md` instruction file.
   - Search host-managed docs, templates, references, journal templates, and active policies for every deleted path or its workflow wording; remove or replace obsolete guidance.
   - Preserve user data. If a host has material user-authored content in a retired artifact, present a migration/export proposal before deletion rather than silently discarding it.

3. **Apply the New User TODO Contract**
   - Ensure root `TODO.md` exists. If missing, initialize it from the upstream starter file; if it already exists, preserve its user-authored content.
   - Ensure the host `AGENTS.md` tells agents that `TODO.md` is user-owned brainstorming space, not agent execution authority.
   - Require agents to inspect, select, prioritize, edit, or work on TODO entries only when the user specifically directs that action.

4. **Adopt the Automatic Journal Contract**
   - Synthesize the current journal template and applicable host-managed playbooks with the new policy.
   - Ensure the host policy states that agents update today's journal automatically after every completed work checkpoint, without requesting permission.
   - Require each entry to say what was completed, why it was done, where the work is heading next (or that it is complete), and relevant follow-up.
   - Keep commit and push approval rules separate: automatic journal updates do not authorize git actions.

5. **Explain the Migration to Host Agents**
   - In the host `AGENTS.md`, direct agents to the updated `./agents/RULES.md` and state the TODO ownership boundary.
   - Add or synthesize this instruction when the host does not already express the same rule:

     ```md
     `TODO.md` is user-owned brainstorming space, not an agent task list. Do not inspect, select, prioritize, edit, or work on TODO entries unless the user specifically directs it. After every completed work checkpoint, update today's journal automatically with what was completed, why, next direction (or completion), and follow-up; commit and push still require their normal approvals.
     ```

   - When host-managed copies exist, synthesize rather than blindly copy `playbooks/`, `references/`, and `templates/`; preserve host-specific instructions that do not conflict with the new policy.
   - Add the completed migration actions, evidence, and any intentionally retained user data to the update synthesis report and today's journal.

6. **Validate Before Closing the Update**
   - Confirm every deleted upstream path has no unintended host mirror or stale documentation reference.
   - Confirm `TODO.md` exists and retains user-owned content.
   - Confirm current agent instructions contain both the TODO explicit-direction boundary and automatic detailed-journal rule.
   - Run `python agents/scripts/regenerate_plan_indexes.py --check --repo-root .` from the host root.
   - Run targeted `rg` checks using the deleted-path inventory and review `git diff --check`.

7. **Rollback If Validation Fails**
   - Restore the prior submodule commit and the host-managed files recorded in the synthesis report.
   - Do not overwrite a user-owned `TODO.md` during rollback; restore only agent-managed policy and workflow artifacts.
   - Re-run the plan-index and stale-reference checks after rollback.

## Verification

- Host-managed framework files reflect approved synthesis outputs.
- No unresolved merge decisions remain.
- Host verification commands pass for current operational paths.
- README/docs impacted by update semantics are synchronized.

## Lifecycle Compliance

Prompt -> Select/Create Plan (using relevant playbook guidance) -> Request approval -> Execute approved plan atoms -> Plan update -> Docs update -> Verification.

If this occurs inside a git repo:
- Review `git status` and relevant diffs.
- Suggest a commit message that summarizes the completed checkpoint.
- Commit after approved checkpoint completion.
