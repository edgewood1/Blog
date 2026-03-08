Sure — here’s a shorter, clearer guide with small examples you can copy-paste and use immediately.

## What they do (plain English)
- Omit<T, K> — take type T and remove the properties named in K. Use it when you want a T-like object but without some fields (e.g., remove server-only fields like `id`).
- Partial<T> — make every property of T optional. Use it for building fixtures, patch/update payloads, or when you only care about a few fields.

Both are TypeScript compile-time helpers only — no runtime behavior changes.

## Tiny definitions (mental model)
- Omit<T, K> ≈ “T minus keys K”
- Partial<T> ≈ “every field on T is optional”

## Minimal code examples

Type to start with:
```ts
type Achievement = {
  id: number;
  title: string;
  earned: boolean;
  meta: { createdAt: string };
};
```

Omit example:
```ts
type PublicAchievement = Omit<Achievement, 'id' | 'meta'>;
// PublicAchievement is { title: string; earned: boolean }
```

Partial example:
```ts
type MaybeAchievement = Partial<Achievement>;
// MaybeAchievement is { id?: number; title?: string; earned?: boolean; meta?: { createdAt: string } }
```

Combine them for an update payload or test fixture:
```ts
type UpdateAchievement = Partial<Omit<Achievement, 'id'>>;
// id removed and remaining fields optional
const update: UpdateAchievement = { title: 'New title' }; // valid
```

## How it maps to your code/tests
- `Achievements[number]` — this gives the element type of an array type named `Achievements`. Useful when `Achievements` is an array type and you want the type of one achievement.
- In tests you often saw casts like:
  `base as unknown as Readonly<Achievements[number]>`
  Instead of `as any`, prefer building fixtures using `Partial<...>` or a factory that returns a properly-typed object.

Example test fixture:
```ts
const base: Partial<Achievements[number]> = {
  achievementID: 22,
  title: 'progressor',
  toAchieveText: 'Keep going',
};
```

## Important gotchas
- Partial is shallow: nested objects remain unchanged. Example:
  ```ts
  type X = { a: { b: number } };
  Partial<X> = { a?: { b: number } } // inner b is still required
  ```
  Use a DeepPartial helper if you want recursion.
- Omit on unions can be surprising — test the result if you’re omitting from union types.
- These are compile-time only; using them won't strip properties at runtime.

## Useful utilities & snippets

DeepPartial (recursive, but simple):
```ts
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};
```
(Refine it if you want to exclude functions or arrays specially.)

Read-only property on a prop:
```ts
type Props = { readonly achievement: Achievements[number] };
```
This prevents code in the component from accidentally mutating `achievement`.

## Quick decision guide
- You need a variant of a type with a few fields removed → Omit<T, 'x' | 'y'>.
- You need to pass an object that may not include every field → Partial<T>.
- You need a nested partial for deep fixtures → make/ use DeepPartial<T>.
- Want to avoid casts in tests? Build typed factories returning Partial<T> or full T.

If you want, I can:
- Convert a test file to use `Partial<>` fixtures and remove `as any` casts, or
- Add a small test factory helper in your `__tests__` folder to produce typed achievements.

Which would you prefer?