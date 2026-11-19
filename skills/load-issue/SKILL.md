---
name: load-issue
description: GitHub issue brief with its live state, a startable verdict and the drift between its description and the code. Use when an issue number comes up to work on, or to check whether it can start.
argument-hint: required GitHub issue (e.g., 42, #42, owner/repo#42 or URL)
---

Load a GitHub issue so the session starts knowing what is true today.

**Prose proposes, the code decides.** Paths and symbols written inside descriptions rot. Every state printed here is read live from GitHub, and every quoted path from the base. Descriptions are read for intent only.

## 1. Setup

Read the argument as `42`, `#42`, `owner/repo#42` or an issue URL, otherwise ask for a valid issue. A bare number belongs to the current repository (`gh repo view --json nameWithOwner`). Then fetch **the base**, the repo's default branch (`git symbolic-ref --short refs/remotes/origin/HEAD`): `git fetch origin <base>`. The drift check of step 3 reads it as `origin/<base>`, and runs only when the working directory is a clone of the issue's repository.

## 2. Fetch

`gh issue view <number> -R <owner/repo> --json number,title,body,state,stateReason,labels,assignees,comments,closedByPullRequestsReferences,url`, alone. Done when the issue's `state` and the state of each PR in `closedByPullRequestsReferences` are read.

## 3. Rule

- **Can it start?** Yes when the issue is `OPEN` and no open PR sits in `closedByPullRequestsReferences`. Otherwise name the state, or the open PR and its author.
- **Drift.** Grep every path and symbol quoted in the description against `origin/<base>` (`git grep <pattern> origin/<base>`) and flag the stale ones. Where a comment changes the description's scope, the latest comment wins, in one line.

## 4. Brief

Free prose in the user's language, `:` or `,` where a dash would go, headings as the issue earns them. Carry the number and title, the description in a few sentences, the startable verdict, the labels and assignees, what the comments settled, and the stale paths. Stay silent on anything the issue has nothing for.

## Rules

Analysis only: the one write is the step 1 `fetch`, and the working tree and the current branch stay as they are. Follow the issue and its comments, nothing beyond.
