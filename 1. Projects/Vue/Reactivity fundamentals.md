Reactive object are  [[Proxies]], The difference is that Vue is able to track the property access an  mutations of a reactive object


### Dom update timing

when you muate reactive state, the DOM is updated automatically. However, it should be noted that the DOM updates are not applied sync, instead vue buffers them until the "next tick" in the upfdate cycle to ensure that each component updates only once no matter how many state changes you have made


to wait for the DOM update to complete after a state change, you can use the [[nextTick]] global API

it is also possible to explicitly ceate [[Shallow reactive]]  objs where the reactivity is only tracked at the top lv

exclusively use the proxied versions of your state


## limitations

we can't easily replace a reactive object because the reactive connection to the first reference is lost, it also means that when we assign or destrure a reactive object's property into local variables, or when we pass that property into a func, we will lose the reactivity connection


Refs can also be passed into functions or destuctured fron plain object without losing reactivily

In other words, `ref()` allows us to create a "reference" to any value and pass it around without losing reactivity. This capability is quite important as it is frequently used when extracting logic into [[Composable Functions]]

