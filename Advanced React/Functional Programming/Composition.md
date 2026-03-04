# Composition

📌 **What is this?**  
The Component Composition pattern is a React technique where you build components by combining smaller, reusable components. Instead of creating many complex components, you compose them together to extend functionality.

🤔 **Why use it?**  
- Promotes reusability and modular design  
- Avoids duplication of code  
- Makes components easier to understand and maintain  
- Allows flexible extension of existing components  

🧠 **Core Idea**  
- Create a base (generic) component  
- Build specialized components on top of it  
- Pass props down and override only what is needed  
- Compose behavior step by step  

⚙️ **Example**

```jsx
import { SmallButton, SmallRedButton } from "./components/composition";

/* ---------- App ---------- */
function App() {
  return (
    <>
      <SmallButton text={"I am small!"} />
      <SmallRedButton text={"I am small and Red"} />
    </>
  );
}

export default App;

/* ---------- Base Component ---------- */
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

export const SmallButton = (props) => {
  return <Button {...props} size={"small"} />;
};

export const SmallRedButton = (props) => {
  return <SmallButton {...props} color={"crimson"} />;
};
