# Rubric: is this a good first issue?

Dates are measured against the bundle's capture date in eval mode, and
against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `not-archived` | `archived:` on the repo line | Says no. An archived repo is read-only. | required |
| `recent-commits` | the last-5-commits list in repo facts | The newest date in that list is within 180 days. Read all five — the list is not always in date order. | required |
| `unclaimed` | the `this issue:` line, plus the comments | No assignee, and no linked PR that is still open. Closed and merged PRs are old attempts, not claims. A claim comment older than 90 days with no open PR behind it is stale and does not block. | required |
| `bounded-scope` | issue title and body | Aims at one outcome — one bug fixed, one topic documented, one behaviour changed. Several files, several suggested causes to investigate, or one main change plus the follow-on edits that keep the rest of the repo consistent with it, all still count as one outcome. It fails only when the pieces are genuinely independent: each a complete change on its own that a different person could take, in any order, without waiting for the others. That is an umbrella or tracking list of sub-issues, or "do X across the whole codebase". Support questions fail too. A short write-up is fine — judge the work, not the prose. | required |
| `settled-approach` | the comment thread, and the states of the linked PRs | Nobody is still arguing about what the change should be, no maintainer says it needs core-internals work, and fewer than two closed-unmerged PRs have already tried it. An empty thread passes. | required |
| `project-acknowledged` | labels, author association, maintainer comments | Any one of: the issue has at least one label, the author is an owner/member/collaborator, or one of them commented to confirm it or invite a taker. An unlabelled request nobody on the project has touched is still a wish. | required |
| `ai-policy-allows` | the contribution-policy line in repo facts | No outright ban on AI-assisted work. Conditions pass — disclosing, testing, understanding your change, "no *fully* AI-generated contributions". Silence passes too. | required |
| `maintainer-responsive` | the first-response sample in repo facts | At least one sampled issue got a maintainer reply within 30 days. "No maintainer comment in thread" is not proof of death by itself. | preferred |
| `recent-release` | `latest release` in repo facts | A release within the last 365 days. `none published` does not fail — plenty of live projects never cut releases. | preferred |
| `newcomer-labelled` | the issue's labels | Carries `good first issue`, `help wanted`, `easy`, or similar. | preferred |

## Verdict rule

Accept if every required check passes; otherwise reject.

`unclear` counts as a fail on a required check — an issue I cannot verify
is not one to take. On a preferred check it just gets reported.

Preferred checks never change a verdict. They rank the issues already
accepted: prefer the candidate with more of them passing.
