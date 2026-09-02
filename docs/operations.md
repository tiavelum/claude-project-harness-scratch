# Harness operations

This document tells a session how to run the harness's user-facing
operations. The always-present wiring names them; this file carries the
steps. The mechanisms are young: where a step is not yet built, the procedure
says so and the gap is an open issue.

## Add a member

1. Ask which repo and Claude project the member pairs (one repo, exactly one
   project). For a new repo, guide Andi to create it on GitHub (manual,
   docs/platform.md) with a README so the default branch exists.
2. Apply the engineering standards (index.yaml first, cite rule ids) and the
   Claude layer this repo itself practices: CLAUDE.md importing
   claude/project-instructions.md (COPY marker master), slim hub README,
   docs/, docs/decisions/. Until the install mechanism and template repo
   exist (see issues), adapt by hand from this repo's layout, never by blind
   copy of harness-specific content.
3. Guide the manual residue one step at a time, waiting for confirmation:
   create/confirm the Claude project, paste the Instructions field from the
   member's master, decide the connector grant scope, connect a folder or
   install an account skill where wanted.
4. Register the member in docs/members.md (the only place naming members)
   and commit each step as it lands.

## Receive member feedback

1. Take the handover in whatever form it arrives (a structured shape is
   pending, see the member-feedback issue).
2. Archive the handover document verbatim under seeds/ if it is a document.
3. Triage every learning: platform facts into docs/platform.md, Claude-layer
   model changes into docs/design.md, general engineering learnings as issues
   on tiavelum/engineering-standards, rationale into a decision record,
   remaining work as GitHub issues.
4. Confirm back what was absorbed and where it now lives.

## Update the bootstrap

1. After any structural change to the harness (files, wiring, operations,
   deployed copies), reread docs/harness-bootstrap.md.
2. Bring it back to the standard: complete enough that another Claude account
   could recreate the whole arrangement from it alone, drawing only on living
   documents.
3. Commit it together with the change that invalidated it (DOC-19).

## Generate a seed clone

Overwrites tiavelum/claude-project-harness-seed with a lossless snapshot of
this repository (decision 0006). Run it after any change worth surviving the
loss of this repository; Andi may also ask for it at any time.

1. Confirm this repository has nothing unpublished (every change committed on
   main); note the HEAD commit SHA.
2. If the seed repository does not exist, guide Andi to create it (private,
   named claude-project-harness-seed, initialized with a README); wait for
   confirmation.
3. Read every file of this repository at HEAD (walk the tree, every path,
   dotfiles included) and record each path with its blob SHA and size.
4. Export every issue of this repository, open and closed, as
   snapshot-issues.json: an array ordered by number with number, title,
   state, state_reason, labels (names) and body.
5. Write snapshot-manifest.json: source repository, source commit, generation
   date, file count, issue count, and the path plus blob SHA of every file.
6. Push to the seed repository's main in one commit: every file under
   snapshot/<path> verbatim, snapshot-issues.json, snapshot-manifest.json,
   README.md from claude/seed-clone-readme.md verbatim, CLAUDE.md from
   claude/seed-clone-claude.md verbatim, and .gitignore, .editorconfig,
   .gitattributes copied from this repository. Message:
   `chore: generate seed clone of <source commit>`.
7. Delete from the seed repository any snapshot/ file that is not in the
   manifest (files removed from the harness since the last generation).
8. Verify: list the seed repository's snapshot/ tree and compare every blob
   SHA with the manifest; every entry must match and no extra file may
   remain. Report the seed commit SHA. A local commit is not a published one.

## Plant a seed clone

Recreates this repository from the seed into an absent or empty harness
repository. The procedure is owned by claude/seed-clone-readme.md, which is
the seed repository's README, so that the seed is self-sufficient when this
repository is gone; follow it from there. Do not plant into a repository that
has content.

## Standing duties in every session

- Compare the injected Instructions field against
  claude/project-instructions.md when suspicious; report drift and offer the
  paste.
- Commit while working, verify publication before reporting it.
- File an issue the moment an open item is identified.
- Never restate an engineering-standards rule in a harness document; cite
  its id. Never record a deviation without Andi's approval in chat
  (decision 0005).
- Never commit to a member repository outside the add-a-member reception;
  member domain work belongs in the member's own project chat (decision
  0004).
- Offer "generate a seed clone" after a session that changed decision
  records, wiring or operations, so the seed never lags a structural change.
