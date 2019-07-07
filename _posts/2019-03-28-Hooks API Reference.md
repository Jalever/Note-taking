---
layout: post
title: Hooks API Reference
subtitle: React Hooks API
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
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
- [Hooks Tutorial](#hooks-tutorial)

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

The clean-up function runs before the component is removed from the UI to prevent memory leaks. Additionally, if a component renders multiple times (as they typically do), **_the previous effect is cleaned up before executing the next effect_**.

###### Timing of effects

`useEffect` is deferred until after the browser has painted, but it’s guaranteed to fire before any new renders.<br>
`React` will always flush a previous render’s effects before starting a new update.

###### Conditionally firing an effect

The default behavior for effects is to fire the effect after every completed render.<br>
However, this may be overkill in some cases, like the subscription example from the previous section.<br>
To implement this, pass a second argument to useEffect that is the array of values that the effect depends on.<br>
Our updated example now looks like this:

```javascript
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    subscription.unsubscribe();
  };
}, [props.source]);
```

Now the subscription will only be recreated when `props.source` changes.<br>

> If you use this optimization, make sure the array includes all values from the component scope (such as `props` and `state`) that change over time and that are used by the effect. Otherwise, your code will reference stale values from previous renders.
> If you want to run an effect and clean it up only once (on `mount` and `unmount`), you can pass an empty array (`[]`) as a second argument. This tells `React` that your effect doesn’t depend on any values from `props` or `state`, so it never needs to re-run.
> If you pass an empty array (`[]`), the `props` and `state` as inside the effect will always have their initial values.
> The array of dependencies is not passed as arguments to the effect function.

#### useContext

```javascript
const value = useContext(MyContext);
```

Accepts `a context object` (the value returned from React.createContext) and returns `the current context value` for that context. The `current context value` is determined by the value `prop` of the nearest `<MyContext.Provider>` above the calling component in the tree.<br>
When the nearest `<MyContext.Provider>` above the component updates, this `Hook` will trigger a rerender with the latest context `value` passed to that `MyContext` provider.<br>
Don’t forget that the argument to `useContext` must be the context object itself:<br>
**_Correct_**: `useContext(MyContext)`<br>
**_Incorrect_**: `useContext(MyContext.Consumer)`<br>
**_Incorrect_**: `useContext(MyContext.Provider)`<br>
A component calling `useContext` will always re-render when the context value changes.

## Additional Hooks

#### useReducer

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

An alternative to `useState`.<br>
Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a `dispatch` method.<br>
`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one.<br>
`useReducer` also lets you optimize performance for components that trigger deep updates because you can pass dispatch down instead of callbacks.
```javascript
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter({initialState}) {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    </>
  );
}
```

###### Specifying the initial state
There’s two different ways to initialize `useReducer` state.<br>
- one depending on the use case
- pass the initial state as a second argument

###### Lazy initialization
You can also create the initial state lazily.<br>
To do this, you can pass an init function as the third argument.<br>
The initial state will be set to `init(initialArg)`
```javascript
function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    </>
  );
}
```

###### Bailing out of a dispatch
If you return the same value from a `Reducer Hook` as the current state, `React` will bail out without rendering the children or firing effects.<br>
Note that `React` may still need to render that specific component again before bailing out.

#### useCallback
```javascript
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```
Returns a memoized callback.<br>
Pass an inline callback and an array of dependencies.<br>
`useCallback` will return a memoized version of the callback that only changes if one of the dependencies has changed.<br>
`useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`.
> The array of dependencies is not passed as arguments to the callback.
> Every value referenced inside the callback should also appear in the dependencies array

#### useMemo
Returns a memoized value.<br>
Pass a “create” function and an array of dependencies.<br>
`useMemo` will only recompute the memoized value when one of the dependencies has changed.<br>
This optimization helps to avoid expensive calculations on every render.<br>
Remember that the function passed to `useMemo` runs during rendering. Don’t do anything there that you wouldn’t normally do while rendering. For example, side effects belong in `useEffect`, not `useMemo`.
***If no array is provided, a new value will be computed on every render***.
> The array of dependencies is not passed as arguments to the callback.
> Every value referenced inside the callback should also appear in the dependencies array

#### useRef
```javascript
const refContainer = useRef(initialValue);
```
`useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`).<br>
The returned object will persist for the full lifetime of the component.<br>
```javascript
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```
If you pass a ref object to React with `<div ref={myRef} />`, `React` will set its `.current` property to the corresponding `DOM` node whenever that node changes.<br>
Keep in mind that `useRef` doesn’t notify you when its content changes.

#### useImperativeHandle
```javascript
useImperativeHandle(ref, createHandle, [deps])
```
`useImperativeHandle` customizes the instance value that is exposed to parent components when using `ref`.
###### an use case
```javascript
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

#### useLayoutEffect
It fires synchronously after all `DOM` mutations.<br>
Use this to read layout from the `DOM` and synchronously re-render.<br>
Updates scheduled inside `useLayoutEffect` will be flushed synchronously, before the browser has a chance to paint.<br>
`useLayoutEffect` fires in the same phase as `componentDidMount` and `componentDidUpdate`.

#### useDebugValue
```javascript
useDebugValue(value)
```
`useDebugValue` can be used to display a label for custom hooks in `React DevTools`.
```javascript
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  // Show a label in DevTools next to this Hook
  // e.g. "FriendStatus: Online"
  useDebugValue(isOnline ? 'Online' : 'Offline');

  return isOnline;
}
```
Don’t recommend adding debug values to every custom `Hook`.
###### Defer formatting debug values
In some cases formatting a value for display might be an expensive operation.<br>
It’s also unnecessary unless a Hook is actually inspected.

## Hooks Tutorial
1. [Introducing Hooks](https://jalever.github.io/2019/03/27/Introducing-Hooks/)
2. [Hooks at a Glance](https://jalever.github.io/2019/03/27/Hooks-at-a-Glance/)
3. [Using the State Hook](https://jalever.github.io/2019/03/27/Using-the-State-Hook/)
4. [Using the Effect Hook](https://jalever.github.io/2019/03/27/Using-the-Effect-Hook/)
5. [Rules of Hooks](https://jalever.github.io/2019/03/27/Rules-of-Hooks/)
6. [Building Your Own Hooks](https://jalever.github.io/2019/03/27/Building-Your-Own-Hooks/)
7. Hooks API Reference
