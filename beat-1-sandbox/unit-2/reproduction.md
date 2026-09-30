# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Vishnutej

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5904152750

Hi, I'd like to work on this as my first contribution here. Others in the course are working on it as well. My reproduction will come from my own setup and runs. Next I'm going to set up the repo on macOS, run the issue's `scrub()` / `detect()` snippet on `(555) 123-4567` with the dashed `555-123-4567` as a control, and run the four tests the issue lists in `tests/unit/test_pii_scrubber.py`. I'll post that here as a reproduction report with my environment, exact commands, and output. After that I'll read the phone pattern in `safety/pii_scrubber.py` to work out why the parenthesized form doesn't match, and check which other formats a wider pattern would start catching before I propose anything.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5904168360

## Reproduction report

Reproduced on macOS: `(555) 123-4567` passes through `scrub()` unredacted and `detect()` returns nothing for it, while the dashed `555-123-4567` is caught.

**Environment:** macOS 26.6.2 (Apple Silicon, arm64), Python 3.13.11 in a fresh `.venv`, repo at `f89c06f` (my fork's `main`, same commit as upstream `main`), pytest 9.1.1. Set up following `docs/SETUP.md`: `.env` copied from `.env.example` (`LLM_PROVIDER=mock`) and the Python half of `make setup` (`python3 -m venv .venv`, `pip install -e ".[dev]"`). The Postgres/Redis containers were not running; `PIIScrubber` doesn't touch them, and the repo's unit suite runs without them:

```
$ make test-unit
...
================= 375 passed, 53 xfailed, 2 warnings in 8.19s ==================
```

**Steps** (from a fresh clone):

```
$ python3 -m venv .venv
$ .venv/bin/pip install -e ".[dev]"
$ .venv/bin/python -c "
from safety.pii_scrubber import PIIScrubber
s = PIIScrubber()
print(repr(s.scrub('Call me at (555) 123-4567 or 555-123-4567')))
print(s.detect('Call me at (555) 123-4567'))
print(s.detect('Call me at 555-123-4567'))
"
'Call me at (555) 123-4567 or [REDACTED]'
[]
[{'type': 'phone_us', 'value': '555-123-4567', 'start': 11, 'end': 23}]
```

(The `pii_detected` structlog lines between the prints are left out; they report `count=0` for the parenthesized input and `count=1` for the dashed one.)

The four tests the issue names:

```
$ .venv/bin/pytest tests/unit/test_pii_scrubber.py -rxX -q -k "test_us_phone_number_redaction or test_us_phone_formats or test_detect_phone_pii or test_phone_at_start_of_text"
xxxx                                                                     [100%]
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii - issue #53: PII scrubber does not redact parenthesized US phone numbers
XFAIL tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text - issue #53: PII scrubber does not redact parenthesized US phone numbers
21 deselected, 4 xfailed in 0.73s
```

**Expected:** both numbers come back as `[REDACTED]`, and `detect()` reports a `phone_us` match for the parenthesized one too.

**Actual:** the parenthesized number is left untouched and `detect()` returns `[]` for it (above); the dashed control is redacted and detected. All four tests xfail with the `issue #53` reason.

**One extra observation**, which I haven't dug into yet. AdithNG's regex check above shows the no-space form matching as `555)123-4567`, without the opening parenthesis. Running the no-space forms through `scrub()` shows what that does to the output: the `(` is left behind.

```
$ .venv/bin/python -c "
from safety.pii_scrubber import PIIScrubber
s = PIIScrubber()
for t in ['(555) 123-4567', '(555)123-4567', '(555)-123-4567']: print(repr(t), '->', repr(s.scrub(t)))
" 2>/dev/null
'(555) 123-4567' -> '(555) 123-4567'
'(555)123-4567' -> '([REDACTED]'
'(555)-123-4567' -> '([REDACTED]'
```

So there may be more to it than the space after `)`. I'll look at the `phone_us` pattern in `safety/pii_scrubber.py` next and check both before proposing a change.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run (20 scored + 4 calibration, calibration unscored): **20/20**, bar PASS, every category matched (`disclosure 1/1`). Calibration 4/4 as well: calib-01 accepted, calib-02/03/04 rejected.
2. Confirming full run with `--save-run eval-run.txt`, same files (same sha256 fingerprints): **20/20 scored items (bar: 18/20: PASS)**. This is the run in `eval-run.txt`.

The revisions happened before the first run, in the in-class calibration worksheet (calib-01..04), and were folded into the rubric before I ran anything against the scored set. That is why both scored runs agree.

**Package analysis**

**pkg-20** (ghostty-org/ghostty#13604, mode-2031 color-scheme report). My rubric decided **reject**; the gold label is **reject** (category `disclosure`).

It is the best repro in the set on every proof check: the environment names the 1.3.1 release build, Fedora RPM, GTK backend and GNOME Wayland; the steps give the exact launch flags and the `printf '\033[?996n'` query; the artifact shows `^[[?997;2n` (light) with a single theme, and the control with a conditional pair shows `^[[?997;1n`. So `env-recorded`, `steps-rerunnable`, `target-faithful`, `behavior-shown`, `outcome-honest`, and `claim-specific` all passed, and so did the preferred `control-run`.

It failed only `ai-disclosure`. The repo facts say "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance", and neither the claim comment nor the report says anything about AI. My rubric treats every course package as AI-assisted work, so the missing sentence is a required fail on its own, and the verdict rule turns one required fail into reject. The proof is ready; the words are not ready for that repo.

**Check rationale**

```
| `env-recorded` | The repro report's environment record, read against the issue's own environment line and any factor the issue or thread says changes the failure (see evidence guide, Environment) | The report names the version of the software it ran and the OS/platform it ran on, **and** every factor the issue or thread marks as changing the behavior (driver, build profile, shell, browser language, release vs. debug build). A report with no environment record at all fails, even when its artifact looks right: a stranger cannot place the attempt. | required |
```

It reads this way because of calib-04 (hyperfine) in the in-class activity. My first draft let a right-looking artifact carry the whole package, so a report with the correct output and no environment line at all would pass. On hyperfine, the issue says the build profile changes the failure mode (debug builds panic, release builds wrap), so an attempt with no environment cannot be placed, and a stranger cannot tell which failure they should expect. I rewrote the check to fail a missing environment record outright, "even when its artifact looks right", and to require every factor the issue or thread marks as changing the behavior, naming examples like the build profile and driver.

**Trade-offs**

`env-recorded` gives up terse reports that skip the environment line. A report that pastes the exact failure but never says what it ran on is now a reject even when a maintainer could guess the environment from the output. I accept that miss: an unplaceable attempt is not ready to post.

The risk was that it would also catch terse-but-complete reports. calib-01 (lazygit) is that trap, rough but complete, and it still graded accept in run 1, with no failed checks. calib-04 still rejected, failing `env-recorded` alone, so the check does exactly the one job it was added for. On the scored set it fails four packages (pkg-04, pkg-06, pkg-13, pkg-17), and each of those also fails other required checks, so it flipped no scored package on its own; calib-04 is the only package it rejects alone. Nothing changed elsewhere: all 8 clear-accept packages passed every required check in run 1, and the confirming run gave the same verdicts on all 20.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
