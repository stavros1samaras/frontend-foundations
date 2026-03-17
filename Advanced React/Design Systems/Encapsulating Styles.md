# Encapsulating Styles

## Why
To avoid **style conflicts** between components and their environment. Components should only care about their **own styles**.



## Principle 1: Components Should Not Lay Themselves Out
- **Do not set:** `position`, `size`, `margin` (controlled by parent)
- **Can set safely:** `border`, `padding`, `font`, `background`, `color`



## Principle 2: Components Should Only Style Themselves and Immediate Children
- Style **only the component** and its **direct children**
- Do **not** style deep nested children
- Safe properties: same as above (`border`, `padding`, etc.)

> Exceptions are allowed, but only for **specific reasons**.
