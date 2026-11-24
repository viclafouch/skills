---
name: start-issue
description: Start a GitHub issue and its companions from a fresh base branch, then route the build to tdd, a plain implement loop, or diagnosing-bugs.
argument-hint: "<GitHub issue number, e.g. 42>"
disable-model-invocation: true
---

Take an issue from GitHub to a reviewed working tree, ready to commit. The run stops at the first red gate and names its cause.

**The base** is the repo's default branch: `git symbolic-ref --short refs/remotes/origin/HEAD`, minus its `origin/` prefix.

## 1. Prepare

Run this first, with no question, whatever branch `HEAD` sits on. The base is fixed, so it is never a choice to offer. A branch left behind keeps its commits, and untracked files ride along. Only a modified or staged tracked file waits for the user.

```sh
git fetch origin <base> && git switch <base> && git merge --ff-only origin/<base>
```

In a worktree, `<base>` is often checked out by another worktree and `git switch <base>` refuses. Run `git switch --detach origin/<base>` instead: step 3 branches from there.

Then **install**: the project's own install and code generation, the way its scripts run them, such as `<pm> install && <pm> run --if-present generate` with the package manager its lockfile names. A failed fetch, merge or install stops the run.

**Done when** `git rev-parse HEAD` equals `git rev-parse origin/<base>`, installed.

## 2. Load

Run `load-issue` on the argument.

A startable verdict of no stops the run, with its cause.

The run takes every companion of the brief on its own initiative, and names them in one line: they share the branch, the build and the PR, and their tensions join the issue's.

Each tension of the brief goes to the user, one AskUserQuestion per tension. Write each call into the description of the issue it belongs to, with `gh issue edit <number> --body-file -`: the issue changes first, the code follows.

Then read in full the product docs the project keeps, such as a vision or a glossary, when it has some. They carry the product's vision and words, and the build serves them.

**Done when** the brief is shown, every tension is settled in the description, every product doc is read, and the issue can start.

## 3. Branch

The branch is the issue's linked branch, so GitHub links it, and the PR opened from it, to the issue on its own.

- No linked branch (`gh issue develop <number> --list` is empty): `gh issue develop <number> --base <base> --checkout`.
- The linked branch exists: switch to it, `git pull --ff-only`, rebase it on `origin/<base>`, then install again.

**Done when** `HEAD` sits on the linked branch, based on today's `<base>`, installed.

## 4. Route

Pick one path from the issue's **Done when**, and say which one in one line, with the reason.

- **diagnose**: a bug whose cause the issue does not name. Run `mattpocock-skills:diagnosing-bugs` first. Its root cause then routes to **tdd**.
- **tdd**: the issue adds or changes behaviour that a public seam can observe, such as a bug with a known cause, a new rule, function, hook or component state.
- **implement**: the **Done when** is iso, such as a refactor, a migration, a dependency bump, tooling, config or docs. The existing tests and the typecheck are the net.

An issue that mixes both runs **tdd** on its behaviour slice and **implement** on the rest.

**Done when** the path is named.

## 5. Build

- **tdd**: run `mattpocock-skills:tdd`. Its seams get your confirmation before the first test.
- **implement**: a change repeated across many files runs as a codemod first, other work in small slices. After each run or slice, run the typecheck and the test files next to the code you touched.

At the end, run the project's lint fix, typecheck and full unit tests, the way its scripts run them, on every package the diff touches and its dependents. A shared config reaches its dependents, so their lint is where its new rules land.

**Done when** every **Done when** line of the issue and of its companions is met by the diff, and lint, typecheck and tests are green.

## 6. Review

Run `mattpocock-skills:code-review` since `<base>`, with the issue and its companions as the spec. Fix the findings that are real, and check them again with the step 5 commands.

**Done when** the review shows no open finding, or each one left has its reason.

## 7. Hand-off

Show the changed files and one line per **Done when**, the companions' included, with the code that meets it. Say the files are ready to read in the editor, and wait for the green light. Then commit, and offer to open the PR carrying a `Closes #<number>` line for the issue and for each companion: through the repo's own pull-request skill when it has one, else `gh pr create` with its body written by `mattpocock-skills:pr`.
