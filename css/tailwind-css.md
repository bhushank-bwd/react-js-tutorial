# Tailwind CSS

## Installation

- Ref. https://tailwindcss.com/docs/guides/vite

1. Create Vite Project
2. Install Tailwind packages

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

3. Configure your template paths
   Add the paths to all of your template files in your `tailwind.config.js` file.

```js
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

4. Add the Tailwind directives to your CSS `src\index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## New Installation

# Run Command

```bash
npm install tailwindcss @tailwindcss/vite
```

# In `vite.config.js`

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

# In `src\index.css`

```css
@import "tailwindcss";
```
