# Design: the harness mental model

This document covers what a Claude-supported, git-backed project needs beyond
the general engineering standards, for anyone (human or session) building or
changing one. It states only what exists because a Claude session is involved.
Everything about a repository as a repository (naming, layout, README, git
workflow, documentation, open items, decision records, tooling, deviations)
is owned by tiavelum/engineering-standards and is cited here by rule id,
never restated.

## Relationship to the engineering standards

The harness layers on top of the standards and specialises them for Claude
surfaces. Where the standards speak, they govern. Where they are silent
(PR-3), this document and docs/platform.md describe the harness's provisional
habits; a habit becomes a norm only when it lands as an atom in the
Claude-specific standards module (issue #14). A harness practice that
contradicts a MUST rule is recorded in deviations.md (PR-5) only after Andi
has approved it in the harness project chat, and the entry names the
approval date.

## The transcript is not memory

A session can end without warning, and on some surfaces its transcript is
never readable again by anything. The working assumption: a session whose
conversation cannot be re-read afterwards is the normal case. So knowledge is
written into the repository WHILE the work happens, in small commits per
GW-5 and GW-10, not in a distillation step at the end, because there may be
no end.

## The repository is the only durable surface

Knowledge lives in the repository, not in copies uploaded into a Claude
project; uploaded copies drift silently, and project memory is read-only from
a session. The mechanism must depend only on the repository's own contents:
no session identifiers, no bookmarks, nothing that requires re-reading a past
conversation.

## Four slots: every text that reaches a session arrives through one

Text reaches a session in exactly four ways, differing in when it is loaded
and what it is for. Putting a fact in the wrong slot is the usual mistake.

| Slot | Loaded | Holds | Claude project surface | Claude Code surface |
|---|---|---|---|---|
| Always present | every turn | pointers and standing rules | the project's Instructions (and Description) fields | CLAUDE.md in the working directory |
| On task match | when a task fits its description | a repeatable procedure | account skills | .claude/skills/, and account skills |
| On demand | when slot 1 or 2 says so | the knowledge itself | repo files via connector | the same files, from the checkout |
| History | when someone asks what happened | append-only record | decision records (DOC-10), git log | the same |

References run in one direction only, from a lighter slot to a heavier one:
slot 1 points at slot 3, slot 2 walks slot 3, slot 3 owns the facts (DOC-3).
Never sideways between two owners, never from a repository back up to the
project using it. Slot 1 is expensive (re-read every turn, forever) and
uncheckable by tooling, so it stays a pointer and never becomes a manual.

Equivalent formulation: entry points (the slot 1 and 2 doors of each surface)
are pure pointers saying "fetch the repo's README and follow it"; the README
is the hub per the readme contract (RL-16); references form a tree with no
cycles and no sideways links. Consequence: entry points almost never change,
so manual syncs almost never fire.

```
  project chat        any chat           Claude Code / VS Code
       |                  |                     |
  [instructions      [account skill]      [CLAUDE.md imports the
   field, pasted      auto-synced          instructions master;
   from master]       from master]         .claude/skills/ read natively]
       \__________________|______________________/
                          v
                     README.md  (the hub, listing every file)
                          v
              the member's content files and records
   (sensitive data file: local + project knowledge only, never in git)
```

## Masters and deployed copies

Everything Claude should know or obey has exactly one hand-edited master in
git. Surfaces that git cannot write (project fields) or that cannot read git
live (the account skill store) get deployed copies, and every copy needs a
sync: automatic where the platform allows (the skill store is writable by
Claude via save_skill), manual where it does not (fields are pasted by hand
from a master whose file carries a COPY marker: a note about the file, the
marker, then the field text verbatim). Drift runs in BOTH directions, master
edited but not pasted, and field edited in the app; nothing can read a field
programmatically, so the only possible detection is a session comparing its
own injected context against the master.

## claude/ and .claude/ are different things, deliberately

claude/ is a member's own machinery (rule, check, budgets, field masters,
installer): ordinary versioned content, liftable anywhere. .claude/ is the
folder the Claude Code tooling reserves and discovers by itself; only what
that product reads lives there. Both are top-level directories with one role
each, stated in the README per RL-9; they are kept apart so it stays visible
which constraint owns which file.

## The author commits; a separate act publishes

Committing is part of authoring, not a later step someone else performs.
Publishing is a distinct act, and a session must VERIFY publication happened
before reporting it; "a local commit is not a published commit" is the
standing failure mode. The publishing mechanism is surface-dependent (see
docs/platform.md) and a per-member choice.

## The regenerate-not-copy pattern

Where a member's subject is a family of documents: documents are generated,
never copied and adapted (DOC-4). Layout lives once in an executable
generator; content structure lives once in a skeleton; volatile and sensitive
values are tokens resolved at build time from a gitignored data file (RL-12,
TL-18); a build-verify loop runs before anything is distributed. The
generator is the executable reference implementation of rules prose cannot
carry precisely, committed together with the rule text it implements
(DOC-19).

## Enforcement on Claude surfaces

The standards already require that what a tool can check, a tool enforces
(TL-1, TL-4, TL-11, TL-13). The harness adds the checks that only exist
because of Claude surfaces: master versus deployed copy (a session holds its
injected context for free, the only possible detection of field drift),
reference direction between slots, and stale pointers in the hub. Where a
check cannot run in CI because the surface is a chat session, it runs as a
session discipline and is named as such, never described as enforced
(TL-11).

## Scope

The same structural and mental machinery applies at every abstraction level:
to every member repo, to the harness repo itself, and to whatever the harness
later produces. Whenever the harness prescribes something it does not itself
practice, that is a bug (decision 0001).
