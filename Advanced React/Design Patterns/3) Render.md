# Render Props Pattern

## 📌 What is this?

The **Render Props Pattern** is a design approach where a component provides data or behavior to its children via a function (the "render prop"). Instead of defining UI inside the component, you pass a function that returns JSX, allowing flexible and reusable composition.

This separates **data/logic** from **presentation**, similar to container components, but gives more control to the consumer via a callback.


## 🤔 Why use it?

- Provides maximum flexibility for rendering  
- Allows different presentations of the same data  
- Keeps data fetching or state logic separate from UI  
- Encourages composable and reusable patterns


## 🧠 Core Idea

- The **data component** fetches or manages state  
- Instead of children elements, it exposes a **render function**  
- The consumer passes a function that receives the data and returns JSX  
- This makes the component reusable for multiple presentations

## ⚙️ Example

```jsx
import React, { useState, useEffect } from "react";

/* ---------- App ---------- */
function App() {
  return (
    <DataSourceWithRenderProps
      getData={() => fetchData("/users/1")}
      render={(resource) => <UserInfo user={resource} />}
    />
  );
}

export default App;

/* ---------- Generic Render Props Component ---------- */
export const DataSourceWithRenderProps = ({ getData = () => {}, render }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return render(resource);
};
