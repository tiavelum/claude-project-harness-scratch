# 0004: harness sessions do not write to member repositories

Date: 2026-09-01. Status: accepted.

## Context

The harness project's connector grant can reach member repositories. During
the first member reception (recipe-collection, 2026-09-01) the session built
the member structure through that grant and could as easily have written
domain content, for example a recipe, from the harness chat. Andi drew the
line the same day.

## Decision

A harness session commits to a member repository only during the
add-a-member reception, to build the member structure. Outside reception,
harness sessions never write to a member repo: domain content is written by
the member's own project sessions, and machinery upgrades are applied by
member sessions pulling from the harness, not pushed by harness sessions.
The registry file docs/members.md lives in the harness repo and is not
affected.

## Alternatives considered

Allowing harness sessions to write to members on request, as a convenience.
Rejected: it blurs the one-owner boundary, invites the harness chat to
become a second workspace for every member, and produces commits that bypass
the member's own wiring and conventions.

## Consequences

A harness session asked for member domain work declines and points to the
member's project chat. The install-upgrade mechanism
(requirements/install-upgrade.md) must shape its upgrade path so member
sessions apply it themselves.
