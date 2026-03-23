# Higher-Order Component (HOC)

📌 **What is this?**  
The HOC pattern is a React technique where you take a component and "wrap" it in a function to add behavior or data. Instead of changing the component’s UI, the HOC adds logic and returns a new component.

⚙️ **Example**

```jsx
import { checkProps } from "./components/check-props";
import { UserInfo } from "./components/user-info";

/* ---------- Wrap Component with HOC ---------- */
const UserInfoWrapper = checkProps(UserInfo);

/* ---------- App ---------- */
function App() {
  return (
    <>
      <UserInfoWrapper propA="test1" blabla={{ a: 1, age: 23 }} />
    </>
  );
}

export default App;

/* ---------- Generic HOC Function ---------- */
export const checkProps = (Component) => {
  return (props) => {
    console.log(props); // added behavior
    return <Component {...props} />; // returns the original component with props
  };
};
```

⚙️ **Example**

```jsx
import { LargeRedButton, SmallButton } from "./components/partial";

function App() {
  return (
    <>
      <SmallButton text={"I am small!"}/>
      <LargeRedButton text="I am large and Red"/>
    </>
  );
}

export default App;
-----------------------------------------------

export const partial = (Component, partialProps) => {
  return (props) => {
    return <Component {...partialProps} {...props} />;
  };
};

export const Button = ({ size, color, text, ...props }) => {
  return (
    <button
      style={{
        fontSize: size === "large" ? "25px" : "16px",
        backgroundColor: color,
      }}
    >
      {text}
    </button>
  );
};

export const SmallButton = partial(Button, { size: "small" });

export const LargeRedButton = partial(Button, {
  size: "large",
  color: "crimson",
});

```
