# Redux Toolkit

## Installation

- Run Command

```bash
npm i react-redux
npm i @reduxjs/toolkit
```

## Slice

- File `src\redux-toolkit\slices\cart.js`

```js
import { createSlice } from "@reduxjs/toolkit";

const cartSlice = createSlice({
  name: "cart",
  initialState: {
    cartItems: [],
  },
  reducers: {
    addCartItem: (state, action) => {
      const { item_id, quantity } = action.payload;
      const existingItem = state.cartItems.find(
        (item) => item.item_id === item_id
      );
      if (existingItem) {
        existingItem.quantity += quantity;
      } else {
        state.cartItems.push({ item_id, quantity });
      }
    },
    deleteCartItem: (state, action) => {
      const item_id = action.payload;
      state.cartItems = state.cartItems.filter(
        (item) => item.item_id !== item_id
      );
    },
  },
});
export const { addCartItem, deleteCartItem } = cartSlice.actions;
export default cartSlice.reducer;
```

## Store

- File `src\redux-toolkit\store.js`

```js
import { configureStore } from "@reduxjs/toolkit";
import cart from "./slices/cart";

const store = configureStore({
  reducer: {
    cart: cart,
  },
});
export default store;
```

## Provider

- src\main.jsx

```js
import { Provider } from "react-redux";
import store from "./redux-toolkit/store.js";
```

## Usage

- Dispatch

```js
import { useDispatch } from "react-redux";
import { addCartItem } from "../redux-toolkit/slices/cart";
dispatch(addCartItem({ item_id, quantity }));
```

- Selector

```js
import { useSelector } from "react-redux";
const cartItems = useSelector((store) => store.cart.cartItems);
```
