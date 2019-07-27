---
layout: post
title: React Component
subtitle: React Lifecycle Methods
date: 2019-03-25
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
Each component has several “lifecycle methods” that you can override to run code at particular times in the process. You can use this lifecycle diagram as a cheat sheet.
![eKP2xP.png](https://s2.ax1x.com/2019/07/27/eKP2xP.png)

#### Mounting
These methods are called in the following order when an instance of a component is being created and inserted into the DOM:
- <strong>constructor()</strong>
- static getDerivedStateFromProps()
- <strong>render()</strong>
- <strong>componentDidMount()</strong>

> These methods are considered legacy and you should avoid them in new code:<br/>
> UNSAFE_componentWillMount()

###### constructor()
![eKFu0U.png](https://s2.ax1x.com/2019/07/27/eKFu0U.png)
<strong>If you don’t initialize state and you don’t bind methods, you don’t need to implement a constructor for your React component.</strong>

The constructor for a React component is called before it is mounted. When implementing the constructor for a `React.Component` subclass, you should call `super(props)` before any other statement. Otherwise, `this.props` will be undefined in the constructor, which can lead to bugs.

Typically, in React constructors are only used for two purposes:
- Initializing <ins>local state</ins> by assigning an object to `this.state`.
- Binding <ins>event handler</ins> methods to an instance.

You <strong>should not call setState()</strong> in the `constructor()`. Instead, if your component needs to use local state, <strong>assign the initial state to this.state</strong> directly in the constructor:
![eKFv4J.png](https://s2.ax1x.com/2019/07/27/eKFv4J.png)

Constructor is the only place where you should assign `this.state` directly. In all other methods, you need to use `this.setState()` instead.

Avoid introducing any side-effects or subscriptions in the constructor. For those use cases, use `componentDidMount()` instead.
> Avoid copying props into state! This is a common mistake:<br/>
> ![eKkiDK.png](https://s2.ax1x.com/2019/07/27/eKkiDK.png)<br/>
> The problem is that it’s both unnecessary (you can use this.props.color directly instead), and creates bugs (updates to the color prop won’t be reflected in the state).<br/>
> <strong>Only use this pattern if you intentionally want to ignore prop updates.</strong> In that case, it makes sense to rename the prop to be called `initialColor` or `defaultColor`. You can then force a component to “reset” its internal state by changing its key when necessary.

###### static getDerivedStateFromProps()
![eKZYwV.png](https://s2.ax1x.com/2019/07/27/eKZYwV.png)

`getDerivedStateFromProps` is invoked right before calling the render method, both on the initial mount and on subsequent updates. It should return an object to update the state, or null to update nothing.

This method exists for rare use cases where the state depends on changes in props over time. For example, it might be handy for implementing a `<Transition>` component that compares its previous and next children to decide which of them to animate in and out.

Deriving state leads to verbose code and makes your components difficult to think about.
Make sure you’re familiar with simpler alternatives:
- If you need to <strong>perform a side effect</strong> (for example, data fetching or an animation) in response to a change in props, use componentDidUpdate lifecycle instead.
- If you want to <strong>re-compute some data only when a prop changes</strong>, use a memoization helper instead.
- If you want to <strong>“reset” some state when a prop changes</strong>, consider either making a component fully controlled or fully uncontrolled with a key instead.

This method doesn’t have access to the component instance. If you’d like, you can reuse some code between `getDerivedStateFromProps()` and the other class methods by extracting pure functions of the component props and state outside the class definition.

Note that this method is fired on every render, regardless of the cause. This is in contrast to `UNSAFE_componentWillReceiveProps`, which only fires when the parent causes a re-render and not as a result of a local `setState`.

<strong>When to Use Derived State</strong><br/>
`getDerivedStateFromProps` exists for only one purpose. It enables a component to update its internal state as the result of <strong>changes in props</strong>. Our previous blog post provided some examples, like RECORDING THE CURRENT SCROLL DIRECTION BASED ON A CHANGING OFFSET PROP or LOADING EXTERNAL DATA SPECIFIED BY A SOURCE PROP.

We did not provide many examples, because as a general rule, <strong>derived state should be used sparingly</strong>. All problems with derived state that we have seen can be ultimately reduced to either (1) unconditionally updating state from props or (2) updating state whenever props and state don’t match.
- If you’re using derived state to memoize some computation based only on the current props, you don’t need derived state.
- If you’re updating derived state unconditionally or updating it whenever props and state don’t match, your component likely resets its state too frequently.

<strong>Updating state based on props</strong> or RECORDING THE CURRENT SCROLL DIRECTION BASED ON A CHANGING OFFSET PROP<br/>
Here is an example of a component that uses the legacy `componentWillReceiveProps` lifecycle to update `state` based on new `props` values:
![eKejUK.png](https://s2.ax1x.com/2019/07/27/eKejUK.png)
Although the above code is not problematic in itself, the `componentWillReceiveProps` lifecycle is often mis-used in ways that do present problems. Because of this, the method will be deprecated.

As of version 16.3, the recommended way to update `state` in response to `props` changes is with the new `static getDerivedStateFromProps` lifecycle. It is called when a component is created and each time it re-renders due to changes to props or state:
![eKmEUf.png](https://s2.ax1x.com/2019/07/27/eKmEUf.png)

You may notice in the example above that `props.currentRow` is mirrored in state (as `state.lastRow`). This enables `getDerivedStateFromProps` to access the previous props value in the same way as is done in `componentWillReceiveProps`.

You may wonder why we don’t just pass previous props as a parameter to `getDerivedStateFromProps`. We considered this option when designing the API, but ultimately decided against it for two reasons:
- A `prevProps` parameter would be null the first time `getDerivedStateFromProps` was called (after instantiation), requiring an if-not-null check to be added any time `prevProps` was accessed.
- Not passing the previous props to this function is a step toward freeing up memory in future versions of React. (If React does not need to pass previous props to lifecycles, then it does not need to keep the previous `props` object in memory.)

<strong>Fetching external data when props change</strong> or LOADING EXTERNAL DATA SPECIFIED BY A SOURCE PROP<br/>
Here is an example of a component that fetches external data based on `props` values:
![eKn701.png](https://s2.ax1x.com/2019/07/27/eKn701.png)
![eKnqk6.png](https://s2.ax1x.com/2019/07/27/eKnqk6.png)
The recommended upgrade path for this component is to move data updates into `componentDidUpdate`. You can also use the new `getDerivedStateFromProps` lifecycle to clear stale data before rendering the new props:
![eKunns.png](https://s2.ax1x.com/2019/07/27/eKunns.png)
![eKu44f.png](https://s2.ax1x.com/2019/07/27/eKu44f.png)
![eKuIC8.png](https://s2.ax1x.com/2019/07/27/eKuIC8.png)

###### UNSAFE_componentWillMount()
![eKKQrd.png](https://s2.ax1x.com/2019/07/27/eKKQrd.png)
> This lifecycle was previously named `componentWillMount`. That name will continue to work until version 17. Use the `rename-unsafe-lifecycles codemod` to automatically update your components.

`UNSAFE_componentWillMount()` is invoked just before mounting occurs. It is called before `render()`, therefore calling `setState()` synchronously in this method will not trigger an extra rendering. Generally, we recommend using the `constructor()` instead for initializing state.

Avoid introducing any side-effects or subscriptions in this method. For those use cases, use `componentDidMount()` instead.

This is the only lifecycle method called on server rendering.

###### render()
![eK345n.png](https://s2.ax1x.com/2019/07/27/eK345n.png)
The `render()` method is the only required method in a class component.

When called, it should examine `this.props` and `this.state` and return one of the following types:
- <strong>React elements</strong>. Typically created via JSX. For example, `<div />` and `<MyComponent />` are React elements that instruct React to render a DOM node, or another user-defined component, respectively.
- <strong>Arrays and fragments</strong>. Let you return multiple elements from render. See the documentation on fragments for more details.
- <strong>Portals</strong>. Let you render children into a different DOM subtree. See the documentation on portals for more details.
- <strong>String and numbers</strong>. These are rendered as text nodes in the DOM.
- <strong>Booleans or null</strong>. Render nothing. (Mostly exists to support `return test && <Child />` pattern, where `test` is boolean.)

The `render()` function should be pure, meaning that it does not modify component state, it returns the same result each time it’s invoked, and it does not directly interact with the browser.

If you need to interact with the browser, perform your work in `componentDidMount()` or the other lifecycle methods instead. Keeping `render()` pure makes components easier to think about.

> Note<br/>
> `render()` will not be invoked if `shouldComponentUpdate()` returns false.

###### componentDidMount()
![eK3o80.png](https://s2.ax1x.com/2019/07/27/eK3o80.png)
`componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.

This method is a good place to set up any subscriptions. If you do that, don’t forget to unsubscribe in `componentWillUnmount()`.

You <strong>may call setState() immediately</strong> in `componentDidMount()`. It will trigger an extra rendering, but it will happen before the browser updates the screen. This guarantees that even though the `render()` will be called twice in this case, the user won’t see the intermediate state. Use this pattern with caution because it often causes performance issues. In most cases, you should be able to assign the initial state in the `constructor()` instead. It can, however, be necessary for cases like modals and tooltips when you need to measure a DOM node before rendering something that depends on its size or position.

#### Updating
An update can be caused by changes to props or state. These methods are called in the following order when a component is being re-rendered:
- static getDerivedStateFromProps()
- shouldComponentUpdate()
- <strong>render()</strong>
- getSnapshotBeforeUpdate()
- <strong>componentDidUpdate()</strong>
> These methods are considered legacy and you should avoid them in new code:<br/><br/>
> - UNSAFE_componentWillUpdate()<br/>
> - UNSAFE_componentWillReceiveProps()<br/>

###### static getDerivedStateFromProps()
[Same as above](https://jalever.github.io/2019/03/25/React-Component/#static-getderivedstatefromprops)

###### shouldComponentUpdate()
![eKo5n0.png](https://s2.ax1x.com/2019/07/27/eKo5n0.png)

Use `shouldComponentUpdate()` to let React know if a component’s output is not affected by the current change in state or props. The default behavior is to re-render on every state change, and in the vast majority of cases you should rely on the default behavior.

`shouldComponentUpdate()` is invoked before rendering when new props or state are being received. Defaults to `true`. This method is not called for the initial render or when `forceUpdate()` is used.

This method only exists as a performance optimization. Do not rely on it to “prevent” a rendering, as this can lead to bugs. Consider using the built-in <strong>PureComponent</strong> instead of writing `shouldComponentUpdate()` by hand. `PureComponent` performs a shallow comparison of props and state, and reduces the chance that you’ll skip a necessary update.

If you are confident you want to write it by hand, you may compare `this.props` with `nextProps` and `this.state` with `nextState` and return `false` to tell React the update can be skipped. Note that returning `false` does not prevent child components from re-rendering when their state changes.

We do not recommend doing deep equality checks or using `JSON.stringify()` in `shouldComponentUpdate()`. It is very inefficient and will harm performance.

Currently, if `shouldComponentUpdate()` returns `false`, then `UNSAFE_componentWillUpdate()`, `render()`, and `componentDidUpdate()` will not be invoked. In the future React may treat `shouldComponentUpdate()` as a hint rather than a strict directive, and returning `false` may still result in a re-rendering of the component.

###### render()
[Same as above](https://jalever.github.io/2019/03/25/React-Component/#render)

###### getSnapshotBeforeUpdate()
![eK71IO.png](https://s2.ax1x.com/2019/07/27/eK71IO.png)
`getSnapshotBeforeUpdate()` is invoked right before the most recently rendered output is committed to e.g. the DOM. It enables your component to capture some information from the DOM (e.g. scroll position) before it is potentially changed. Any value returned by this lifecycle will be passed as a parameter to `componentDidUpdate()`.

This use case is not common, but it may occur in UIs like a chat thread that need to handle scroll position in a special way.

A snapshot value (or `null`) should be returned.

For example:
![eKHSYD.png](https://s2.ax1x.com/2019/07/27/eKHSYD.png)
![eKHCSH.png](https://s2.ax1x.com/2019/07/27/eKHCSH.png)
![eKHAmt.png](https://s2.ax1x.com/2019/07/27/eKHAmt.png)
![eKHE0P.png](https://s2.ax1x.com/2019/07/27/eKHE0P.png)
In the above examples, it is important to read the `scrollHeight` property in `getSnapshotBeforeUpdate` because there may be delays between “render” phase lifecycles (like `render`) and “commit” phase lifecycles (like `getSnapshotBeforeUpdate` and `componentDidUpdate`).

###### UNSAFE_componentWillUpdate()
![eKHIBt.png](https://s2.ax1x.com/2019/07/27/eKHIBt.png)
> This lifecycle was previously named `componentWillUpdate`. That name will continue to work until version 17. Use the rename-unsafe-lifecycles codemod to automatically update your components.

`UNSAFE_componentWillUpdate()` is invoked just before rendering when new props or state are being received. Use this as an opportunity to perform preparation before an update occurs. This method is not called for the initial render.

Note that you cannot call `this.setState()` here; nor should you do anything else (e.g. dispatch a Redux action) that would trigger an update to a React component before `UNSAFE_componentWillUpdate()` returns.

Typically, this method can be replaced by `componentDidUpdate()`. If you were reading from the DOM in this method (e.g. to save a scroll position), you can move that logic to `getSnapshotBeforeUpdate()`.

> `UNSAFE_componentWillUpdate()` will not be invoked if `shouldComponentUpdate()` returns false.

###### componentDidUpdate()
![eKqFdP.png](https://s2.ax1x.com/2019/07/27/eKqFdP.png)

componentDidUpdate() is invoked immediately after updating occurs. This method is not called for the initial render.

Use this as an opportunity to operate on the DOM when the component has been updated. This is also a good place to do network requests as long as you compare the current props to previous props (e.g. a network request may not be necessary if the props have not changed).
![eKqoY8.png](https://s2.ax1x.com/2019/07/27/eKqoY8.png)
You <strong>may call setState() immediately</strong> in `componentDidUpdate()` but note that <strong>it must be wrapped in a condition</strong> like in the example above, or you’ll cause an infinite loop. It would also cause an extra re-rendering which, while not visible to the user, can affect the component performance. If you’re trying to “mirror” some state to a prop coming from above, consider using the prop directly instead. Read more about why copying props into state causes bugs.

If your component implements the `getSnapshotBeforeUpdate()` lifecycle (which is rare), the value it returns will be passed as a third “snapshot” parameter to `componentDidUpdate()`. Otherwise this parameter will be undefined.

> `componentDidUpdate()` will not be invoked if `shouldComponentUpdate()` returns false.

###### UNSAFE_componentWillReceiveProps()
![eKbZuR.png](https://s2.ax1x.com/2019/07/27/eKbZuR.png)
> This lifecycle was previously named `componentWillReceiveProps`. That name will continue to work until version 17. Use the rename-unsafe-lifecycles codemod to automatically update your components.

> Using this lifecycle method often leads to bugs and inconsistencies<br/><br/>
> - If you need to <strong>perform a side effect</strong> (for example, data fetching or an animation) in response to a change in props, use `componentDidUpdate` lifecycle instead.<br/>
> - If you used `componentWillReceiveProps` for <strong>re-computing some data only when a prop changes</strong>, use a memoization helper instead.<br/>
> - If you used `componentWillReceiveProps` to <strong>“reset” some state when a prop changes</strong>, consider either making a component <ins>fully controlled</ins> or <ins>fully uncontrolled with a key</ins> instead.

`UNSAFE_componentWillReceiveProps()` is invoked before a mounted component receives new props. If you need to update the state in response to prop changes (for example, to reset it), you may compare `this.props` and `nextProps` and perform state transitions using `this.setState()` in this method.

Note that if a parent component causes your component to re-render, this method will be called even if props have not changed. Make sure to compare the current and next values if you only want to handle changes.

React doesn’t call `UNSAFE_componentWillReceiveProps()` with initial props during mounting. It only calls this method if some of component’s props may update. Calling `this.setState()` generally doesn’t trigger `UNSAFE_componentWillReceiveProps()`.

#### Unmounting
This method is called when a component is being removed from the DOM:
- <strong>componentWillUnmount()</strong>

###### componentWillUnmount()
![eKbLa6.png](https://s2.ax1x.com/2019/07/27/eKbLa6.png)

`componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount()`.

You <strong>should not call setState()</strong> in `componentWillUnmount()` because the component will never be re-rendered. Once a component instance is unmounted, it will never be mounted again.

#### Error Handling
These methods are called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.
- static getDerivedStateFromError()
- componentDidCatch()

`Error boundaries` are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

A class component becomes an error boundary if it defines either (or both) of the lifecycle methods `static getDerivedStateFromError()` or `componentDidCatch()`. Updating state from these lifecycles lets you capture an unhandled JavaScript error in the below tree and display a fallback UI.

Only use error boundaries for recovering from unexpected exceptions; <strong>don’t try to use them for control flow</strong>.
> Error boundaries only catch errors in the components below them in the tree. An error boundary can’t catch an error within itself.

###### static getDerivedStateFromError()
![eKzYAs.png](https://s2.ax1x.com/2019/07/27/eKzYAs.png)
This lifecycle is invoked after an error has been thrown by a descendant component. It receives the error that was thrown as a parameter and should return a value to update state.
![eKzwcT.png](https://s2.ax1x.com/2019/07/27/eKzwcT.png)

> `getDerivedStateFromError()` is called during the “render” phase, so side-effects are not permitted. For those use cases, use `componentDidCatch()` instead.

###### componentDidCatch()
![eKzfgK.png](https://s2.ax1x.com/2019/07/27/eKzfgK.png)
This lifecycle is invoked after an error has been thrown by a descendant component. It receives two parameters:
1. <strong>error</strong> &minus; The error that was thrown.
2. <strong>info</strong> &minus; An object with a `componentStack` key containing information about which component threw the error.

`componentDidCatch()` is called during the “commit” phase, so side-effects are permitted. It should be used for things like logging errors:
![eMpFdH.png](https://s2.ax1x.com/2019/07/27/eMpFdH.png)
![eMpEFA.png](https://s2.ax1x.com/2019/07/27/eMpEFA.png)
> In the event of an error, you can render a fallback UI with `componentDidCatch()` by calling `setState`, but this will be deprecated in a future release. Use `static getDerivedStateFromError()` to handle fallback rendering instead.

## Other APIs
Each component also provides some other APIs:
- setState()
- forceUpdate()

#### setState()
![eM9sHg.png](https://s2.ax1x.com/2019/07/27/eM9sHg.png)
`setState()` enqueues changes to the component state and tells React that this component and its children need to be re-rendered with the updated state. This is the primary method you use to update the user interface in response to event handlers and server responses.

Think of `setState()` as a request rather than an immediate command to update the component. For better perceived performance, React may delay it, and then update several components in a single pass. React does not guarantee that the state changes are applied immediately.

`setState()` does not always immediately update the component. It may batch or defer the update until later. This makes reading `this.state` right after calling `setState()` a potential pitfall. Instead, use `componentDidUpdate` or a `setState` callback &#40;`setState(updater, callback)`&#41;, either of which are guaranteed to fire after the update has been applied. If you need to set the state based on the previous state, read about the `updater` argument below.

`setState()` will always lead to a re-render unless `shouldComponentUpdate()` returns `false`. If mutable objects are being used and conditional rendering logic cannot be implemented in `shouldComponentUpdate()`, calling `setState()` only when the new state differs from the previous state will avoid unnecessary re-renders.

The first argument is an `updater` function with the signature:
![eMPFwF.png](https://s2.ax1x.com/2019/07/27/eMPFwF.png)

`state` is a reference to the component state at the time the change is being applied. It should not be directly mutated. Instead, changes should be represented by building a new object based on the input from `state` and `props`. For instance, suppose we wanted to increment a value in state by `props.step`:
![eMPZWR.png](https://s2.ax1x.com/2019/07/27/eMPZWR.png)

Both `state` and `props` received by the updater function are guaranteed to be up-to-date. The output of the updater is shallowly merged with `state`.

The second parameter to `setState()` is an optional callback function that will be executed once `setState` is completed and the component is re-rendered. Generally we recommend using `componentDidUpdate()` for such logic instead.

You may optionally pass an object as the first argument to `setState()` instead of a function:
![eMPU6P.png](https://s2.ax1x.com/2019/07/27/eMPU6P.png)
This performs a shallow merge of `stateChange` into the new state, e.g., to adjust a shopping cart item quantity:
![eMPBTg.png](https://s2.ax1x.com/2019/07/27/eMPBTg.png)
This form of `setState()` is also asynchronous, and multiple calls during the same cycle may be batched together. For example, if you attempt to increment an item quantity more than once in the same cycle, that will result in the equivalent of:
![eMPfmT.png](https://s2.ax1x.com/2019/07/27/eMPfmT.png)
Subsequent calls will override values from previous calls in the same cycle, so the quantity will only be incremented once. If the next state depends on the current state, we recommend using the updater function form, instead:
![eMP47F.png](https://s2.ax1x.com/2019/07/27/eMP47F.png)

#### forceUpdate()
![eMiHUg.png](https://s2.ax1x.com/2019/07/27/eMiHUg.png)
By default, when your component’s state or props change, your component will re-render. If your `render()` method depends on some other data, you can tell React that the component needs re-rendering by calling `forceUpdate()`.

Calling `forceUpdate()` will cause `render()` to be called on the component, skipping `shouldComponentUpdate()`. This will trigger the normal lifecycle methods for child components, including the `shouldComponentUpdate()` method of each child. React will still only update the DOM if the markup changes.

Normally you should try to avoid all uses of `forceUpdate()` and only read from `this.props` and `this.state` in `render()`.

## Class Properties
- defaultProps
- displayName

#### defaultProps
`defaultProps` can be defined as a property on the component class itself, to set the default props for the class. This is used for undefined props, but not for null props. For example:
![eMFWoF.png](https://s2.ax1x.com/2019/07/27/eMFWoF.png)
If `props.color` is not provided, it will be set by default to <strong>'blue'</strong>:
![eMF4JJ.png](https://s2.ax1x.com/2019/07/27/eMF4JJ.png)
If `props.color` is set to null, it will remain null:
![eMEPIS.png](https://s2.ax1x.com/2019/07/27/eMEPIS.png)

#### displayName
The `displayName` string is used in debugging messages. Usually, you don’t need to set it explicitly because it’s inferred from the name of the function or class that defines the component. You might want to set it explicitly if you want to display a different name for debugging purposes or when you create a higher-order component.

The container components created by HOCs show up in the React Developer Tools like any other component. To ease debugging, choose a display name that communicates that it’s the result of a HOC.

The most common technique is to wrap the display name of the wrapped component. So if your higher-order component is named `withSubscription`, and the wrapped component’s display name is `CommentList`, use the display name `WithSubscription(CommentList)`:
![eMEUZ6.png](https://s2.ax1x.com/2019/07/27/eMEUZ6.png)

## Instance Properties
- props
- state

#### props
`this.props` contains the props that were defined by the caller of this component.

In particular, `this.props.children` is a special prop, typically defined by the child tags in the JSX expression rather than in the tag itself.

#### state
The state contains data specific to this component that may change over time. The state is user-defined, and it should be a plain JavaScript object.

If some value isn’t used for rendering or data flow (for example, a timer ID), you don’t have to put it in the state. Such values can be defined as fields on the component instance.

Never mutate `this.state` directly, as calling `setState()` afterwards may replace the mutation you made. Treat `this.state` as if it were immutable.
