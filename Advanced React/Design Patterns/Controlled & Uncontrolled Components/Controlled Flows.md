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

## ✅ When to use

- Multi-step forms, onboarding flows, or wizards
- When steps are sequential and isolated from each other
- Use **uncontrolled** when the parent doesn't need to know the current step
- Use **controlled** when the parent needs to react to step changes (e.g. save progress, validate, skip steps)

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
    setData(dataFromStep);
    setCurrentStepIndex(currentStepIndex + 1);
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
