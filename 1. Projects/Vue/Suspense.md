
`<Suspense>` is a built-in component for orchestrating async dependencies in a component tree. It can render a loading state while waiting for multiple nested async dependencies down the component tree to be resolved.

## Async Dependencies[​](https://vuejs.org/guide/built-ins/suspense.html#async-dependencies)

To explain the problem `<Suspense>` is trying to solve and how it interacts with these async dependencies, let's imagine a component hierarchy like the following:

```
<Suspense>
└─ <Dashboard>
   ├─ <Profile>
   │  └─ <FriendStatus> (component with async setup())
   └─ <Content>
      ├─ <ActivityFeed> (async component)
      └─ <Stats> (async component)
```

In the component tree there are multiple nested components whose rendering depends on some async resource to be resolved first. Without `<Suspense>`, each of them will need to handle its own loading / error and loaded states. In the worst case scenario, we may see three loading spinners on the page, with content displayed at different times.

The `<Suspense>` component gives us the ability to display top-level loading / error states while we wait on these nested async dependencies to be resolved.

There are two types of async dependencies that `<Suspense>` can wait on:

1. Components with an async `setup()` hook. This includes components using `<script setup>` with top-level `await` expressions.
    
2. [Async Components](https://vuejs.org/guide/components/async.html).
    

### `async setup()`[​](https://vuejs.org/guide/built-ins/suspense.html#async-setup)

A Composition API component's `setup()` hook can be async:

js

```
export default {
  async setup() {
    const res = await fetch(...)
    const posts = await res.json()
    return {
      posts
    }
  }
}
```

If using `<script setup>`, the presence of top-level `await` expressions automatically makes the component an async dependency:

vue

```
<script setup>
const res = await fetch(...)
const posts = await res.json()
</script>

<template>
  {{ posts }}
</template>
```

### Async Components[​](https://vuejs.org/guide/built-ins/suspense.html#async-components)

Async components are **"suspensible"** by default. This means that if it has a `<Suspense>` in the parent chain, it will be treated as an async dependency of that `<Suspense>`. In this case, the loading state will be controlled by the `<Suspense>`, and the component's own loading, error, delay and timeout options will be ignored.

The async component can opt-out of `Suspense` control and let the component always control its own loading state by specifying `suspensible: false` in its options.