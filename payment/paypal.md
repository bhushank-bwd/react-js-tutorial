# PayPal

## Installation

1. Run Command

```bash
npm i @paypal/react-paypal-js
```

## Code

1. Env. Variable

```bash
VITE_PAYPAL_CLIENT_ID=<your-paypal-client-id>
```

2. In `src\components\payment\Paypal.jsx`

- imports

```js
import { PayPalButtons, PayPalScriptProvider } from "@paypal/react-paypal-js";
```

- PayPal Button Render

```js
<PayPalScriptProvider
  options={{
    "client-id": import.meta.env.VITE_PAYPAL_CLIENT_ID,
  }}
>
  <PayPalButtons
    style={{ layout: "horizontal" }}
    createOrder={createOrder}
    onApprove={onApprove}
    onError={onError}
  />
</PayPalScriptProvider>
```

- Error function

```js
const onError = (_data, _actions) => {
  console.log(_data, _actions);
};
```

- Approve/Success function

```js
const onApprove = (data, actions) => {
  return actions.order.capture().then(function (details) {
    console.log(details, data);
  });
};
```

- Create Order Function

```js
const createOrder = (_data, actions) => {
  return actions.order
    .create({
      purchase_units: [
        {
          description: "Order Description",
          amount: {
            currency_code: "USD",
            value: 15.0,
          },
          payee: {
            email_address: "joe@example.com",
            merchant_id: "YQZCHTGHUK5P8", // User's merchant id
          },
        },
      ],
    })
    .then((orderID) => {
      return orderID;
    });
};
```
