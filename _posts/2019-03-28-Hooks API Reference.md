---
layout: post
title: Hooks API Reference
subtitle: React Hooks学习笔记系列 7
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

- [Table of Contents](#table-of-contents)
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
    - [useCallback](#usecallback)
    - [useMemo](#usememo)
    - [useRef](#useref)
    - [useImperativeHandle](#useimperativehandle)
    - [useLayoutEffect](#uselayouteffect)
    - [useDebugValue](#usedebugvalue)

## Table of Contents

## Basic Hooks

#### useState

```javascript
const [state, setState] = useState(initialState);
```

Returns `a stateful value`, and `a function` to update it.<br>
During the initial render, the returned state (`state`) is the same as the value passed as the first argument (`initialState`).<br>
The `setState` function is used to update the state. It accepts a new state value and enqueues a re-render of the component.

```javascript
setState(newState);
```

During subsequent re-renders, the first value returned by `useState` will always be the most recent state after applying updates.

###### Functional updates

If the new state is computed using the previous state, you can pass a function to `setState`.<br>
The function will receive the previous value, and return an updated value.<br>
Here’s an example of a counter component that uses both forms of `setState`:

```javascript
function Counter({ initialCount }) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
    </>
  );
}
```

> Note: Unlike the `setState` method found in class components, `useState` does not automatically merge update objects.

###### Lazy initial state

The `initialState` argument is the state used during the initial render.<br>
In subsequent renders, it is disregarded. <br>
If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed **_only_** on the initial render

```javascript
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

###### Bailing out of a state update

If you update a State Hook to the same value as the current state, `React` will bail out without rendering the children or firing effects.<br>

> Note that `React` may still need to render that specific component again before bailing out.

#### useEffect

```javascript
useEffect(didUpdate);
```

Accepts a function that contains imperative, possibly effectful code.<br>
`Mutations`, `subscriptions`, `timers`, `logging`, and other side effects are not allowed inside the main body of a function component (referred to as React’s render phase). <br>
Instead, use `useEffect`. The function passed to `useEffect` will run after the render is committed to the screen. <br>
Think of effects as an escape hatch from `React`’s purely functional world into the imperative world.<br>
By default, effects run after every completed render, but you can choose to fire it only when certain values have changed.

###### Cleaning up an effect
Often, effects create resources that need to be cleaned up before the component leaves the screen, such as a subscription or timer ID. To do this, the function passed to useEffect may return a clean-up function. 
For example, to create a subscription:
```javascript
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
});
```
The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), ***the previous effect is cleaned up before executing the next effect***.

###### Timing of effects
`useEffect` is deferred until after the browser has painted, but it’s guaranteed to fire before any new renders.<br>
`React` will always flush a previous render’s effects before starting a new update.

###### Conditionally firing an effect
The default behavior for effects is to fire the effect after every completed render.<br>
However, this may be overkill in some cases, like the subscription example from the previous section.<br>
To implement this, pass a second argument to useEffect that is the array of values that the effect depends on.<br>
Our updated example now looks like this: 
```javascript
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```
Now the subscription will only be recreated when `props.source` changes.<br>
> If you use this optimization, make sure the array includes all values from the component scope (such as `props` and `state`) that change over time and that are used by the effect. Otherwise, your code will reference stale values from previous renders.
> If you want to run an effect and clean it up only once (on `mount` and `unmount`), you can pass an empty array (`[]`) as a second argument. This tells `React` that your effect doesn’t depend on any values from `props` or `state`, so it never needs to re-run.
> If you pass an empty array (`[]`), the `props` and `state` as inside the effect will always have their initial values.
The array of dependencies is not passed as arguments to the effect function.

#### useContext
```javascript
const value = useContext(MyContext);
```

Accepts `a context object` (the value returned from React.createContext) and returns `the current context value` for that context. The `current context value` is determined by the value `prop` of the nearest `<MyContext.Provider>` above the calling component in the tree.<br>
When the nearest `<MyContext.Provider>` above the component updates, this `Hook` will trigger a rerender with the latest context `value` passed to that `MyContext` provider.<br>
Don’t forget that the argument to `useContext` must be the context object itself:<br>
***Correct***: `useContext(MyContext)`<br>
***Incorrect***: `useContext(MyContext.Consumer)`<br>
***Incorrect***: `useContext(MyContext.Provider)`<br>
A component calling `useContext` will always re-render when the context value changes. 

## Additional Hooks

#### useReducer

#### useCallback

#### useMemo

#### useRef

#### useImperativeHandle

#### useLayoutEffect

#### useDebugValue
