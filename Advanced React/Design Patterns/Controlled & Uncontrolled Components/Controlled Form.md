# Controlled & Uncontrolled Components

## 📌 What is this?

In React, **controlled** and **uncontrolled** components are patterns for handling form inputs and UI elements:

- **Uncontrolled Components:** The DOM maintains the state. React does not directly track input values. Access is done via `refs`.
- **Controlled Components:** React state manages the input values. Every change is handled via `onChange` and stored in `useState`.

This distinction affects flexibility, reusability, and how you handle user input.

## 🧠 Core Idea

- **Uncontrolled:** Let the browser manage state. Access input values with `refs` only when needed.
- **Controlled:** Keep input state in React, updating on every change, giving full control over the UI.

## ✅ When to use

- Use **uncontrolled** when you only need the value on submit and don't need to track it continuously
- Use **controlled** when you need real-time validation, dynamic input manipulation, or integration with other stateful logic
- Prefer **controlled** for most form-heavy UIs where predictability matters

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
