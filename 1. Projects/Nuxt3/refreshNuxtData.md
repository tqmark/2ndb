
`refreshNuxtData` re-fetches all data from the server and updates the page as well as invalidates the cache of `useAsyncData`, `useLazyAsyncData`, `useFetch` and `useLazyFetch`.

## [Type](https://nuxt.com/docs/api/utils/refresh-nuxt-data#type)

```
refreshNuxtData(keys?: string | string[])
```

Copy to clipboard

**Parameters:**

- `keys`:  
    **Type**: `String | String[]`  
    `refreshNuxtData` accepts a single or an array of strings as `keys` that are used to fetch the data. This parameter is **optional**. All `useAsyncData` and `useFetch` are re-fetched when no `keys` are specified.