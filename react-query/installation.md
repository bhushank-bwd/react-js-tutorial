# React Query

## Installation

1. Create React Project
2. Install query packages

```bash
npm i @tanstack/react-query
```

## Dev Tools

```bash
npm i @tanstack/react-query-devtools
```

### Usage

- ReactQueryDevtools import

```js
import { ReactQueryDevtools } from "@tanstack/react-query-devtools";
```

- Add <ReactQueryDevtools initialIsOpen={false} /> as children in QueryClientProvider

```js
<QueryClientProvider client={queryClient}>
  <RouterProvider router={appRouter}></RouterProvider>
  <ReactQueryDevtools initialIsOpen={false} />
</QueryClientProvider>
```
