# Layout Pattern

## 📌 What is this?

The **Layout Pattern** is a design approach used to organize a user interface into distinct sections or regions, where each section can display independent content.

It focuses on structuring the UI consistently and clearly, without being tied to any specific implementation or technology.

## 🤔 Why use it?

- Promotes reusable layout components
- Separates layout logic from content
- Allows flexible control over proportions (e.g. equal or asymmetric layouts)
- Encourages better component composition

## 🧠 Core Idea

Instead of combining layout and content in the same component:

- A **layout component** is responsible only for positioning
- Content is injected dynamically (e.g. via `children` or props)

This makes the layout reusable across different use cases.

## 🚀 When to Use

- When you need side-by-side layouts
- When the same layout structure is reused with different content
- When building scalable UI systems (e.g. dashboards, panels)
- When you want clean separation between structure and data

## ⚙️ Example

### App.jsx
``` jsx
export default function App() {
  return (
    <SplitScreen leftWidth={1} rightWidth={3}>
      <LeftSideComp title="Right" />
      <RightSideComp title="Left" />
    </SplitScreen>
  );
}
```
### SplitScreen.jsx
``` jsx
const SplitScreen = ({ children, leftWidth = 1, rightWidth = 1 }) => {
  const [left, right] = children;

  return (
    <div className="flex w-full">
      <div style={{ flex: leftWidth }}>
        {left}
      </div>
      <div style={{ flex: rightWidth }}>
        {right}
      </div>
    </div>
  );
};
```
### Secondary.jsx
``` jsx
const LeftSideComp = ({ title }) => {
  return (
    <h2 className="bg-red-600 text-white p-4">
      {title}
    </h2>
  );
};

const RightSideComp = ({ title }) => {
  return (
    <h2 className="bg-yellow-300 p-4">
      {title}
    </h2>
  );
};
```

## ⚙️ Example

### App.jsx
``` jsx
/* ---------- Example App Usage ---------- */
function export default App() {
  const books = [
    { name: "To Kill a Mockingbird", pages: 281, title: "Harper Lee", price: 12.99 },
    { name: "The Catcher in the Rye", pages: 224, title: "J.D. Salinger", price: 9.99 },
    { name: "The Little Prince", pages: 85, title: "Antoine de Saint-Exupéry", price: 7.99 },
  ];

  const authors = [
    { name: "Sarah Waters", age: 55, country: "UK", books: ["Fingersmith", "The Night Watch"] },
    { name: "Haruki Murakami", age: 71, country: "Japan", books: ["Norwegian Wood", "Kafka on the Shore"] },
    { name: "Chimamanda Ngozi Adichie", age: 43, country: "Nigeria", books: ["Half of a Yellow Sun", "Americanah"] },
  ];

  return (
    <>
      <RegularList items={authors} ItemComponent={SmallAuthorItem} itemPropName="author" />
      <NumberedList items={authors} ItemComponent={LargeAuthorItem} itemPropName="author" />
      <RegularList items={books} ItemComponent={SmallBookItem} itemPropName="book" />
      <NumberedList items={books} ItemComponent={LargeBookItem} itemPropName="book" />
    </>
  );
}
```
### Secondary.jsx
``` jsx
/* ---------- Generic List Components ---------- */
export const RegularList = ({ items, ItemComponent, itemPropName }) => {
  return (
    <>
      {items.map((item, i) => (
        <ItemComponent key={i} {...{ [itemPropName]: item }} />
      ))}
    </>
  );
};

export const NumberedList = ({ items, ItemComponent, itemPropName }) => {
  return (
    <>
      {items.map((item, i) => (
        <div key={i}>
          <h3>{i + 1}</h3>
          <ItemComponent {...{ [itemPropName]: item }} />
        </div>
      ))}
    </>
  );
};

/* ---------- Example Item Components ---------- */
export const SmallBookItem = ({ book }) => {
  return (
    <h2>
      {book.name} / {book.price}
    </h2>
  );
};

export const LargeBookItem = ({ book }) => {
  return (
    <>
      <h2>{book.name}</h2>
      <p>Price: {book.price}</p>
      <p>Author: {book.title}</p>
      <p># of Pages: {book.pages}</p>
    </>
  );
};

export const SmallAuthorItem = ({ author }) => {
  return <p>Name: {author.name}, Age: {author.age}</p>;
};

export const LargeAuthorItem = ({ author }) => {
  return (
    <>
      <h2>{author.name}</h2>
      <p>Age: {author.age}</p>
      <p>Country: {author.country}</p>
      <h3>Books</h3>
      <ul>
        {author.books.map((book) => (
          <li key={book}>{book}</li>
        ))}
      </ul>
    </>
  );
};
```


## ⚙️ Example
### App.jsx
``` jsx
export default function App() {
  return (
    <Modal>
      <ExampleContent />
    </Modal>
  );
}
```
### Modal.jsx
``` jsx
export const Modal = ({ children }) => {
  const [show, setShow] = useState(false);

  return (
    <>
      <button
        className="px-4 py-2 bg-blue-600 text-white rounded"
        onClick={() => setShow(true)}
      >
        Show Modal
      </button>

      {show && (
        <div
          className="fixed inset-0 bg-black/60 flex justify-center items-start overflow-auto"
          onClick={() => setShow(false)}
        >
          <div
            className="mt-24 w-1/2 bg-white p-6 rounded shadow-lg"
            onClick={(e) => e.stopPropagation()}
          >
            <button
              className="mb-4 px-3 py-1 bg-red-500 text-white rounded"
              onClick={() => setShow(false)}
            >
              Hide Modal
            </button>
            {children}
          </div>
        </div>
      )}
    </>
  );
};
```
### Content.jsx
```jsx
export const ExampleContent = () => {
  return <h2 className="text-xl font-semibold">This is some modal content</h2>;
};
