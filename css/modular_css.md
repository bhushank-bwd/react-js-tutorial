# Modular CSS

## In `src\css\index.module.css`

```css
.error {
  color: red;
}
```

## In `src\css\vanilla.css`

```css
.error {
  color: rgb(232, 156, 156);
}
```

## In Component `src\Modularcss.js`

```js
import styles from "./css/index.module.css";
const Modularcss = () => {
  return (
    <div>
      <p className={styles.error}>This is error by modular css</p>
      <p className={`error`}>This is error by vanilla css</p>
    </div>
  );
};

export default Modularcss;
```

## Notes

1. error class will not clash.
