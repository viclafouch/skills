# Agent Skills

A collection of agent skills that extend capabilities across planning, development, and code review.

**Install all skills at once:**

```
npx skills@latest add viclafouch/skills
```

## Planning & Design

These skills help you think through problems before writing code.

- **deep-dive** — Interview relentlessly about a specific phase of the plan until reaching shared understanding. Walks down each branch of the design tree, resolving dependencies between decisions one-by-one.

  ```
  npx skills@latest add viclafouch/skills/deep-dive
  ```

## Development

These skills help you write, refactor, and maintain code.

- **update-deps** — Audit all outdated dependencies with detailed research on changelogs, breaking changes, bug fixes, and deprecations. Creates a temporary plan without updating anything.

  ```
  npx skills@latest add viclafouch/skills/update-deps
  ```

## Code Review

These skills help you review and improve existing code.

- **react-useeffect** — Audit React components for unnecessary useEffect hooks. Identifies anti-patterns like derived state, chained effects, event-driven effects and suggests better alternatives.

  ```
  npx skills@latest add viclafouch/skills/react-useeffect
  ```

- **web-design-guidelines** — Review UI code for Web Interface Guidelines compliance. Checks accessibility, UX patterns, and design best practices.

  ```
  npx skills@latest add viclafouch/skills/web-design-guidelines
  ```
