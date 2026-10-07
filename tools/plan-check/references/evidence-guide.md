# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

In an eval package, read the `## Repro evidence` block first, including
its environment, numbered steps, expected result, and actual result.
Then read the `Cause` and `Change` statements in `## Candidate plan`
and compare them with the `## Issue` description. In live mode, use the
student's posted reproduction comment on the issue and the diagnosis
and proposed change in the draft plan. Good evidence identifies a
specific cause that explains the observed failure and proposes a change
that addresses that cause; it does not contradict the reproduction or
merely hide the visible symptom.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

In an eval package, read the `Change` statement in `## Candidate plan`,
especially its `In` and `Out` boundaries, and compare them with the
requested outcome in `## Issue` and the relevant files or areas in
`## Repo facts`. In live mode, inspect the draft plan's scope and named
files against the issue request and repository documentation. Good
evidence shows one finite change tied to the issue, with unrelated
cleanup, refactors, and feature work explicitly excluded or absent.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

In an eval package, read the implementation details in `## Candidate
plan` and check their file paths, symbols, callbacks, commands, and
dependencies against `## Repo facts`. In live mode, read the draft
plan's implementation steps and the repository files or docs it cites.
Good evidence lets a stranger identify where to start, what to change,
and the order or dependency that matters, without needing an unstated
decision from the plan author.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

In an eval package, read the `Test` statement in `## Candidate plan` and
compare its commands, scenarios, expected results, and regression
coverage with the numbered steps and artifacts in `## Repro evidence`.
Use `## Repo facts` to check whether named test commands or tools are
available. In live mode, inspect the draft plan's validation steps and
the student's reproduction evidence. Good evidence specifies an
observable corrected outcome for the original failure and a meaningful
regression check; "run tests" without an expected result is not enough.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

In an eval package, inspect the diagnosis, scope, implementation, and
test statements in `## Candidate plan` for assumptions, risks,
unknowns, fallback investigation, and recorded deviations, and compare
claims with `## Issue`, `## Repro evidence`, and `## Repo facts`. In live
mode, inspect the draft plan and any deviation note added after a build
changed course. Good evidence distinguishes observed facts from
hypotheses, names unresolved questions with a way to answer them, and
records a deviation with its reason and impact instead of silently
changing the plan.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

In an eval package, read `## Candidate plan comment` against `## Thread
highlights`, `## Repo facts`, and the issue request. Check the repo's
bug-report or contribution template, review-bandwidth guidance,
required fields, and AI-use disclosure requirement when present. In
live mode, read the draft comment against the live issue thread and
repository docs or templates. Good evidence shows that the comment
accurately summarizes the plan, responds to relevant maintainer signals,
states the needed validation, and follows the repository's communication
and disclosure rules rather than using generic boilerplate.
