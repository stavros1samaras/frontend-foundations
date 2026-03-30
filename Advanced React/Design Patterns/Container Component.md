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

## ✅ When to use

- When you want to **reuse the same data logic** across multiple different UIs
- When you need a clean separation between **data concerns and rendering**
- When building generic data-fetching wrappers that work with any child component

## ⚙️ Example

```jsx
import React, { useState, useEffect } from "react";

/* ---------- App ---------- */
function App() {
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

export default App;

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
