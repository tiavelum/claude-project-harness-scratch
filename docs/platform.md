# Platform facts and the automation boundary

This document covers what the Claude platform can and cannot do for
harness-governed projects, for anyone deciding what to automate. It is owned
centrally here so members link to it and never restate it; it must be kept
current as the product changes. Facts below are observations, dated where
they were re-tested.

## What can run automatically

- Account-skill deployment: Claude edits the skill master in the repo and
  re-saves the account skill via save_skill in the same session, unasked.
- Domain builds and validation in Claude's own environment; the user runs no
  tools locally.
- Commits and pushes from connector sessions, immediately after every
  adaptation.
- A convention check script: one command, one exit code, runnable unattended
  on a schedule.
- A publish transport: sessions without credentials commit locally, a
  separate agent publishes and writes a verifiable status.
- Claude Code's native skill discovery and CLAUDE.md imports.

## What stays manual, and why

- Pasting project fields from their masters (no API writes them): the most
  repeated manual step, made rare by keeping fields pure pointers.
- Installing an account-level skill the first time.
- Creating (and renaming) a GitHub repository. Re-tested 2026-09-01: the
  connector exposes a create-repository call, but GitHub refuses it with 403
  (insufficient grant), so creation stays manual.
- Pressing Sync on a project's knowledge (pull-only, stale by default; chats
  fetch fresh from the repo anyway).
- Keeping the sensitive-data file in project knowledge and beside local
  builds; it never enters git.
- Deciding the connector grant scope (a security decision every member
  faces).

## Hard platform constraints (the surface matrix)

The most expensive knowledge a new member would otherwise re-derive, and the
most likely to change with the product. As currently observed:

| Surface | Repository access | Transcript readable later |
|---|---|---|
| plain chat | none: text only | no |
| Cowork on the computer | connected folders plus the GitHub connector | yes, by other on-computer sessions |
| Cowork in the cloud | GitHub connector only; a connected folder only via the device bridge | never, by anything |
| Claude Code | native on the machine with the user's credentials, real git push | not applicable |

- A cloud session cannot push (no credentials, no SSH route); the device
  bridge cannot unlink, so commits there leave git lock/tmp debris and some
  git commands are unusable on that mount.
- The connector: writes whole files only; guards against stale writes by
  blob SHA (a feature, it makes two independent writers survivable); pushes
  text only, no binaries; cannot create repositories (see above).
- Repo-hosted steering (CLAUDE.md, .claude/skills) activates ONLY in
  checkouts; connector surfaces see only account skills and project fields,
  hence the deployed copies. Claude Code supports @path imports in CLAUDE.md,
  letting one master text feed both the pasted field and the checkout.
- Local session output files do not survive the session; a new session
  starts cold; project fields are injected live every turn but can never be
  read programmatically (which is what makes field drift undetectable by
  tooling).

## The two-writer boundary

Two independent writers exist: sessions writing through a connected clone and
sessions writing through the connector API. That is the root of divergence
and conflicts; the SHA guard is what makes it survivable. Whether to keep
both routes is a per-member decision.
