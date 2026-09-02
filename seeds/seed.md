# The seed

**What this document is.** The founding seed for a new Claude project, working
title "claude-project-harness". Its mission: develop, centrally and
iteratively, the general mechanism for setting up and running Claude-supported
git-backed knowledge projects. This seed carries what the harness birth needs:
the mental model, the platform facts, the user's direction, the work items,
and the first assignment. It is written for a Claude session with zero prior
context, is planted exactly once, and is then done: further systems are set up
from the harness's own harness-bootstrap.md, and member input arrives through
the harness's reception route - never through another seed.

**The generative principle.** Everything the harness is and everything it
produces must be derivable from this seed at birth, and from the harness's own
living documents thereafter: the harness repo's structure, its Claude wiring,
its README, its mental-model documentation, its mechanisms, and its affiliated
artifacts (template repo, registry, bootstraps, member interaction). The seed
is DNA: at birth its content is transplanted into the organism's own living
documents, which then evolve under the standing rules; the planted seed file
itself retires into the archive. Nothing may remain that only the seed knows.

**Terminology - member projects.** Projects that inherit the structure, rules,
and recipes the harness prescribes, and that feed their learnings back to the
harness for consolidation and refinement. The set of members is open and grows
over time; the live list belongs in a member registry the harness maintains,
and member names are never hardcoded into harness mechanisms or documents.
RECEIVING members - registering a new or existing project and taking in member
feedback - is a first-class harness function, and it must be proactive: the
harness project's own always-present wiring and skills make Claude offer and
drive these operations ("add a member", "receive member feedback"), rather
than depending on the user having read the README.

**Normative dependency - engineering standards.** The repo
tiavelum/engineering-standards holds the general engineering norms for ALL
repositories, Claude-related or not: naming, repository layout, the README
contract, git workflow, documentation and decision records. It is
machine-consumable and must be consumed per its own consumer contract,
starting at index.yaml. It is a norm source, not a member - naming it here is
like naming a platform. The structure the harness prescribes LAYERS ON TOP
of these general standards and never replaces them; the harness repo itself complies
from birth, and deviations are recorded per the standards' precedence rules.
The standards repo predates the harness and is expected to later join as a
member itself, through normal reception, to receive its Claude wiring. This
block is the seed's single statement about the standards: their content is
never restated elsewhere in this seed, and wherever a practice below touches
ground the standards own - naming, layout, README, commits, documentation,
work tracking - the standards govern.

**Nothing in this seed is normative.** Sections 1 and 2 are learned
observations handed over as knowledge, not rules. A norm exists only where a
standards repository states it with an identifier and a check behind it. The
Claude-specific norm layer starts as an EMPTY repository and grows one
deliberately decided atom at a time (work item 14); until an atom lands
there, the harness follows the practices below as provisional habits, freely
revisable - never as inherited law. Implicit content must never silently
become explicit norm.

---

## 1. Core mental model

### 1.1 The transcript is not memory

A session can end without warning, and on some surfaces its transcript is
never readable again by anything. The working assumption: a session whose
conversation cannot be re-read afterwards is the normal case. So knowledge is
written into the repository WHILE the work happens, in small, individually
meaningful commits - not in a distillation step at the end, because there may
be no end.

### 1.2 The repository is the only durable surface

Knowledge lives in the repository, not in copies uploaded into a Claude
project; uploaded copies drift silently, and project memory is read-only from
a session. The mechanism must depend only on the repository's own contents:
no session identifiers, no bookmarks, nothing that requires re-reading a past
conversation.

### 1.3 Four slots: every text that reaches a session arrives through one

Text reaches a session in exactly four ways, differing in when it is loaded
and what it is for. Putting a fact in the wrong slot is the usual mistake.

| Slot | Loaded | Holds | Claude project surface | Claude Code surface |
|---|---|---|---|---|
| Always present | every turn | pointers and standing rules | the project's Instructions (and Description) fields | CLAUDE.md in the working directory |
| On task match | when a task fits its description | a repeatable procedure | account skills | .claude/skills/, and account skills |
| On demand | when slot 1 or 2 says so | the knowledge itself, one owner per fact | repo files via connector | the same files, from the checkout |
| History | when someone asks what happened | append-only record | ledgers / journal, git log | the same |

References run in one direction only, from a lighter slot to a heavier one:
slot 1 points at slot 3, slot 2 walks slot 3, slot 3 owns the facts - never
sideways between two owners, never from a repository back up to the project
using it. Slot 1 is expensive (re-read every turn, forever) and uncheckable by
tooling, so it stays a pointer and never becomes a manual.

Equivalent formulation: entry points (the slot 1 and 2 doors of each surface)
are pure pointers saying "fetch the repo's README and follow it"; the README
is the hub, the only file knowing the full inventory; references form a tree -
no cycles, no sideways links, a fact lives in exactly one place. Consequence:
entry points almost never change, so manual syncs almost never fire.

```
  project chat        any chat           Claude Code / VS Code
       |                  |                     |
  [instructions      [account skill]      [CLAUDE.md imports the
   field, pasted      auto-synced          instructions master;
   from master]       from master]         .claude/skills/ read natively]
       \__________________|______________________/
                          v
                     README.md  (the hub - lists every file)
                          v
              the member's content files and ledgers
   (sensitive data file: local + project knowledge only, never in git)
```

### 1.4 Masters and deployed copies

Everything Claude should know or obey has exactly one hand-edited master in
git. Surfaces that git cannot write (project fields) or that cannot read git
live (the account skill store) get deployed copies, and every copy needs a
sync: automatic where the platform allows (the skill store is writable by
Claude via save_skill), manual where it does not (fields are pasted by hand
from a master whose file carries a COPY marker: a note about the file, the
marker, then the field text verbatim). Drift runs in BOTH directions - master
edited but not pasted, and field edited in the app - and nothing can read a
field programmatically, so the only possible detection is a session comparing
its own injected context against the master.

### 1.5 claude/ and .claude/ are different things, deliberately

claude/ is a member's own machinery (rule, check, budgets, field masters,
installer): ordinary versioned content, liftable anywhere. .claude/ is the
folder the Claude Code tooling reserves and discovers by itself; only what
that product reads lives there. Kept apart so it stays visible which
constraint owns which file.

### 1.6 Conventions with enforcement, or no convention at all

Two laws, offered as harness laws: **a rule that cannot be checked is not
adopted**, and **when rule and behaviour disagree, the rule loses** - change
the rule or change the check, never leave a rule nothing enforces, because
that is how a convention becomes decoration. Corollaries: the instruction is
the checked artifact (one short convention file, the only copy, a script
verifies its observable consequences), and a check that cries wolf stops being
read (imprecise checks warn instead of fail).

### 1.7 One owner per fact, and four kinds of statement

Each fact has exactly one owning document; everywhere else links to it. Where
a statement belongs: *do this* (steps, order, verification) in a procedures
document; *this is how it is* (state, facts, the rule a decision left behind)
in a knowledge document; *this is why* (rationale) in the history record -
where exactly is an open convention choice, see work item 11; *this is still
missing* is an open item, tracked as the standards prescribe.

### 1.8 Documents describe the present; history is append-only

Knowledge documents are present tense and rewritten freely, carrying no
narrated history. Journals, ledgers of record, and the git log are append-only
and never edited. Never mix the two conventions in one file unlabelled.

### 1.9 Budgets are forcing functions

Line budgets, configured and enforced: a convention file has one because it
must be read in full every time; knowledge documents have one because a
document nobody finishes is a document nobody uses. When a budget is hit,
split the document, do not raise the number.

### 1.10 A mechanism and its document move together

Where a tool and its documentation live apart, a change is two commits with
nothing connecting them; something must make the gap visible while it is cheap
to fix.

### 1.11 The author commits; a separate act publishes

Committing is part of authoring, not a later step someone else performs.
Publishing is a distinct act, and a member must be able to VERIFY publication
happened before reporting it - "a local commit is not a published commit" is
the standing failure mode. The publishing mechanism is surface-dependent (see
work item 11).

### 1.12 The machinery must stay small

All of this is a component of a project, not the project: infrastructure for
the work, not the work. It is the part that grows fastest and pays back least,
and every mechanism is one more thing that can drift from its own description.
A harness is exactly the kind of thing that can violate this - a standing
design constraint.

### 1.13 The regenerate-not-copy pattern

Where a member's subject is a family of documents: documents are generated,
never copied and adapted. Layout lives once in an executable generator;
content structure lives once in a skeleton; volatile and sensitive values are
tokens resolved at build time from a gitignored data file; a build-verify loop
runs before anything is distributed. The generator is the executable reference
implementation of rules prose cannot carry precisely, committed together with
the rule text it implements.

## 2. Automation boundary

### 2.1 What can run automatically

- Account-skill deployment: Claude edits the skill master in the repo and
  re-saves the account skill via save_skill in the same session, unasked.
- Domain builds and validation in Claude's own environment; the user runs no
  tools locally.
- Commits and pushes from connector sessions, immediately after every
  adaptation.
- A convention check script: one command, one exit code, runnable unattended
  on a schedule.
- A publish transport: sessions without credentials commit locally, a separate
  agent publishes and writes a verifiable status.
- Claude Code's native skill discovery and CLAUDE.md imports.

### 2.2 What stays manual, and why

- Pasting project fields from their masters (no API writes them) - the most
  repeated manual step; made rare by keeping fields pure pointers.
- Installing an account-level skill the first time.
- Creating (and renaming) a GitHub repository - the connector cannot.
- Pressing Sync on a project's knowledge (pull-only, stale by default; chats
  fetch fresh from the repo anyway).
- Keeping the sensitive-data file in project knowledge and beside local
  builds; it never enters git.
- Deciding the connector grant scope (a security decision every member faces;
  see work items).

### 2.3 Hard platform constraints (the surface matrix)

The most expensive knowledge a new member would otherwise re-derive, and the
most likely to change with the product - the argument for the harness owning
it centrally. As currently observed:

| Surface | Repository access | Transcript readable later |
|---|---|---|
| plain chat | none: text only | no |
| Cowork on the computer | connected folders plus the GitHub connector | yes, by other on-computer sessions |
| Cowork in the cloud | GitHub connector only; a connected folder only via the device bridge | never, by anything |
| Claude Code | native on the machine with the user's credentials, real git push | not applicable |

- A cloud session cannot push (no credentials, no SSH route); the device
  bridge cannot unlink, so commits there leave git lock/tmp debris and some
  git commands are unusable on that mount.
- The connector: writes whole files only; guards against stale writes by blob
  SHA (a feature - it makes two independent writers survivable); pushes text
  only, no binaries; cannot create repositories.
- Repo-hosted steering (CLAUDE.md, .claude/skills) activates ONLY in
  checkouts; connector surfaces see only account skills and project fields -
  hence the deployed copies. Claude Code supports @path imports in CLAUDE.md,
  letting one master text feed both the pasted field and the checkout.
- Local session output files do not survive the session; a new session starts
  cold; project fields are injected live every turn but can never be read
  programmatically (which is what makes field drift undetectable by tooling).

### 2.4 The two-writer boundary

Two independent writers exist: sessions writing through a connected clone and
sessions writing through the connector API. That is the root of divergence and
conflicts; the SHA guard is what makes it survivable. Whether to keep both
routes is a per-member decision.

## 3. Direction from the user

1. The manual copy-paste processes (account skills, instructions field) are a
   pain point to reduce.
2. Graphical explanations of the setup are wanted; make such visuals standard.
3. Open work and requirements are tracked as the engineering standards
   prescribe, never in committed backlog or requirements files.
4. Standardize the communication route from member projects to the harness: a
   structured way to hand over learnings, planted as a feed into the harness
   project. An account skill producing such handover documents on request may
   be the right implementation.
5. Probably a template repo tied to the harness as well - a separate repo is
   cleaner than using the harness repo itself, which carries harness overhead.
6. A claude-account-skills repo: high-level account skills that exist only in
   the Claude account, maintained manually there, need a versioned git home
   too. Member-born skills already have their master in their member's repo,
   and their account-wide availability is desired.
7. A mechanism to maintain account skills and, if possible, auto-update them,
   generalizing the save_skill re-save pattern.

## 4. Work items for the harness

For the harness to triage into its issue tracker at birth, not a
commitment.

1. Define the harness artifacts: harness repo (development, ledgers) vs a
   clean template repo new members copy (direction note 5) vs an
   installer-lifting model - and decide where the shared machinery
   itself lives, explicitly rather than by inheritance.
2. Practice the standards' work tracking from day one (direction note 3),
   and design its recirculation into member repos as the first feedback
   loop - the harness eating its own dog food before prescribing it.
3. Build the install/upgrade mechanism. Requirements: a manifest instead of a
   hard-coded file list, a version marker so the registry can say which
   generation a member runs, an upgrade path that preserves member-local
   rules, a template set covering at minimum the README router, the CLAUDE.md
   import file, and a COPY-marker instructions master with the standing
   lines.
4. Generalize the enforcement, keeping its two laws (1.6): convention
   presence and size, history-record presence and append-only-ness, document
   budgets, commits-since-last-history-entry, uncommitted work as a note, a
   member-local extension point - plus the checks nobody has: master-vs-
   deployed-copy comparison (a session holds its injected context for free -
   the only possible detection of field drift), reference-direction checking,
   stale-pointer checking (README completeness).
5. Own the surface matrix (2.3) centrally; members link to it, never restate
   it; keep it current as the product changes; answer open platform questions
   once for all members.
6. Account-skill lifecycle (direction notes 6, 7): the claude-account-skills
   repo for account-only skills; generalize the auto-re-save sync; investigate
   whether anything stronger than session discipline is possible.
7. Standardize member-to-harness communication (direction note 4): handover
   shape, recurring feedback loop, possibly an account skill producing
   handovers on request.
8. Maintain harness-bootstrap.md as a first-class deliverable: the harness's
   living self-description sufficient to recreate the whole arrangement on any
   other Claude account, updated continuously, linked from the slim README.
   The bootstrap is a living file inside the harness repo, never a repo of its
   own; for delivery to another account the harness may GENERATE a one-shot
   capsule from it (a minimal repo whose CLAUDE.md makes it self-executing in
   a checkout - the same pattern as the founding seed capsule), which retires
   after its single use.
9. Build member reception as a first-class, proactive function: the harness
   project's instructions field and/or an account skill make Claude itself
   offer and drive the operations - add a member (new or existing project),
   receive member feedback - so discoverability never depends on the user
   reading the README first. Design member-bootstrap.md as the creation half:
   one repo maps to exactly one Claude project; the member's configuration is
   inherited from the harness; the user's manual involvement is limited to
   what only a human can do, with the session guiding those steps one at a
   time, waiting for confirmation - and the bootstrap names its manual residue
   honestly (create repo, paste fields, install account skill, decide
   connector scope, connect folder), because a bootstrap that pretends
   everything is automatable produces a half-configured member that does not
   know it. Creating a member should feel like founding the harness from this
   seed: one file, one word, guided from there.
10. Member registry: one file in the harness repo (e.g. members.md) as the
    ONLY place naming member projects - repo, paired Claude project, joined
    date, status, machinery version. Everything else refers to the registry;
    member reception registers each member there.
11. Settle two open convention choices and publish the decision to members.
    (a) Where decision rationale lives: a ledger file in the repo (trivially
    fetchable by connector sessions, prevents relitigating settled questions)
    vs commit messages plus a one-line journal entry (cannot drift from the
    change, no third record to go stale, keeps documents lean). A candidate
    synthesis: commit message always, ledger entry only for decisions that
    closed off an alternative someone might re-propose, under the same line
    budget as everything else. (b) Publishing: mandate the boundary (the
    author commits; a separate, verifiable act publishes) and leave the
    mechanism per member - direct push where sessions hold credentials, a
    transport with a status file where they do not. Also: a recommended
    default for the connector grant scope, argued once centrally; and
    triggers-on-open-issues as a member-level convention. Note for (a):
    the engineering standards already prescribe decision records (DOC-10 to
    DOC-12) - arbitration reconciles the member conventions with that
    standard rather than choosing freely.
12. Standard graphical explainer(s) of the setup per member (direction
    note 2).
13. Self-application (hard requirement, section 6 and the generative
    principle): the harness repo is the first example of its own description.
14. The Claude-specific standards module. Its character is fixed in
    advance: an EXTENSION of the engineering standards, never a sibling -
    same rule format (stable ids, machine-readable index, validator in CI,
    consumer contract), its own repository because it is its own module, and
    together with the general standards the complete rule foundation for
    Claude-specific repositories. It starts as an EMPTY repository and is
    grown with the atomic method described in the engineering-standards
    repo's open issue "Regrow the standards atomically in a new
    repository": one self-sufficient atom per commit, each deliberately
    decided against what already exists, conservative extension at every
    step, the whole tree satisfying the whole accumulated rule set at every
    commit, replay-verifiable. Contradiction with the base is structurally
    excluded: the Claude layer only specialises, and the monotonicity
    constraint runs across the repo boundary - adding the extension must
    never invalidate what the general standards guarantee. The seed's mental
    model and the members' practices are raw material to be re-examined atom
    by atom - what carries over is what was learned, never the text; nothing
    becomes a rule by having been practiced or written down elsewhere. Also
    bring the standards repo itself in as a member through normal reception,
    giving it the Claude wiring it predates.

## 5. Source material

Deeper source material - full self-descriptions of existing implementations
of this pattern, and extended argument on the convention choices of work item
11 - may be provided by the user at any time, or never: equivalent depth is
also reachable through registered members' repos. Whatever is provided is
archived in the harness repo's seeds/ folder and consulted on demand; nothing
in the birth and nothing in daily harness work depends on it.

## 6. First assignment for the session receiving this seed

Your first job is not to discuss - it is to guide Andi through setting up the
harness, applying this seed's own rules to yourselves. Concretely:

1. Walk Andi step by step through the manual parts only he can do (create the
   repo on GitHub - the connector cannot; name it, e.g. claude-project-harness;
   create/confirm the Claude project; paste the instructions field when its
   master exists). One step at a time, wait for his confirmation.
2. Do everything else yourself: set up the initial repo structure according to
   this seed. The instructions master you write must already name the
   harness's user-facing operations (add a member, receive member feedback,
   update the bootstrap) so every future session offers them proactively.
   Structure: CLAUDE.md as import of the instructions master,
   claude/project-instructions.md with COPY marker, README as slim hub/router
   with a file table, and a history record (default: decision records per
   the standards, noting the choice pends work item 11). Everything you
   create complies with the normative dependency: consume the standards per
   their consumer contract and apply them to everything you make - name,
   layout, README, commits, documents, and work tracking.
3. Transplant the seed's content into the harness's own living documents:
   the mental model (section 1) and the platform facts (section 2) become
   knowledge documents of the harness repo (for example docs/design.md and
   docs/platform.md), owned and evolved there under the standing rules. From
   this moment the living documents are the reference, and the seed is
   history - nothing may remain that only the seed knows.
4. File the work items from section 4 as issues on the harness repository,
   one per item, as the standards prescribe; from then on the issue tracker
   is the only home of open work.
5. Record in your own history record that the repo self-applies its pattern
   ("first example of its own description").
6. Create a seeds/ folder and archive this founding seed there. Any source
   documents Andi provides, now or later (section 5), join it - versioned
   where they are consumed, never required.
7. Start harness-bootstrap.md: the living self-description, complete enough
   that any other Claude account could recreate the whole arrangement from it
   alone - drawing on the living documents of step 3, never on the archived
   seed. Continuously maintained; linked from the README. (member-bootstrap.md
   is a design deliverable, work item 9, not a day-one file.)
8. Only then start the design discussions.

**Birth completeness criterion.** The founding is finished only when the
harness is a fully functional newborn: its behavior, its know-how, its rules,
its instructions, and its skills are entirely contained in its own repository
and its deployed copies - every operation the harness offers is either wired
into the always-present slot or carried by a skill, and a fresh session in the
project, given nothing but that wiring, can run any harness operation
correctly. From that moment on, the harness has nothing left to learn except
what its members teach it and what its own work produces.

The same structural and mental machinery applies at every abstraction level -
to every member repo, to the harness repo itself, and to whatever the harness
later produces. Whenever the harness prescribes something it does not itself
practice, that is a bug.
