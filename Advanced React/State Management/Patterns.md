# React State Updates Cheat Sheet

When working with **React state** that is an **object** or **array**, you should **never modify it directly**. Always create a **new object/array** to trigger a re-render.

---

## Object

```js
const [user, setUser] = useState({ name: "Sam", age: 21 });

// Updating a single property
setUser((prev) => ({
  ...prev,
  age: prev.age + 1,
}));

// Updating multiple properties
setUser((prev) => ({
  ...prev,
  name: "Alex",
  age: 22,
}));
```

## Array

```jsx
const [todos, setTodos] = useState(["task1", "task2"]);

// Adding an item
setTodos((prev) => [...prev, "task3"]);

// Removing an item
setTodos((prev) => prev.filter((todo) => todo !== "task1"));
```

## Array of Objects

```jsx
const [todos, setTodos] = useState([
  { id: 1, task: "Buy milk", done: false },
  { id: 2, task: "Do homework", done: false },
]);

//  Updating a single object
setTodos((prev) =>
  prev.map((todo) => (todo.id === 2 ? { ...todo, done: true } : todo)),
);

// Adding a new object
setTodos((prev) => [...prev, { id: 3, task: "Go for a run", done: false }]);
```

## Key Tip

Always create a new object or array when updating state. React detects the change by reference and triggers a re-render.
