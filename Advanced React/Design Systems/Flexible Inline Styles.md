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
