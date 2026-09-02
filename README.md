# claude-project-harness

The central mechanism for setting up and running Claude-supported, git-backed
knowledge projects, for Andi and for the Claude sessions working in the
paired Claude project. This README is the hub: it is the only file that knows
the full inventory, and every session starts here.

## What it is for

It solves one problem: knowledge projects run with Claude lose their know-how
to ended sessions, drifting copies and undocumented wiring. The harness
develops the general structure, rules and recipes centrally, applies them to
itself first, and hands them to member projects, which feed learnings back.
It does not hold any member's domain content, and it does not restate the
general engineering norms in tiavelum/engineering-standards: those own every
rule about a repository as a repository, and the harness adds only what
exists because a Claude session is involved (decision 0005).

## Getting started

### Prerequisites

- For sessions: the Claude project "claude-project-harness" with the GitHub
  connector granted to this repo and to tiavelum/claude-project-harness-seed.
- For humans: git >= 2.30 and read access to tiavelum/claude-project-harness.

### First run

```bash
git clone https://github.com/tiavelum/claude-project-harness.git
cd claude-project-harness
ls docs
```

Expected output:

```
decisions  design.md  harness-bootstrap.md  members.md  operations.md  platform.md
```

A session needs no clone: it fetches this README through the connector and
follows the table below.

## Example

Andi, in the harness project chat: "add a member for my recipe collection".
The session fetches this README, opens docs/operations.md, and answers: "I
will register it in the registry and set up the structure. First manual step:
create a private repo named recipe-collection on GitHub with a README, and
confirm here." It then builds the member structure, guides each manual step,
and appends the member to docs/members.md.

## Content and structure

| Path | Contains |
|---|---|
| CLAUDE.md | Claude Code entry point; imports the instructions master |
| claude/project-instructions.md | Master for the Claude project's Instructions field (COPY marker) |
| claude/seed-clone-readme.md | Master for the seed repository's README, including the planting procedure |
| claude/seed-clone-claude.md | Master for the seed repository's CLAUDE.md |
| deviations.md | Recorded, owner-approved deviations from the engineering standards (PR-5) |
| docs/design.md | The Claude layer of the mental model: slots, masters, drift, Claude-specific checks |
| docs/platform.md | Platform facts, automation boundary, surface matrix |
| docs/operations.md | Procedures: add a member, receive feedback, update the bootstrap, generate and plant a seed clone |
| docs/harness-bootstrap.md | Living self-description; how the arrangement is recreated |
| docs/members.md | Member registry, the only place naming members |
| docs/decisions/ | Immutable decision records (DOC-10), numbered from 0001 |
| seeds/ | Archived founding seed and later source material (history, not reference) |
| .gitignore, .editorconfig | Stack hygiene (RL-3, RL-5) |

Start here, then docs/design.md. Open work lives in this repo's GitHub
issues, never in files (decision 0002). The lossless snapshot of this repo
lives in tiavelum/claude-project-harness-seed (decision 0006). Known
limitation: the install mechanism, template repo, enforcement script, sprout
seed and member feedback shape are open issues, not built;
docs/operations.md says what works today.

## Mental model

One durable surface (this repo), four slots through which text reaches a
session, one master per deployed copy, a regenerated seed clone as the second
copy, and the engineering standards underneath everything. The Claude layer:
[docs/design.md](docs/design.md).

## Contributing

Raise anything as a GitHub issue on this repo, or say it in the harness
project chat; sessions file issues and commit changes directly to main
(deviations.md).
