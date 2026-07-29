# Playbook: Daily Kickoff and Snapshot Capture

*Status: Stable*

## Objective
Run a startup workflow that discovers daily journal state, captures daily intent, updates the journal automatically after completed work, and prepares a checkpoint summary.

## Prerequisites

- Read `README.md` and `RULES.md` before making changes.
- Journal template available at `./templates/daily_journal_entry.md`.

## Step-by-Step Instructions

1. **Resolve Local Date**
   - Determine current local date as `YYYY-MM-DD`.

2. **Discover Today's Journal State (Read-Only)**
   - Target path: `./journal/YYYY-MM-DD.md`.
   - Record whether it exists.

3. **Present Startup Status**
   - Report:
     - what exists already,
     - what is missing,
     - what files would be created/updated.

4. **Create Missing Artifacts**
   - If `./journal/YYYY-MM-DD.md` is missing, create from `./templates/daily_journal_entry.md` and replace all `YYYY-MM-DD` tokens with the resolved date.

5. **Startup Interaction**
   - Greet the user with:
     - what exists today,
     - what was created,
     - what information is still needed.
   - Ask the smallest set of questions required to capture:
     - `Today's Intentions` from the user (verbatim user text only),
     - immediate task flow details.

6. **Confirm Active Plan Before Non-Trivial Execution**
   - Identify the governing active plan path in `./plans/current/` for non-trivial repository changes.
   - If no suitable active plan exists, create a quick-start plan scaffold via `./playbooks/how_to_create_and_maintain_task_execution_plans.md` and request approval before implementation.
   - Quick-start scaffold minimum:
     - objective checklist item,
     - implementation checklist decomposition,
     - verification checklist decomposition.
   - Promote `future -> current` immediately before the first non-trivial implementation edit.
   - Map intended checkpoint work to explicit plan checklist items.

7. **Prepare Journal Update Content**
   - Capture `Today's Intentions` using verbatim user-provided text only.
   - Do not author, infer, summarize, or rewrite intentions.
   - If the user does not provide intentions, keep `Today's Intentions` as an empty list item (`-`).
   - Draft required repo work log entries for repository changes made during the checkpoint.

8. **Present Snapshot Summary**
   - List files changed.
   - List what was added/updated.
   - List active plan path and checklist items updated in this checkpoint.

9. **Update Journal Automatically**
   - Before the completion summary, create or append to today's journal entry without asking permission.
   - Record what was completed, why it was done, where the work is heading next (or that it is complete), and relevant follow-up.

10. **Commit + Push Journal Checkpoint**
   - For journal checkpoint commits, follow `./playbooks/how_to_commit_and_push_journal_checkpoints.md`.

## Verification

- `./journal/YYYY-MM-DD.md` exists and has kickoff/intent/log sections filled.
- `Today's Intentions` contains user-provided text or an empty list item (`-`).
- Snapshot summary matches actual diffs.
- Active plan path and checklist deltas are captured when non-trivial repository work occurred.

## Lifecycle Compliance

Prompt -> Select/Create Plan (using relevant playbook guidance) -> Request approval -> Execute approved plan atoms -> Plan update -> Docs update -> Verification.

If this occurs inside a git repo:
- Review `git status` and relevant diffs.
- Suggest a commit message that summarizes the completed task.
- Update today's journal automatically before the completion summary and commit flow.
- Commit after approved checkpoint completion.
