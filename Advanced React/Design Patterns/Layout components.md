# Layout Pattern

## 📌 Layout Pattern

The **Layout Pattern** is a design approach used to organize a user interface into clear, structured sections, where each section can display independent content.

## 🧠 Core Idea

Instead of combining layout and content in the same component:

- A **layout component** is responsible _only for positioning_
- The **content is injected dynamically** (e.g. via `children` or props)

## 🚀 When to Use

- When the same layout structure is reused with different content
- When building scalable UI systems (e.g. dashboards, panels)
- When you want clean separation between structure and data

## ⚙️ Example

### App.jsx

```jsx
export default function App() {
  return (
    <SplitScreen leftWidth={1} rightWidth={3}>
      <LeftSideComp title="Right" />
      <RightSideComp title="Left" />
    </SplitScreen>
  );
}
```

### SplitScreen.jsx

```jsx
const SplitScreen = ({ children, leftWidth = 1, rightWidth = 1 }) => {
  const [left, right] = children;

  return (
    <div className="flex w-full">
      <div style={{ flex: leftWidth }}>{left}</div>
      <div style={{ flex: rightWidth }}>{right}</div>
    </div>
  );
};
```

### Secondary.jsx

```jsx
const LeftSideComp = ({ title }) => {
  return <h2 className="bg-red-600 text-white p-4">{title}</h2>;
};

const RightSideComp = ({ title }) => {
  return <h2 className="bg-yellow-300 p-4">{title}</h2>;
};
```
