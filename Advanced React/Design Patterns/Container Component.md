# Container Component Pattern

## 📌 What is this?

The **Container Component Pattern** is a design approach where a component (the "container") handles data fetching, state management, or other logic, and passes the results to child components that are focused on presentation.

This separates **data logic** from **UI presentation**, improving modularity and reusability.

## 🧠 Core Idea

- **Container component** (smart):
  - Fetches or manages data
  - Handles side effects (API calls, state updates)
- **Children components** (dumb/presentational):
  - Receive data as props
  - Focus purely on rendering UI
- Container passes data dynamically via props (e.g., using `React.cloneElement`)

## ✅ Advantages

- Clear separation of concerns — container handles data/logic, children handle presentation
- Reusable data-fetching or state logic across multiple components
- Improves maintainability and modularity in large apps
- Children remain simple and focused on UI
- Works with React and Next.js for both client-side and server-side data patterns

---

## ❌ Disadvantages

- Slight overhead from additional wrapper components
- Can become verbose for simple components or one-off cases
- May need careful handling of `React.cloneElement` or dynamic prop injection
- Debugging prop injection issues can be tricky
- Contextual state sharing is less direct than with hooks or context

---

## 🕐 When to Use

- When you need **shared data fetching or state logic** for multiple UIs
- When separating **logic from presentation** improves clarity
- When building **generic container components** usable with any child
- When you want to centralize side effects (API calls, caching)

---

## 💼 Use Cases

- API data fetching for dashboards or forms
- Wrapping multiple presentational components with the same resource
- Stateful wrappers for local storage, session data, or Redux selectors
- Generic list/detail patterns where children only render UI

---

## ⚠️ Caveats

- Avoid over-engineering for simple UI — sometimes direct props suffice
- React.cloneElement requires valid React elements; skip non-elements
- Be aware of unnecessary re-renders if container updates frequently
- For Next.js server components, ensure data fetching is compatible with server/client boundaries
- Testing containers may require mocking async calls

---

## 📊 Pattern Metrics

| Metric               | Rating                                                  |
| -------------------- | ------------------------------------------------------- |
| Developer Ergonomics | High — separation makes components easy to reason about |
| Flexibility          | High — container can wrap any child component           |
| Performance          | Medium — extra render and prop injection overhead       |
| Testability          | High — logic can be tested independently from UI        |
| Reusability          | High — containers can be reused across different UIs    |
| Scalability          | Medium — works well, but complex prop mappings can grow |

## ⚙️ Example

```jsx
/* ---------- App ---------- */
export default function App() {
  return (
    <>
      <DataSource getData={() => fetchData("/users/1")} resourceName="user">
        <UserInfo />
      </DataSource>

      <DataSource
        getData={() => getFromLocalStorage("test")}
        resourceName="msg"
      >
        <Message />
      </DataSource>
    </>
  );
}

/* ---------- Container Component ---------- */
export const DataSource = ({ getData = () => {}, resourceName, children }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return (
    <>
      {React.Children.map(children, (child) => {
        if (React.isValidElement(child)) {
          return React.cloneElement(child, { [resourceName]: resource });
        }
        return child;
      })}
    </>
  );
};

/* ---------- Fetch Functions ---------- */
const fetchData = async (url) => {
  const response = await fetch(url);
  return await response.json();
};

const getFromLocalStorage = (key) => () => {
  return localStorage.getItem(key);
};

/* ---------- Example Presentational Components (schematic) ---------- */
export const UserInfo = ({ user }) => {
  if (!user) return <p className="text-gray-500">Loading user…</p>;
  return (
    <div className="p-4 border rounded bg-gray-50">
      <p>user.name: …</p>
      <p>user.age: …</p>
      <p>user.country: …</p>
    </div>
  );
};

export const Message = ({ msg }) => {
  if (!msg) return <p className="text-gray-500">Loading message…</p>;
  return <h1 className="text-lg font-medium">msg: …</h1>;
};
```
