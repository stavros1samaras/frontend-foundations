# Event / Observer Pattern in React (Minimal Tailwind)

## 📌 What is this?

The **Event / Observer Pattern** lets components communicate without any direct parent-child relationship. A global event emitter acts as the message bus — components emit events without knowing who's listening, and listeners react without knowing who emitted.

## 🧠 Core Idea

- A **global emitter** (e.g. `mitt`) is created once and shared across the app
- **Emitters** fire named events with optional payload — no coupling to receivers
- **Subscribers** listen for events and react, cleaning up in the `useEffect` return
  ⚙️ **Example**

## ✅ Advantages

- Decouples components — no direct parent-child relationship needed
- Lightweight pub/sub mechanism without a full state manager
- Easy to add new listeners or emitters anywhere in the app
- Works well for **cross-cutting concerns** like notifications, analytics, or keyboard shortcuts
- Integrates seamlessly with React and Next.js

---

## ❌ Disadvantages

- Global state can become hard to track in large apps
- Debugging can be challenging — event flow is implicit
- Overuse can lead to unpredictable side effects
- Cleanup is necessary to avoid memory leaks (`useEffect` cleanup)
- Not type-safe unless TypeScript or proper typings are used

---

## 🕐 When to Use

- When components are **far apart in the component tree**
- When passing props or using context is awkward or impractical
- For **lightweight, decoupled cross-cutting events**
- When you want a simple **pub/sub mechanism** without Redux or Zustand

---

## 💼 Use Cases

- Global notifications / toasts
- Analytics or logging events
- Keyboard shortcuts or global input handlers
- Cross-component messaging in dashboards or complex layouts
- Toggling shared UI states (e.g., modals, sidebars)

---

## ⚠️ Caveats

- Always **unsubscribe in cleanup** to prevent memory leaks
- Avoid overusing for tightly-coupled components — props/context is simpler
- Keep payloads simple and well-documented
- Consider TypeScript interfaces for event types for safety
- Event order and timing can introduce subtle bugs if not handled carefully

---

## 📊 Pattern Metrics

| Metric               | Rating                                                                    |
| -------------------- | ------------------------------------------------------------------------- |
| Developer Ergonomics | Medium — easy to implement, harder to trace events                        |
| Flexibility          | High — listeners and emitters are independent                             |
| Performance          | High — lightweight, minimal overhead                                      |
| Testability          | Medium — requires mocking emitter or spying on events                     |
| Reusability          | High — emitter can be used anywhere in the app                            |
| Scalability          | Medium — works well for moderate apps, can get chaotic in very large apps |

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
