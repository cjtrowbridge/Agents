# Submodule Update Synthesis Report

## Scope

- Host repository:
- Submodule path: `./agents`
- Prior submodule commit:
- New submodule commit:
- Report date:

## Managed Artifact Set

- `./AGENTS.md` and other root shims
- `./playbooks/`
- `./references/`
- `./templates/`
- `./scripts/`

## Three-Way Synthesis Inputs

1. File: `[path]`
   - Old upstream source (`./agents/...` @ old commit):
   - New upstream source (`./agents/...` @ new commit):
   - Current host-managed file (`./...`):

## Proposed Merge Decisions

1. File: `[path]`
   - Host behavior to preserve:
   - Upstream changes to integrate:
   - Proposed merged output summary:
   - Risks/tradeoffs:
   - User approval status: `[pending | approved | rejected]`

## Migration / Integration Actions

1. `[Action]`
   - Trigger type: `[path change | policy/schema change | script behavior change]`
   - Files affected:
   - Verification step:

## Breaking-Change Migration Checklist

- Prior and new upstream commits recorded: `[ ]`
- Deleted upstream-path inventory captured from `git -C agents diff --diff-filter=D --name-only <old> <new>`: `[ ]`
- Matching host mirrors reviewed; retired agent-managed mirrors removed or user-data preservation proposal approved: `[ ]`
- Host `AGENTS.md` directs agents to `./agents/RULES.md` and includes the TODO explicit-direction boundary: `[ ]`
- Root `TODO.md` exists; existing user-authored content was preserved: `[ ]`
- Host-managed journal template and playbooks require automatic detailed journal updates after completed work: `[ ]`
- Stale-reference checks completed from the deleted-path inventory: `[ ]`
- `python agents/scripts/regenerate_plan_indexes.py --check --repo-root .` passed: `[ ]`
- `git diff --check` passed: `[ ]`
- Rollback sources and commands recorded: `[ ]`

## Verification Results

- `python agents/scripts/regenerate_plan_indexes.py --check --repo-root .`:
- Path consistency grep checks:
- Additional checks:

## Rollback Plan

- Submodule rollback command:
- Host file rollback source:
- Re-validation command(s):

## Final Summary

- Files synthesized:
- Files deferred:
- Remaining open decisions/questions:
