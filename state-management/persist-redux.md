# Persistent Redux

## Install Package

```bash
npm i redux-persist
```

## In `src\redux-toolkit\store.js`

1. Import Modules

```js
import storage from "redux-persist/lib/storage";
import { persistReducer } from "redux-persist";
import counter from "./slices/counter";
```

2. Create Config

```js
const persistConfig = {
  key: "root",
  version: 1,
  storage,
  whitelist: ["cart"],
};
```

- WhiteList is array of reducer which need to be persist

3. Combine all reducer

```js
const reducer = combineReducers({
  cart: cart,
  counter: counter,
});
```

4. Create Persist reducer

```js
const persistedReducer = persistReducer(persistConfig, reducer);
```

5. Create and export store

```js
const store = configureStore({
  reducer: persistedReducer,
});
export default store;
```

## In `src\main.jsx`

1. Import modules

```js
import { persistStore } from "redux-persist";
import { PersistGate } from "redux-persist/integration/react";
```

2. Create persistor variable

```js
let persistor = persistStore(store);
```

3. Wrap App or other component by PersistGate

```js
<PersistGate persistor={persistor}>
  <App />
</PersistGate>
```
