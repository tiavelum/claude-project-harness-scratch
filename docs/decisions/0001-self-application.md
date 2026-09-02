# 0001: the harness self-applies its own pattern

Date: 2026-09-01. Status: accepted.

## Context

The harness prescribes structure, rules and recipes to member projects. A
prescription the prescriber does not follow decays into decoration, and the
founding seed makes self-application a hard requirement.

## Decision

This repository is the first example of its own description. Every rule,
structure and mechanism the harness prescribes to members is practiced here
first; whenever the harness prescribes something it does not itself practice,
that is a bug to be fixed on the harness side.

## Alternatives considered

A pure specification repository that describes the pattern without embodying
it. Rejected: it cannot detect that its prescriptions are impractical, and it
forfeits the first feedback loop (the harness eating its own dog food before
prescribing).

## Consequences

The harness repo carries the full member structure (wiring, masters, hub
README, decision records, requirement specs) from birth, and every future
harness mechanism is validated here before it reaches a member.
