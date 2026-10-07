# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

Vishnutej

**Plan comment**

Comment permalink: `https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-6030580195`

Comment text:

> I reproduced issue #53 on the fork's current `main` with the following
> outputs:
>
> ```text
> 'Call me at (555) 123-4567 or [REDACTED]'
> []
> [{'type': 'phone_us', 'value': '555-123-4567', 'start': 34, 'end': 46}]
> '(555)123-4567' -> '([REDACTED]'
> ```
>
> The parenthesized number passes through `scrub()` and `detect()` returns
> no phone match, while the dashed control is redacted and detected. The
> no-space form leaves the opening `(` behind, so this is not only a
> spacing issue.
>
> My diagnosis is that the current pattern has no whitespace separator
> after `)` or between later groups, and its leading `\b` cannot start a
> complete match at `(`. I plan to add a complete parenthesized-area-code
> branch with explicit optional spaces/separators and a safe opening
> boundary in `safety/pii_scrubber.py`, then remove the seeded issue #53
> `xfail` markers in the focused tests. This is the proposed fix; I will
> confirm the exact grouping against the focused tests.
>
> The change stays limited to that pattern and its tests; other PII
> patterns and the scrubber API are out of scope.
>
> I’ll rerun the Unit 2 reproduction, verify that both `scrub()` and
> `detect()` cover the complete parenthesized number, run the focused
> issue tests, and then run `make test-unit`. I’ll report any change from
> this plan in the `Deviations` section before submitting the fix.

## Your branch

**Branch**

`fix/53-parenthesized-phone-pii`

**Evidence**

Before the fix, the Unit 2 reproduction returned:

```text
'Call me at (555) 123-4567 or [REDACTED]'
[]
[{'type': 'phone_us', 'value': '555-123-4567', 'start': 11, 'end': 23}]
```

Additional before results:

```text
'(555) 123-4567' -> '(555) 123-4567'
'(555)123-4567' -> '([REDACTED]'
'(555)-123-4567' -> '([REDACTED]'
```

After the fix, the same reproduction returned:

```text
'Call me at [REDACTED] or [REDACTED]'
[{'type': 'phone_us', 'value': '(555) 123-4567', 'start': 11, 'end': 25}]
[{'type': 'phone_us', 'value': '555-123-4567', 'start': 11, 'end': 23}]
```

Additional after results:

```text
'(555) 123-4567' -> '[REDACTED]'
'(555)123-4567' -> '[REDACTED]'
'(555)-123-4567' -> '[REDACTED]'
```

The focused phone tests passed: `4 passed, 21 deselected`.
The full unit suite passed: `379 passed, 49 xfailed, 1 warning`.

## Eval iterations

### Run history

- First full run: `19/20 scored items` — PASS.
- Targeted retry of `pkg-14`: `1/1 scored items`.
- Confirming full run: `19/20 scored items` — PASS.

The final `eval-run.txt` records `agreement: 19/20 scored items (bar:
18/20: PASS)` and all category floors passed.

### Package analysis

`pkg-14`: my rubric decided `reject`, while the gold label was `accept`.
The package was a clear accept whose implementation named the affected
area and whose uncertainty was explicitly bounded, but the first rubric
run treated its investigation-level edit-site uncertainty too strictly.
I revised the executable-implementation and honest-uncertainty pass
conditions to accept a bounded investigation that pins the exact edit
site and to require labeled uncertainty with a concrete validation
method. The targeted retry accepted `pkg-14`; the confirming full run
remained at 19/20 because the grader was not fully stable on that item.

### Check rationale

> A stranger can begin the work without asking the author what to change
> next: the approach identifies the relevant code or artifacts, describes
> the change or the bounded investigation needed to pin the exact edit
> site in actionable order, and names important dependencies or
> decisions.

I revised this condition after `pkg-14`: a plan can be executable while
still reserving a bounded investigation to confirm the exact symbol or
edit site. This keeps the check from requiring false precision while
still requiring actionable files, order, and dependencies.

### Trade-offs

The rubric accepts a clearly bounded investigation when the exact edit
site is not yet certain, which improved the clear-accept behavior for
`pkg-14`. It still requires the investigation to be labeled and paired
with a concrete validation method, so an unsupported guess does not pass.
The final full run preserved all category matches and the 19/20
agreement score.
