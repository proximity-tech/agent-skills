# Proximity agent skills

Reusable skills for Codex. Currently this repository contains **weekly-work-summary**, which creates a report from a developer's recent Git activity, available GitHub activity, and Jira tickets they confirm.

## Install

In Codex, ask:

> `$skill-installer` Install `skills/weekly-work-summary` from `proximity-tech/agent-skills` on GitHub.

Or run the Codex skill installer from a terminal:

```sh
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo proximity-tech/agent-skills \
  --path skills/weekly-work-summary \
  --ref main
```

You need access to this repository and GitHub credentials configured for it. The installer supports private repositories through existing Git credentials or `GH_TOKEN` / `GITHUB_TOKEN`. It installs the skill in `~/.codex/skills/weekly-work-summary` by default. It won't overwrite an existing installation; remove or update an older copy deliberately before reinstalling.

If your Proximity GitHub account uses an SSH host alias such as `proximity-github.com`, you can instead clone with that alias and copy the skill:

```sh
git clone git@proximity-github.com:proximity-tech/agent-skills.git
mkdir -p ~/.codex/skills
test ! -e ~/.codex/skills/weekly-work-summary && cp -R agent-skills/skills/weekly-work-summary ~/.codex/skills/
```

If the destination already exists, review it before replacing it. The alias must already be configured in your SSH config.

## Generate a report

Start Codex in the parent directory containing the repositories you want to include, then enter:

```text
$weekly-work-summary Create my work summary for the past week.
```

The skill searches local repository history, uses accessible GitHub pull requests and reviews when available, asks which Jira tickets you worked on, and fetches those confirmed tickets. Share any Git author emails or GitHub usernames that differ from your local Git configuration. A connected Jira integration is needed for Jira enrichment; GitHub access is needed for GitHub activity. Local Git history remains useful when those connections aren't available.

The report groups work by ticket or project and describes substantive changes from commits and related evidence. The skill uses only information available to the current user, so share work that is not recorded in those sources when prompted.

## Repository layout

```text
skills/weekly-work-summary/SKILL.md   Skill instructions
AGENTS.md                             Guidance for contributors using agents
```
