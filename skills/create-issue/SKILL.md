---
name: create-issue
description: Create a GitHub issue. Use when the user gives the go on the issues shaped in the conversation (one run per issue), or asks to file something in GitHub.
user-invocable: true
argument-hint: <problem-or-topic>
---

Create one GitHub issue per run, through the `gh` CLI. A fresh session picks the issue up later with nothing but the issue, so the issue is evergreen: it names the objective and its finish line, official docs carry the reader the rest of the way, and nothing in it rots at the next commit.

## Definition of done

The run is done when the issue exists in GitHub and its `gh issue view` read-back shows every item of this checklist. Tick each item against the read-back.

- [ ] Title and description, written to step 4
- [ ] Sources, every link checked in step 3
- [ ] Repository
- [ ] Labels
- [ ] Assignee

Mark any item you could not confirm, and say where you looked.

Report one line: number, URL, then every checklist item with its value.

## When to stop and ask

Keep going on your own through every step. Stop only in these cases:

- `gh` is missing from the session, or `gh auth status` fails: tell the user and end the run.
- Two repositories fit the issue equally.

Ask with AskUserQuestion, one question per case, your pick as the first option.

## Batch runs

In an issue session the user shapes several issues, then says go. The go approves every issue discussed in the session: create each issue in turn.

- Before the first issue, order the batch so each issue that another one names comes before it. The later issue takes the earlier issue's number from its read-back.
- After the last issue, post one table: number, title, repository, labels, assignee, URL.

## Step 1: Settle the scope

First read in full the product docs the repo's `AGENTS.md` points to. The issue serves their vision and speaks their words.

An issue shaped in this conversation arrives settled: take its facts and decisions as they stand.

Otherwise, explore the codebase until you know what changes and where it stops. When it could mean several things, or the scope could be one file or fifty, run `mattpocock-skills:grilling` on the open decisions, with your findings as settled facts.

One issue is one PR. Work that needs two PRs becomes two issues.

An issue that retires a pattern ships its **lock**, or names the issue right after it that does.

Done when the product docs are read, and the issue has one objective, one boundary, one PR of work, and its lock where one is due.

## Step 2: Resolve the fields

| Field | Source |
|---|---|
| Repository | The repository the issue's PR changes: the current one (`gh repo view --json nameWithOwner`) when it fits, else the best fit in `gh repo list --no-archived`. |
| Labels | What the conversation says, else the topic labels the repository's neighbouring issues carry. When a label is missing in the repository, pick the closest one and say so. |
| Assignee | What the conversation says, else `@me`. |

Done when every field has a value.

## Step 3: Gather the sources

The sources are the fresh session's way in: official documentation for every tool, library, API or standard the issue touches. Collect as many as the issue supports: the vendor's docs, the spec, the release notes.

When the doc site serves an `llms-full.txt` or an `llms.txt` at its root, it is the first link.

Prefer the markdown variant of each page: swap the extension for `.md`, or append `.md` when there is none. Keep the `.md` URL only when it answers `200` with a `text/markdown` or `text/plain` content type, because some sites answer `200` with HTML on any path. Else keep the original. Keep only the links that answer `200`.

Done when each thing the issue touches has its official link, or you have said that none exists.

## Step 4: Write the issue

Write the whole issue in English, title included, whatever the language of the conversation.

Evergreen means names, never snapshots. Exports, packages and config files appear by name in backticks. Code blocks, counts, measurements and line numbers go stale at the first commit, so none of them appear: the fresh session measures on its own branch.

The issue says what changes and where it stops, and leaves the how to the session that takes it. A design choice the issue leaves open is named as "this issue's call".

The issue fits on one screen: most run near 120 words, few past 200. An issue that grows past that holds two issues.

The structure, with illustrative content:

~~~~
Every frontend import of `isEmpty` from `@repo/utils` moves to `isEmpty` from `es-toolkit/compat`. `@repo/utils` stops exporting `isEmpty`.

Read [llms-full.txt](https://es-toolkit.dev/llms-full.txt) first, then the [`isEmpty` page](https://es-toolkit.dev/compat/reference/predicate/isEmpty.md).

**Check**: the compat `isEmpty` follows lodash, and returns `true` for a number or a boolean. Check the type of the value at each call site.

**Done when**

* No frontend package imports `isEmpty` from `@repo/utils`
* `@repo/utils` no longer holds `isEmpty` or its test
* The behaviour is iso-prod

A backend package that imports `isEmpty` stops the issue: comment here.
~~~~

- The opening states the objective in 1 to 3 sentences.
- The sources line comes next, in reading order.
- **Codemod**, before **Check**, for a change repeated across many files: the script's path, or that writing it comes first.
- **Check** holds the gotcha a fresh session would miss. Leave it out when there is none.
- **Done when** is the finish line: 2 to 4 bullets, each one a state the session can check on its branch. The lock is one of them, as `@repo/utils` no longer holding `isEmpty` is above.
- The stop line names the case that ends the issue early, and says to comment on the issue.

The title is an imperative objective of about 6 words, lowercase after the prefix, with names in backticks:

- One package: the package name, then the objective. `hooks: add useMediaQuery`
- The objective already names the package: no prefix. ``Replace `isEmpty` of `@repo/utils` with es-toolkit``

## Step 5: Create and read back

Create the issue with every field of step 2, the description on stdin:

```sh
gh issue create -R <repo> --title <title> --body-file - --label <label> --assignee <login>
```

Then read it back with `gh issue view <number> -R <repo> --json title,body,labels,assignees,url`, and tick the definition of done.
