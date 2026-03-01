# Container Component Pattern

## 📌 What is this?

The **Container Component Pattern** is a design approach where a component (the "container") handles data fetching, state management, or other logic, and passes the results to child components that are focused on presentation.

This separates **data logic** from **UI presentation**, improving modularity and reusability.

## 🤔 Why use it?

- Keeps UI components purely presentational  
- Handles data fetching, caching, or state in one place  
- Allows multiple child components to share the same data  
- Promotes clean separation of concerns  
- Easy to test and maintain

## 🧠 Core Idea

- **Container component** (smart):
  - Fetches or manages data
  - Handles side effects (API calls, state updates)  
- **Children components** (dumb/presentational):
  - Receive data as props
  - Focus purely on rendering UI  
- Container passes data dynamically via props (e.g., using `React.cloneElement`)

## ⚙️ Example

```jsx
import React, { useState, useEffect } from "react";

/* ---------- App ---------- */
function App() {
  return (
    <>
      <ResourceLoader resourceUrl="/users/1" resourceName="user">
        <UserInfo />
      </ResourceLoader>

      <ResourceLoader resourceUrl="/books/1" resourceName="book">
        <BookInfo />
      </ResourceLoader>
    </>
  );
}

export default App;

/* ---------- Container Component ---------- */
export const ResourceLoader = ({ resourceUrl, resourceName, children }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const response = await fetch(resourceUrl);
      const data = await response.json();
      setResource(data);
    })();
  }, [resourceUrl]);

  return (
    <>
      {React.Children.map(children, (child) => {
        if (React.isValidElement(child)) {
          return React.cloneElement(child, { [resourceName]: resource });
        }
        return child;
      })}
    </>
  );
};

/* ---------- Example Presentational Components ---------- */
export const UserInfo = ({ user }) => {
  if (!user) return <p>Loading user...</p>;
  return (
    <div className="p-4 border rounded bg-gray-50">
      <h2 className="text-xl font-semibold">{user.name}</h2>
      <p>Age: {user.age}</p>
      <p>Country: {user.country}</p>
    </div>
  );
};

export const BookInfo = ({ book }) => {
  if (!book) return <p>Loading book...</p>;
  return (
    <div className="p-4 border rounded bg-gray-50">
      <h2 className="text-xl font-semibold">{book.name}</h2>
      <p>Author: {book.title}</p>
      <p>Pages: {book.pages}</p>
      <p>Price: ${book.price}</p>
    </div>
  );
};
```

## Better example with Suspense 
```jsx
import React, { Suspense, use } from "react";

/* ---------- App ---------- */
function App() {
  return (
    <>
      <ResourceLoader resourceUrl="/users/1" resourceName="user">
        <UserInfo />
      </ResourceLoader>

      <ResourceLoader resourceUrl="/books/1" resourceName="book">
        <BookInfo />
      </ResourceLoader>
    </>
  );
}

export default App;

/* ---------- ResourceLoader ---------- */
export const ResourceLoader = ({ resourceUrl, resourceName, children }) => {
  async function fetchResource(url) {
    const res = await fetch(url);
    if (!res.ok) {
      throw new Error(`Failed to fetch ${url}: ${res.status}`);
    }
    return res.json();
  }

  const resourcePromise = fetchResource(resourceUrl);

  return (
    <Suspense fallback={<p>Loading...</p>}>
      {React.Children.map(children, (child) => {
        if (React.isValidElement(child)) {
          return React.cloneElement(child, { [resourceName]: resourcePromise });
        }
        return child;
      })}
    </Suspense>
  );
};

/* ---------- Presentational Components ---------- */
export const UserInfo = ({ user }) => {
  const resolvedUser = use(user);

  return (
    <div className="p-4 border rounded bg-gray-50">
      <h2 className="text-xl font-semibold">{resolvedUser.name}</h2>
      <p>Age: {resolvedUser.age}</p>
      <p>Country: {resolvedUser.country}</p>
    </div>
  );
};

export const BookInfo = ({ book }) => {
  const resolvedBook = use(book);

  return (
    <div className="p-4 border rounded bg-gray-50">
      <h2 className="text-xl font-semibold">{resolvedBook.name}</h2>
      <p>Author: {resolvedBook.title}</p>
      <p>Pages: {resolvedBook.pages}</p>
      <p>Price: ${resolvedBook.price}</p>
    </div>
  );
};
```


## ⚙️ More generic example

```jsx
import React, { useState, useEffect } from "react";

/* ---------- App ---------- */
function App() {
  return (
    <>
      <DataSource getData={() => fetchData("/users/1")} resourceName="user">
        <UserInfo />
      </DataSource>

      <DataSource getData={() => getFromLocalStorage("test")} resourceName="msg">
        <Message />
      </DataSource>
    </>
  );
}

export default App;

/* ---------- Container Component ---------- */
export const DataSource = ({ getData = () => {}, resourceName, children }) => {
  const [resource, setResource] = useState(null);

  useEffect(() => {
    (async () => {
      const data = await getData();
      setResource(data);
    })();
  }, [getData]);

  return (
    <>
      {React.Children.map(children, (child) => {
        if (React.isValidElement(child)) {
          return React.cloneElement(child, { [resourceName]: resource });
        }
        return child;
      })}
    </>
  );
};

/* ---------- Fetch Functions ---------- */
const fetchData = async (url) => {
  const response = await fetch(url);
  return await response.json();
};

const getFromLocalStorage = (key) => () => {
  return localStorage.getItem(key);
};

/* ---------- Example Presentational Components (schematic) ---------- */
export const UserInfo = ({ user }) => {
  if (!user) return <p className="text-gray-500">Loading user…</p>;
  return (
    <div className="p-4 border rounded bg-gray-50">
      <p>user.name: …</p>
      <p>user.age: …</p>
      <p>user.country: …</p>
    </div>
  );
};

export const Message = ({ msg }) => {
  if (!msg) return <p className="text-gray-500">Loading message…</p>;
  return <h1 className="text-lg font-medium">msg: …</h1>;
};
