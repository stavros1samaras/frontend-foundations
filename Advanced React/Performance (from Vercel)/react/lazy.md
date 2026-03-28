# Lazy-loading

Usually, you import components with the static import declaration:

```jsx
import MarkdownPreview from "./MarkdownPreview.js";
```

To defer loading this component’s code until it’s rendered for the first time, replace this import with:

```jsx
import { lazy } from "react";

const MarkdownPreview = lazy(() => import("./MarkdownPreview.js"));
```

Now that your component’s code loads on demand

```jsx
<Suspense fallback={<Loading />}>
  <h2>Preview</h2>
  <MarkdownPreview />
</Suspense>
```
