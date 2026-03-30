# Event / Observer Pattern in React (Minimal Tailwind)

## 📌 What is this?

The **Event / Observer Pattern** lets components communicate without any direct parent-child relationship. A global event emitter acts as the message bus — components emit events without knowing who's listening, and listeners react without knowing who emitted.

## 🧠 Core Idea

- A **global emitter** (e.g. `mitt`) is created once and shared across the app
- **Emitters** fire named events with optional payload — no coupling to receivers
- **Subscribers** listen for events and react, cleaning up in the `useEffect` return
  ⚙️ **Example**

## ✅ When to use

- When components are **far apart in the tree** and connecting them via props or context would be awkward
- For truly **decoupled, cross-cutting events** (e.g. notifications, analytics, keyboard shortcuts)
- When you need lightweight pub/sub without pulling in a full state manager

```jsx
/* ---------- App.js ---------- */
/* Global emitter */
export const emitter = mitt();

export default function App() {
  return (
    <div className="p-2 space-y-2">
      <Buttons />
      <Counter />
    </div>
  );
}

/* ---------- Buttons.js ---------- */
export default function Buttons () {
  const onIncrement = () => emitter.emit("increment");
  const onDecrement = () => emitter.emit("decrement");

  return (
    <div className="flex gap-1">
      <button onClick={onIncrement}>➕</button>
      <button onClick={onDecrement}>➖</button>
    </div>
  );
};

/* ---------- Counter.js ---------- */
export default function Counter () {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const handleIncrement = () => setCount((c) => c + 1);
    const handleDecrement = () => setCount((c) => c - 1);

    emitter.on("increment", handleIncrement);
    emitter.on("decrement", handleDecrement);

    return () => {
      emitter.off("increment", handleIncrement);
      emitter.off("decrement", handleDecrement);
    };
  }, []);

  return <div className="font-bold">Count: {count}</div>;
};
```
