# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

**Verdict output**

Live-mode run on three candidates (#73, #53, #60), pasted as printed:

````
## Evidence gathered

**Repo facts** (`codepath/pathreview-ai301-fa26-s1`, checked 2026-09-22): `archived: false`; newest default-branch commit 2026-09-16 (6 days old, all five by `Aburke225`); no releases published; `docs/CONTRIBUTING.md` has no AI-policy text and the PR template has no AI-disclosure clause; only one PR exists in the repo (#74, open).

**Maintainer first-response sample** (#72, #68, #63, #62): every comment is `author_association: NONE` — students and a TF. No Owner/Member/Collaborator reply in any sampled thread, so `maintainer-responsive` fails for all three candidates equally.

---

### Ranked read-out

**1. #73 — README and `.env.example` disagree about which LLM API key to set** → accept
All 7 required checks pass. Fit: this is the smallest job of the three and the closest thing on the board to the "docs fix" the profile asks for — two text files to reconcile against `core/config.py`, no code path, no database, no running server. Labelled `docs` and `good first issue`, opened by a collaborator, zero comments and no PR behind it.

**2. #53 — PII scrubber fails to redact parenthesized US phone numbers** → accept
All 7 required checks pass. Fit: one regex in one function in `pii_scrubber.py` — plain Python, obvious file, and per `docs/CONTRIBUTING.md` seeded bugs ship with an `xfail` marker you remove, so the test flipping green is an easy way to tell it worked. Ranked second only because it's a slightly larger job than #73, and the profile said size is what matters most.

**3. #60 — Faithfulness checker crashes when a context chunk has `text: None`** → reject
Sunk by `unclaimed`. PR #74, `fix(rag): handle None text in faithfulness checker (#60)`, is open and unmerged (opened 2026-09-21 from `nianiiier`, base `codepath/pathreview-ai301-fa26-s1`). The Path Review house rule waives other students' *claim comments*, not open linked PRs, and the rubric's condition is "no linked PR that is still open." Every other required check on #60 passes, so if #74 closes unmerged this becomes a strong candidate.

Both accepted issues share the same preferred-check profile (`newcomer-labelled` pass, `recent-release` pass by the "none published does not fail" clause, `maintainer-responsive` fail), so the ranking between them comes entirely from fit.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "Repo API: \"archived\": false"},
      {"name": "recent-commits", "grade": "pass", "evidence": "Newest of last 5 commits is 2026-09-16, 6 days before today (2026-09-22)"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; comments: 0; repo-wide PR search returns only #74, which targets #60"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One outcome — align README.md and .env.example on the LLM API key that core/config.py already defines"},
      {"name": "settled-approach", "grade": "pass", "evidence": "Comment thread is empty (0 comments); no closed-unmerged PRs against it"},
      {"name": "project-acknowledged", "grade": "pass", "evidence": "Labels bug, good first issue, docs, tier-1; author Aburke225 is COLLABORATOR"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI policy text — silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled #72, #68, #63, #62: all comments are author_association NONE, no maintainer reply"},
      {"name": "recent-release", "grade": "pass", "evidence": "Releases array empty — \"none published does not fail\""},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Carries the `good first issue` label"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "Repo API: \"archived\": false"},
      {"name": "recent-commits", "grade": "pass", "evidence": "Newest of last 5 commits is 2026-09-16, 6 days before today (2026-09-22)"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; comments: 0; the repo's only PR (#74) references #60, not #53"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One outcome — extend the phone-number pattern in pii_scrubber.py to match (555) 123-4567"},
      {"name": "settled-approach", "grade": "pass", "evidence": "Comment thread is empty (0 comments); no closed-unmerged PRs against it"},
      {"name": "project-acknowledged", "grade": "pass", "evidence": "Labels bug, good first issue, safety, tier-1; author Aburke225 is COLLABORATOR"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI policy text — silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled #72, #68, #63, #62: all comments are author_association NONE, no maintainer reply"},
      {"name": "recent-release", "grade": "pass", "evidence": "Releases array empty — \"none published does not fail\""},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Carries the `good first issue` label"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "Repo API: \"archived\": false"},
      {"name": "recent-commits", "grade": "pass", "evidence": "Newest of last 5 commits is 2026-09-16, 6 days before today (2026-09-22)"},
      {"name": "unclaimed", "grade": "fail", "evidence": "PR #74 \"fix(rag): handle None text in faithfulness checker (#60)\" is open and unmerged (created 2026-09-21, base codepath/pathreview-ai301-fa26-s1); the house rule waives claim comments, not open linked PRs"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "One outcome — make check() tolerate chunk text of None; reproduction and a failing test are given"},
      {"name": "settled-approach", "grade": "pass", "evidence": "Comment thread is empty (0 comments); zero closed-unmerged PRs have tried it"},
      {"name": "project-acknowledged", "grade": "pass", "evidence": "Labels bug, good first issue, rag, tier-1; author Aburke225 is COLLABORATOR"},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI policy text — silence passes"},
      {"name": "maintainer-responsive", "grade": "fail", "evidence": "Sampled #72, #68, #63, #62: all comments are author_association NONE, no maintainer reply"},
      {"name": "recent-release", "grade": "pass", "evidence": "Releases array empty — \"none published does not fail\""},
      {"name": "newcomer-labelled", "grade": "pass", "evidence": "Carries the `good first issue` label"}
    ],
    "verdict": "reject"
  }
]
```
````

The verdict for issue #53 is `accept`.

---

## Eval iterations

**Run history**

Five runs, in order. Partial runs are marked, since only the full runs are scored
against the bar.

1. Partial, `--only issue-20,issue-09,issue-06,issue-14,issue-12,issue-15`:
   `agreement: 6/6 scored items`. These were the six I expected my rubric to be
   most likely to get wrong, so I graded them before paying for a full run.
2. Full: `agreement: 18/20 scored items  (bar: 18/20: PASS)`. The two misses were
   `issue-01  accept  reject   NO     failed: bounded-scope, maintainer-responsive (preferred), newcomer-labelled (preferred)`
   and
   `issue-19  accept  reject   NO     failed: bounded-scope, newcomer-labelled (preferred)`.
3. Partial, `--only issue-01,issue-19,issue-10,issue-05` after a first rewrite of
   `bounded-scope`: `agreement: 3/4 scored items`. issue-19 flipped to accept and
   the two umbrellas stayed rejected, but issue-01 still failed.
4. Partial, `--only issue-01,issue-10` after a second rewrite:
   `agreement: 2/2 scored items`.
5. Full, the committed run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`,
   with `categories: claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 4/4`.

The last score matches the agreement line in `eval-run.txt`.

**Issue analysis**

`issue-04` (zxcalc/zxlive#555). My rubric said reject. The gold label says
`accept`, with the note "small active repo, maintainer-filed bounded bug,
unclaimed". So this is the one disagreement in the committed run:
`issue-04  accept  reject   NO     failed: bounded-scope`.

Nine of my ten checks passed it. The whole reject rests on `bounded-scope`, and
the run recorded this reasoning for the fail:

> issue lists multiple independent missing rule previews ('remove identity, fuse
> spiders, remove self loops, etc.') each implementable separately, with an
> open-ended 'etc.'

That reading comes straight from the bundle. The title is "Missing several basic
rule previews" and the entire body is one line:

> Including remove identity, fuse spiders, remove self loops, etc.

So my check saw a list of three named items plus "etc." and applied its own test,
"each a complete change on its own that a different person could take, in any
order, without waiting for the others." Each rule preview does pass that test in
isolation. What my check could not weigh is that these are three small previews
of the same kind in a 101-star repo, which a maintainer would expect in one pull
request, and that the "etc." is a maintainer being casual rather than opening a
tracking list. The instructor read the batch as one job. My rubric read it as
three.

**Check rationale**

The check is `bounded-scope`, quoted as it currently stands in
`tools/issue-select/rubric.md`:

> | `bounded-scope` | issue title and body | Aims at one outcome — one bug fixed, one topic documented, one behaviour changed. Several files, several suggested causes to investigate, or one main change plus the follow-on edits that keep the rest of the repo consistent with it, all still count as one outcome. It fails only when the pieces are genuinely independent: each a complete change on its own that a different person could take, in any order, without waiting for the others. That is an umbrella or tracking list of sub-issues, or "do X across the whole codebase". Support questions fail too. A short write-up is fine — judge the work, not the prose. | required |

It is this long because two shorter versions were wrong, and the eval showed me
how. My first version was "Asks for one change that fits in one pull request.
Fails if it is an umbrella or tracking list, a sweep across the whole codebase,
or a support question." Run 2 rejected `issue-01` and `issue-19` on it. Both are
gold accepts. The model was counting files and suggestions: for `issue-19` it
wrote "body lists 2 'potential causes which should be fixed' plus 3 separate
'additional suggestions' ... a tracking list of multiple distinct approaches".

So I added that several files or several suggested causes still count as one
outcome. That fixed `issue-19` but not `issue-01`, where the note became "issue
lists five independent deliverables ... each its own likely PR". Reading the
bundle, `issue-01` is a new docs page plus edits to four pages that point at it.
Those edits are not independent. They point at a page that would not exist
without the main change. The word doing the work was "independent", and I had
never said what it meant. The final sentence defines it as a test someone else
can apply: could a different person take this piece, in any order, without
waiting for the others.

I kept `bounded-scope` required rather than preferred because scope is what the
eval set punishes hardest. Four of the twenty scored issues are scope rejects,
and `issue-10` fails on this check alone, so demoting it would cost the scope
category.

**Trade-offs**

It gives up `issue-04`, and I decided to accept that rather than chase it.

Widening the check to pass a short list of similar small items is exactly the
shape of `issue-10`, the "Documentation request megaissue", which my run rejects
with "titled 'Documentation request megaissue', body is a list of 100+ linked
sub-issues". `issue-10` fails on `bounded-scope` and nothing else, so any wording
loose enough to let `issue-04` through risks letting the megaissue through too,
and that would cost a category rather than a single item. The only real
difference between them is how many items are in the list, and I did not want a
rubric whose scope test is a count.

I did check the change rather than assume it. After each rewrite I re-ran the
affected issues with `--only`: first `--only issue-01,issue-19,issue-10,issue-05`
and then `--only issue-01,issue-10`, keeping `issue-10` and `issue-05` in both as
canaries to confirm the umbrellas still failed while `issue-01` and `issue-19`
started passing. Both canaries held at every step.

Worth naming: `issue-04` passed `bounded-scope` in run 2 under the older, stricter
wording and failed it in run 5 under the looser one, while `issue-01` and
`issue-19` went the other way. It is a genuinely arguable call that sits near my
threshold, so I expect it to move between runs rather than fail every time.

---

## Selection rationale

**Selection rationale**

1. Fit. I can write Python, and what is new to me is the contribution workflow
   rather than the language, so I wanted the code part small enough that the fork
   and pull request part is the thing I am actually learning. Issue #53 is one
   regex in one function in `pii_scrubber.py`. I am interested in most of this
   repo and did not have a strong preference between subsystems, so what decided
   it was the size and shape of the job rather than the topic. The PII scrubber
   being a safety feature is a nice bonus.

2. What the verdict got right, and what I weighed on top. The skill was right
   about the thing I would have got wrong on my own. I had #60 on my shortlist
   because the issue page looks completely free: no assignee, no comments. The
   skill found PR #74 already open against it and rejected it on `unclaimed`. I
   would have claimed an issue somebody else is mid way through fixing.

   What I weighed that the rubric could not: it ranked #73 first and #53 second,
   on size alone, and I took the second one. #73 is a README and `.env.example`
   mismatch. It is a real bug and a smaller job, but Unit 2 asks me to set up the
   environment and reproduce the issue, and there is not much to reproduce in two
   text files disagreeing. #53 has a failing test I can actually run and watch go
   green. My rubric has no idea what Unit 2 is going to ask of me, so that part
   was mine to judge, not its.

3. Anticipated difficulty. The fix itself looks small, and the risk is that it is
   deceptively so. Phone number regexes have more edge cases than they first
   appear, and if I widen the pattern carelessly I will start matching things that
   are not phone numbers, which on a PII scrubber is the worse failure. I expect
   the real work to be in the test cases rather than the pattern. The other thing
   I am watching is that `maintainer-responsive` failed for every candidate in
   this repo, since every sampled reply came from students and a TF rather than an
   owner, so I should not count on a fast review and should make the pull request
   easy to read on the first pass. Classmates may also pick the same issue, which
   the house rule says is fine and costs nobody anything.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
