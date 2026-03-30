# Function as Children Pattern

## 📌 What is this?

The Function as Children is similar to Render Props, but instead of passing a `render` prop, you pass a function directly as the child. The child function receives data or behavior and returns JSX.

This keeps the JSX cleaner and avoids defining a separate `render` prop.

## 🧠 Core Idea

- The component fetches or manages state
- Passes the data to its **child function**
- The child function returns the UI based on that data
- Eliminates the need for a dedicated `render` prop

## ✅ When to use

- When you want to share behavior (mouse position, scroll, data fetching) across - components with different UIs
- When the consumer needs full control over rendering — more explicit than HOCs
- When you prefer a named prop over the children convention (see: Function as Children)

## ⚙️ Example

```jsx
/* ---------- App ---------- */
export default function App() {
  return (
    <DataSourceWithChildren getData={() => fetchData("/users/1")}>
      {(resource) => <UserInfo user={resource} />}
    </DataSourceWithChildren>
  );
}

/* ---------- Generic Component (children as function) ---------- */
export const DataSourceWithChildren = ({ getData = () => {}, children }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return children(resource); // pass data to child function
};
```
