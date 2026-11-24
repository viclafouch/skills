---
name: load-issue
description: GitHub issue brief from its live state: a startable verdict, its companions, its tensions, and the drift between its description and the code. Use when an issue number comes up to work on, or to check whether it can start.
argument-hint: required GitHub issue (e.g., 42, #42, owner/repo#42 or URL)
---

Load a GitHub issue so the session starts knowing what is true today.

**Prose proposes, the code decides.** Paths and symbols written inside descriptions rot. Every state printed here is read live from GitHub, and every quoted path from the base. Descriptions are read for intent only.

## 1. Setup

Read the argument as `42`, `#42`, `owner/repo#42` or an issue URL, otherwise ask for a valid issue. A bare number belongs to the current repository (`gh repo view --json nameWithOwner`). When the working directory is a clone of the issue's repository, fetch **the base**, its default branch (`git symbolic-ref --short refs/remotes/origin/HEAD`): `git fetch origin <base>`.

## 2. Fetch

`gh issue view <number> -R <owner/repo> --json number,title,body,state,stateReason,labels,assignees,comments,closedByPullRequestsReferences,url`. Then the issues and PRs that mention this one, from the `cross-referenced` events of its timeline (`gh api repos/<owner>/<repo>/issues/<number>/timeline --paginate`), and its dependencies (`gh api repos/<owner>/<repo>/issues/<number>/dependencies/blocked_by`, and `.../blocking`).

Done when the issue's `state`, the state of each PR in `closedByPullRequestsReferences`, each issue that mentions it and each dependency are read.

## 3. Rule

- **Mentions.** Read each open issue or PR that mentions this one, at the part that names it, and keep what it adds here: a source, a dependency, a decision.
- **Shared links.** Open again each link a comment shares, and name what changed since the comment was posted: a new release, a moved page, a dead link.
- **Companions.** An open issue tied to this one, through a mention, a dependency or the same code, is a **companion** when one PR can carry both and stay one coherent change to review. Name each companion and what ties it. An open blocker is a companion first, so the PR carries it instead of waiting for it.
- **Tensions.** A comment, a shared link or an issue that mentions this one can go against what the description decides. Name each **tension**: the decided point, what goes against it, and where each side comes from. The user settles it.
- **Drift.** With the base fetched, grep every path and symbol quoted in the description against `origin/<base>` (`git grep <pattern> origin/<base>`) and flag the stale ones.
- **Can it start?** Yes when the issue is `OPEN`, no open PR sits in `closedByPullRequestsReferences`, and every open blocker rides as a companion. Otherwise name the state, the open PR and its author, or the blocker.

## 4. Brief

Free prose in the user's language, `:` or `,` where a dash would go, headings as the issue earns them. Carry the number and title, the description in a few sentences, the labels and assignees, what the comments settled, and every finding of step 3. Stay silent on anything the issue has nothing for.

## Rules

Analysis only: the one write is the step 1 `fetch`, and the working tree and the current branch stay as they are. Follow the issue, its comments and the issues that mention it, nothing beyond.
