## Why
To **centralize colors** for the app, avoid magic strings, and ensure **consistency** across components.


## How
- Each color is an **object** with numbered shades (`100`, `200`, `300`, …)
- Exported as **constants** so they can be reused anywhere in the app
- Example: `blue[100]` → `#03045e`


## Color Constants Example

```ts
export const blue = {
  100: "#03045e",
  200: "#0804b8",
  300: "#030086",
  400: "#5f25a4",
  500: "#5f25a4",
};

export const red = {
  100: "#e5383b",
  200: "#ba181b",
  300: "#a4161a",
};

export const yellow = {
  100: "#E1C542",
  200: "#faa307",
  300: "#f48c06",
};

export const balanced = {
  100: "#ffffff",
  200: "#F0F0F0",
  300: "#D0D0D0",
  400: "#6E707F",
  500: "#43454E",
  600: "#111111",
};
```
## App.jsx
``` jsx
export const App = () => {
  return (
    <div style={{ backgroundColor: blue[100], padding: '1rem' }}>
      <h1 style={{ color: red[100] }}>Hello World</h1>
      <p style={{ color: yellow[100] }}>Dynamic colors example</p>
      <button style={{ backgroundColor: balanced[100], color: blue[200], padding: '0.5rem 1rem' }}>
        Click
      </button>
    </div>
  );
};
