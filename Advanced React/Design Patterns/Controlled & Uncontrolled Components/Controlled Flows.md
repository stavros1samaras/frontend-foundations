# 🔁 Uncontrolled & Controlled Flow Pattern

## 📌 What is this?

This pattern is used in React to manage multi-step UIs (like wizards or forms).

- **Uncontrolled Flow:** The component manages its own state internally.
- **Controlled Flow:** The parent component manages the state and controls the flow.

## 🧠 Core Idea

- Steps are children of a flow component.
- Only one step is rendered at a time (`currentStepIndex`).
- Each step receives a `next()` function to move forward.
- **Uncontrolled:** the flow component keeps state internally.
- **Controlled:** the parent keeps state and can conditionally render steps.

## ✅ Advantages

- Parent has full control over current step and collected data
- Enables conditional steps based on previous step data (e.g. `data.age > 25 && <StepThree />`)
- Progress can be persisted, synced to URL, or sent to an API at any point
- Easy to add back navigation — parent just decrements `currentStepIndex`
- Step logic is fully unit-testable in isolation from the flow container

## ❌ Disadvantages

- More boilerplate — parent must manage both `currentStepIndex` and accumulated `data`
- `React.cloneElement` is fragile — no type safety on injected `next` prop without explicit generics
- Conditional steps shift the children array — requires careful index management
- All step components must be client components in Next.js App Router

## 🕐 When to Use

- When the parent needs to react to step changes (save progress, validate, analytics)
- When steps are conditional based on data collected in previous steps
- When you need URL-synced navigation (Next.js `useRouter` + `currentStepIndex`)
- When you need to support back navigation or arbitrary step jumping

## 💼 Use Cases

- Checkout flows with conditional steps (e.g. skip shipping if digital product)
- KYC / identity verification with branching based on user input
- Onboarding wizards where later steps depend on earlier answers
- Next.js multi-step forms with `?step=2` URL sync
- Admin setup flows where some steps are role-dependent

## ⚠️ Caveats

- **Conditional steps shift indices** — `{data.age > 25 && <StepThree />}` changes the children array length; `React.Children.toArray` rekeys, which can cause remounts
- **No end-of-steps guard** — when `currentStepIndex` exceeds the children count, the component renders nothing; always handle the completion case explicitly
- **Next.js App Router** — wrap in `"use client"`; cloneElement does not work across server/client component boundaries
- **`onDone` is declared but never called** in the example — wire it up when `currentStepIndex` exceeds the last step

## 📊 Pattern Metrics

| Metric               | Uncontrolled                                       | Controlled                                                 |
| -------------------- | -------------------------------------------------- | ---------------------------------------------------------- |
| Developer Ergonomics | High — minimal setup, self-contained               | Medium — parent manages more state                         |
| Flexibility          | Low — no skip logic, no external control           | High — full control from parent                            |
| Reusability          | Medium — flow is reusable, steps are not           | High — parent can swap steps dynamically                   |
| Performance          | Good — single step rendered at a time              | Good — same, with slightly more parent re-renders          |
| Testability          | Medium — must test flow component + steps together | High — parent logic is isolated and easy to unit test      |
| Scalability          | Low — grows painful beyond ~4 steps                | Medium — manageable, but consider XState for complex flows |

## ⚙️ Uncontrolled Example

```jsx
export default function App() {
  return (
    <UncontrolledFlow>
      <StepOne />
      <StepTwo />
      <StepThree />
    </UncontrolledFlow>
  );
}

export const UncontrolledFlow = ({ children, onDone }) => {
  const [data, setData] = useState({});
  const [currentStepIndex, setCurrentStepIndex] = useState(0);

  const currentChild = React.Children.toArray(children)[currentStepIndex];

  const next = () => {
    setCurrentStepIndex(currentStepIndex + 1);
  };

  if (React.isValidElement(currentChild)) {
    return React.cloneElement(currentChild, { next });
  }

  return currentChild;
};

const StepOne = ({ next }) => {
  return (
    <>
      <h1>Step #1</h1>
      <button onClick={next}>Next</button>
    </>
  );
};

const StepTwo = ({ next }) => {
  return (
    <>
      <h1>Step #2</h1>
      <button onClick={next}>Next</button>
    </>
  );
};

const StepThree = ({ next }) => {
  return (
    <>
      <h1>Step #3</h1>
      <button onClick={next}>Next</button>
    </>
  );
};
```

## ⚙️ Controlled Example

```jsx
export default function App() {
  const [data, setData] = useState({});
  const [currentStepIndex, setCurrentStepIndex] = useState(0);

  const next = (dataFromStep) => {
    setData((prev) => ({ ...prev, ...dataFromStep }));
    setCurrentStepIndex((s) => s + 1);
  };

  return (
    <>
      <ControlledFlow currentStepIndex={currentStepIndex} onNext={next}>
        <StepOne />
        <StepTwo />
        {data.age > 25 && <StepThree />}
      </ControlledFlow>
    </>
  );
}

export const ControlledFlow = ({
  children,
  onDone,
  currentStepIndex,
  onNext,
}) => {
  const next = (data) => {
    onNext(data);
  };

  const currentChild = React.Children.toArray(children)[currentStepIndex];

  if (React.isValidElement(currentChild)) {
    return React.cloneElement(currentChild, { next });
  }

  return currentChild;
};

const StepOne = ({ next }) => {
  return (
    <>
      <h1>Step #1: Enter your name</h1>
      <button onClick={() => next({ name: "TestName" })}>Next</button>
    </>
  );
};
const StepTwo = ({ next }) => {
  return (
    <>
      <h1>Step #2: Enter your age</h1>
      <button onClick={() => next({ age: 30 })}>Next</button>
    </>
  );
};
const StepThree = ({ next }) => {
  return (
    <>
      <h1>Step #3: You qualify!</h1>
      <button onClick={() => next({})}>Next</button>
    </>
  );
};
```
