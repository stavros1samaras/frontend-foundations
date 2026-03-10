# Using `as const` in Custom Hooks

When returning a tuple from a custom hook like `[state, setState]`, TypeScript by default may infer a general array type:

```ts
const [url, setUrl] = useUrl("google.com"); 
// Type: (string | Dispatch<SetStateAction<string>>)[]
```

By adding as const:
```ts
return [url, setUrl] as const;
```

TypeScript infers a readonly tuple:
```
readonly [string, Dispatch<SetStateAction<string>>]
```

This preserves the exact type and order of elements.
It enables accurate destructuring and better type safety.
