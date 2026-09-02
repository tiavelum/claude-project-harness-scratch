# 0006: the seed is a regenerated lossless clone of the harness

Date: 2026-09-02. Status: accepted.

## Context

The founding capsule was a hand-written seed, planted exactly once and then
retired; its own rule said any later system is created from the living
bootstrap, never from the capsule. That leaves two gaps Andi named on
2026-09-02: the harness cannot be recreated losslessly if its repository is
deleted (decision records and issues would be reconstructed approximately at
best), and a seed that is never regenerated is stale from the day the
harness moves on. The harness must be recreatable from a seed at any time,
and the seed must be recreatable from the harness at any time, both from the
newest content.

## Decision

1. The seed is a lossless snapshot of the harness: every file at a named
   commit, every issue (title, body, state, labels), plus a manifest and the
   planting procedure. It lives in one fixed repository,
   tiavelum/claude-project-harness-seed, which is overwritten by every
   generation and may be deleted and recreated at will.
2. Two harness operations exist, wired into the always-present slot:
   "generate a seed clone" (harness to seed) and "plant a seed clone" (seed
   to an absent or empty harness). Both are session-driven through the
   GitHub connector; repository creation and deletion stay manual.
3. The seed repository's README and CLAUDE.md are deployed copies of masters
   held in the harness (claude/seed-clone-readme.md,
   claude/seed-clone-claude.md), so the seed is self-sufficient when the
   harness is gone without a second hand-edited owner.
4. The seed carries no git history and no issue comments. The harness git
   log is the only history; a mirror clone is the complementary backup for
   it (#15).
5. A second, lighter artifact, the sprout seed (DNA only, generated from the
   bootstrap and living docs, approximate on replant), is a separate
   operation with its own issue and does not replace the clone.

## Alternatives considered

Maintaining the founding seed by hand: rejected, a second hand-edited copy
of the harness drifts by construction (DOC-3).

Generating a distilled seed only: rejected as the primary mechanism, because
it cannot reproduce decision records and issues verbatim; kept as the
sprout seed for handing the pattern elsewhere.

Dated seed repositories per generation: rejected, they accumulate and the
harness git log already holds the history.

A GitHub Actions workflow: rejected for now, it needs a PAT secret and cannot
perform the reverse direction; the connector route works from any surface.

## Consequences

The "planted exactly once" retirement rule of the founding capsule is
superseded: its repository becomes the seed clone target and is overwritten.
The archived founding seed stays in seeds/ as history. The instructions
master names two more operations, so the Instructions field must be
re-pasted. docs/harness-bootstrap.md now recreates the arrangement by
planting a clone. Issue #8 is narrowed to the clone; the sprout seed gets
its own issue. The seed's snapshot-issues.json is a transport payload, not an
open-work file in the sense of DOC-22.
