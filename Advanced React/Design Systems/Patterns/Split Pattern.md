# Split Pattern

A React component for creating a grid layout with configurable **column fractions** and **gap**, using inline styles instead of styled-components.

```jsx
// Predefined fraction mappings
const fractions = {
  "1/4": "1fr 3fr",
  "1/3": "1fr 2fr",
  "1/2": "1fr 1fr",
  "2/3": "2fr 1fr",
  "3/4": "3fr 1fr",
  "auto-start": "auto 1fr",
  "auto-end": "1fr auto",
};

// Generic Split component
export const Split = ({ children, fraction = "1/2", gap = "16px" }) => {
  const columns = fractions[fraction] || fractions["1/2"];
  return (
    <div style={{ display: "grid", gap, gridTemplateColumns: columns }}>
      {children}
    </div>
  );
};
```

## Example Usage

```jsx
export const InfoForm = () => {
  return (
    <Split fraction="1/3" gap="24px">
      <div>
        <h3>General Information</h3>
        <span>
          All the information you provide via this form will be exposed to the
          public.
        </span>
      </div>
      <Form />
    </Split>
  );
};
```
