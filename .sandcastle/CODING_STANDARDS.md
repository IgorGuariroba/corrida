# Coding Standards

The reviewer agent loads these standards from `@.sandcastle/CODING_STANDARDS.md`.

## TypeScript and style

- Keep TypeScript in strict mode and preserve strict compiler checks.
- Do not use `any` unless an external boundary makes it unavoidable; document the reason and narrow the value as soon as possible. Prefer `unknown` for untrusted input.
- Keep functions and modules small, focused, and named by intent.
- Prefer explicit domain types and immutable data where practical.
- Avoid hidden global state and non-deterministic behavior in game rules.

## Architecture

- Separate game rules, state transitions, physics, scoring, and timing from rendering and browser I/O.
- Keep core game logic deterministic and testable without a DOM, canvas, or real clock.
- Put rendering behind a narrow interface; rendering consumes game state but does not own game rules.
- Isolate input, audio, persistence, and other side effects at system boundaries.
- Prefer composition and clear module contracts over inheritance or large multipurpose classes.

## Testing

- Add or update tests for every behavior change, including relevant edge cases and failure paths.
- Test observable behavior rather than private implementation details.
- Use controlled clocks, seeded randomness, or injected dependencies when time or randomness affects behavior.
- Keep tests deterministic, isolated, and descriptive.

## Quality gates

Before code is considered complete, all of these project scripts must pass:

- `npm run typecheck`
- `npm test`
- `npm run build`

Do not bypass or weaken these gates to make a change pass.
