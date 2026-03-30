# Generic Container Component with Inline Props

A lightweight React component that allows passing any CSS property directly as a prop.

- className → for responsive classes, media queries, Tailwind, etc.
- props → for fixed styles that don't change with screen size

```jsx
// General Div that gets the styles from props
const Div = ({ children, className, ...props }) => {
  return (
    <div className={className} style={{ ...props }}>
      {children}
    </div>
  );
};

// Grid: display grid
export const Grid = ({ className = "", ...props }) => {
  const defaultStyles = "sm:grid-cols-1 md:grid-cols-3";
  const combinedStyles = `${defaultStyles} ${className}`.trim();
  return <Div display="grid" className={combinedStyles} {...props} />;
};

// Flex: display flex
export const Flex = ({ className = "", ...props }) => {
  const defaultStyles = "flex-col sm:flex-row";
  const combinedStyles = `${defaultStyles} ${className}`.trim();

  return <Div display="flex" className={combinedStyles} {...props} />;
};
```

## Usage Examples:

```jsx
// Grid with default responsive columns (1 column small, 3 medium+)
<Grid
  gap="10px"
  padding="20px"
  backgroundColor="#f0f0f0"
>
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</Grid>

{/* Grid with user override of columns */}
<Grid
  className="sm:grid-cols-2 lg:grid-cols-4" // override default columns
  gap="10px"
  padding="20px"
>
  <div>Item A</div>
  <div>Item B</div>
  <div>Item C</div>
  <div>Item D</div>
</Grid>

<Flex
  className="flex-col md:flex-row justify-center"
  gap="8px"
  padding="16px"
  backgroundColor="#e0f7fa"
>
  <div>Item A</div>
  <div>Item B</div>
  <div>Item C</div>
</Flex>
```

# Flexible Grid Component with Inline Styles

A lightweight React component for creating a grid layout, allowing custom inline styles via props.

```jsx
export default function GridBox({ children, gap = "16px", ...rest }) {
  return <div style={{ display: "grid", gap, ...rest }}>{children}</div>;
}

// Usage
<GridBox gap="10px" padding="20px" backgroundColor="#f0f0f0">
  <div>Item 1</div>
  <div>Item 2</div>
</GridBox>;
```
