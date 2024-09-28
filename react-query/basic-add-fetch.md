# Basic add and fetch using React query

## QueryClientProvider

- Wrap Main Component by QueryClientProvider eg. `src\App.jsx`

1. Import

```js
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
```

2. Create queryClient Object

```js
const queryClient = new QueryClient();
```

3. Wrap component

```js
<QueryClientProvider client={queryClient}>
  <RouterProvider router={appRouter}></RouterProvider>
</QueryClientProvider>
```

## List Component

1. Import useQuery

```js
import { useQuery } from "@tanstack/react-query";
```

2. Use useQuery hooks

```js
const { error, data, isLoading } = useQuery({
  queryKey: ["fetch-students"],
  queryFn: getStudentList,
});
```

- getStudentList is function that may contain data or fetch functionality

3. Render JSX

```js
if (isLoading) return <>Loading</>;
if (error) <>{error}</>;
return <div>{data?.list && data.list.map((item) => <></>)}</div>;
```

## Add Component

1. Import useMutation, useQueryClient

```js
import { useMutation, useQueryClient } from "@tanstack/react-query";
```

2. Create mutation

```js
const mutation = useMutation({
  mutationFn: addStudent,
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ["fetch-students"] });
  },
  onError: (error) => {
    console.log(error);
  },
});
```

- addStudent is add student fetch function

3. Call Mutation

```js
<button
  onClick={() => {
    mutation.mutate({ arguments });
  }}
>
  Add
</button>
```

## Query Function

```js
export const getStudentList = async () => {
  try {
    const studentRes = await fetch("your-fetch-url");
    const studentResData = await studentRes.json();
    return studentResData;
  } catch (error) {
    throw error;
  }
};
export const addStudent = async (parameterObj) => {
  try {
    const addStudentRes = await fetch("your-add-url", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(parameterObj),
    });
    const apiCode = addStudentRes.status;
    if (apiCode === 404) {
      throw "invaild api endpoint";
    }

    const addStudentResData = await addStudentRes.json();
    if (addStudentResData.status) return addStudentResData;
    else throw addStudentResData.message;
  } catch (error) {
    console.log(error);
    throw error;
  }
};
```

- Use your API URL and payload(for both request and response)
