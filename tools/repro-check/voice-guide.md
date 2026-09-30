# Voice guide: how I talk upstream

## Who I am in threads

I'm a first-time contributor working through AI301, taking on one
issue at a time in repos I'm still learning. I say that plainly and
don't pretend to know the codebase better than I do. Readers can
expect me to show what I ran, say what I don't know yet, and come back
with what I find.

## Rules I write by

### Rule: Show it, don't vouch for it

Every "I reproduced it" has the output right under it. If I didn't
paste it, I don't claim it.

- Wrong: "Confirmed, this is 100% reproducible on my machine."
- Right: "Reproduced on 1.3.1 with the issue's command; output below."

### Rule: Say what differed

When my environment, version, or input isn't the reporter's, I name
the difference in the same sentence as the result.

- Wrong: "Reproduced it, same error as the issue."
- Right: "Reproduced on 15.2.0 (the issue was filed on 13.0.0); same
  wrong line numbers."

### Rule: Guesses are labeled as guesses

I can point at where I think the bug is, but unless I've shown it, it
reads as a hypothesis, not a finding.

- Wrong: "The root cause is a race in the debounced save."
- Right: "My guess is the debounced save gets cancelled on switch; I
  haven't confirmed that yet, and that's what I'll check next."

### Rule: Ask for the issue, don't reserve it

I say I'd like to work on it and what I'll do next. I don't ask to be
assigned, don't set a deadline I can't guarantee, and don't ask anyone
to hold it for me.

- Wrong: "Please assign this to me, I'll have a fix in 2 days."
- Right: "I'd like to work on this. Next I'm going to read
  `contract_repo_path` and report back what I find."

### Rule: Disclose AI help where the repo asks

If the repo's policy asks for AI disclosure in comments, I say what
tool I used and for what, in one plain sentence.

- Wrong: (no mention, on a repo whose policy says all AI use must be
  disclosed)
- Right: "I used Claude Code to help organize this report; I ran and
  checked every step myself."

## Things I never post

- A timeline promise ("in 2 days", "by this weekend").
- "+1", "same here", or "any update?" with nothing of my own attached.
- Flattery or filler to open a comment ("Hello sir! Great project!").
- A root cause I haven't shown evidence for.
- A claim that I understand internals I haven't read yet.
- "Same as above" on a classmate's repro: my comment carries my own run.
