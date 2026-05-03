# Claude Code /loop Prompts

Three production-tested `/loop` workflows from [Alireza Rezvani's article](https://towardsdatascience.com/how-to-use-claude-codes-loop-to-run-ai-agents-on-autopilot/) on running Claude Code agents on autopilot.

## 1. PR Babysitting

Watches your CI pipeline, catches and fixes failures, and pings you when a PR is ready for human review.

```bash
claude /loop "check open PRs on the current branch. If CI is failing,
read the error logs, fix the issue, and push. If CI passes and the PR
has no requested changes, post a comment saying 'Ready for human review.'
Summarize what you did in the PR description." --every 30m --for 2d
```

## 2. Dependency Monitoring

Runs `npm audit`, patches high/critical vulnerabilities, verifies tests pass, and opens PRs with CVE details.

```bash
claude /loop "run npm audit. If any high or critical vulnerabilities exist,
create a branch, update the affected packages, run the test suite, and
open a PR if tests pass. Include the vulnerability details in the PR body."
--every 4h --for 3d
```

## 3. Daily Standup Digest

Summarizes all commits merged to main in the last 24 hours and saves a Markdown standup report.

```bash
claude /loop "summarize all commits merged to main in the last 24 hours.
Include: PR titles, authors, files changed count, and any test coverage
changes. Write the summary as a Markdown standup update and save it to
./reports/standup-$(date +%Y-%m-%d).md" --every 24h --for 3d
```
