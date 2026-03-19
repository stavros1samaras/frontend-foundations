# Layers Pattern

The **Layers pattern** is a simple and flexible way to stack elements vertically while maintaining consistent spacing. It is ideal for forms, cards, or any grouped content.

This version uses **inline styles** and allows the developer to set a custom `gap` directly via a prop.

## React Component

```jsx
// Layers.jsx
import React from "react";

const Layers = ({ children, gap = "16px" }) => {
  return (
    <div style={{ display: "grid", gap }}>
      {children}
    </div>
  );
};

export default Layers;
```

## Example Usage

```jsx
// SubscribeForm.jsx
import React from "react";
import Layers from "./Layers";

const SubscribeForm = () => {
  return (
    <Layers gap="5px">
      <Layers gap="10px">
        <h2>Subscribe To Our Newsletter</h2>
        <p>
          Subscribe to our newsletter to keep up to date on all our amazing
          products.
        </p>
      </Layers>

      <Layers gap="8px">
        <Layers gap="4px">
          <label htmlFor="name">Name</label>
          <input type="text" id="name" />
        </Layers>

        <Layers gap="4px">
          <label htmlFor="email">Email</label>
          <input type="text" id="email" />
        </Layers>

        <button>Subscribe</button>
      </Layers>
    </Layers>
  );
};

export default SubscribeForm;
```
