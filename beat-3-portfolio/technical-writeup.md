# Auto labeler that speeds up PR review process

## Overview

As [repository](https://github.com/Raftersecurity/rafter-cli/) continues to
grow, it becomes tedious for maintainer to manually label every PR to the
correct tags.

## What happened

I designed a GitHub Actions workflow that matches a rule for changed files and
executes a github script for PR titles. The workflow then apples the above two
steps and labels those PR to the existing tags.

The workflow was first tested on my own fork. A Claude code agent opened a few
random pull requests on my fork. It opened PR with correct titles, ill-format
titles, changed files and dummy PRs that don't match any rules. The auto
labeler tried to catch all those cases and labeled them correctly.

The Pull Request were
[merged](https://github.com/Raftersecurity/rafter-cli/pull/356) into main later
with a small modification on pinning down the GitHub Actions commit SHAs. It
now has been a part of the latest draft release of rafter-cli. Before that, it
has already been working to label incoming Pull Requests.

## Limitations and what's next

The GitHub Actions has labeler based on the rules but not for the PR titles.
This requires maintaining a separate set of rules for PR titles. The workflow
does not sync or update the tag status if the content or title of PR changes
later.

Next plan is to design or elaborate on the rules and think how this GitHub
Actions workflow can be implemented for other repositories.
