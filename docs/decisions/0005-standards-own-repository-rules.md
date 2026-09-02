# 0005: The engineering standards own every repository rule; the harness adds only the Claude layer

Date: 2026-09-02. Status: accepted.

## Context

The founding seed carried a mental model written before the engineering
standards existed in their current form. Several of its sections restate
rules the standards now own: one owner per fact (DOC-3), documents describe
the present (DOC-6, DOC-12), no rule without a check (TL-1, TL-4, TL-11,
TL-13), mechanism and document move together (DOC-19), README as hub (RL-9,
RL-16), open work in issues (DOC-21, DOC-22), decision records (DOC-10 to
DOC-12). The seed also introduced a requirements/ directory of fourteen
"specs" that are the fourteen work items relabelled; by purpose they are an
open-work file (DOC-22) and duplicate the issues. Two seed ideas, line
budgets on documents and "the machinery must stay small", are general
engineering concerns with no home yet. None of this was recorded as a
deviation, and no deviation had been approved by the repository owner.

## Decision

1. tiavelum/engineering-standards owns everything about a repository as a
   repository. Harness documents never restate such a rule; they cite its id.
2. The harness owns only what exists because a Claude session is involved:
   slots and pointer direction, masters and deployed copies, claude/ versus
   .claude/, the surface matrix and automation boundary, transcript-is-not-
   memory, verified publication, regenerate-not-copy, member reception,
   registry, bootstraps, skills, and the Claude-specific checks.
3. A harness practice that contradicts a standards MUST rule is recorded in
   deviations.md (PR-5) only after Andi has approved it in chat; the entry
   names the approval date. Unapproved divergence is a defect.
4. requirements/ is removed. Its content is already the issue tracker.
5. Line budgets and machinery-must-stay-small are raised as proposed atoms
   on engineering-standards (or the Claude module, issue #14), not kept as
   harness prose.
6. seeds/seed.md is replaced by the seed version that was actually planted
   (the final state of the founding capsule).

## Alternatives considered

Keep restating the rules in docs/design.md for readability: rejected, a
second copy drifts (DOC-3) and hides which layer a rule belongs to.

Keep requirements/ as specifications and record a DOC-22 deviation: rejected,
the files state work items, not requirements, and the issues already hold
them with better lifecycle.

## Consequences

docs/design.md shrinks to the Claude layer and cites ids. The README file
table loses the requirements/ rows. Issue #2 (recirculate the requirements
habit) is closed as not planned and superseded by issue #4 (the enforcement
script gains a check that harness documents cite rather than restate). Any
future overlap is resolved by moving text to the standards, never by
duplicating it.
