# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

[The individual Path Review issue page. A link to the repository or the issue list
does not satisfy this field.]

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
paste the output here, including the closing JSON block
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]
12/20
17/20
17/20
17/20
18/20
**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]
| item | gold | verdict |
| ---  | ---  | --- |
| issue-9  | accept  | reject  |

The failed check for issue-09 is Open issues: is not linked to any open or
closed PR, is not claimed by others in the comment. This issue is closed on
Sep 2, so my rubric rejects it.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]


| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Does not prohibit LLM contributions  | repo's documents, license, readme  | Does not have a policy that prohibits LLM/AI contributions in README, docs/ or any related files  | required  |

Rationale: we are going to use LLM and AI coding agent to fix the issue. So if
the repository has such a policy such as many repositories hosted on
codeberg.org, our pull request won't be accepted by the maintainer and there may
 be legal, copyright or code contributors' problems involved.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check treat AI policy as on and off. However, in many repos, maintainer has
a very specific policy on how AI agent can contribute to the repository. The
check may sometimes give incorrect result on the AI policy of repo.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

selected item:

link: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

verdict:
```json
[
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
      "checks": [
        {"name": "Maintaining Status", "grade": "pass", "evidence": "repo pushedAt 2026-09-16T21:48:27Z, 5 days before today (2026-09-21), commits by Andrew Burke through that date"},
        {"name": "Does not prohibit LLM contributions", "grade": "pass", "evidence": "README, docs/CONTRIBUTING.md, and .github/PULL_REQUEST_TEMPLATE.md contain no AI/LLM ban or disclosure requirement"},
        {"name": "Good documents for contributors", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has branch naming, commit convention, CI requirements, and 'Adding a New Parser/Tool' sections"},
        {"name": "Clear description of the issue", "grade": "pass", "evidence": "body names exact defect (UnknownHashError escaping instead of returning  False), file core/security.py, xfail manifest id H-05, effort estimate 1-2h"},
        {"name": "Clear status the issue", "grade": "pass", "evidence": "state: OPEN, closedAt: null, no closedByPullRequestsReferences"},
        {"name": "Open issues", "grade": "pass", "evidence": "comments: [] and closedByPullRequestsReferences/timelineItems both empty — no assignee, no linked PR, no claim comment"}
      ],
      "verdict": "accept"
    }
]
```

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

1. I am interested in the Python corelib and security related problems. I am
   available to spend 1 - 2 hours for the issue.
2. The verdict identified the current issue status and repository policy
   correctly, but it could not identify whether the issue reports a genuine bug
   or provides relevant details.
3. The anticipated difficulty is mainly setting up the environment to
   reproducing the bug, debugging the root cause, applying the code changes and
   integrating the new changes into CI/CD workflow.


Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
