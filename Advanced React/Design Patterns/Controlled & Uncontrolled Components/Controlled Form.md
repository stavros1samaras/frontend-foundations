# Controlled & Uncontrolled Components

## 📌 What is this?

In React, **controlled** and **uncontrolled** components are patterns for handling form inputs and UI elements:

- **Uncontrolled Components:** The DOM maintains the state. React does not directly track input values. Access is done via `refs`.
- **Controlled Components:** React state manages the input values. Every change is handled via `onChange` and stored in `useState`.

This distinction affects flexibility, reusability, and how you handle user input.

## 🧠 Core Idea

- **Uncontrolled:** Let the browser manage state. Access input values with `refs` only when needed.
- **Controlled:** Keep input state in React, updating on every change, giving full control over the UI.

## ✅ Advantages

- Full control over every input value — UI always reflects React state
- Enables real-time validation, conditional rendering, and derived state
- Easy to integrate with other stateful logic (e.g. disable submit until valid)
- Straightforward to test — assert state values directly without querying the DOM
- Predictable behavior — single source of truth in React state

## ❌ Disadvantages

- Re-renders on every keystroke — can hurt performance on large forms
- More boilerplate — every field needs `value` + `onChange`
- `useEffect` for validation adds an extra render cycle; synchronous validation in the handler is more efficient
- Scales poorly without a form library (React Hook Form, Zod) beyond ~5 fields

## 🕐 When to Use

- When you need real-time validation or inline error feedback
- When input values drive other UI (e.g. disabling a button, filtering a list)
- When form state needs to be shared with parent components or other logic
- Prefer controlled for most form-heavy UIs where predictability matters

## 💼 Use Cases

- Login / signup forms with inline validation
- Search inputs with live filtering or debounce
- Multi-step forms passing accumulated data between steps
- Forms where submit button should be disabled until all fields are valid
- Any input that affects other parts of the UI in real time

## ⚠️ Caveats

- **`useEffect` for validation runs after render** — for synchronous validation on submit, validate inside the handler directly instead
- **`value` without `onChange` makes the input read-only** — React will warn and the user can't type; always pair them
- **Don't switch between controlled and uncontrolled** — changing `value` from `undefined` to a string throws a React warning and causes unpredictable behavior
- **For large forms**, reach for React Hook Form — it uses uncontrolled inputs under the hood and avoids per-keystroke re-renders while keeping a controlled-like API

## 📊 Pattern Metrics

| Metric               | Rating                                                       |
| -------------------- | ------------------------------------------------------------ |
| Developer Ergonomics | Medium — more wiring per field, but intuitive                |
| Flexibility          | High — full control over every keystroke and value           |
| Performance          | Medium — re-render on every change; use RHF for large forms  |
| Testability          | High — state lives in React, easy to assert                  |
| Reusability          | High — logic lives in state and handlers, easy to extract    |
| Scalability          | Medium — manageable up to ~5 fields; use RHF/Zod beyond that |

## ⚙️ Examples

### Uncontrolled Form

```jsx
export const UncontrolledForm = () => {
  const nameRef = createRef();
  const ageRef = createRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Name:", nameRef.current.value);
    console.log("Age:", ageRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={nameRef} type="text" />
      <input ref={ageRef} type="number" />
      <button type="submit">Submit</button>
    </form>
  );
};
```

### Controlled Form with Validation

```jsx
export const ControlledForm = () => {
  const [name, setName] = useState("");
  const [age, setAge] = useState("");
  const [error, setError] = useState("");

  useEffect(() => {
    if (name.length < 1) {
      setError("The name cannot be empty");
    } else {
      setError("");
    }
  }, [name]);

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Name:", name);
    console.log("Age:", age);
  };

  return (
    <form onSubmit={handleSubmit}>
      {error && <p>{error}</p>}
      <input
        name="name"
        type="text"
        placeholder="Enter name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <input
        name="age"
        type="number"
        placeholder="Enter age"
        value={age}
        onChange={(e) => setAge(e.target.value)}
      />
      <button type="submit">Submit</button>
    </form>
  );
};
```
