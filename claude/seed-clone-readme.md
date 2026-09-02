# claude-project-harness-seed

A lossless snapshot of the harness repository tiavelum/claude-project-harness,
for Andi and for the Claude session that has to recreate the harness when it
is gone. This repository is generated from the harness; nothing in it is
edited by hand.

## What it is for

It solves one problem: the harness must survive the deletion of its own
repository. The seed clone holds every harness file at a known commit, every
issue (title, body, state), and the procedure to plant them into a fresh
repository, so that deleting the harness and recreating it is a round trip
without loss. It is also the harness's second copy (backup).

It is not a place to read harness knowledge (read the harness), not a place
to track work (issues live on the harness), and not a place to change
anything: the harness regenerates it, and edits here are overwritten. It does
not carry git history or issue comments; those live only in the harness.

## Getting started

### Prerequisites

- A Claude session with the GitHub connector granted to this repository and
  to the (new) harness repository, or a checkout with Claude Code and gh.
- The harness repository tiavelum/claude-project-harness absent, or freshly
  created and empty apart from an initial README. Planting into a repository
  that has content is a restore, not a planting; do not do it.

### Plant

In a Claude project or chat with the connector, say:

```
plant the seed clone from tiavelum/claude-project-harness-seed
```

The session then follows the planting procedure below, step by step, asking
you to confirm each manual step.

### First run

To inspect the snapshot without planting:

```bash
git clone https://github.com/tiavelum/claude-project-harness-seed.git
cd claude-project-harness-seed
ls snapshot
```

Expected output:

```
CLAUDE.md  README.md  claude  deviations.md  docs  seeds
```

## Example

Andi, in a chat: "plant the seed clone from
tiavelum/claude-project-harness-seed". The session reads
snapshot-manifest.json, reports "snapshot of claude-project-harness at the
commit named in the manifest, generated 2026-09-02, 21 files, 16 issues", and
asks: "First manual step: create a private repository
tiavelum/claude-project-harness on GitHub, initialized with a README, and
confirm here." After confirmation it pushes the 21 files in one commit,
recreates the 16 issues in number order, verifies every blob SHA against the
manifest, and asks for the next manual step: the Claude project and its
Instructions field.

## Content and structure

| Path | Contains |
|---|---|
| README.md | This file: what the seed is and how to plant it (generated from the harness master claude/seed-clone-readme.md) |
| CLAUDE.md | Claude Code entry point; imports this README |
| snapshot/ | The harness repository tree, verbatim, at the commit named in the manifest |
| snapshot-issues.json | Every harness issue: number, title, state, state_reason, labels, body |
| snapshot-manifest.json | Source commit, generation date, and path plus blob SHA of every snapshot file |
| .gitignore, .editorconfig, .gitattributes | Stack hygiene (RL-3, RL-5) |

Start here, then snapshot-manifest.json. snapshot-issues.json is a transport
payload describing the harness at generation time, not a work list of this
repository.

## Planting procedure

Owned by the harness (claude/seed-clone-readme.md); copied here so the seed
is self-sufficient when the harness is gone.

1. Read snapshot-manifest.json and report source commit, generation date,
   file count and issue count. If the harness repository exists and is not
   empty, stop: planting is only into an absent or empty harness.
2. Manual: Andi creates the private repository tiavelum/claude-project-harness
   on GitHub, initialized with a README. Wait for confirmation.
3. Push every file under snapshot/ to the root of the new repository, in one
   commit on main with the message
   `chore: plant seed clone of <source commit> generated <date>`.
   The snapshot's own README.md replaces the initial one.
4. Recreate the issues from snapshot-issues.json in ascending number order,
   every issue including closed ones, each with its title, body and labels;
   close the ones whose state is closed with their state_reason. On a fresh
   repository the numbers come out identical, which keeps cross-references
   like #3 valid. If a number differs, stop and report it before continuing.
5. Verify: fetch each file of the new repository and compare its blob SHA
   with the manifest; every entry must match. Report the harness commit SHA.
6. Manual: Andi creates the Claude project claude-project-harness, grants the
   connector to the new repository, and pastes the Instructions field from
   claude/project-instructions.md (everything below its COPY marker). One
   step at a time, wait for confirmation.
7. Birth check: in the new project, a fresh session reads README.md and runs
   one operation from docs/operations.md without further help.

## Mental model

The harness is the organism; this repository is its frozen copy. Generating
the clone is a harness operation (docs/operations.md in the snapshot, "Generate
a seed clone") that overwrites this repository from the harness at HEAD.
Planting is the reverse. Neither direction is ever merged: the harness is the
only place where content changes.

## Troubleshooting

**Issue numbers differ after step 4.** The harness repository was not fresh
(it had issues or pull requests before planting). Delete the repository and
plant again into a fresh one.

**A blob SHA does not match in step 5.** The push was partial or a file was
altered by line-ending conversion. Re-push the file from snapshot/ and verify
again.

**The manifest names a commit that no longer exists.** Expected after the
harness was deleted; the commit SHA is informational. After planting, the new
harness starts its own history.

## Contributing

Nothing is changed here. Change the harness, then run "generate a seed
clone" from the harness project chat; that overwrites this repository.
