# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/228

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]

fix/72-verify-password

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

- First run:
  categories: clear-accept 7/7  not-tested 3/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3
  agreement: 19/20 scored items  (bar: 18/20: PASS)
- Second run:
  categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3
  agreement: 20/20 scored items  (bar: 18/20: PASS)

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

| item | category |gold | verdict |
| ---  | ---  | --- | --- |
| pkg-04 | not-tested | reject | reject |

The package is rejected by gold label and my rubric. The failed check is: Correct testing, New test for the fix/functionality is correct and passes. The test evidence section only describes results for some commands. It does not match the result in the plan context.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

One quoted check is:

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Correct testing | New test for the fix/functionality is correct and passes | Test evidence should matches the result in the test plan | required |

This asks candidate to write a PR that has a working test that matches its test plan. This check is to ensure the PR gives something observable.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

The Correct testing check does not check what the new test is actually doing. It does not check existing testcases neither. This is because different PR may have specific workflow or reproducible steps to check whether the bug is fixed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
