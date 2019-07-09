---
layout: post
title: React Component
subtitle: React Lifecycle Methods
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [The Component Lifecycle](#the-component-lifecycle)
    - [Mounting](#mounting)
        - [constructor()](#constructor)
        - [static getDerivedStateFromProps()](#static-getderivedstatefromprops)
        - [UNSAFE_componentWillMount()](#unsafecomponentwillmount)
        - [render()](#render)
        - [componentDidMount()](#componentdidmount)
    - [Updating](#updating)
        - [static getDerivedStateFromProps()](#static-getderivedstatefromprops-1)
        - [shouldComponentUpdate()](#shouldcomponentupdate)
        - [render()](#render-1)
        - [getSnapshotBeforeUpdate()](#getsnapshotbeforeupdate)
        - [UNSAFE_componentWillUpdate()](#unsafecomponentwillupdate)
        - [componentDidUpdate()](#componentdidupdate)
        - [UNSAFE_componentWillReceiveProps()](#unsafecomponentwillreceiveprops)
    - [Unmounting](#unmounting)
        - [componentWillUnmount()](#componentwillunmount)
    - [Error Handling](#error-handling)
        - [static getDerivedStateFromError()](#static-getderivedstatefromerror)
        - [componentDidCatch()](#componentdidcatch)
- [Other APIs](#other-apis)
    - [setState()](#setstate)
    - [forceUpdate()](#forceupdate)
- [Class Properties](#class-properties)
    - [defaultProps](#defaultprops)
    - [displayName](#displayname)
- [Instance Properties](#instance-properties)
    - [props](#props)
    - [state](#state)

## The Component Lifecycle

Each component has several “lifecycle methods” that you can override to run code at particular times in the process.<br>
You can use [this lifecycle diagram](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) as a cheat sheet.

#### Mounting

These methods are called in the following order when an instance of a component is being created and inserted into the `DOM`:

- constructor()
- static getDerivedStateFromProps()
- render()
- componentDidMount()

> legacy but avoid them:<br> > `UNSAFE_componentWillMount()`

###### constructor()

```javascript
constructor(props);
```

&nbsp;&nbsp;If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your `React` component.<br>
&nbsp;&nbsp;The constructor for a React component is called before it is mounted.<br>
&nbsp;&nbsp;When implementing the constructor for a `React.Component` subclass, you should call `super(props)` before any other statement. Otherwise, `this.props` will be undefined in the constructor, which can lead to bugs.<br>
Typically, in `React` constructors are only used for two purposes:

- Initializing local state by assigning an object to this.state.
- Binding event handler methods to an instance.

&nbsp;&nbsp;You should not call `setState()` in the `constructor()`. Instead, if your component needs to use local state, assign the initial state to `this.state` directly in the constructor<br>

```javascript
constructor(props) {
  super(props);
  // Don't call this.setState() here!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

Avoid introducing any `side-effects` or `subscriptions` in the constructor. For those use cases, use `componentDidMount()` instead.<br>

> Note
> Avoid copying props into state!
> The problem is that it’s both unnecessary (you can use `this.props.color` directly instead), and creates bugs (updates to the `color` prop won’t be reflected in the state).

```javascript
constructor(props) {
 super(props);
 // Don't do this!
 this.state = { color: props.color };
}
```

###### static getDerivedStateFromProps()

```javascript
static getDerivedStateFromProps(props, state)
```

&nbsp;&nbsp;`getDerivedStateFromProps` is invoked right before calling the render method, both on the initial mount and on subsequent updates.<br>
&nbsp;&nbsp;It should return an object to update the state, or null to update nothing.<br>
Make sure you’re familiar with simpler alternatives:

- If you need to **_perform a side effect_** (for example, `data fetching` or an `animation`) in response to a change in props, use `componentDidUpdate`lifecycle instead.
- If you want to re-compute some data only when a prop changes, use a `memoization helper` instead.
- If you want to “reset” some state when a prop changes, consider either making a component `fully controlled` or `fully uncontrolled with a key` instead.
  Note that this method is fired on every render, regardless of the cause.This is in contrast to `UNSAFE_componentWillReceiveProps`, which only fires when the parent causes a re-render and not as a result of a local `setState`.

###### UNSAFE_componentWillMount()

`UNSAFE_componentWillMount()` is invoked just before mounting occurs. It is called before `render()`, therefore calling `setState()` synchronously in this method will not trigger an extra rendering.

###### render()

```javascript
render();
```

The `render()` method is the only required method in a class component.<br>
When called, it should examine `this.props` and `this.state` and return one of the following types:

- React elements
  - Typically created via `JSX`. For example, `<div />` and `<MyComponent />` are `React` elements that instruct `React` to render a `DOM` node, or another `user-defined component`, respectively.
- Arrays and fragments
  - return multiple elements from render
- Portals
  - render children into a different `DOM` subtree
- String and numbers
  - rendered as text nodes in the `DOM`
- Booleans or null
  - Render nothing. (Mostly exists to support return `test` && `<Child />` pattern, where `test` is boolean.)

> Note
> `render()` will not be invoked if shouldComponentUpdate() returns false.

###### componentDidMount()

```javascript
componentDidMount();
```

&nbsp;&nbsp;`componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree).<br>
&nbsp;&nbsp;Initialization that requires DOM nodes should go here.<br>
&nbsp;&nbsp;If you need to load data from a remote endpoint, this is a good place to instantiate the network request.
&nbsp;&nbsp;This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in `componentWillUnmount()`.<br>
&nbsp;&nbsp;You may call `setState()` immediately in `componentDidMount()`. It will trigger an extra rendering, but it will happen before the browser updates the screen.<br>
&nbsp;&nbsp;This guarantees that even though the `render()` will be called twice in this case, the user won’t see the intermediate state. Use this pattern with caution because it often causes performance issues.<br>
&nbsp;&nbsp;In most cases, you should be able to assign the initial state in the `constructor()` instead. It can, however, be necessary for cases like `modals` and `tooltips` when you need to measure a `DOM` node before rendering something that depends on its size or position.

#### Updating

An update can be caused by changes to `props` or `state`. These methods are called in the following order when a component is being re-rendered:

- static getDerivedStateFromProps()
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()
  > legacy but avoid them:<br>
  >
  > > `UNSAFE_componentWillUpdate()` <br> >> `UNSAFE_componentWillReceiveProps()`<br>

###### static getDerivedStateFromProps()

###### shouldComponentUpdate()

```javascript
shouldComponentUpdate(nextProps, nextState);
```

&nbsp;&nbsp;Use `shouldComponentUpdate()` to let `React` know if a component’s output is not affected by the current change in `state` or `props`. <br>
&nbsp;&nbsp;`shouldComponentUpdate()` is invoked before rendering when new `props` or `state` are being received. Defaults to `true`. This method is not called for the `initial render` or when `forceUpdate()` is used.<br>
&nbsp;&nbsp;Consider using the built-in PureComponent instead of writing shouldComponentUpdate() by hand.<br>
&nbsp;&nbsp;Note that returning false does not prevent child components from re-rendering when their state changes.<br>
&nbsp;&nbsp;We do not recommend doing deep equality checks or using JSON.stringify() in shouldComponentUpdate().<br>
if `shouldComponentUpdate()` returns false, then `UNSAFE_componentWillUpdate()`, `render()`, and `componentDidUpdate()` will not be invoked.<br>

###### render()

###### getSnapshotBeforeUpdate()

```javascript
getSnapshotBeforeUpdate(prevProps, prevState);
```

&nbsp;&nbsp;`getSnapshotBeforeUpdate()` is invoked right before the most recently rendered output is committed to e.g. the `DOM`.<br>
&nbsp;&nbsp;It enables your component to capture some information from the `DOM` (e.g. scroll position) before it is potentially changed.This use case is not common, but it may occur in UIs like a **_chat thread_** that need to handle scroll position in a special way.<br>
&nbsp;&nbsp;Any value returned by this lifecycle will be passed as a parameter to `componentDidUpdate()`.
&nbsp;&nbsp;A snapshot value (or `null`) should be returned.

```javascript
class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // Are we adding new items to the list?
    // Capture the scroll position so we can adjust scroll later.
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // If we have a snapshot value, we've just added new items.
    // Adjust scroll so these new items don't push the old ones out of view.
    // (snapshot here is the value returned from getSnapshotBeforeUpdate)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return <div ref={this.listRef}>{/* ...contents... */}</div>;
  }
}
```

###### UNSAFE_componentWillUpdate()

`UNSAFE_componentWillUpdate()` is invoked just before rendering when new props or state are being received.

###### componentDidUpdate()

```javascript
componentDidUpdate(prevProps, prevState, snapshot);
```

`componentDidUpdate()` is invoked immediately after updating occurs. <br>
&nbsp;&nbsp;This method is not called for the initial render.<br>
&nbsp;&nbsp;This is also a good place to do `network requests` as long as you compare **_the current props_** to **_previous props_** (e.g. a network request may not be necessary if the props have not changed).

```javascript
componentDidUpdate(prevProps) {
  // Typical usage (don't forget to compare props):
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

&nbsp;&nbsp;You may call `setState()` immediately in `componentDidUpdate()` but note that it must be wrapped in a condition like in the example above, or you’ll cause an infinite loop. It would also cause an extra re-rendering which, while not visible to the user, can affect the component performance.<br>
&nbsp;&nbsp;If your component implements the `getSnapshotBeforeUpdate()` lifecycle (which is rare), the value it returns will be passed as a third “snapshot” parameter to `componentDidUpdate()`. Otherwise this parameter will be `undefined`.

> Note
> `componentDidUpdate()` will not be invoked if `shouldComponentUpdate()` returns false

###### UNSAFE_componentWillReceiveProps()

&nbsp;&nbsp;`UNSAFE_componentWillReceiveProps()` is invoked before a mounted component receives new props.<br>
&nbsp;&nbsp;If you need to update the state in response to prop changes (for example, to reset it), you may compare `this.props` and `nextProps` and perform state transitions using `this.setState()` in this method.

#### Unmounting

This method is called when a component is being removed from the DOM:

- componentWillUnmount()

###### componentWillUnmount()

&nbsp;&nbsp;componentWillUnmount() is invoked immediately before a component is unmounted and destroyed.<br>
&nbsp;&nbsp;Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in componentDidMount().<br>
&nbsp;&nbsp;You should not call setState() in componentWillUnmount() because the component will never be re-rendered.

#### Error Handling

These methods are called when there is an error during rendering, in a `lifecycle method`, or in the `constructor` of any `child component`.

- static getDerivedStateFromError()
- componentDidCatch()

`Error boundaries` are `React` components that catch `JavaScript` errors anywhere in their child component tree, `log those errors`, and `display a fallback UI` instead of the component tree that crashed.<br>
A class component becomes an error boundary if it defines either (or both) of the lifecycle methods `static getDerivedStateFromError()` or `componentDidCatch()`.<br>
Updating state from these lifecycles lets you capture an `unhandled JavaScript error` in the below tree and display a fallback UI.

> Note
> `Error boundaries` only catch errors in the components below them in the tree.
> An error boundary can’t catch an error within itself.

###### static getDerivedStateFromError()

```javascript
static getDerivedStateFromError(error)
```

This lifecycle is invoked after an error has been thrown by a descendant component.<br>
It receives the error that was thrown as a parameter and should return a value to update state.

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

> `getDerivedStateFromError()` is called during the “render” phase, so side-effects are not permitted.
> For those use cases, use `componentDidCatch()` instead.

###### componentDidCatch()

```javascript
componentDidCatch(error, info);
```

This lifecycle is invoked after an error has been thrown by a descendant component.<br>
It receives two parameters:

- error
  - The error that was thrown.
- info
  - An object with a `componentStack key` containing information about which component threw the error.
    `componentDidCatch()` is called during the “commit” phase, so side-effects are permitted.<br>

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    // Example "componentStack":
    //   in ComponentThatThrows (created by App)
    //   in ErrorBoundary (created by App)
    //   in div (created by App)
    //   in App
    logComponentStackToMyService(info.componentStack);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

## Other APIs

#### setState()

```javascript
setState(updater[, callback])
```

1. `setState()` enqueues changes to the component state and tells `React` that this component and its children need to be re-rendered with the updated state. <br>
2. For better perceived performance, React may delay `setState()`, and then update several components in a single pass. <br>
3. `setState()` does not always immediately update the component. It may batch or defer the update until later.<br>
4. `setState()` will always lead to a re-render unless `shouldComponentUpdate()` returns false. <br>
5. The first argument is an updater function with the signature:

```javascript
(state, props) => stateChange;
```

6. `state` is a reference to the component state at the time the change is being applied.<br>
7. It should not be directly mutated. Instead, changes should be represented by building a new object based on the input from `state` and `props`. <br>
8. The second parameter to `setState()` is an optional callback function that will be executed once `setState` is completed and the component is re-rendered.<br>
9. Generally we recommend using `componentDidUpdate()` for such logic instead.
10. You may optionally pass an object as the first argument to `setState()` instead of a function.

#### forceUpdate()

```javascript
component.forceUpdate(callback);
```

1. If your `render()` method depends on some other data, you can tell `React` that the component needs re-rendering by calling `forceUpdate()`.
2. Calling `forceUpdate()` will cause `render()` to be called on the component, skipping `shouldComponentUpdate()`.
3. `React` will still only update the `DOM` if the markup changes.

## Class Properties

#### defaultProps

1. `defaultProps` can be defined as a property on the component class itself, to set the default props for the class.
2. This is used for undefined props, but not for null props.
3. For example:

```javascript
class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {
  color: "blue"
};
```

If `props.color` is not provided, it will be set by default to 'blue':

```javascript
render() {
 return <CustomButton /> ; // props.color will be set to blue
}
```

If `props.color` is set to null, it will remain null:

```javascript
  render() {
    return <CustomButton color={null} /> ; // props.color will remain null
  }
```

#### displayName
1. The `displayName` string is used in debugging messages.

## Instance Properties

#### props
1. `this.props` contains the props that were defined by the caller of this component.
2. In particular, `this.props.children` is a special prop, typically defined by the child tags in the JSX expression rather than in the tag itself.

#### state
1. The state contains data specific to this component that may change over time.
2. The state is user-defined, and it should be a plain JavaScript object.
3. Never mutate `this.state` directly, as calling `setState()` afterwards may replace the mutation you made.
