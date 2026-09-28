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

[Your GitHub username, exactly as it appears on your profile — no `@`, no profile URL. Your
comments upstream are identified by this name.]

kwfcfc
---

## Posted upstream

**Claim comment**

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5862069638

```markdown
Hi, I'd like to pick up this issue. I plan to first run the `test_verify_with_wrong_hash_format`
unit test and write up a bug reproduction report. Then I will propose an exception handler for the
`verify_password` function when the `passlib.CryptContext` fails to decode malformed hashed
password.
```

**Reproduction comment**

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5862828554

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

- Run 1:
  categories: clear-accept 3/8  disclosure 0/1  no-evidence 4/4  unfollowable-comms 2/3  wrong-target 4/4
  agreement: 13/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)
- Run 2:
  categories: clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4
  agreement: 19/20 scored items  (bar: 18/20: PASS)

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

| item | gold | verdict |
| ---  | ---  | --- |
| pkg-01 | accept  | reject  |

The failed check is: correct reproduction steps. This check asks for reproduction
report to follow the issue ste by step and use equivalent command and input. In
the pkg-01, the candidate use `http --offline ...` command, so the check fails
because it is not an equivalent command.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

One quoted check is:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| correct reproduction steps | reproduction must follow the steps in the issue | the reproduction should follow the steps in the issue, and use equivalent command and input to reproduce the issue | required |

This asks candidate to follow the exact steps of commands and inputs to
successfullly reproduce the issue. If the candidate does not follow these steps,
they may fail to reproduce the issue or give false negative result.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check says equivalent commands but it does not distinguish whether an
argument is required for the reproduction. In the `pkg-01`, candidate used
`--offline` because it is sufficient to reproduce the issue by printing out the
headers instead of sending the actual request.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
