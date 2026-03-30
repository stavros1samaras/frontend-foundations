# Debounce vs Throttling

Debounce and Throttling both limit how often a function runs, but in different ways:

---

## Debounce — waits until you stop

Executes the function only after X time has passed with no new event.

```js
// Fires only 300ms after the user stops typing
input.addEventListener("input", debounce(search, 300));
```

Use for: search input, resize, form validation.

---

## Throttling — runs at a steady rate

Executes the function at most once per X time, regardless of how many events come in.

```js
// Runs max once every 200ms while scrolling
window.addEventListener("scroll", throttle(updatePosition, 200));
```

Use for: scroll handlers, mouse move, resize animations.

---

## Timeline summary

```
Events:   ─●─●─●─●─●─●──────────────●
                           300ms gap ↑

Debounce: ────────────────────────────●   (only at the end)
Throttle: ─●──────●──────●──────●────●   (every Xms)
```

Debounce = "once you settle down", Throttle = "every so often".

## Libraries & Custom Implementations

Neither `debounce` nor `throttle` are built into JavaScript. You can use a library or write your own.

### Libraries

```js
// lodash
import { debounce, throttle } from "lodash";

// radash
import { debounce, throttle } from "radash";
```

### Custom Debounce

```js
function debounce(fn, delay) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}
```

### Custom Throttle

```js
function throttle(fn, limit) {
  let lastCall = 0;
  return (...args) => {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn(...args);
    }
  };
}
```

---
