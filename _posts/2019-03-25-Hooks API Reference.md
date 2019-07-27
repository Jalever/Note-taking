---
layout: post
title: Hooks API Reference
subtitle: React Hooks API
date: 2019-03-25
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [Basic Hooks](#basic-hooks)
    - [useState](#usestate)
        - [Functional updates](#functional-updates)
        - [Lazy initial state](#lazy-initial-state)
        - [Bailing out of a state update](#bailing-out-of-a-state-update)
    - [useEffect](#useeffect)
        - [Cleaning up an effect](#cleaning-up-an-effect)
        - [Timing of effects](#timing-of-effects)
        - [Conditionally firing an effect](#conditionally-firing-an-effect)
    - [useContext](#usecontext)
- [Additional Hooks](#additional-hooks)
    - [useReducer](#usereducer)
        - [Specifying the initial state](#specifying-the-initial-state)
        - [Lazy initialization](#lazy-initialization)
        - [Bailing out of a dispatch](#bailing-out-of-a-dispatch)
    - [useCallback](#usecallback)
    - [useMemo](#usememo)
    - [useRef](#useref)
    - [useImperativeHandle](#useimperativehandle)
        - [an use case](#an-use-case)
    - [useLayoutEffect](#uselayouteffect)
    - [useDebugValue](#usedebugvalue)
        - [Defer formatting debug values](#defer-formatting-debug-values)

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

This page describes the APIs for the built-in Hooks in React.

## Basic Hooks
#### useState
![enD4yR.png](https://s2.ax1x.com/2019/07/26/enD4yR.png)

Returns a stateful value, and a function to update it.

During the initial render, the returned state (`state`) is the same as the value passed as the first argument (`initialState`).

The `setState` function is used to update the state. It accepts a new state value and enqueues a re-render of the component.
![enrMkT.png](https://s2.ax1x.com/2019/07/26/enrMkT.png)

During subsequent re-renders, the first value returned by `useState` will always be the most recent state after applying updates.

> React guarantees that `setState` function identity is stable and won’t change on re-renders. This is why it’s safe to omit from the `useEffect` or `useCallback` dependency list.

###### Functional updates
If the new state is computed using the previous state, you can pass a function to `setState`. The function will receive the previous value, and return an updated value. Here’s an example of a counter component that uses both forms of `setState`:
![enryjA.png](https://s2.ax1x.com/2019/07/26/enryjA.png)
The ”+” and ”-” buttons use the functional form, because the updated value is based on the previous value. But the “Reset” button uses the normal form, because it always sets the count back to the initial value.

> Unlike the `setState` method found in class components, `useState` does not automatically merge update objects. You can replicate this behavior by combining the function updater form with object spread syntax:
![enrbBq.png](https://s2.ax1x.com/2019/07/26/enrbBq.png)
> Another option is useReducer, which is more suited for managing state objects that contain multiple sub-values.

###### Lazy initial state
The `initialState` argument is the state used during the initial render. In subsequent renders, it is disregarded. If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render:
![ensfq1.png](https://s2.ax1x.com/2019/07/26/ensfq1.png)

###### Bailing out of a state update
If you update a State Hook to the same value as the current state, React will bail out without rendering the children or firing effects. (React uses the <strong>Object.is</strong> comparison algorithm.)

Note that React may still need to render that specific component again before bailing out. That shouldn’t be a concern because React won’t unnecessarily go “deeper” into the tree. If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.

#### useEffect
![enyfSg.png](https://s2.ax1x.com/2019/07/26/enyfSg.png)

Accepts a function that contains imperative, possibly effectful code.

Mutations, subscriptions, timers, logging, and other side effects are not allowed inside the main body of a function component (referred to as React’s <strong>render phase</strong>). Doing so will lead to confusing bugs and inconsistencies in the UI.

Instead, use `useEffect`. The function passed to `useEffect` will run after the render is committed to the screen. Think of effects as an escape hatch from React’s purely functional world into the imperative world.

By default, effects run after every completed render, but you can choose to fire it <ins>only when certain values have changed</ins>.

###### Cleaning up an effect
Often, effects create resources that need to be cleaned up before the component leaves the screen, such as a subscription or timer ID. To do this, the function passed to `useEffect` may return a clean-up function. For example, to create a subscription:
![en6n0I.png](https://s2.ax1x.com/2019/07/26/en6n0I.png)
The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), the <strong>previous effect is cleaned up before executing the next effect</strong>. In our example, this means a new subscription is created on every update. To avoid firing an effect on every update, refer to the next section.

###### Timing of effects
Unlike `componentDidMount` and `componentDidUpdate`, the function passed to `useEffect` fires <strong>after</strong> layout and paint, during a deferred event. This makes it suitable for the many common side effects, like setting up subscriptions and event handlers, because most types of work shouldn’t block the browser from updating the screen.

However, not all effects can be deferred. For example, a DOM mutation that is visible to the user must fire synchronously before the next paint so that the user does not perceive a visual inconsistency. (The distinction is conceptually similar to passive versus active event listeners.) For these types of effects, React provides one additional Hook called <strong>useLayoutEffect</strong>. It has the same signature as `useEffect`, and only differs in when it is fired.

Although `useEffect` is deferred until after the browser has painted, it’s guaranteed to fire before any new renders. React will always flush a previous render’s effects before starting a new update.

###### Conditionally firing an effect
The default behavior for effects is to fire the effect after every completed render. That way an effect is always recreated if one of its dependencies changes.

However, this may be overkill in some cases, like the subscription example from the previous section. We don’t need to create a new subscription on every update, only if the `source` props has changed.

To implement this, pass a second argument to `useEffect` that is the array of values that the effect depends on. Our updated example now looks like this:
![engUYV.png](https://s2.ax1x.com/2019/07/26/engUYV.png)
Now the subscription will only be recreated when `props.source` changes.

> Note<br/>
> If you use this optimization, make sure the array includes <strong>all values from the component scope (such as props and state) that change over time and that are used by the effect.</strong> Otherwise, your code will reference stale values from previous renders.<br/>
> If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array (<strong>[]</strong>) as a second argument. This tells React that your effect doesn’t depend on any values from props or state, so it never needs to re-run. This isn’t handled as a special case — it follows directly from how the dependencies array always works.<br/>
> If you pass an empty array (<strong>[]</strong>), the props and state as inside the effect will always have their initial values. While passing <strong>[]</strong> as the second argument is closer to the familiar <strong>componentDidMount</strong> and <strong>componentWillUnmount</strong> mental model, there are usually better solutions to avoid re-running effects too often. Also, don’t forget that React defers running <strong>useEffect</strong> until after the browser has painted, so doing extra work is less of a problem.

The array of dependencies is not passed as arguments to the effect function. Conceptually, though, that’s what they represent: every value referenced inside the effect function should also appear in the dependencies array. In the future, a sufficiently advanced compiler could create this array automatically.

#### useContext
![enRE5t.png](https://s2.ax1x.com/2019/07/26/enRE5t.png)
Accepts a context object (the value returned from `React.createContext`) and returns the current context value for that context. The current context value is determined by the `value` prop of the nearest `<MyContext.Provider>` above the calling component in the tree.

When the nearest `<MyContext.Provider>` above the component updates, this Hook will trigger a rerender with the latest context `value` passed to that `MyContext` provider.

Don’t forget that the argument to `useContext` must be the context object itself:
- <strong>Correct</strong>: `useContext(MyContext)`
- <strong>Incorrect</strong>: `useContext(MyContext.Consumer)`
- <strong>Incorrect</strong>: `useContext(MyContext.Provider)`

A component calling `useContext` will always re-render when the context value changes. If re-rendering the component is expensive, you can <ins>optimize it by using memoization</ins>.
![enfp0H.png](https://s2.ax1x.com/2019/07/26/enfp0H.png)
![enfitI.png](https://s2.ax1x.com/2019/07/26/enfitI.png)
![enfFht.png](https://s2.ax1x.com/2019/07/26/enfFht.png)
![enfA9P.png](https://s2.ax1x.com/2019/07/26/enfA9P.png)
![enfE1f.png](https://s2.ax1x.com/2019/07/26/enfE1f.png)

> Tip<br/>
> If you’re familiar with the context API before Hooks, `useContext(MyContext)` is equivalent to `static contextType = MyContext` in a class, or to `<MyContext.Consumer>`.<br/>
> `useContext(MyContext)` only lets you read the context and subscribe to its changes. You still need a `<MyContext.Provider>` above in the tree to provide the value for this context.

## Additional Hooks
The following Hooks are either variants of the basic ones from the previous section, or only needed for specific edge cases. Don’t stress about learning them up front.

#### useReducer
![en4wSx.png](https://s2.ax1x.com/2019/07/26/en4wSx.png)

An alternative to `useState`. Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a `dispatch` method. (If you’re familiar with Redux, you already know how this works.)

`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. `useReducer` also lets you optimize performance for components that trigger deep updates because you can pass dispatch down instead of callbacks.

Here’s the counter example from the `useState` section, rewritten to use a reducer:
![en504s.png](https://s2.ax1x.com/2019/07/26/en504s.png)

> Note<br/>
> React guarantees that `dispatch` function identity is stable and won’t change on re-renders. This is why it’s safe to omit from the `useEffect` or `useCallback` dependency list.

###### Specifying the initial state
There are two different ways to initialize `useReducer` state. You may choose either one depending on the use case. The simplest way is to pass the initial state as a second argument:
![en5I81.png](https://s2.ax1x.com/2019/07/26/en5I81.png)
> Note<br/>
> React doesn’t use the `state = initialState` argument convention popularized by Redux. The initial value sometimes needs to depend on props and so is specified from the Hook call instead. If you feel strongly about this, you can call `useReducer(reducer, undefined, reducer)` to emulate the Redux behavior, but it’s not encouraged.

###### Lazy initialization
You can also create the initial state lazily. To do this, you can pass an `init` function as the third argument. The initial state will be set to `init(initialArg)`.

It lets you extract the logic for calculating the initial state outside the reducer. This is also handy for resetting the state later in response to an action:
![enIJi9.png](https://s2.ax1x.com/2019/07/26/enIJi9.png)
![enIYGR.png](https://s2.ax1x.com/2019/07/26/enIYGR.png)

###### Bailing out of a dispatch
If you return the same value from a Reducer Hook as the current state, React will bail out without rendering the children or firing effects. (React uses the <strong>Object.is</strong> comparison algorithm.)

Note that React may still need to render that specific component again before bailing out. That shouldn’t be a concern because React won’t unnecessarily go “deeper” into the tree. If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.

#### useCallback
![euvqB9.png](https://s2.ax1x.com/2019/07/27/euvqB9.png)

Returns a `memoized` callback.

Pass an inline callback and an array of dependencies. `useCallback` will return a memoized version of the callback that only changes if one of the dependencies has changed. This is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders (e.g. `shouldComponentUpdate`).

`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.

> The array of dependencies is not passed as arguments to the callback. Conceptually, though, that’s what they represent: every value referenced inside the callback should also appear in the dependencies array. In the future, a sufficiently advanced compiler could create this array automatically.

#### useMemo
![euvXA1.png](https://s2.ax1x.com/2019/07/27/euvXA1.png)

Returns a `memoized` value.

Pass a “create” function and an array of dependencies. `useMemo` will only recompute the memoized value when one of the dependencies has changed. This optimization helps to avoid expensive calculations on every render.

Remember that the function passed to `useMemo` runs during rendering. Don’t do anything there that you wouldn’t normally do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.

If no array is provided, a new value will be computed on every render.

<strong>You may rely on useMemo as a performance optimization, not as a semantic guarantee.</strong> In the future, React may choose to “forget” some previously memoized values and recalculate them on next render, e.g. to free memory for offscreen components. Write your code so that it still works without `useMemo` — and then add it to optimize performance.

> The array of dependencies is not passed as arguments to the function. Conceptually, though, that’s what they represent: every value referenced inside the function should also appear in the dependencies array. In the future, a sufficiently advanced compiler could create this array automatically.

#### useRef
![eux9je.png](https://s2.ax1x.com/2019/07/27/eux9je.png)
`useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

A common use case is to access a child imperatively:
![euxYCV.png](https://s2.ax1x.com/2019/07/27/euxYCV.png)
Essentially, `useRef` is like a “box” that can hold a mutable value in its `.current` property.

You might be familiar with refs primarily as a way to access the DOM. If you pass a ref object to React with `<div ref={myRef} />`, React will set its `.current` property to the corresponding DOM node whenever that node changes.

However, `useRef()` is useful for more than the `ref` attribute. It’s handy for keeping any mutable value around similar to how you’d use instance fields in classes.

This works because `useRef()` creates a plain JavaScript object. The only difference between `useRef()` and creating a `{current: ...}` object yourself is that `useRef` will give you the same ref object on every render.

Keep in mind that `useRef` doesn’t notify you when its content changes. Mutating the `.current` property doesn’t cause a re-render. If you want to run some code when React attaches or detaches a ref to a DOM node, you may want to use a callback ref instead.

#### useImperativeHandle
![euxfDH.png](https://s2.ax1x.com/2019/07/27/euxfDH.png)
`useImperativeHandle` customizes the instance value that is exposed to parent components when using `ref`. As always, imperative code using refs should be avoided in most cases. `useImperativeHandle` should be used with `forwardRef`:
![eux7PP.png](https://s2.ax1x.com/2019/07/27/eux7PP.png)
In this example, a parent component that renders `<FancyInput ref={fancyInputRef} />` would be able to call `fancyInputRef.current.focus()`.

#### useLayoutEffect
The signature is identical to useEffect, but it fires synchronously after all DOM mutations. Use this to read layout from the DOM and synchronously re-render. Updates scheduled inside useLayoutEffect will be flushed synchronously, before the browser has a chance to paint.

Prefer the standard useEffect when possible to avoid blocking visual updates.

> If you’re migrating code from a class component, note `useLayoutEffect` fires in the same phase as `componentDidMount` and `componentDidUpdate`. However, <strong>we recommend starting with useEffect first</strong> and only trying `useLayoutEffect` if that causes a problem.<br/><br/>
> If you use server rendering, keep in mind that neither `useLayoutEffect` nor `useEffect` can run until the JavaScript is downloaded. This is why React warns when a server-rendered component contains `useLayoutEffect`. To fix this, either move that logic to `useEffect` (if it isn’t necessary for the first render), or delay showing that component until after the client renders (if the HTML looks broken until `useLayoutEffect` runs).<br/><br/>
> To exclude a component that needs layout effects from the server-rendered HTML, render it conditionally with `showChild && <Child />` and defer showing it with `useEffect(() => { setShowChild(true); }, [])`. This way, the UI doesn’t appear broken before hydration.

#### useDebugValue
![euzYdA.png](https://s2.ax1x.com/2019/07/27/euzYdA.png)
`useDebugValue` can be used to display a label for custom hooks in React DevTools.

For example, consider the `useFriendStatus` custom Hook described in “Building Your Own Hooks”:
![euzUit.png](https://s2.ax1x.com/2019/07/27/euzUit.png)
> We don’t recommend adding debug values to every custom Hook. It’s most valuable for custom Hooks that are part of shared libraries.

###### Defer formatting debug values
In some cases formatting a value for display might be an expensive operation. It’s also unnecessary unless a Hook is actually inspected.

For this reason `useDebugValue` accepts a formatting function as an optional second parameter. This function is only called if the Hooks are inspected. It receives the debug value as a parameter and should return a formatted display value.

For example a custom Hook that returned a `Date` value could avoid calling the `toDateString` function unnecessarily by passing the following formatter:
![euzDsg.png](https://s2.ax1x.com/2019/07/27/euzDsg.png)
