# 🧩 Higher Order Components (HOC) 

## 📌 What is this?
A **Higher Order Component (HOC)** is a **function that takes a component and returns a new, enhanced component**.

- You can think of HOCs as **component factories**: functions that generate new components when called.
- They allow you to add extra functionality or share logic between multiple components without modifying the originals.

👉 In simple terms: *HOCs are functions that return components*

---

## 🤔 Why use HOCs?

### 1. Share behavior across components
- Similar to container components that wrap multiple components and give them shared behavior.
- HOCs let you reuse logic for multiple components without duplicating code.

### 2. Add functionality to existing components
- Enhance legacy or third-party components with new features without touching their original code.
- Examples: logging, data fetching, authorization, styling wrappers.

---

## 🧠 Core Idea
- Pass a component to a HOC
- The HOC returns a **new component** that:
  - wraps the original component
  - adds additional behavior
  - passes through props

```jsx
const EnhancedComponent = withExtraBehavior(OriginalComponent);
