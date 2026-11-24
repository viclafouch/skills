---
name: file-lead
description: Files a lead from the tech watch (veille), such as a link, an X post or a screenshot, into the GitHub issues of the current repository. Use when the user shares a find to keep for later.
argument-hint: <link-or-find>
---

A **lead** is a find from the user's tech watch: a repository, a blog post, an X post, a screenshot. You are a **clerk**: you note what was found and what it brings to the project, at the place where the work will meet it. The topic may start in a week or in three months, when the source may have moved on, and the session that takes it then weighs the lead on its own merits, from its latest state.

## 1. Read the lead

Read each source, and the screenshots the user gives. X serves a post without a login through the endpoint behind its embeds: `https://cdn.syndication.twimg.com/tweet-result?id=<post-id>&token=a`, with the text in `text` and the photos in `mediaDetails`.

Several finds about the same thing are one lead.

Done when you can say, for each lead, what it is, what it is for, and what it brings.

## 2. Place it

Read enough of the project to see where the lead fits: its README, its open issues, and its milestones when it has some. Then pick:

- **An open issue on the same topic**: a comment there.
- **No such issue**: a new issue, with the labels and the milestone of the repository that fit, when it has some.

When two places fit equally, or the repository takes no issues, ask, your pick first. A link already in the issue is filed: skip it.

## 3. Write

In the language of the repository's issues, so that a reader who opens the issue months later sees at a glance what the lead brings:

- A short description of the project, package or service.
- What it could serve in this project, and which part.
- The advantages it brings, one per line.
- The user's take, only when they gave one, as theirs.

Keep to what stays true over months: versions, numbers and setup stay in the source.

An image that helps to see the lead, from the user or from the source, goes in with `gh`'s `--attach`. On a public repository, the images show the find, not people.

## 4. Report

One line per lead: where it went, with its URL.
