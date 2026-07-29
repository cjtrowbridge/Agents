# agents

Framework policy, playbooks, references, templates, and scripts for plan-governed agent execution.

## Purpose

This repository is intended to be consumed upstream as a git submodule in a host repository.

Primary deployment model:
- host repository root contains project-specific operational artifacts,
- this framework is mounted at `./agents`,
- host shims and host-managed framework copies are synchronized from the submodule over time.

## Canonical Rules

- Canonical policy source: `./agents/RULES.md` (from host root)
- The root `AGENTS.md` instruction file should direct runtimes to that policy source.
- Root `TODO.md` is mandatory, user-owned brainstorming space; agents use it only when the user specifically directs them to do so.

## Host Bootstrap (First-Time Integration)

1. Add the framework as a submodule at `./agents`.
2. Initialize/update submodule content.
3. Ensure required host operational directories exist:
   - `./plans/future/`, `./plans/current/`, `./plans/past/`
   - `./journal/`
   - `./downtime/reports/pending/`, `./downtime/reports/reviewed/`
4. Ensure host `./AGENTS.md` points to `./agents/RULES.md`, and create a root user-owned `./TODO.md`.
5. Copy host-managed framework directories from `./agents/` when missing:
   - `./playbooks/`
   - `./references/`
   - `./templates/`
   - `./scripts/`
6. If host already has those directories/files, synthesize host + upstream updates:
   - preserve host custom behavior,
   - integrate new upstream safety/features,
   - ask user approval before final merge resolutions.

Example command sequence from host root:

```bash
git submodule add <framework-repo-url> agents
git submodule update --init --recursive agents
mkdir -p plans/future plans/current plans/past journal downtime/reports/pending downtime/reports/reviewed
cp agents/AGENTS.md AGENTS.md
cp -R agents/playbooks playbooks
cp -R agents/references references
cp -R agents/templates templates
cp -R agents/scripts scripts
```

If host files/directories already exist, do not overwrite blindly; follow synthesis merge workflow.

## Host vs Submodule Ownership

Host-owned runtime artifacts (project-specific state):
- `./plans/`
- `./journal/`
- `./downtime/reports/`
- `./TODO.md` (user-owned; not agent execution work unless explicitly directed)

Host-managed framework working copies (copied/synthesized from submodule):
- `./playbooks/`
- `./references/`
- `./templates/`
- `./scripts/`
- host `./AGENTS.md`

Submodule-owned upstream defaults:
- `./agents/RULES.md` (authoritative policy contract)
- all upstream source artifacts under `./agents/` used for synchronization and update synthesis

Precedence rule:
- host-managed copies are runtime-active in host workflows,
- submodule artifacts are the upstream source for updates,
- merge/synthesis recommendations must be presented to user for approval before final application.

## Agent Resolution Rules From Host Root

When an agent starts from host `./AGENTS.md`, it should:
1. Read `./agents/RULES.md`.
2. Use host-managed `./playbooks`, `./references`, `./templates`, `./scripts` when present.
3. If a host-managed artifact is missing, fall back to `./agents/<artifact-path>`.
4. For host-owned plan/index operations, run:
   - `python agents/scripts/regenerate_plan_indexes.py --repo-root .`

## Submodule Update + Synthesis Merge Workflow

1. Record current submodule pointer and host-local customizations.
2. Update submodule pointer to new upstream revision.
3. Compare:
   - old upstream version,
   - new upstream version,
   - current host-managed copy.
4. Produce synthesis recommendations per changed host-managed file.
5. Ask user approval before final merge decisions.
6. Apply approved merged outputs.
7. Run migration/integration checks (paths, policy/schema shifts, script mode changes).
8. Verify host operational behavior.

Primary playbooks for this workflow:
- `./playbooks/how_to_bootstrap_framework_submodule_into_host_repo.md`
- `./playbooks/how_to_update_submodule_and_synthesize_host_overrides.md`

## Migration / Integration Checklist During Updates

Always evaluate and handle:
- path and structure changes,
- policy/schema changes (including plan key semantics and required metadata),
- script interface/behavior changes.

Required verification examples:
- `python agents/scripts/regenerate_plan_indexes.py --check --repo-root .`
- grep checks for stale paths or deprecated wording in host-managed copies.

Rollback expectation:
- keep a rollback path for submodule pointer and synthesized host files if validation fails.

## Downstream Migration for the Current Breaking Change

When updating a downstream `./agents` submodule to this revision, follow the detailed procedure in `./playbooks/how_to_update_submodule_and_synthesize_host_overrides.md` under **Required Migration for This Upstream Change**.

The host update must:

1. Compare old and new upstream revisions to inventory retired artifacts before altering host files.
2. Remove matching agent-managed host mirrors and stale guidance while preserving any user-authored data through an approved migration/export decision.
3. Ensure root `TODO.md` exists, remains user-owned, and is never used as agent task discovery unless the user explicitly directs it.
4. Synthesize host-managed journal playbooks/templates so completed work is logged automatically with what changed, why, next direction, and follow-up.
5. Validate the host with the deleted-path inventory, plan-index check, and `git diff --check`; record results and rollback sources in the synthesis report.

The migration does not authorize agents to overwrite an existing user-owned `TODO.md`, or to commit/push without the normal approval required by host policy.

## Downstream Compatibility Maintenance (README Contract)

This README is a downstream integration contract and must be updated whenever upstream changes alter:
- bootstrap instructions,
- host vs submodule ownership rules,
- synthesis merge workflow,
- migration requirements,
- verification commands.

When breaking changes are unavoidable, README updates must include:
- explicit impact summary,
- required migration steps,
- verification steps,
- rollback notes.

## Plan Governance Model

- Execution authority comes from an approved active plan file, not from a playbook alone.
- Agents execute only approved atomic checklist items in the active plan.
- Divergence requires a proposed plan revision and user approval before continuing.
- Canonical plan lifecycle workflow: `./playbooks/how_to_create_and_maintain_task_execution_plans.md`.

### Plan Lifecycle Semantics

- `plans/future/`: queued work.
- `plans/current/`: active execution plans only.
- `plans/past/`: archived plans with no planned follow-up.
- `plans/current/` may be empty when no plan is active.
- Promote `future -> current` immediately before first non-trivial implementation edit.
- Archive `current -> past` when no further execution is planned.

### Plan File Standard

- Filename: `YYYY-MM-DD-HH-mm-ss_slug.md`.
- Required front matter: `plan_id`, `title`, `summary`, `status`, `created_at`.
- `plan_id` must match filename stem.
- Required key line:
  - Key: `[ ]` pending task, `[x]` completed task, `[?]` needs validation, `[-]` closed task
- `[-]` means intentionally closed/de-scoped, not completed implementation.

### Plan Indexing

- Regenerate indexes after plan create/update/move/archive.
- Ordering:
  - `future/current` by filesystem last-write time,
  - `past` by `created_at`.

## Key Paths

- Framework policy: `RULES.md`
- Playbooks: `playbooks/`
- References: `references/`
- Templates: `templates/`
- Scripts: `scripts/`
- Plans: `plans/future|current|past`

## Runtime Notes

Plan index command in this repository:
- `python scripts/regenerate_plan_indexes.py`

Host/submodule mode command from host root:
- `python agents/scripts/regenerate_plan_indexes.py --repo-root .`

## Known Opportunities

- Canonical backlog location: `plans/future/index.md`
- Traceability map: `docs/plan_migration_traceability.md`

