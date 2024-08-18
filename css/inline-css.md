# Inline CSS

## In `src\Body.jsx`

```jsx
const btnStyle = {
  color: `white`,
  backgroundColor: `${btnType == "success" ? "green" : "red"}`,
  textTransform: "capitalize",
  borderRadius: "6px",
  border: "none",
  padding: "7px",
};
return (
  <div>
    <button style={btnStyle} onClick={addCartItem}>
      add Cart Item
    </button>
  </div>
);
```

## Advantages

1. Easy to add
2. Only affect specified element

## Disadvantage

1. No separation of css and jsx
2. Style every component individually
