# Routing

## Installation

- Run Command

```bash
npm i react-router-dom
```

## In `src\App.jsx`

- import element

```bash
import { createBrowserRouter, RouterProvider } from "react-router-dom";
```

- create router

```bash
const router = createBrowserRouter([
{
    path: "/",
    element: <Body />,
    errorElement: <Error />,
    children: [
    {
        path: "about",
        element: <About />,
    },
    {
        path: "",
        element: <Home />,
    },
    {
        path: "contact",
        children: [
        {
            path: "career",
            element: <Career />,
        },
        {
            path: "",
            element: <Contact />,
        },
        ],
    },
    ],
},
]);
```

- Use router

```bash
 <RouterProvider router={router}></RouterProvider>
```

## in `src\components\Body.jsx`

```bash
import { Outlet } from "react-router-dom";
const Body = () => {
  return (
    <>
      <h1>This is Header</h1>
      <Outlet />
      <h1>This is Footer</h1>
    </>
  );
};
export default Body;
```

## Error page

- `import Error from "./components/Error";`
- In router add `errorElement: <Error />,` in first object or array element

- Create Error Component

```bash
import { useRouteError } from "react-router-dom";
const Error = () => {
  const { status, statusText } = useRouteError();
  return (
    <div>
      <h1>{status}</h1>
      <h2>{statusText}</h2>
    </div>
  );
};
export default Error;
```

## Dynamic segment

- Router element

```bash
{
    path: "blog/:id",
    element: <Blog />,
},
```

- In Blog component

```bash
import { useParams } from "react-router-dom";
const { id } = useParams();
```
