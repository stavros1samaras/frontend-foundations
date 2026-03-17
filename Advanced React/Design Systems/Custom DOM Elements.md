# Custom DOM Elements for Better Control

Instead of using native HTML elements directly (`h1`, `p`, `code`, etc.), we can create **wrapper components** around them.

This adds a small abstraction layer that helps with:

* consistent styling
* centralized control
* cleaner component usage

For example, instead of writing:

```html
<h1>Hello World</h1>
```

we can use a custom component:

```tsx
<H1>Hello World</H1>
```



## Example

Example `H1` component with **Tailwind styles** and **props support**:

```tsx
type H1Props = {
  children: React.ReactNode
  size?: "sm" | "md" | "lg" | "xl"
}

export const H1 = ({ children, size = "lg" }: H1Props) => {
  const sizes = {
    sm: "text-2xl",
    md: "text-3xl",
    lg: "text-4xl",
    xl: "text-5xl",
  }

  return (
    <h1 className={`font-bold tracking-tight ${sizes[size]}`}>
      {children}
    </h1>
  )
}
```

# Example Set of Custom Elements

| Component    | Underlying Element |
| ------------ | ------------------ |
| `H1`         | `h1`               |
| `H2`         | `h2`               |
| `H3`         | `h3`               |
| `H4`         | `h4`               |
| `P`          | `p`                |
| `Lead`       | `p`                |
| `Blockquote` | `blockquote`       |
| `InlineCode` | `code`             |


This pattern keeps typography **consistent**, **reusable**, and **easy to control** across the codebase.

