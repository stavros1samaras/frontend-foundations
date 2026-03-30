# Layout Pattern

## 📌 Layout Pattern

The **Layout Pattern** is a design approach used to organize a user interface into clear, structured sections, where each section can display independent content.

## 🧠 Core Idea

Instead of combining layout and content in the same component:

- A **layout component** is responsible _only for positioning_
- The **content is injected dynamically** (e.g. via `children` or props)

## ✅ Advantages

- Clear separation of **structure vs content**
- Reusable layout across multiple screens or components
- Flexible — content can vary while maintaining consistent layout
- Improves maintainability in large UI systems (dashboards, admin panels)
- Works seamlessly with React and Next.js (server or client rendering)

---

## ❌ Disadvantages

- May require extra boilerplate for simple one-off layouts
- Limited flexibility if layout needs to change dynamically per child
- Can be confusing if children order matters but is not enforced
- Less useful for deeply nested or highly dynamic UIs
- Minor performance overhead from additional wrapper components

---

## 🕐 When to Use

- When a **layout structure is reused** with different content
- When building **scalable UI systems**
- When you want **clean separation of layout and data/content**
- When multiple screens/components share the same structural design

---

## 💼 Use Cases

- Split screens, sidebars, dashboards
- Panels with header/body/footer layout
- Responsive grid layouts with dynamic content
- Multi-column forms or wizard steps
- Layouts where content changes but structure remains consistent

---

## ⚠️ Caveats

- Ensure children are passed in the expected order (e.g., `[left, right]`)
- Avoid over-nesting layout components for readability
- Dynamic content sizing may require extra styling logic
- Not ideal for highly dynamic, unpredictable layouts
- TypeScript users may need tuple typing for `children`

---

## 📊 Pattern Metrics

| Metric               | Rating                                                 |
| -------------------- | ------------------------------------------------------ |
| Developer Ergonomics | High — simple, clear separation of concerns            |
| Flexibility          | Medium — fixed structure, flexible content             |
| Performance          | High — minimal overhead                                |
| Testability          | High — layout can be tested independently from content |
| Reusability          | High — same layout works with multiple components      |
| Scalability          | High — works well for large UI systems                 |

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
