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
constructor(props)
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
Avoid introducing any `side-effects` or `subscriptions` in the constructor. For those use cases, use `componentDidMount()` instead.


###### static getDerivedStateFromProps()

###### UNSAFE_componentWillMount()

###### render()

###### componentDidMount()

#### Updating
An update can be caused by changes to `props` or `state`. These methods are called in the following order when a component is being re-rendered:

- static getDerivedStateFromProps()
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()
> legacy but avoid them:
> `UNSAFE_componentWillUpdate()`
> `UNSAFE_componentWillReceiveProps()`


###### static getDerivedStateFromProps()

###### shouldComponentUpdate()

###### render()

###### getSnapshotBeforeUpdate()

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
