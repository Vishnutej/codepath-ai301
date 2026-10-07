# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Evidence-grounded diagnosis | The plan's stated cause and proposed change read against the issue context and the reproduced-evidence block's observed behavior, reproduction steps, and artifacts. | The diagnosis explains the reproduced behavior and the proposed change addresses that cause rather than only masking a symptom; it does not contradict any observed evidence. | required |
| Bounded scope | The plan's scope statement, named files or areas, and explicit exclusions read against the issue request and repo-facts block. | The plan commits to one bounded change that addresses the issue, identifies the affected surface clearly enough to prevent scope creep, and excludes unrelated cleanup or feature work. | required |
| Executable implementation | The plan's implementation steps read against the repo-facts block's files, symbols, conventions, and available commands. | A stranger can begin the work without asking the author what to change next: the approach identifies the relevant code or artifacts, describes the change or the bounded investigation needed to pin the exact edit site in actionable order, and names important dependencies or decisions. | required |
| Observable validation | The plan's test plan and expected results read against the reproduced-evidence block's reproduction steps and artifacts. | The validation reproduces the original failure or behavior, demonstrates the intended corrected outcome, and includes a regression check or other observable proof appropriate to the affected surface. | required |
| Honest uncertainty | The plan's assumptions, risks, unknowns, fallback or investigation steps, and any deviation notes read against the available evidence in the package. | Claims are no more certain than the evidence supports; unresolved questions are labeled and paired with a concrete way to resolve or validate them, and any deviation is recorded with its reason and impact. | required |
| Thread- and repo-aware communication | The candidate plan comment read against issue or thread highlights, repo-facts conventions, contribution policy, and AI-use disclosure requirements. | The comment accurately summarizes the bounded plan, responds to relevant maintainer or thread requests, states the needed evidence or validation, and follows the repository's communication and disclosure requirements. | required |
| Ready-to-post coherence | The candidate plan and candidate plan comment read together against the issue context, diagnosis, scope, implementation, and test evidence. | The comment and plan describe the same change, cause, boundaries, and validation; no material contradiction, omitted blocker, or unsupported commitment would prevent posting and starting the build. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. A required check graded
`fail` or `unclear` produces `reject`. Preferred checks never change
the verdict; record their results in the output, but do not let them
override a required check.
