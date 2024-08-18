# Vanilla CSS

## CSS File `src\css\vanilla.css`

- sample code :

```css
p {
  color: blue;
}
```

## JSX Components

- First Component `src\Vanilla.jsx`

```js
import React from "react";
import "./css/vanilla.css";
const Vanilla = () => {
  return <p>This is text from vanilla one and vanilla css imported here</p>;
};
export default Vanilla;
```

- Second Component `src\VanillaTwo.jsx`

```js
import React from "react";
const VanillaTwo = () => {
  return (
    <p>This is text from vanilla two and but vanilla css not imported here</p>
  );
};

export default VanillaTwo;
```

- Note: if we import css in one file then it applies to other components also.

## Advantage

1. CSS and JSX separate from each other
2. Due to external css file, it gives minimal access for UI developer

## Disadvantage

1. It is not scoped means if we import css in one file then it applies to other components also.
