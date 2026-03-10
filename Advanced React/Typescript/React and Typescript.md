# React with TypeScript - Comprehensive Guide

## Components

```typescript
// Children prop
interface LayoutProps {
  name: string;
  age: number;
  children: React.ReactNode;
}

function Layout({ name, age, children }: LayoutProps) { ... }

// Exporting components
export function Welcome({ name, children }: { name: string; children?: React.ReactNode }) { ... }

// Unified props type
interface MyComponentProps {
  title: string;
  onButtonClick: () => void;
  onInputChange: (e: React.ChangeEvent<HTMLInputElement>) => void;
}

function MyComponent(props: MyComponentProps): JSX.Element;
```

## Hooks

### useState

```typescript
const [count, setCount] = useState<number>(0);

const [user, setUser] = useState<{ name: string; age: number }>({
  name: "",
  age: 0,
});

const [data, setData] = useState<string | null>(null);
```

### useEffect

```typescript
useEffect((): (() => void) => {
  const subscription = subscribe();
  return () => subscription.unsubscribe(); // Cleanup
}, []);
```

### useContext

```typescript
const ThemeContext = createContext<string | undefined>(undefined);

const theme = useContext(ThemeContext);
```

### useRef

```typescript
const inputRef = useRef<HTMLInputElement>(null);

const countRef = useRef<number>(0);
```

### useCallback

```typescript
const handleClick = useCallback<(item: string) => void>((item: string) => {
  console.log(item);
}, []);
```

### useMemo

```typescript
const sum = useMemo<number>(() => {
  return items.reduce((a, b) => a + b, 0);
}, [items]);
```

### useReducer

```typescript
type Action = { type: "INCREMENT" } | { type: "DECREMENT" };

function reducer(state: number, action: Action): number {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
  }
}

const [state, dispatch] = useReducer(reducer, 0);
```

## HTML Element Types

### React Refs with HTML Elements

```typescript
// Input ref
const inputRef = useRef<HTMLInputElement>(null);

// Button ref
const buttonRef = useRef<HTMLButtonElement>(null);

// Div ref
const divRef = useRef<HTMLDivElement>(null);

// Form ref
const formRef = useRef<HTMLFormElement>(null);

// Select ref
const selectRef = useRef<HTMLSelectElement>(null);

// Video/Audio ref
const videoRef = useRef<HTMLVideoElement>(null);
```

### Event Types

```typescript
// Input/Change events
const handleInputChange = (e: React.ChangeEvent<HTMLInputElement>) => {};

// Form events
const handleFormSubmit = (e: React.FormEvent<HTMLFormElement>) => {};

// Mouse events
const handleMouseEnter = (e: React.MouseEvent<HTMLDivElement>) => {};

// Keyboard events
const handleKeyDown = (e: React.KeyboardEvent<HTMLInputElement>) => {};

// Focus events
const handleFocus = (e: React.FocusEvent<HTMLInputElement>) => {};

// Click events
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {};

// Select events
const handleSelectChange = (e: React.ChangeEvent<HTMLSelectElement>) => {};

// Textarea events
const handleTextareaChange = (e: React.ChangeEvent<HTMLTextAreaElement>) => {};
```

## Generic Components in React + TypeScript

```typescript
// Define props with a generic type T
interface ListProps<T> {
  items: T[];
  render: (item: T) => JSX.Element;
}

// Generic component
function List<T>({ items, render }: ListProps<T>) {
  return <>{items.map(render)}</>;
}

// Usage with strings
<List
  items={['apple', 'banana', 'cherry']}
  render={(item) => <div>{item}</div>}
/>

// Usage with numbers
<List
  items={[1, 2, 3]}
  render={(item) => <div>{item * 2}</div>}
/>
```

## React Event Handlers
```typescript
// Input/Change events
///////////////////////////
const handleInputChange: React.ChangeEventHandler<HTMLInputElement> = (e) => {};
// ChangeEventHandler<HTMLInputElement> if import type { ChangeEventHandler } from "react";

// Form events
///////////////////////////
const handleFormSubmit: React.FormEventHandler<HTMLFormElement> = (e) => {};
// FormEventHandler<HTMLFormElement> if import type { FormEventHandler } from "react";

// Mouse events
///////////////////////////
const handleMouseEnter: React.MouseEventHandler<HTMLDivElement> = (e) => {};
// MouseEventHandler<HTMLDivElement> if import type { MouseEventHandler } from "react";

const handleMouseLeave: React.MouseEventHandler<HTMLDivElement> = (e) => {};
// MouseEventHandler<HTMLDivElement> if import type { MouseEventHandler } from "react";

const handleClick: React.MouseEventHandler<HTMLButtonElement> = (e) => {};
// MouseEventHandler<HTMLButtonElement> if import type { MouseEventHandler } from "react";

const handleDoubleClick: React.MouseEventHandler<HTMLButtonElement> = (e) => {};
// MouseEventHandler<HTMLButtonElement> if import type { MouseEventHandler } from "react";

// Keyboard events
///////////////////////////
const handleKeyDown: React.KeyboardEventHandler<HTMLInputElement> = (e) => {};
// KeyboardEventHandler<HTMLInputElement> if import type { KeyboardEventHandler } from "react";

const handleKeyUp: React.KeyboardEventHandler<HTMLInputElement> = (e) => {};
// KeyboardEventHandler<HTMLInputElement> if import type { KeyboardEventHandler } from "react";

const handleKeyPress: React.KeyboardEventHandler<HTMLInputElement> = (e) => {};
// KeyboardEventHandler<HTMLInputElement> if import type { KeyboardEventHandler } from "react";

// Focus events
///////////////////////////
const handleFocus: React.FocusEventHandler<HTMLInputElement> = (e) => {};
// FocusEventHandler<HTMLInputElement> if import type { FocusEventHandler } from "react";

const handleBlur: React.FocusEventHandler<HTMLInputElement> = (e) => {};
// FocusEventHandler<HTMLInputElement> if import type { FocusEventHandler } from "react";

// Select events
///////////////////////////
const handleSelectChange: React.ChangeEventHandler<HTMLSelectElement> = (e) => {};
// ChangeEventHandler<HTMLSelectElement> if import type { ChangeEventHandler } from "react";

// Touch events (mobile)
///////////////////////////
const handleTouchStart: React.TouchEventHandler<HTMLDivElement> = (e) => {};
// TouchEventHandler<HTMLDivElement> if import type { TouchEventHandler } from "react";

const handleTouchEnd: React.TouchEventHandler<HTMLDivElement> = (e) => {};
// TouchEventHandler<HTMLDivElement> if import type { TouchEventHandler } from "react";

const handleTouchMove: React.TouchEventHandler<HTMLDivElement> = (e) => {};
// TouchEventHandler<HTMLDivElement> if import type { TouchEventHandler } from "react";
