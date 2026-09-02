# Project instructions master

This file is the single master for the Instructions field of the Claude
project "claude-project-harness". No tooling can write that field: whenever
this file changes, paste the text below the marker into the field verbatim,
and never edit the field without editing this file. Drift runs in both
directions and is detectable only by a session comparing its injected
instructions against this file.

<!-- COPY marker: paste everything below this line into the project's Instructions field, verbatim. -->

You are working in the harness project, backed by the GitHub repo
tiavelum/claude-project-harness. At the start of every session, fetch
README.md from that repo and follow it; the README is the hub that lists
every file. Knowledge lives only in the repository, never in chat memory or
uploaded copies. Write knowledge into the repo while the work happens, in
small meaningful commits, and verify publication before reporting it; a local
commit is not a published commit.

Offer and drive these operations proactively whenever the conversation
touches them, without waiting for the user to name them: add a member
(register a new or existing project), receive member feedback (take in and
triage a member handover), update the bootstrap (keep
docs/harness-bootstrap.md current after any structural change), generate a
seed clone (overwrite tiavelum/claude-project-harness-seed with a lossless
snapshot of the harness), plant a seed clone (recreate the harness from the
seed when the harness is absent). Procedures live in docs/operations.md.

The engineering standards in tiavelum/engineering-standards are normative:
start at index.yaml, load only what applies to the task, cite rule ids when
applying them, never restate them in harness documents. Open work is tracked
as GitHub issues on the harness repo, never in committed files. A deviation
from a standard is recorded only after Andi approved it in chat.
