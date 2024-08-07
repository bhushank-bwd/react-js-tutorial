# Context API

## Create Context `src\utils\cartContext.js`

```js
const { createContext } = require("react");
const CartContext = createContext({
  cartItem: [],
});
export default CartContext;
```

## Wrap

1. Import CartContext

```js
import CartContext from "./utils/cartContext";
```

2. Create state

```js
const [cartItems, setCartItem] = useState([]);
```

3. Wrap Component with context provider

```js
<CartContext.Provider value={{ cartItems, setCartItem }}>
  <div className="App">
    <Header />
    <Body />
  </div>
</CartContext.Provider>
```

## Usage

- import

```js
import { useContext } from "react";
import CartContext from "./utils/cartContext";
```

1. Show data

- in `src\Header.jsx`

```js
const cart = useContext(CartContext);
console.log(cart);
return <div>cart count = {cart?.cartItems.length}</div>;
```

2. Use function `src\Body.jsx`

```js
const { setCartItem } = useContext(CartContext);
const addCartItem = () => {
  setCartItem((prev) => {
    const tempProductID = Math.floor(100 * Math.random() + 1);
    return [...prev, tempProductID];
  });
};
```

## Use By Consumer

```js
<CartContext.Consumer>
  {({ cartItems }) => {
    console.log(cartItems);
    return <h1 className="font-bold">Cart Count = {cartItems?.length}</h1>;
  }}
</CartContext.Consumer>
```
