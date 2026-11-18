# An auto-labeler that speeds up pull request reviews

## Overview

As the [rafter-cli repository](https://github.com/Raftersecurity/rafter-cli/) grew, maintainers had to spend time labeling incoming pull requests (PRs) by hand. I built a GitHub Actions workflow that automatically classifies new PRs by their titles and changed files, so maintainers can focus on reviewing the changes rather than assigning labels. After testing and revising it in response to a failure and maintainer feedback, my [contribution, PR #356](https://github.com/Raftersecurity/rafter-cli/pull/356), was merged on November 15, 2026, and included in the [v0.12.0 release](https://github.com/Raftersecurity/rafter-cli/releases/tag/v0.12.0) later that day. It has since labeled another contributor's PR automatically.

## What happened

I designed a GitHub Actions workflow—a script GitHub runs whenever a PR is opened or updated—with two labeling jobs. `actions/labeler` checks the files changed in a PR, while `actions/github-script` reads the PR title and maps prefixes such as `feat`, `fix`, `test`, `docs`, and `pattern` to the repository's existing labels. For example, the file-based rules include this excerpt from [`.github/labeler.yml`](https://github.com/Raftersecurity/rafter-cli/blob/main/.github/labeler.yml):

```yaml
secret-pattern:
  - changed-files:
    - any-glob-to-any-file:
      - node/src/scanners/secret-patterns.ts
      - python/rafter_cli/scanners/secret_patterns.py
documentation:
  - changed-files:
    - any-glob-to-any-file: 'recipes/**'
```

Before opening the upstream PR, I tested the workflow on [my fork](https://github.com/kwfcfc/rafter-cli/pulls) with **30 test PRs** submitted through a second account, `jose-C2OaWi`, using Claude Code to simulate first-time contributors. The tests covered expected title prefixes, malformed titles, file-path rules, and edge cases. Selected results were:

| Fork PR | Test case | Observed result |
| --- | --- | --- |
| [#1](https://github.com/kwfcfc/rafter-cli/pull/1) | `feat:` title | `enhancement` label |
| [#6](https://github.com/kwfcfc/rafter-cli/pull/6) | Mixed-case `Feat(scanner)!:` title | `enhancement` label |
| [#9](https://github.com/kwfcfc/rafter-cli/pull/9) | Malformed `feat :` title | No title label |
| [#23](https://github.com/kwfcfc/rafter-cli/pull/23) | File renamed into `recipes/` | `documentation` label |
| [#21](https://github.com/kwfcfc/rafter-cli/pull/21) | Prototype-key regression test, then `feat:` | No label for prototype keys; `enhancement` for `feat:` |

The first version did **not** pass every test. On [fork PR #11](https://github.com/kwfcfc/rafter-cli/pull/11), the title `constructor:` matched the title format, but JavaScript treated `constructor` as an inherited property of the rule object. The script attempted to send an invalid label to GitHub, and the job failed with HTTP 422. I fixed the issue in [commit `4fdfb58`](https://github.com/kwfcfc/rafter-cli/commit/4fdfb580c2b9378821f5cd596765ebd72f26dba4) by checking `Object.hasOwn(map, key)` before looking up a label. I then used [PR #21](https://github.com/kwfcfc/rafter-cli/pull/21) to check `constructor:`, `__proto__:`, `toString:`, and `hasOwnProperty:` followed by a valid `feat:` title. The regression test completed successfully.

I opened [upstream PR #356](https://github.com/Raftersecurity/rafter-cli/pull/356) on November 5. On November 12, maintainer [Rome-1 reviewed it](https://github.com/Raftersecurity/rafter-cli/pull/356#issuecomment-6839852822). Because `pull_request_target` can run with a write-capable token even for PRs submitted from forks, they asked: **“Please pin both actions to full commit SHAs”**. Unlike version tags, full commit SHAs cannot be moved to point at different code. The workflow did not check out or execute contributors' PR code, but pinning the official GitHub Actions further reduced supply-chain risk.

I made the requested change in [commit `35bc5f2`](https://github.com/kwfcfc/rafter-cli/commit/35bc5f2c1612092222a0473904d0380de983ec42), replacing version tags with exact commit hashes:

```diff
- uses: actions/labeler@v7
+ uses: actions/labeler@bf12e9b00b37c5c0ca2b87b79b2daf7891dbda13
- uses: actions/github-script@v9
+ uses: actions/github-script@3a2844b7e9c422d3c10d287c895573f7108da1b3
```

I also added readable version comments (`v7.0.0` and `v9.0.0`) in [commit `b087fe5`](https://github.com/kwfcfc/rafter-cli/commit/b087fe56f85f4a961a0fa3f9b51cddd24bea85a0). I replied to the reviewer, and Rome-1 merged the PR on November 15.

The workflow shipped in the official [v0.12.0 release](https://github.com/Raftersecurity/rafter-cli/releases/tag/v0.12.0) published on November 15, which also listed my contribution under “New Contributors.” Shortly after the release, [another contributor's PR #358](https://github.com/Raftersecurity/rafter-cli/pull/358) was automatically given both `secret-pattern` and `testing` labels by `github-actions[bot]`. This provided a real-world confirmation beyond the fork tests.

## Limitations and what's next

The solution still maintains two sets of rules: `actions/labeler` supports matching changed files and branch names, but not PR titles, so title prefixes require a separate script. The workflow also adds labels without removing outdated ones when a title or set of changed files is updated. For example, in [fork PR #19](https://github.com/kwfcfc/rafter-cli/pull/19), changing the title from `feat:` to `fix:` left both `enhancement` and `bug` labels in place.

My next step is to improve coverage for common PR types. Among the first five upstream PRs opened after the merge, [#367 (`ci(publish):`)](https://github.com/Raftersecurity/rafter-cli/pull/367), [#369 (`release:`)](https://github.com/Raftersecurity/rafter-cli/pull/369), and [#371 (`chore:`)](https://github.com/Raftersecurity/rafter-cli/pull/371) received no labels. I plan to ask the maintainers whether `ci` and `chore` should get explicit mappings, starting by proposing a new `ci` label, which the repository does not currently have. That would extend the workflow using actual unclassified PRs as test cases.

I also want to make this workflow easier to adopt in other repositories. Right now, the title-to-label mappings (such as `feat` to `enhancement`) are hard-coded in `.github/workflows/auto-label.yml`, and the paths in `.github/labeler.yml`, such as `node/src/scanners/secret-patterns.ts` and `recipes/**`, are specific to rafter-cli. I plan to move the title mappings into a configuration file, so another repository could copy the workflow and customize its title mappings and file-path rules without editing the labeling script. My fork tests also showed why setup matters: the missing `testing` and `secret-pattern` labels were initially created with default gray styling, and deleting and recreating them removed those labels from seven test PRs ([#3](https://github.com/kwfcfc/rafter-cli/pull/3), [#5](https://github.com/kwfcfc/rafter-cli/pull/5), [#12](https://github.com/kwfcfc/rafter-cli/pull/12), [#13](https://github.com/kwfcfc/rafter-cli/pull/13), [#15](https://github.com/kwfcfc/rafter-cli/pull/15), [#16](https://github.com/kwfcfc/rafter-cli/pull/16), and [#18](https://github.com/kwfcfc/rafter-cli/pull/18)). As a first step, I will try the configurable workflow in another repository I control, create its required labels in advance, and open sample PRs to check that both title-based and file-based labeling produce the expected results.
