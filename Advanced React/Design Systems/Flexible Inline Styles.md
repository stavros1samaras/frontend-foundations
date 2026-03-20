# Generic Container Component with Inline Props

A lightweight React component that allows passing any CSS property directly as a prop.

```jsx
// Generic Box that applies all props as inline styles and className
const Box = ({ children, className, ...props }) => {
  return (
    <div className={className} style={{ ...props }}>
      {children}
    </div>
  );
};

// Aliases for convenience
export const Grid = (props) => <Box display="grid" {...props} />;
export const Flex = (props) => <Box display="flex" {...props} />;
export const Section = (props) => <Box {...props} />;

// Usage Examples:

<Grid className="my-grid" gap="10px" padding="20px" backgroundColor="#f0f0f0">
  <div>Item 1</div>
  <div>Item 2</div>
</Grid>

<Flex className="my-flex" gap="8px" justifyContent="center">
  <div>Item A</div>
  <div>Item B</div>
</Flex>
```

# Flexible Grid Component with Inline Styles

A lightweight React component for creating a grid layout, allowing custom inline styles via props.

```jsx
import React from "react";

const GridBox = ({ children, gap = "16px", ...rest }) => {
  return (
    <div style={{ display: "grid", gap, ...rest }}>
      {children}
    </div>
  );
};

export default GridBox;

// Usage
<GridBox gap="10px" padding="20px" backgroundColor="#f0f0f0">
  <div>Item 1</div>
  <div>Item 2</div>
</GridBox>
```

