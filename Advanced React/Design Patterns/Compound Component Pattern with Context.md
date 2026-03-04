# Compound Component Pattern with Context

📌 **What is this?**  
The Compound Component pattern allows you to build a parent component with multiple subcomponents that communicate via React Context. This pattern keeps related components together and allows shared state or props without prop drilling.

🤔 **Why use it?**  
- Groups related components (Header, Body, Footer) logically  
- Shares state easily between subcomponents using Context  
- Keeps UI flexible and composable  
- Clean API for consumers  

🧠 **Core Idea**  
- Create a parent component with a Context provider  
- Build child components that consume Context  
- Export child components as properties of the parent  
- Users can compose the children in any order inside the parent  

⚙️ **Example with Tailwind CSS**

```jsx
import { createContext, useContext } from "react";

const Context = createContext(null);

/* ---------- Subcomponents ---------- */
const Body = ({ children }) => {
  return <div className="p-2">{children}</div>;
};

const Header = ({ children }) => {
  const { test } = useContext(Context);
  return (
    <div className="border-b border-black p-2 mb-2 flex justify-between items-center">
      {children}
      <span>{test}</span>
    </div>
  );
};

const Footer = ({ children }) => {
  return (
    <div className="border-t border-black p-2 mt-2 flex justify-end gap-2">
      {children}
    </div>
  );
};

/* ---------- Parent Component ---------- */
const Card = ({ test, children }) => {
  return (
    <Context.Provider value={{ test }}>
      <div className="border border-black rounded-md">{children}</div>
    </Context.Provider>
  );
};

export default Card;

/* ---------- Export Compound Components ---------- */
Card.Header = Header;
Card.Body = Body;
Card.Footer = Footer;
