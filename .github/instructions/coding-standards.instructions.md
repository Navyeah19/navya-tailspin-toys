---
description: 'Shared commenting, documentation, and TypeScript standards'
applyTo: '**/*.{ts,astro,css}'
---

# Coding Standards

## Comments and Documentation

- Comment intent, constraints, and non-obvious decisions; do not restate what the code already says.
- Keep comments close to the code they explain, and update or remove them whenever the related code changes. An outdated comment is a bug.
- Use TSDoc/JSDoc for every exported function in `db/` and `src/lib/`. Describe the function's purpose, every parameter (including injectable `db` arguments), and the return value. Link to related types when that makes the contract clearer.
- Document reusable Astro component `Props` interfaces with property-level comments when a prop's purpose, accepted values, default, or rendering effect is not obvious. Keep the interface itself clear and self-explanatory.
- Prefer naming and types that explain straightforward behavior instead of adding explanatory comments.

```ts
/**
 * Return games in title order so static route generation is reproducible.
 *
 * @param db Drizzle client used to query the game's data.
 * @returns Games mapped to the application-facing shape.
 */
export async function getAllGames(db: Database): Promise<Game[]> {
  // Query ordering is part of the build-time contract, not presentation logic.
  return queryGames(db);
}
```

## TypeScript Formatting

- Use two spaces for indentation, single quotes for strings, semicolons, and trailing commas in multiline literals and parameters.
- Use `interface` for object contracts and explicit parameter and return types for exported functions.
- Use `import type` for type-only imports and avoid `any`; narrow unknown values with a type guard instead.
- Keep lines readable and format related declarations consistently. ESLint enforces the core punctuation, quote, spacing, and control-flow rules; run `npm run lint` through the `quality-checks` skill.
