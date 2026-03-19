# Columns Pattern

A simple grid system using React and inline styles.


## Components

### Columns - Column

```jsx
const Columns = ({ children, columns = 4, gap = "24px" }) => (
  <div
    style={{
      display: "grid",
      gridTemplateColumns: `repeat(${columns}, 1fr)`,
      gap: gap,
    }}
  >
    {children}
  </div>
);

// columns: number of columns in the grid (default 4)
// gap: space between columns (default "24px")

const Column = ({ children, span = 1 }) => (
  <div
    style={{
      gridColumn: `span ${span} / auto`,
    }}
  >
    {children}
  </div>
);

// span: number of columns this column should span (default 1)
```
### Example Usage

```jsx
<Columns columns={4} gap="32px">
  <Column span={3}>
    <InputGroup htmlFor="firstName" label="First Name">
      <input type="text" id="firstName" />
    </InputGroup>
  </Column>

  <Column span={1}>
    <InputGroup htmlFor="lastName" label="Last Name">
      <input type="text" id="lastName" />
    </InputGroup>
  </Column>

  <Column span={4}>
    <InputGroup htmlFor="email" label="Email">
      <input type="text" id="email" />
    </InputGroup>
  </Column>
</Columns>
```
