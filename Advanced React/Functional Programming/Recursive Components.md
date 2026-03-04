# Recursive Component

📌 **What is this?**  
The Recursive Component pattern is a technique in React where a component calls itself to render nested or hierarchical data. It is commonly used for structures like trees, menus, JSON objects, or comments.

🤔 **Why use it?**  
- Perfect for rendering deeply nested data  
- Eliminates the need for complex loops  
- Keeps the code clean and scalable  
- Works for unknown or dynamic depth structures  

🧠 **Core Idea**  
- Check if the current data is a base value (primitive)  
- If yes → render it directly  
- If not → iterate over its entries  
- For each entry → call the same component again (recursion)  
- This continues until all nested levels are rendered  

⚙️ **Example**

```jsx
const isValidObj = (data) => typeof data === "object" && data !== null;

export const Recursive = ({ data }) => {
  if (!isValidObj(data)) {
    return <li>{data}</li>;
  }

  const pairs = Object.entries(data);
  console.log(data);

  return (
    <>
      {pairs.map(([key, value]) => {
        return (
          <li>
            {key}:
            <ul>
              <Recursive data={value} />
            </ul>
          </li>
        );
      })}
    </>
  );
};

import { Recursive } from "./components/recursive";

const myNestedObject = {
  key1: "value1",
  key2: {
    innerKey1: "innerValue1",
    innerKey2: {
      innerInnerKey1: "innerInnerValue1",
      innerInnerKey2: "innerInnerValue2",
    },
  },
  key3: "value3",
};

function App() {
  return (
    <>
      <Recursive data={myNestedObject} />
    </>
  );
}

export default App;
