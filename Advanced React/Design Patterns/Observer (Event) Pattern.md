# Event / Observer Pattern in React (Minimal Tailwind)

📌 **What is this?**  
The Event (or Observer) Pattern allows components to communicate without direct parent-child relationships. Components emit and listen to events via a central emitter, decoupling sender and receiver.

🧠 **Core Idea**  
- Create a **global event emitter**  
- Components **emit events** without knowing listeners  
- Components **subscribe** to events to react  
- Clean up subscriptions to avoid memory leaks  

⚙️ **Example**

```jsx
/* ---------- App.js ---------- */
import mitt from "mitt";
import Buttons from "./components/Buttons";
import Counter from "./components/Counter";

/* Global emitter */
export const emitter = mitt();

function App() {
  return (
    <div className="p-2 space-y-2">
      <Buttons />
      <Counter />
    </div>
  );
}

export default App;
/* ---------- Buttons.js ---------- */
import { emitter } from "../App";

const Buttons = () => {
  const onIncrement = () => emitter.emit("increment");
  const onDecrement = () => emitter.emit("decrement");

  return (
    <div className="flex gap-1">
      <button onClick={onIncrement}>➕</button>
      <button onClick={onDecrement}>➖</button>
    </div>
  );
};

export default Buttons;

/* ---------- Counter.js ---------- */
import { useEffect, useState } from "react";
import { emitter } from "../App";

const Counter = () => {
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

export default Counter;
