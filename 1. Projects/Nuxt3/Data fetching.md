Nuxt comes with two composables and a built-in library to perform data-fetching in browser or server environments: [[useFetch]], [[useAsyncData]] and [[$fetch]]

Used together, they ensure cross-environment compatibility and efficient caching and avoid duplicate network calls.

`useFetch` is the most straightforward way to handle data fetching in a component setup function.

On the other hand, when wanting to make a network request based on user interaction, `$fetch` is almost always the right handler to go for.

If you need more fine-grained control, you can use `useAsyncData` and `$fetch` independently.

The two composables share a common set of options and patterns that we will detail in the last sections.

When using a framework like Nuxt that can perform calls and render pages on both client and server environments, some challenges must be addressed. This is why Nuxt provides composables to wrap your queries.

The `useFetch` and `useAsyncData` composables ensure that once an API call is made on the server, the data is properly forwarded to the client in the payload. This JavaScript object is accessible through [`useNuxtApp().payload`](https://nuxt.com/docs/api/composables/use-nuxt-app#payload) and is used on the client to avoid refetching the same data when the code is executed in the browser.

### [Effective caching](https://nuxt.com/docs/getting-started/data-fetching#effective-caching)

`useFetch` and `useAsyncData` both use a key to cache API responses and further reduce API calls. We will detail later how to invalidate this cache.

nuxt use [[Suspense]] component under the hood to prevent navigation before every async data is available in the view. The data  fetching composable can help you leverage this feature and use what suit best on a pre calls basic

nuxt 3 use ofetch library is built on top of the fetch api adds handy feature to it

- Works the same way in browser, Node or worker environments
- Automatic response parsing
- Error handling
- Auto-retry
- Interceptors

## [Options](https://nuxt.com/docs/getting-started/data-fetching#options)

`useAsyncData` and `useFetch` return the same object type and accept a common set of options as their last argument. They can help you control the composables behavior, such as navigation blocking, caching or execution.

### [Lazy](https://nuxt.com/docs/getting-started/data-fetching#lazy)

y default, data fetching composables will wait for the resolution of their asynchronous function before navigating to a new page by using Vue’s Suspense. This feature can be ignored on client-side navigation with the `lazy` option. In that case, you will have to manually handle loading state using the `pending` value.

You can alternatively use `useLazyFetch` and `useLazyAsyncData` as convenient methods to perform the same.

### [Client-only fetching](https://nuxt.com/docs/getting-started/data-fetching#client-only-fetching)

By default, data fetching composables will perform their asynchronous function on both client and server environments. Set the `server` option to `false` to only perform the call on the client-side. Combined with the `lazy` option, this can be useful for data that are not needed on the first render (for example, non-SEO sensitive data).

/* This call will only be performed on the client */ const { pending, data: posts } = useFetch('/api/comments', { lazy: true, server: false })


### [Minimize payload size](https://nuxt.com/docs/getting-started/data-fetching#minimize-payload-size)

The `pick` option helps you to minimize the payload size stored in your HTML document by only selecting the fields that you want returned from the composables.

 
 ### [Caching and refetching](https://nuxt.com/docs/getting-started/data-fetching#caching-and-refetching)

`useFetch` and `useAsyncData` use keys to prevent refetching the same data.

- `useFetch` uses the provided URL as a key. Alternatively, a `key` value can be provided in the `options` object passed as a last argument.
- `useAsyncData` uses its first argument as a key if it is a string. If the first argument is the handler function that performs the query, then a key that is unique to the file name and line number of the instance of `useAsyncData` will be generated for you.
- 
- [[useNuxtData]]

[[refreshNuxtData]]


## [Passing Headers and cookies](https://nuxt.com/docs/getting-started/data-fetching#passing-headers-and-cookies)

When we call `$fetch` in the browser, user headers like `cookie` will be directly sent to the API. But during server-side-rendering, since the `$fetch` request takes place 'internally' within the server, it doesn't include the user's browser cookies, nor does it pass on cookies from the fetch response.

## [Passing Headers and cookies](https://nuxt.com/docs/getting-started/data-fetching#passing-headers-and-cookies)

When we call `$fetch` in the browser, user headers like `cookie` will be directly sent to the API. But during server-side-rendering, since the `$fetch` request takes place 'internally' within the server, it doesn't include the user's browser cookies, nor does it pass on cookies from the fetch response.

### [Pass Cookies From Server-side API Calls on SSR Response](https://nuxt.com/docs/getting-started/data-fetching#pass-cookies-from-server-side-api-calls-on-ssr-response)

If you want to pass on/proxy cookies in the other direction, from an internal request back to the client, you will need to handle this yourself.

composables/fetch.ts

```
import { appendResponseHeader, H3Event } from 'h3'

export const fetchWithCookie = async (event: H3Event, url: string) => {
  const res = await $fetch.raw(url)
  const cookies = (res.headers.get('set-cookie') || '').split(',')
  for (const cookie of cookies) {
    appendResponseHeader(event, 'set-cookie', cookie)
  }
  return res._data
}
```

