<img width="1002" height="973" alt="εικόνα" src="https://github.com/user-attachments/assets/a9603b32-2878-4055-9331-081af7b7b2f8" />




# Browser

## Runtime (V8, SpiderMonkey, Node.js, ...)
  - Event Loop
  - JIT Compilation
  - Call Stack
  - Execution Context
  - Heap
  - Task Queue (Macrotasks)
  - Microtask Queue
  - Garbage Collection

## Rendering Engine (Blink, WebKit, Gecko)
- DOM Tree
- CSSOM Tree
- Render Tree
- Accessibility Tree
- Layout (Reflow) 
- Paint 
- Compositing 

## Web APIs
- DOM API
- Fetch API
- Web Storage API
- Geolocation API
- Canvas API
- WebSockets API
- Notifications API
- Web Audio API
- Web Workers API
- Crypto API

# Javascript

## Fundamentals
  - Closures
  - Scope Chain
  - Hoisting
  - this Binding
  - Prototypal Inheritance
  - Event Bubbling/Capturing
  - Callbacks
  - Promises
  - Async/Await

---

# React Internals

## Architecture
- React Fiber architecture
- Scheduler / prioritization
- Concurrent rendering (React 18+)
- Rendering phase (pure) vs Commit phase (side effects)

### Rendering Model
- Component render / Mount / Update / Unmount
- Re-renders (on state/props change)
- Virtual DOM
- Reconciliation (diffing algorithm)
- Efficient DOM updates

### Events System
- Synthetic events
- Event handlers (onClick etc.)
- Cleanup functions

### State Mechanics
- Batching updates
- Async state updates
- State drives UI

https://medium.com/@canpolat.dev/deep-dive-into-reacts-internal-architecture-from-virtual-dom-to-fiber-08dcf66b309d
