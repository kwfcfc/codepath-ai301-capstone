# Contribution: ci: add GitHub Actions auto-labeling for PRs

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Pusen
**GitHub Username:** kwfcfc
**Issue:** https://github.com/Raftersecurity/rafter-cli/issues/32
**Pull Request:** https://github.com/Raftersecurity/rafter-cli/pull/356

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: a general one time issue search in direct mode**

2026-11-9
I chose my issue before setting up the issue-scout. Mostly I just use the
issue-scout to double check some standard. My search strategy is some innovative
features and community improvement with good automation system.

**Unit 6: template voice-guard and a claude side project level memory**

2026-11-05
The voice-guard was from beat-1 with little revise. Mostly because the general
voice guard applies and the claude code has project level memory instead of a
Claude.local.md on the GitHub repo.

**Unit 7: ship-gate with fork side GitHub workflow simulation**

2026-11-06
The ship-gate skipped the npm and python test workflow and only used GitHub
Actions workflow to collect labeling behavior. It did find labeling for
previously missing labels testing and secret-pattern are correct but later
deleted by myself because I forgot to set up those labels before the simulation
test.

**Unit 8: No reply from maintainer, PR was too inactive to start monitoring**

EST: 2026-11-12
I haven't received reply yet, so PR monitor wasn't installed to start its first 
run. I plan to add a notification on the GitHub side and forward notice to me.

---

## Why I Chose This Issue

I searched from the course issue selection site with `good first issue` and
found out this issue. It aligned with my interest on CI/CD tools, small
community contribution with a proper amount to time to work on.


**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

rafter-cli has no automation that labels pull requests. The labels `bug`,
`enhancement`, `testing`, `documentation` and `secret-pattern` already exist
in the repository. Each PR needs maintainer to manually apply labels, so recent
PRs carry no labels at all as contribution scales. Issue #32 asks for a GitHub
Actions workflow that labels a PR by its title prefix and by the files it
changes because "manual labeling doesn't scale."

**Expected Behavior**

When a PR is opened, edited or updated, a workflow adds labels by the two rule
sets in the issue:

| Title prefix | Label |
|---|---|
| `feat:` | `enhancement` |
| `fix:` | `bug` |
| `test:` | `testing` |
| `docs:` | `documentation` |
| `pattern:` | `secret-pattern` |

| Changed path | Label |
|---|---|
| `node/src/scanners/secret-patterns.ts` | `secret-pattern` |
| `python/rafter_cli/scanners/secret_patterns.py` | `secret-pattern` |
| `recipes/**` | `documentation` |
| `node/tests/**` or `python/tests/**` | `testing` |

**Current Behavior**

At upstream `main` (`1ebad94`, release v0.11.7), `.github/workflows/` holds
only `publish.yaml`, `test-action.yml`, `test-comprehensive.yml`,
`test-github-action.yml` and `validate-release.yml`. There is no labeling
workflow and no `.github/labeler.yml`. Every PR from #342 to #356 has no
label.

**Affected Components**

- `.github/workflows/`: a new workflow, `auto-label.yml`.
- `.github/labeler.yml`: a new rule file for `actions/labeler`.
- The paths the rules watch (matched, not modified):
  `node/src/scanners/secret-patterns.ts`,
  `python/rafter_cli/scanners/secret_patterns.py`, `recipes/`, `node/tests/`,
  `python/tests/`.
- No Node or Python source, no tests, and no `shared-docs/CLI_SPEC.md` change.

**Toolkit**

- Tool: gh
- What it produced: json format for issue requirements and listed output of
  file scopes required to watch
- Difficulties: None
- What changed: None, only downloading the json

---

## Reproduction Process

**Environment Setup**

- OS: macOS 26.7.2 (Apple Silicon).
- Tools: git 2.54.0 and GitHub CLI 2.103.3, logged in with two accounts:
  `kwfcfc` (mine) and `jose-C2OaWi` (a second account used only to open test
  PRs).
- Project: `Raftersecurity/rafter-cli` at `1ebad94` (release v0.11.7).
  Node 22 (`node/package.json` requires `>=22`) and pnpm 12.9.0,
  from a nix shell.

Setup:

1. Forked the repo to `kwfcfc/rafter-cli` on 2026-11-04, cloned it, added
   the upstream remote, and worked on branch `feat/32-auto-label`.
2. The change is a GitHub Actions workflow, so it runs on GitHub, not on my
   laptop. I pushed it to my fork's `main`, because `pull_request_target`
   loads the workflow from the base branch.
3. The second account forked `kwfcfc/rafter-cli` to `jose-C2OaWi/rafter-cli`
   and opened PRs from there into `kwfcfc/rafter-cli:main`. Every test PR
   came from an outside fork, simulating a first-time contributor's PR upstream.

Challenges:

- `pnpm` was not on `PATH` in a fresh shell, so `cd node && pnpm test`
  exited 127. Inside the nix shell the suite ran but failed in
  `tests/skill.test.ts` (`ENOENT … .rafter/config.json`), a test unrelated
  to `.github/`. See Testing Strategy for how I treated it.
- The second account's token has no `workflow` scope, so it cannot push a
  branch that changes a workflow file. Test branches were based on the
  second account's own `main` instead.
- My global git config signs commits with my SSH key, so the second
  account's test commits showed "Unverified". Test commits were then made
  with `-c commit.gpgsign=false` per command; the global config is
  unchanged.
- `testing` and `secret-pattern` did not exist in my fork before testing.
  The first labeling run created them as plain gray labels, and recreating
  them later removed them from 7 test PRs (see Testing Strategy). Upstream
  already has all five labels.

**Steps to Reproduce**

1. Check which workflows upstream has:
   `git ls-tree --name-only 1ebad94 .github/workflows/` lists
   `publish.yaml`, `test-action.yml`, `test-comprehensive.yml`,
   `test-github-action.yml` and `validate-release.yml`, with no labeling
   workflow. `git ls-tree 1ebad94 .github/labeler.yml` prints nothing.
2. List recent upstream PRs with their labels:
   `gh pr list -R Raftersecurity/rafter-cli --state all --limit 15 --json number,title,labels`
3. Observed result: every PR from #342 to #356 has `"labels": []`. #353
   (`fix(risk-rules): …`) and #344 (`docs(spec): …`) match the issue's rules
   but have no `bug` or `documentation` label. #356 (this PR) is unlabeled
   too: `pull_request_target` runs the workflow from upstream `main`, where
   it does not exist yet.

**Reproduction Evidence**

- **Commit showing reproduction:**
  https://github.com/kwfcfc/rafter-cli/tree/1ebad941815d91d45d7befe3295d15f23a8b05ad/.github/workflows
  (my fork at the upstream base commit, with no labeling workflow)
- **Screenshots/logs:** the failed run of my first version on fork PR #11
  (https://github.com/kwfcfc/rafter-cli/actions/runs/42128497331):

  ```text
  ##[error]Unhandled error: HttpError: Invalid request.
  No subschema in "anyOf" matched.
  For 'anyOf/0', {"labels" => [nil]} is not an array.
  For 'anyOf/1', {"labels" => [nil]} is not an array.
  For 'items', nil is not a string or object.
  ```

- **My findings:**
  - The feature is missing, as the issue says.
  - The issue points to `actions/labeler@v5`. The current `actions/labeler@v7`
    can only match `changed-files`, `head-branch` and `base-branch`, so
    labeler alone cannot apply the title rules.
  - Testing my first version on the fork found a real bug in my own code: a
    PR titled `constructor: …` (https://github.com/kwfcfc/rafter-cli/pull/11)
    made the title job fail with HTTP 422. Root cause and fix are in Solution
    Approach.

**Toolkit**

- Tool: gh, actions/labeler@v7
- What it produced: a simple workflow to auto label based on changed files
- Difficulties: cannot handle auto labeling based on PR titles
- What changed: None

---

## Solution Approach

**Analysis**

Two things are missing, and testing found one bug in my first version.

1. **No workflow adds labels.** Nothing in `.github/workflows/` labels a PR.
   A normal `pull_request` workflow cannot do it either, because GitHub gives
   it only read access on PRs from forks. A `pull_request_target` workflow
   gets write access. It is safe here because it never runs the PR's own
   code; it only reads the PR title and the list of changed files.
2. **The labeler cannot read titles.** `actions/labeler` only matches changed
   files and branch names. It handles the path rules (in
   `.github/labeler.yml`), but the title rules need a short script.
3. **A bug in my first title script** (job `label-by-title`, fixed in
   `4fdfb58`). The script looked up the title's type in a small table of
   labels. In JavaScript, such a table also inherits a few built-in names,
   such as `constructor`. So a PR titled `constructor: …` found a built-in
   function instead of "no label", the script sent it to GitHub as a label,
   and the request failed with HTTP 422. Ordinary unknown types like `chore:`
   were not affected. The fix uses `Object.hasOwn` to accept only the five
   types I actually wrote in the table.

**Proposed Solution**

Add one workflow, `.github/workflows/auto-label.yml`, with two jobs, plus one
rule file:

- `label-by-files` runs `actions/labeler@v7` with the path rules in
  `.github/labeler.yml`.
- `label-by-title` runs `actions/github-script@v9`. It reads the PR title,
  takes the conventional-commit type, and adds the mapped label.

Only official `actions/*` actions are used. CONTRIBUTING.md says "every
dependency is attack surface", and this is a security tool. I did not take
`github/issue-labeler`, which is built mainly for issues and would need
testing on PRs, or `srvaroa/labeler`, a third-party action that would need
SHA pinning and other toolchain security scanning.

Deliberately NOT changed:

- No Node or Python code, no tests, and no `shared-docs/CLI_SPEC.md`. CLI
  behavior does not change.
- Labels are only added, never removed. If a title changes from `feat:` to
  `fix:`, the PR keeps `enhancement` and gains `bug` (fork PR #19).
  `sync-labels` is not enabled for the path rules.
- `label-by-title` is skipped on `synchronize`, because a new push does not
  change the title.

**Implementation Plan**

1. Add `.github/workflows/auto-label.yml`. It runs when a PR is opened,
   edited, reopened, or gets new commits (`pull_request_target`).
2. Job `label-by-files` runs `actions/labeler@v7`. It can read the repository
   and write to pull requests.
3. Add `.github/labeler.yml` with the three path rules from the issue: the
   two secret-pattern files → `secret-pattern`, `recipes/` →
   `documentation`, and the two test folders → `testing`.
4. Job `label-by-title` is a short script in `actions/github-script@v9`. It
   takes the type at the start of a conventional-commit title (`feat`, `fix`,
   …; case, scope and `!` do not matter), checks it against the five types in
   the issue with `Object.hasOwn`, and adds the matching label. It can only
   write to pull requests, and it skips new pushes, which do not change the
   title.
5. Test on my fork with PRs from the second account (see Testing Strategy).
   The repo's own Node and Python test suites do not cover `.github/`.

Deviations and mid-build changes:

- Before the first commit, the trigger section (`on:`) of my workflow had
  the wrong YAML shape, so GitHub would have rejected the workflow. I fixed
  it and added the "reopened" and "new commits" triggers.
- `plan.md` named the rule file `label.yml`. It shipped as
  `.github/labeler.yml`, the name labeler looks for by default, so no extra
  setting is needed.
- `plan.md` described one job with two steps. It shipped as two jobs with
  separate permissions; the title job cannot read repository contents.
- The `Object.hasOwn` check (`4fdfb58`) was added after fork PR #11 failed.
  It was not in the plan.

**Toolkit**

- Tool: GitHub Actions, gh
- What it produced: GitHub Actions running logs from simulated PR
- Difficulties: triggering outside real world workflow, slow and sometimes hard
  to debug
- What changed: `.github/labeler.yml` and workflow `.github/workflow/auto-label.yml`
---

## Testing Strategy

Two observable checks.

**Check 1: the reproduction steps, before and after.** Before is Steps to
Reproduce above: no workflow, and no labels on any upstream PR. After is the
workflow on my fork's `main`, plus 30 PRs from the second account's fork,
each built to hit one rule or one edge case. The labels below are what
`github-actions[bot]` applied, read from each PR's timeline.

| Fork PR | Case | Expected | Bot applied |
|---|---|---|---|
| #1–#5 | `feat:` / `fix:` / `test:` / `docs:` / `pattern:` | enhancement / bug / testing / documentation / secret-pattern | same \* |
| #6 | `Feat(scanner)!:` (case, scope, `!`) | enhancement | enhancement |
| #7–#10 | `feature:`, no colon, `feat :`, `docs(scope:` | none | none |
| #11 | `constructor:` | none | **job failed, HTTP 422** (before `4fdfb58`) |
| #12, #13 | Node / Python secret-pattern file | secret-pattern | secret-pattern \* |
| #14 | `recipes/**` | documentation | documentation |
| #15, #16 | `node/tests/**`, `python/tests/**` | testing | testing \* |
| #17 | near-miss paths | none | none |
| #18 | `feat:` + `node/tests/` + `recipes/` | enhancement, documentation, testing | all three \* |
| #19 | title edited `feat:` → `fix:` | bug added, enhancement kept | enhancement, bug |
| #20 | new push (`synchronize`) | documentation | documentation |
| #21 | regression: `constructor:` → `__proto__:` → `toString:` → `hasOwnProperty:` → `feat:` | none until `feat:`, then enhancement | same, all 5 runs green |
| #22, #23, #25, #26 | delete in `recipes/`, rename into `recipes/`, nested dir, dotfile | documentation | documentation |
| #24 | rename a file out of `recipes/` | none (labeler only sees the new path) | none |
| #27, #28 | look-alike paths, case variants (`Recipes/`, `NODE/tests/`) | none | none |
| #29 | permission-only change in `node/tests/` | testing | testing |
| #30 | 351 files, the `recipes/` file last (past the first API page) | documentation | documentation |

\* The bot applied these labels correctly. On 2026-11-05 I recreated `testing`
and `secret-pattern` in my fork, which removed them from #3, #5, #12, #13, #15,
#16 and #18. Each PR's timeline shows the bot's `labeled` event and my later
`unlabeled` event. I did not re-run these.

**Check 2: the repo's own checks.**

- The new `Pull Request Auto Labeler` workflow ran on every test PR. All runs
  are green except #11 before the fix:
  https://github.com/kwfcfc/rafter-cli/actions/workflows/auto-label.yml
- `test-github-action.yml` (the repo's test for its composite action),
  dispatched on my fork: run 42149364176, success. It shows the existing
  action still works; it does not exercise the new workflow because it triggers
  real GitHub Action request.
- Node (`pnpm test`) and Python (`pytest`) suites: not run against this
  change, because the diff only touches `.github/`. Locally, `pnpm test`
  fails in `tests/skill.test.ts` (ENOENT on `.rafter/config.json`) on a
  branch whose `node/` is identical to `main`.
- The repo's `Comprehensive Test Suite` on the test PRs stayed at "action
  required" (fork PRs from a new contributor need approval), so it did not
  run.

**Toolkit**

- Tool: gh with a separate account, claude code
- What it produced: test PRs on my own fork to test labeling
- Difficulties: needs to wait for GitHub to running real PRs, requires extra
  configuration to simulate a first time contributor.
- What changed: GitHub Action Running Logs on my own fork

---

## Implementation Notes


**2026-11-04**

Forked `Raftersecurity/rafter-cli` to `kwfcfc/rafter-cli`.

Ran repro-check on my claim draft. It refused to grade, because no scout
read-out existed for this issue. It also pointed out that the draft said
"pull request commit messages" where the issue means the PR title. I fixed
that and posted the claim:
https://github.com/Raftersecurity/rafter-cli/issues/32#issuecomment-6650429003

Label by title with `actions/labeler@v7`. Labeler v7 cannot match titles, so I
chose labeler for paths and another job `actions/github-script` for titles.

**2026-11-05**

Claude Code ran a script that opened test PRs #1–#20 from the second account.
#11 (`constructor:`) failed with HTTP 422. Editing the auto-created gray
labels in the web UI failed with "Could not update label".

Deleted and recreated `testing` and `secret-pattern` in the fork, which
removed them from 7 test PRs. Wrong turn: I should have created the labels
before testing.


Committed `4fdfb58` (the `Object.hasOwn` guard). Regression PR #21 passed for
`constructor:`, `__proto__:`, `toString:`, `hasOwnProperty:`, and `feat:`.


Installed the ship-gate and ran it 15 times; every run was BLOCK. Manifest
changes:

- `pnpm test` (exit 127, then the `skill.test.ts` failure) → moved the Node
  and Python suites to the excluded table;
- `gh workflow run` on upstream (HTTP 403) → `gh run watch 42149364176`, the
  ship-gate cannot handle the case where the upstream is the base but gh
  workflow runs on my own fork to simulate the new test

Simulated PRs opened by-changed-files cases #22–#30, and fixed `label.yml` → `labeler.yml` in the PR description. 

Opened PR #356. The last ship-gate run was still BLOCK. ship-gate cannot handle
the case where the upstream is the base but gh workflow runs on my own fork to
simulate the new test. It also refused to pass without a reproduction result
though this is a new feature request that cannot trigger the GitHub Action on
the upstream. The ship-gate passes on the PR's draft and overall changes. So I
opened the PR on the web.

**2026-11-09**

Fixed the PR checklist boxes (`[ x ]` → `[x]`). Installed issue-scout and
graded #32 in direct mode. Verdict: reject, on "Open issues", because the
rubric counts my own claim and PR.

**Toolkit**

- Tool: python, nix, uv, gh
- What it produced: rerun the ship-gate, diagnoised the GitHub Action running
  and privilege issues.
- Difficulties: Hard to modify the ship-gate to fit in the new feature workflow
  that integrated with GitHub's own workflow
- What changed: a new PR on th

---

## Pull Request

**PR Link:** https://github.com/Raftersecurity/rafter-cli/pull/356

**PR Description:** The title is `feat(ci): add a GitHub Action for auto
labeling PRs (#32)`. The body follows the format in CONTRIBUTING.md:

- **Summary:** adds `.github/workflows/auto-label.yml` and
  `.github/labeler.yml`; labels by changed files and by title; labels are not
  synced when files or the title change.
- **Test plan:** PRs opened on my fork to simulate first-time contributors,
  with a link to the fork's PR list. The labels `testing` and `secrete-patterns`
  of 7 tests were deleted because I forgot to add them in my own fork before I
  start the test.
- **Spec update:** CLI behavior is unchanged, so `shared-docs/CLI_SPEC.md` is
  unchanged.
- **Checklist:** "Versions match" and "No secrets" are checked. The Node,
  Python and spec items are unchecked, because the diff only touches
  `.github/`.
- **AI usage disclosure:** Claude Code suggests the rules format and simulated
  the PR tests

Diff: 2 files, +58/−0, in 2 commits (`af5fff5`, `4fdfb58`), from
`kwfcfc:feat/32-auto-label` into `main`.

**Maintainer Feedback:**

- 2026-11-09: none yet (0 comments, 0 reviews).

**Status:** Awaiting review

**Toolkit**

- Tool: None
- What it produced: waiting feedback
- Difficulties: external waiting time
- What changed: None

---

## Learnings and Reflections

**Technical Skills Gained**

1. GitHub Actions workflow, especially github-scripts
2. Concepts of auto managing PR and issues with automated labeling tools
3. Diagnoise and analysis ability for real CI/CD issues

**Challenges Overcome**

1. debugging the github-scripts to handle undefined feature injected in the PR
   title
2. manage different accounts and simulate PR triggered with correct privileges.

**What I'd Do Differently Next Time**

1. identify demand first, send more communication to explore more possible
   approaches
2. try other locally available test environment to avoid waiting response from
   external GitHub service

---

## Resources Used

- `actions/labeler` README, https://github.com/actions/labeler: what v7 can
  match (`changed-files`, `head-branch`, `base-branch`, but no titles) and the
  `labeler.yml` format. The issue itself points here.
- GitHub REST API, "Add labels to an issue",
  https://docs.github.com/rest/issues/labels#add-labels-to-an-issue: linked
  from the HTTP 422 error on fork PR #11. It shows that `labels` must be an
  array of strings.
- rafter-cli `CONTRIBUTING.md`,
  https://github.com/Raftersecurity/rafter-cli/blob/main/CONTRIBUTING.md: the
  PR title and body format, the checklist, and the Use of AI section.
- Conventional Commits 1.0.0, https://www.conventionalcommits.org/en/v1.0.0/:
  the `type(scope)!:` format that `TITLE_RE` parses.
