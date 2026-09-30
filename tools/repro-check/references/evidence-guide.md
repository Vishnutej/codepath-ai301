# Evidence guide: where proof lives in a reproduction package

This is the map for the rubric's checks. Each family says where to
look (in an eval bundle, and live on GitHub or in the student's
drafts) and what good looks like once you are there. In eval mode the
bundle is the whole world: quote it, never fetch. In live mode the
drafts are the candidate package; read them as a stranger on the
thread will, so a file the drafts do not contain or quote is not
evidence.

Read the issue first, both the body and the thread. An owner or
member comment that narrows the trigger ("`--replace` is also
required") or the target ("cannot reproduce on the Store release") is
part of what the report has to match.

## Environment

**Where it lives.**

- Eval: the repro report's environment line (usually `Environment:`
  near the top of the report, sometimes a table), compared against the
  issue section's environment line (version, OS, install method,
  build type) and the thread highlights. The repo-facts `latest
  release` line tells you what "current" meant on the capture date.
- Live: the student's repro draft for the candidate side; the issue
  body, its template fields, and the thread on GitHub (`gh issue view
  <n> --comments`) for the target side. `gh release list` gives the
  current release.

**What good looks like.** The report names the version it ran and the
OS/platform, plus every factor the issue or thread says changes the
behavior (driver, build profile, shell, browser language setting).
Where the tested environment differs from the issue's, the report
says so in a sentence ("filed against 13.0.0; unchanged on 15.2.0").
Testing a newer version than the issue's is fine when stated; testing
an older version than the one the issue confirms the bug on, without
saying so, is not. A report with no environment record at all is
unplaceable no matter how good its artifact looks, most of all when
the issue says the environment changes the failure mode (for example,
debug builds panic and release builds wrap).

## Steps

**Where it lives.**

- Eval: the repro report's steps: the shell transcript lines starting
  with `$` or `>>>`, the numbered list, the files it says it created
  (with their contents shown or said to be the issue's verbatim). Set
  them beside the issue's own "steps to reproduce" and the thread's
  notes on what the trigger needs.
- Live: the student's repro draft; the issue body's steps on GitHub.

**What good looks like.** A stranger with only public resources could
go from a starting state to the trigger: every command and input is
shown or is unambiguously the issue's own. Compare the command and
input to the issue's token by token: the same operator, the same
range syntax, the same variable names, the same required flags. A
reduction is fine when it keeps every element the issue names as
required (a minimal `env.yml` with the offending section; `--offline`
to print the request without sending). Steps fail when they lean on
something the stranger cannot get (a private monorepo, an unshared
config), or silently drop part of the trigger (no driver on a
driver-specific issue). Count none of it by length: four clear steps
beat twelve vague ones.

## Behavior shown

**Where it lives.**

- Eval: the fenced output blocks in the repro report (terminal
  output, log excerpts, printed CSS/JSON, `git status` state, console
  messages), read against the issue's "actual behavior": its error
  text, panic message, exit code, wrong output, or described state.
  A "screenshot I took" that is only described in prose is not an
  artifact in a bundle.
- Live: the output blocks the student pasted into the repro draft,
  against the issue body's actual-behavior section and any output the
  reporter or maintainers pasted in the thread.

**What good looks like.** The artifact carries the issue's failure
signature: the same panic or error message, the same exit code, the
same wrong output, the same observable state. Watch for adjacent
failures that only look related: a graceful argument-validation error
(exit 1) where the issue has a panic (exit 101); a compile error where
the issue has a runtime `Invalid path expression`; an HCL syntax error
where the issue has `panic: not a string`; garbled escape sequences
with the window still open where the issue has a crash; a version
banner and session list where the issue has a blank pane. None of
those show the bug. A control run (the same command with the trigger
removed, output shown) is strong supporting evidence when present.

For a cannot-reproduce, good looks like an artifact of the actual
attempt on the issue's trigger (the marker order, the rendered prompt)
that shows the bug did not appear.

## Honesty

**Where it lives.**

- Eval: the sentences around the artifacts in the repro report: any
  summary or conclusion, the "Expected:" and "Actual:" lines, and
  claims in the claim comment ("I have reproduced", "I understand",
  "tracked down the root cause"). Hold each one against the artifact
  it rests on.
- Live: the same sentences in the student's drafts.

**What good looks like.** Every claim of fact points at something
shown: "matches the issue" sits next to an artifact that matches; a
cause is either shown (a trace, a control run that isolates it) or
labeled as a guess ("suggests", "looks plausible"). Expected and
actual agree with the issue's, not reversed. An honest
cannot-reproduce says so in its first lines, shows what was run, names
what differed from the report's conditions (OS, shell, argument
lengths, `ARG_MAX`), and says what a triggering setup likely needs.
The warning signs: certainty words ("100%", "conclusively",
"guaranteed reproducible", "I verified this race condition") with no
artifact under them; "confirms the reported crash" over an artifact
that shows something else; widening the bug to an environment the
thread says does not reproduce.

## Comms

**Where it lives.**

- Eval: the candidate claim comment, read against the issue and
  thread; the repo-facts `contribution policy` line (for any AI-use
  disclosure rule and where it applies: issues/comments or only pull
  requests) and `bug reports` line (the template's asks).
- Live: the student's claim draft; the repo's `CONTRIBUTING.md`,
  `AI_POLICY.md` or similar, and `.github/ISSUE_TEMPLATE/` on GitHub.
  The scope file's house rules also apply in live mode (a classmate's
  claim does not block the student's own).

**What good looks like.** The claim comment could only have been
written for this issue: it names the symptom, version, code location,
or a thread pointer, and a next step the claimant can do (read a
function, test a draft patch, check a dependency version, report
back). It asks, it does not demand: "I'd like to take this" is fine;
"kindly assign it to me, guaranteed in 2 days, keep it reserved" is
not, and neither is a +1 or a self-assignment. It claims no more than
the report shows.

For AI disclosure, treat every package as AI-assisted. If the repo's
policy requires disclosing AI use in issues or comments, a sentence in
the claim or report discloses it, naming the tool and extent if the
policy asks (for example: "I used an AI assistant to help organize
this report; I ran every step myself"). A policy that asks only for
disclosure in pull requests, asks that comments be in the
contributor's own words, is permissive with responsibility, or is
silent does not require a disclosure in the comments.
