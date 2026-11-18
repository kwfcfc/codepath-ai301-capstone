I recently got my first contribution to rafter-cli merged!

I built a GitHub Actions workflow that automatically labels pull requests (PRs) based on their titles and changed files when they match the repository's rules. This helps maintainers quickly understand the scope of incoming PRs without manually categorizing each one.

Before submitting my contribution, I tested the workflow with 30 PRs on my fork and fixed an edge case the tests uncovered. I also made a security improvement based on the maintainer's feedback.

The PR was merged on November 15, 2026, and included in the official v0.12.0 release later that day. The workflow has already labeled another contributor's PR!

Next, I plan to move the title-to-label mappings into a configuration file so other repositories can adapt the workflow to their own rules. I'll first create the required labels in another repository I control and open test PRs to verify that the workflow works as expected.

https://github.com/Raftersecurity/rafter-cli/pull/356
