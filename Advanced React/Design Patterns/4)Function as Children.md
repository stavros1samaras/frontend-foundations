# Function as Children Pattern

## 📌 What is this?

The Function as Children is similar to Render Props, but instead of passing a `render` prop, you pass a function directly as the child. The child function receives data or behavior and returns JSX.

This keeps the JSX cleaner and avoids defining a separate `render` prop.

## 🤔 Why use it?

- Simplifies the API by using the `children` prop  
- Keeps JSX concise and readable  
- Separates data/logic from presentation  
- Fully composable and reusable

## 🧠 Core Idea

- The component fetches or manages state  
- Passes the data to its **child function**  
- The child function returns the UI based on that data  
- Eliminates the need for a dedicated `render` prop

## ⚙️ Example

```jsx
import React, { useState, useEffect } from "react";

/* ---------- App ---------- */
function App() {
  return (
    <DataSourceWithChildren getData={() => fetchData("/users/1")}>
      {(resource) => <UserInfo user={resource} />}
    </DataSourceWithChildren>
  );
}

export default App;

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
