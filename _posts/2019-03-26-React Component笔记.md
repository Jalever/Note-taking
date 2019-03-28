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

If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your `React` component.<br>
The constructor for a React component is called before it is mounted.<br>
When implementing the constructor for a `React.Component` subclass, you should call `super(props)` before any other statement. Otherwise, `this.props` will be undefined in the constructor, which can lead to bugs.<br>
Typically, in `React` constructors are only used for two purposes:

- Initializing local state by assigning an object to this.state.
- Binding event handler methods to an instance.
  You should not call `setState()` in the `constructor()`. Instead, if your component needs to use local state, assign the initial state to `this.state` directly in the constructor<br>

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

`getDerivedStateFromProps` is invoked right before calling the render method, both on the initial mount and on subsequent updates.<br>
It should return an object to update the state, or null to update nothing.<br>
Make sure you’re familiar with simpler alternatives:

- If you need to **_perform a side effect_** (for example, `data fetching` or an `animation`) in response to a change in props, use `componentDidUpdate`lifecycle instead.
- If you want to re-compute some data only when a prop changes, use a `memoization helper` instead.
- If you want to “reset” some state when a prop changes, consider either making a component `fully controlled` or `fully uncontrolled with a key` instead.
Note that this method is fired on every render, regardless of the cause.This is in contrast to `UNSAFE_componentWillReceiveProps`, which only fires when the parent causes a re-render and not as a result of a local `setState`.

###### UNSAFE_componentWillMount()

###### render()
```javascript
render()
```
The `render()` method is the only required method in a class component.
When called, it should examine `this.props` and `this.state` and return one of the following types:
- React elements
  - Typically created via `JSX`. For example, `<div />` and `<MyComponent />` are `React` elements that instruct `React` to render a `DOM` node, or another `user-defined component`, respectively.
- Arrays and fragments
  - return multiple elements from render
- Portals
  - render children into a different `DOM` subtree
- String and numbers
  -  rendered as text nodes in the `DOM`
- Booleans or null
  - Render nothing. (Mostly exists to support return `test` && `<Child />` pattern, where `test` is boolean.)

> Note
> `render()` will not be invoked if shouldComponentUpdate() returns false.

###### componentDidMount()

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

###### render()

###### getSnapshotBeforeUpdate()
```javascript
getSnapshotBeforeUpdate(prevProps, prevState)
```
&nbsp;&nbsp;`getSnapshotBeforeUpdate()` is invoked right before the most recently rendered output is committed to e.g. the `DOM`.<br>
&nbsp;&nbsp;It enables your component to capture some information from the `DOM` (e.g. scroll position) before it is potentially changed.This use case is not common, but it may occur in UIs like a ***chat thread*** that need to handle scroll position in a special way.<br>
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
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}

```

###### UNSAFE_componentWillUpdate()

###### componentDidUpdate()

###### UNSAFE_componentWillReceiveProps()

#### Unmounting

This method is called when a component is being removed from the DOM:

- componentWillUnmount()

###### componentWillUnmount()

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
