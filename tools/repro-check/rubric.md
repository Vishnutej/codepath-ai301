# Rubric: is this reproduction package ready to post?

Every check reads the thing itself against the issue: the artifacts
against the issue's described behavior, the environment against the
issue's target, the words against the repo's stated policy. None of
them reads formatting, length, or headings. A terse report with the
right artifact passes; a long, confident, well-formatted one with the
wrong artifact fails. Where a check says "the issue", read the issue
body together with its thread highlights: an owner or member comment
that narrows the trigger or the target is part of the issue.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `env-recorded` | The repro report's environment record, read against the issue's own environment line and any factor the issue or thread says changes the failure (see evidence guide, Environment) | The report names the version of the software it ran and the OS/platform it ran on, **and** every factor the issue or thread marks as changing the behavior (driver, build profile, shell, browser language, release vs. debug build). A report with no environment record at all fails, even when its artifact looks right: a stranger cannot place the attempt. | required |
| `steps-rerunnable` | The repro report's commands, inputs, and setup, read as a stranger with only public resources would (see evidence guide, Steps) | A stranger could re-run the attempt from a starting state to the trigger: the exact commands and inputs are shown, or are unambiguously the issue's own ("ran the issue's script verbatim"). Fails when any step depends on something the stranger cannot get (a private repo, an unshared config, "our internal setup"), or when a step the issue names as part of the trigger is left out (the driver on a driver-specific issue, the flag the owner says is required). | required |
| `target-faithful` | The report's command, input, and environment, compared token by token with the issue's trigger and target, plus the thread's notes on what is required (see evidence guide, Environment and Steps) | The report ran the issue's trigger (the same command, input, syntax, and flags, or a reduction that keeps every element the issue or thread names as required) on the version the issue targets or a newer one, and every difference from the issue's environment that the issue or thread says matters is named in the report. Fails when the command or input was changed in a way that changes the trigger (a swapped operator, a different range syntax, a renamed variable, a dropped required flag) without saying so; when the version tested is older than the one the issue confirms the bug on and the report does not say so; or when the report tested a build or platform the thread says does not reproduce and generalizes the bug to it. | required |
| `behavior-shown` | The report's artifacts (output excerpts, logs, printed state, measured results) read against the actual behavior the issue describes (see evidence guide, Behavior shown) | An artifact shows the issue's specific failure: the same panic, error message, or exit code, the same wrong output, or the same observable state. For a cannot-reproduce report, it passes when the artifact shows the real result of running the issue's trigger and the report calls it a non-reproduction. Fails when there is no artifact (prose only), when the artifact only shows that the tool runs or the setup exists (a version banner, a session list), or when it shows a different failure: a graceful validation or syntax error where the issue has a panic, a compile error where the issue has a runtime path error, garbled output with the process still alive where the issue has a crash. | required |
| `outcome-honest` | Every assertion in the repro report (summary, expected/actual, conclusion) and in the claim comment, set next to what the artifacts actually show (see evidence guide, Honesty) | Each claim of fact ("reproduced", "confirmed on X", "the cause is Y") is backed by an artifact in the report or is plainly framed as a hypothesis, and the report's expected/actual agrees with the issue's. A cannot-reproduce passes when it says so plainly, shows what was tried, and names what differed from the report's conditions. Fails only when a claim changes what the evidence means: "crash confirmed" over an artifact that shows no crash, a root cause stated as verified with nothing shown, "not limited to X" when the only run was on a build the thread says does not reproduce, or expected/actual stated backwards from the issue. Repetition counts ("ran it 5 times") attached to a shown run are not a fail on their own. | required |
| `claim-specific` | The claim comment, read against the issue and its thread (see evidence guide, Comms) | The claim comment (a) refers to something only this issue has (the specific symptom, version, code location, or a pointer from the thread), (b) states a next step the claimant can actually take (what they will read, test, or report back), and (c) promises nothing it cannot back. Fails for a +1 or me-too with no intent; for interchangeable boilerplate that could be pasted onto any issue; for a guaranteed delivery date; for demanding to be assigned or to have the issue reserved, or self-assigning; or for claiming understanding or results the repro report does not show ("I understand the compiler internals", "tracked down the root cause"). "I'd like to take this" is a claim, not a demand, and passes. | required |
| `ai-disclosure` | The contribution-policy line in repo facts (live: the repo's CONTRIBUTING / AI policy files), then the claim comment and repro report (see evidence guide, Comms) | Treat the package as AI-assisted work (every course package is). If the stated policy requires disclosing AI use in issues or comments (for example "all AI usage in any form must be disclosed"), the claim comment or repro report contains that disclosure, including the tool and the extent when the policy asks for them. Passes when the policy has no disclosure requirement, when it is silent, when it asks for disclosure only in pull requests, or when it asks for comments to be in the contributor's own words (that is a voice rule, read by `claim-specific`, not a disclosure rule). | required |
| `control-run` | The repro report's artifacts | The report includes a contrast run that isolates the trigger: the same command without the triggering element (a different character, one flag dropped, English-first instead of Japanese-first), with its output shown. | preferred |
| `template-asks-covered` | The bug-reports line in repo facts (live: the repo's issue template), against the repro report | Every item the repo's bug template asks for (version, OS, install method, config, command, expected, actual) is present in the report or visibly not applicable. | preferred |

## Verdict rule

Accept if every required check passes; otherwise reject. Preferred
checks are reported but never change the verdict.

`unclear` on a required check counts as a fail: proof I cannot verify
is proof that is not ready to post. The one exception is a claim-only
draft in live mode: `env-recorded`, `steps-rerunnable`,
`target-faithful`, `behavior-shown`, `outcome-honest`, `control-run`,
and `template-asks-covered` read the repro report, so they are graded
`unclear` with evidence `not yet applicable: claim-only draft` and
left out of the verdict. The claim-only verdict is decided by
`claim-specific` and `ai-disclosure` alone.

An honest, evidenced cannot-reproduce is an accept when every required
check passes: it is proof of an attempt, stated truthfully.

<!--
Revisions from the in-class calibration worksheet (calib-01..04):

- calib-01 (lazygit, terse but complete): my first draft had a check
  that read the report's completeness by its sections. It held a
  report that was rough but had everything a stranger needs. Every
  check now reads the proof, not the shape: "looks rough, is fine".
- calib-03 (yq, operator swap): my first draft's behavior check
  accepted "an error in the same area as the issue". The trap package
  used `:` instead of `=` and got a graceful HCL syntax error, not the
  panic. `target-faithful` now compares the command and input token by
  token with the issue's, and `behavior-shown` names "graceful
  validation or syntax error where the issue has a panic" as a fail.
- calib-04 (hyperfine, no environment record): my first draft let a
  right-looking artifact carry the whole package. The issue says the
  build profile changes the failure mode, and the report records no
  environment at all, so nobody can place the attempt.
  `env-recorded` now fails a missing environment record outright,
  and names issue-marked factors (like build profile) as required.
- calib-02 (joplin, emphatic me-too): held by `behavior-shown` (no
  artifact) and `outcome-honest` (a cause asserted with nothing
  shown); no change needed.
-->
