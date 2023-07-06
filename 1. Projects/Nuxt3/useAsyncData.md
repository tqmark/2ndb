[[useFetch]]  receives a URL and gets that data, whereas `useAsyncData` might have more complex logic. `useFetch(url)` is nearly equivalent to `useAsyncData(url, () => $fetch(url))` - it's developer experience sugar for the most common use case.

or a third-party provide their own query layer. In this case, you can use `useAsyncData` to wrap your calls and still keep the benefits provided by the composable:

```
const { data, error } = await useAsyncData('users', () => myGetFunction('users'))
```

