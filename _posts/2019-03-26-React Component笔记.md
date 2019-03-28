---
layout: post
title: React.Component笔记
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.png
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

> legacy but avoid them:
> `UNSAFE_componentWillMount()`

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
  > legacy but avoid them:
  > `UNSAFE_componentWillUpdate()` > `UNSAFE_componentWillReceiveProps()`

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

###### static getDerivedStateFromError()

###### componentDidCatch()

## Other APIs

#### setState()

#### forceUpdate()

## Class Properties

#### defaultProps

#### displayName

## Instance Properties

#### props

#### state
