# Agent Skills

A collection of agent skills that extend capabilities across planning, development, and code review.

**Install all skills at once:**

```
npx skills@latest add viclafouch/skills -a claude-code
```

## Planning & Design

These skills help you think through problems before writing code.

- **deep-dive** — Interview relentlessly about a specific phase of the plan until reaching shared understanding. Walks down each branch of the design tree, resolving dependencies between decisions one-by-one.

  ```
  npx skills@latest add viclafouch/skills/deep-dive -a claude-code
  ```

## Development

These skills help you write, refactor, and maintain code.

- **update-deps** — Audit all outdated dependencies with detailed research on changelogs, breaking changes, bug fixes, and deprecations. Creates a temporary plan without updating anything.

  ```
  npx skills@latest add viclafouch/skills/update-deps -a claude-code
  ```

## Code Review

These skills help you review and improve existing code.

- **react-useeffect** — Audit React components for unnecessary useEffect hooks. Identifies anti-patterns like derived state, chained effects, event-driven effects and suggests better alternatives.

  ```
  npx skills@latest add viclafouch/skills/react-useeffect -a claude-code
  ```

- **web-design-guidelines** — Review UI code for Web Interface Guidelines compliance. Checks accessibility, UX patterns, and design best practices.

  ```
  npx skills@latest add viclafouch/skills/web-design-guidelines -a claude-code
  ```

## Useful Commands

```bash
npx skills check                # Check for available updates
npx skills update               # Update all skills to latest versions
npx skills list                 # List installed skills (project)
npx skills ls -g                # List installed skills (global)
npx skills find [query]         # Search for skills interactively
npx skills remove               # Remove a skill interactively
npx skills init my-skill        # Scaffold a new SKILL.md
npx skills add viclafouch/skills --list   # List available skills without installing
npx skills add viclafouch/skills -g       # Install globally (~/.claude/skills/)
```
