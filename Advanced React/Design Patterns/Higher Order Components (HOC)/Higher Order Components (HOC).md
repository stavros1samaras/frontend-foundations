# Higher-Order Component (HOC)

📌 **What is this?**  
The HOC pattern is a React technique where you take a component and "wrap" it in a function to add behavior or data. Instead of changing the component’s UI, the HOC adds logic and returns a new component.

🤔 **Why use it?**  
- Allows reuse of logic without changing the UI  
- Can add logging, validation, auth checks, analytics, etc.  
- Keeps the UI clean and separates concerns  
- Makes it easy to extend multiple components with the same behavior  

🧠 **Core Idea**  
- Take a component as input  
- Wrap the component in a function  
- Add behavior or data  
- Return a new component with the same UI but enhanced functionality  

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
