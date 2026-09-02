# 0003: decision rationale lives in decision records

Date: 2026-09-01. Status: accepted.

## Context

The seed left open where decision rationale lives: a ledger file in the repo
versus commit messages plus a journal line. The engineering standards already
prescribe decision records (DOC-10 to DOC-12: docs/decisions/, numbered,
immutable, superseded rather than edited). A harness-wide arbitration of
member conventions against that standard is still open work (see the issue on
convention choices).

## Decision

The harness follows DOC-10 to DOC-12 from birth: a decision that constrains
future work and is not obvious from the artifacts gets a numbered record in
docs/decisions/, containing context, decision, alternatives and consequences.
Commit messages still carry the what and the immediate why of each change
(GW-8).

## Alternatives considered

Commit messages plus a one-line journal entry only. Not chosen for the
harness because settled questions would be relitigated; kept on the table for
the member-level arbitration, which this record does not preempt.

## Consequences

Records are append-only and immutable once accepted. If the arbitration later
chooses a different member convention, a superseding record says so here.
