# Markdown

## Package installation

```bash
npm i marked dompurify
npm install -D @tailwindcss/typography
```

## Component

1. Import

```js
import { marked } from "marked";
import dompurify from "dompurify";
```

2. JSX

```js
const [markdown, setMarkDown] = useState("");

const parsed = dompurify.sanitize(marked.parse(markdown));

return (
  <div className="flex flex-colum h-full">
    <textarea
      className="h-full w-1/2 p-1"
      onChange={(e) => setMarkDown(e.target.value)}
    ></textarea>
    <div
      className="bg-gray-900 prose prose-invert w-1/2 p-1 prose-headings:underline text-left"
      dangerouslySetInnerHTML={{ __html: parsed }}
    ></div>
  </div>
);
```

- use prose style or classes to show proper display

## In `tailwind.config.js` add following plugin

```js
plugins: [require("@tailwindcss/typography")],
```
