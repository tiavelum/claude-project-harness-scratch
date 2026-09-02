# 0002: open work is tracked as GitHub issues, not files

Date: 2026-09-01. Status: accepted.

## Context

The founding seed sketched a committed backlog file (open-items.md). The
normative engineering standards forbid files whose purpose is to list
outstanding work (DOC-22) and require GitHub issues instead (DOC-21). Andi
chose between the two on 2026-09-01.

## Decision

Open work on the harness lives in GitHub issues on this repository. The
requirements/ directory stays, per Andi's standing direction, but its files
are requirement specifications: contracts stating what the harness must
provide, true before and after implementation. Execution against them is
tracked by issues that reference them, closed by the work that resolves them
(DOC-25).

## Alternatives considered

A committed open-items.md with a recorded DOC-22 deviation (PR-5). Rejected:
a hand-pruned list goes stale by default, while issues close themselves with
the resolving change.

## Consequences

No backlog file may be committed. Seed work items became issues at founding;
new open items are filed as issues at the moment they are identified.
