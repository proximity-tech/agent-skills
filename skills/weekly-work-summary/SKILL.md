---
name: weekly-work-summary
description: Summarize a developer's work across repositories over the last seven days using local Git, available GitHub activity, and confirmed Jira issues. Use for a weekly work report or recap.
---

# Weekly Work Summary

Create a work report for the last seven calendar days, ending today. Use the local date and calculate the cutoff as today minus seven days. Explain the substantive work done on each feature across repositories, using commit details as evidence.

## Gather evidence

1. Define the window from local midnight on today minus seven days through the current time, and state the timezone. Discover Git repositories and linked worktrees throughout the current workspace, including `.git` files. Deduplicate worktrees by Git common directory and commits by hash; examine each worktree's status separately. Note inaccessible directories and incomplete or shallow histories.
2. Resolve identity from the user's supplied names, emails and GitHub login, local Git configuration, and authenticated GitHub account when available. Ask for missing identities only when attribution is unclear, and invite the user to add aliases. GitHub usernames do not automatically match Git author emails. Search all available local branches and remote-tracking refs for each known author identity, checking author and committer timestamps against the window. Treat committer-only matches as leads requiring further attribution, since committing or merging another person's work does not establish authorship. Do not fetch or alter repositories.
3. Inspect matching commit messages, timestamps, changed-file summaries, relevant diffs and branch/PR context. Read enough of the actual changes to explain what was implemented and why, where the evidence supports it. Exclude Git notes, stash bookkeeping and routine merge-only activity; retain meaningful integration work when supported by context. Treat uncommitted changes as current, undated leads requiring attribution, rather than dated weekly work. Do not infer when work happened from file timestamps.
4. When an authenticated GitHub integration or `gh` is available, search accessible organizations and repositories for the user's authored pull requests and reviews during the window, including activity on PRs created earlier. Inspect event dates and details to distinguish work during the window from older activity; follow pagination where possible. Use those records to discover repositories absent locally and non-commit contributions. Include issue or PR comments when accessible and attributable. Don't equate a PR updated by someone else with the user's activity. Account for access, search-scope and rate-limit constraints when interpreting results.
5. Look for Jira keys (for example, `ABC-123`) in commits, branches, PRs and project names, and identify broader headings from repository names and repeated themes. Group work across repositories when a shared key, PR link, branch or clear subject/theme supports the connection; label uncertain links. Inspect the actual change summary or PR details when subjects alone are vague. Treat ticket references as leads, not proof of ownership or completion.
6. Ask the user which ticket IDs they specifically worked on during the period. Show candidates and invite corrections or additions, including work with no commit or PR. If the user has already supplied the IDs, use them without asking again. Fetch candidate IDs only once the user identifies or confirms them; if none were found, still ask for IDs to include.

## Enrich with Jira

After the user replies, retrieve each confirmed ticket using the available Jira integration. If using Atlassian tools that require a `cloudId`, resolve it with `getAccessibleAtlassianResources` and use `getJiraIssue` for each key. Fetch only issues the user identified or confirmed. If Jira access is unavailable or a key cannot be retrieved, say so and summarize the Git evidence without inventing ticket details.

Use the Jira summary, status, and description when available to clarify the work. A ticket's current status does not by itself prove that the user completed the work during this week; use Git activity and the user's confirmation for attribution and timing.

## Write the report

Group related work by confirmed Jira ticket or broad project heading, and show the repositories involved. Under each heading, describe the distinct substantive changes in a few concrete bullets, drawing from commit messages and diffs across all related repositories. Explain what changed and its purpose when supported by the evidence; combine related commits and omit routine intermediate revisions. Include meaningful PR and review work when available. Include the reporting window and confirmed Jira keys and summaries. Do not add effort or coverage sections, worklog totals, activity counts, commit time windows, or statements about estimated time. If a source failure materially affects an asserted item, briefly qualify that item rather than claiming unsupported detail. Do not claim impact, completion, or ownership unsupported by the evidence.

Suggested format:

```markdown
## Work Summary — [start date] to [today]

**[KEY-123] — [Jira summary or project heading]**

- [Specific change and its purpose, supported by commits.]
- [Another substantive change across the relevant repositories.]

Repositories: [repo A, repo B]
```
