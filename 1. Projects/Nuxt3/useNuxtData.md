`useNuxtData` gives you access to the current cached value of [[useAsyncData]], [[useFetch]]

// We can access same data later using 'posts' key const { data } = await useFetch('/api/posts', { key: 'posts' })


// Access to the cached value of useFetch in archive.vue const { data: posts } = useNuxtData('posts') const { data } = await useFetch(`/api/posts/${postId}`, { key: `post-${postId}`, default: () => { // Find the individual post from the cache and set it as the default value. return posts.value.find(post => post.id === postId) } })

```js

```