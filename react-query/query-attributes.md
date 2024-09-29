# React Query Attributes & Features

## staleTime

1. For example.

```js
const { error, data, isLoading } = useQuery({
  queryKey: ["query-Key"],
  queryFn: queryFunction,
  staleTime: 5 * 1000,
});
```

2. By default 0
3. Use case if we set 5 \* 1000 (5000 ms) then if navigate between different routes and return to query route then if 5000 not completes from last successful queryFunction then did not call network endpoint or query function

4. `staleTime: Infinity;` means that the data fetched by the query will never be considered stale. This means that the component will continue to render the cached data even if the underlying data has changed on the server.

## gcTime

1. The `gcTime` property is used to specify the amount of time in milliseconds that a route match's loader data will be kept in memory after a preload or it is no longer in use. This helps in managing the memory by garbage collecting the data that is no longer needed.

```js
const { error, data, isLoading } = useQuery({
  queryKey: ["query-Key"],
  queryFn: queryFunction,
  gcTime: 5 * 1000,
});
```

## retry

1. the retry is used to retry query function n times after failed
2. Code

```js
const { error, data, isLoading } = useQuery({
  queryKey: ["query-Key"],
  queryFn: queryFunction,
  retry: 3,
});
```

## Pagination

1. Query

```js
const [page, setPage] = useState(1);
const { error, data, isLoading } = useQuery({
  queryKey: ["query-function", page],
  queryFn: () => queryFunction({ page }),
  staleTime: Infinity,
  keepPreviousData: true,
});
```

2. Buttons

```js
 <button
 disabled={page <= 1}
 onClick={() => setPage(page - 1)}
 >
    Previous
 </button>
 <p>Page {page}</p>
 {data?.data?.hasMore && (
<button onClick={() => setPage(page + 1)}>Next</button>
    )}
```
