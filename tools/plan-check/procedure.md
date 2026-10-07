# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

### What to read first

1. Read the entire package bundle supplied for this item before grading
   any check. Treat the bundle as the only available evidence; do not
   fetch files, open links, or infer facts that are not present in it.
2. Read the issue or task context first and record the requested outcome,
   constraints, affected area, and any maintainer or contributor
   requirements.
3. Read the reproduced-evidence block next and record the observed
   behavior, reproduction steps, expected behavior, actual behavior, and
   any artifacts or logs it names. Use this as the behavioral baseline,
   not the candidate plan's explanation.
4. Read the repo-facts block and record relevant conventions, files,
   available commands, contribution policy, and AI-use disclosure
   requirements.
5. Read the candidate plan's diagnosis and scope, then its implementation
   steps and test plan. Compare every claim against the context,
   reproduced evidence, and repo facts already recorded.
6. Read the candidate plan's comment or communication section last and
   record whether it responds to thread guidance and follows the stated
   repository conventions.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

### How to gather the evidence

1. For diagnosis and grounding checks, locate the plan's stated cause
   and the reproduced-evidence steps or artifacts that support it.
   Record the exact behavior the evidence demonstrates and whether the
   proposed cause explains that behavior without contradicting it.
2. For scope checks, locate the plan's in-scope and out-of-scope
   statements, named files or areas, and stated boundaries. Record the
   smallest concrete change the plan commits to and any unrelated work
   it includes.
3. For executability checks, locate each implementation step and the
   files, symbols, commands, or ordering it names. Record any missing
   decision or dependency that would force a stranger to ask the author
   what to do next.
4. For test-plan checks, locate the proposed validation commands,
   assertions, expected results, and links to the reproduced behavior.
   Record which test or observable artifact proves the fix and whether
   the plan covers regression risk.
5. For honesty checks, locate stated unknowns, risks, assumptions,
   fallback plans, and any conditions for revising the approach. Record
   whether uncertainty is explicitly bounded or presented as settled
   fact without evidence.
6. For communication checks, compare the plan comment with the issue
   context, thread highlights, repo-facts conventions, contribution
   policy, and AI-use disclosure requirements. Record each request the
   comment addresses and each relevant request it ignores.
7. If a rubric check names an evidence family that is absent from the
   bundle, record the evidence as unavailable and grade that check
   `unclear`; do not substitute general impressions or outside knowledge.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

### How to grade each check

1. Read the check's Evidence and Pass condition columns before judging
   it. Grade only the outcome described by that check, not the plan's
   formatting, length, or use of headings.
2. Use the evidence gathered for that check and compare it directly with
   the pass condition. Do not award credit because another check passed.
3. Mark the check `pass` only when the evidence satisfies the complete
   pass condition.
4. Mark the check `fail` when the evidence contradicts the pass
   condition, shows a missing required outcome, or shows that the plan
   would not meet the condition.
5. Mark the check `unclear` only when the required evidence is genuinely
   absent or cannot distinguish pass from fail. Do not use `unclear` to
   avoid deciding a condition that the bundle makes observable.
6. Record a short justification that names the decisive evidence and
   explains the comparison to the pass condition. Quote or paraphrase
   only material present in the bundle.
7. Grade every rubric row exactly once, including preferred checks, and
   preserve the check names and grades for verdict assembly.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

### How to reach the verdict

1. Confirm that every rubric row has exactly one recorded grade:
   `pass`, `fail`, or `unclear`, with a justification.
2. Apply the rubric's Verdict rule literally. Do not invent a threshold,
   override a required check, or let a preferred check change the result
   unless the rule explicitly says so.
3. Treat `unclear` exactly as the Verdict rule specifies. If the rule
   does not specify how to treat `unclear`, treat it as a failure.
4. Return `accept` only when the rubric's conditions for acceptance are
   satisfied; otherwise return `reject`.
5. Identify every failed or unclear required check in the result. If
   preferred checks fail, identify them separately without treating them
   as verdict-determining unless the rule says they are.
6. State the final verdict and cite the decisive evidence from the
   bundle, including the check name and the relevant observed behavior,
   scope boundary, execution gap, test result, uncertainty, or
   communication requirement.
