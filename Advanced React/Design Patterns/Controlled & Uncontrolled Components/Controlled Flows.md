# 🔁 Uncontrolled & Controlled  Flow Pattern

## 📌 What is this?
**Uncontrolled Flow** is a React pattern where a multi-step UI (like a wizard or step form) manages its own flow internally.

- The parent just provides the steps (`children`)
- The flow component controls:
  - which step is active
  - when to move to the next step

👉 In simple terms: *the flow logic is hidden inside the component*


## 🤔 Why use it?
- No need to manage state in the parent
- Cleaner and simpler code
- Great for:
  - multi-step forms
  - onboarding flows
  - simple step-by-step UI


## 🧠 Core Idea
- Convert `children` into an array
- Keep a `currentStepIndex`
- Render only the current step
- Inject a `next` function into each step

👉 Steps don’t control the flow — they just call `next()`


## ⚙️ Uncontrolled Example

### Uncontrolled Flow Component
```jsx
import React, { useState } from "react";

import { UncontrolledFlow } from "./components/uncontrolled-flow";

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

function App() {
  return (
    <UncontrolledFlow>
      <StepOne />
      <StepTwo />
      <StepThree />
    </UncontrolledFlow>
  );
}

export default App;

------------------------------------------------------------

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
```

## ⚙️ Controlled Example

```jsx

import { useState } from "react";
import { UncontrolledFlow } from "./components/uncontrolled-flow";
import { ControlledFlow } from "./components/controlled-flow";

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

const StepFour = ({ next }) => {
  return (
    <>
      <h1>Step #4: Enter your country</h1>
      <button onClick={() => next({ country: "Poland" })}>Next</button>
    </>
  );
};

function App() {
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
        <StepFour />
      </ControlledFlow>
    </>
  );
}

export default App;

import React, { useState } from "react";

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
```
