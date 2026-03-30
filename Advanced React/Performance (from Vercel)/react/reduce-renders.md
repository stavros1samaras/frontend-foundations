# useTransition & useDeferredValue

Both hooks use **Concurrent Mode** to mark renders as low priority, keeping the UI responsive. The difference is how they handle the in-between state and where you have control.

---

## useTransition

Wraps the **setter call**. Gives you an `isPending` flag to handle the loading state yourself.

```jsx
const [isPending, startTransition] = useTransition();

function handleChange(e) {
  setQuery(e.target.value); // urgent — updates immediately

  startTransition(() => {
    setResults(filterItems(allItems, e.target.value)); // non-urgent
  });
}

return (
  <>
    <input value={query} onChange={handleChange} />
    {isPending && <Spinner />}
    <BigList items={results} />
  </>
);
```

- If a new urgent update comes in, it **interrupts** the low-priority render
- You decide what to show in the meantime via `isPending`
- Does not require `<Suspense>`

---

## useDeferredValue

Wraps a **value**. Keeps the old value in the UI until the new render is ready.

```jsx
const deferred = useDeferredValue(query);

return (
  <Suspense fallback={<Spinner />}>
    <Results query={deferred} /> {/* shows stale data instead of spinner */}
  </Suspense>
);
```

- Works with a real `<Suspense>` boundary
- The UI **doesn't break** — it holds the old content until the new render finishes
- Useful when the value comes from a prop and you don't have access to the setter

---

## Comparison

|                           | `useTransition` | `useDeferredValue` |
| ------------------------- | --------------- | ------------------ |
| Wraps                     | setter call     | value              |
| `isPending` flag          | ✅              | ❌                 |
| Works with `<Suspense>`   | ❌              | ✅                 |
| Needs access to setter    | yes             | no                 |
| Good for controlled forms | ❌              | ❌                 |

---

## When to use which

- **You have access to the setter** → `useTransition`
- **Value comes from a prop** → `useDeferredValue`
- **You want `isPending` for a custom loading UI** → `useTransition`
- **You want to hold stale content with Suspense** → `useDeferredValue`

---

## What they are NOT

Neither hook reduces the number of renders — they just make them low priority so the UI stays responsive. For reducing renders use `memo`, `useMemo`, `useCallback`, debounce/throttle.
