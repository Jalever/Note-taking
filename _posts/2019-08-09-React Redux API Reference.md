---
layout: post
title: (React Redux)React Redux API Reference
subtitle: Getting Started with React Redux
date: 2019-08-09
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---
- [connect()](#connect)
- [Provider](#provider)
- [connectAdvanced()](#connectadvanced)
- [batch()](#batch)
- [Hooks](#hooks)

## connect()
#### Overview
The <strong>connect()</strong> function connects a React component to a Redux store.

It provides its connected component with the pieces of the data it needs from the store, and the functions it can use to dispatch actions to the store.

It does not modify the component class passed to it; instead, it returns a new, connected component class that wraps the component you passed in.
![eHYhiq.png](https://s2.ax1x.com/2019/08/09/eHYhiq.png)
The <strong>mapStateToProps</strong> and <strong>mapDispatchToProps</strong> deals with your Redux store’s <strong>state</strong> and <strong>dispatch</strong>, respectively. <strong>state</strong> and <strong>dispatch</strong> will be supplied to your <strong>mapStateToProps</strong> or <strong>mapDispatchToProps</strong> functions as the first argument.

The returns of <strong>mapStateToProps</strong> and <strong>mapDispatchToProps</strong> are referred to internally as <strong>stateProps</strong> and <strong>dispatchProps</strong>, respectively. They will be supplied to <strong>mergeProps</strong>, if defined, as the first and the second argument, where the third argument will be <strong>ownProps</strong>. The combined result, commonly referred to as <strong>mergedProps</strong>, will then be supplied to your connected component.

#### connect() Parameters
<strong>connect</strong> accepts four different parameters, all optional. By convention, they are called:
![eHYhiq.png](https://s2.ax1x.com/2019/08/09/eHYhiq.png)
1. `mapStateToProps`?: <strong>Function</strong>
2. `mapDispatchToProps`?: <strong>Function</strong> | <strong>Object</strong>
3. `mergeProps`?: <strong>Function</strong>
4. `options`?: <strong>Object</strong>

###### mapStateToProps
If a mapStateToProps function is specified, the new wrapper component will subscribe to Redux store updates. This means that any time the store is updated, mapStateToProps will be called. The results of mapStateToProps must be a plain object, which will be merged into the wrapped component’s props. If you don't want to subscribe to store updates, pass null or undefined in place of mapStateToProps.
![eHUkGt.png](https://s2.ax1x.com/2019/08/09/eHUkGt.png)

<strong>Parameters</strong><br/>
1. state: Object
2. ownProps?: Object
A <em><ins>mapStateToProps</ins></em> function takes a maximum of two parameters. The number of declared function parameters (a.k.a. arity) affects when it will be called. This also determines whether the function will receive ownProps.

&nbsp;&nbsp;&nbsp;&nbsp;1.state
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your mapStateToProps function is declared as taking one parameter, it will be called whenever the store state changes, and given the store state as the only parameter.
![eHULwQ.png](https://s2.ax1x.com/2019/08/09/eHULwQ.png)

&nbsp;&nbsp;&nbsp;&nbsp;2.ownProps
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your <em><ins>mapStateToProps</ins></em> function is declared as taking two parameters, it will be called whenever the store state changes or when the wrapper component receives new props (based on shallow equality comparisons). It will be given the store state as the first parameter, and the wrapper component's props as the second parameter.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second parameter is normally referred to as <em><ins>ownProps</ins></em> by convention.
![eHaZf1.png](https://s2.ax1x.com/2019/08/09/eHaZf1.png)

<strong>Returns</strong><br/>
Your <em><ins>mapStateToProps</ins></em> functions are expected to return an object. This object, normally referred to as <em><ins>stateProps</ins></em>, will be merged as props to your connected component. If you define <em><ins>mergeProps</ins></em>, it will be supplied as the first parameter to <em><ins>mergeProps</ins></em>.
> You may define <em><ins>mapStateToProps</ins></em> and <em><ins>mapDispatchToProps</ins></em> as a factory function, i.e., you return a function instead of an object. In this case your returned function will be treated as the real <em><ins>mapStateToProps</ins></em> or <em><ins>mapDispatchToProps</ins></em>, and be called in subsequent calls.

###### mapDispatchToProps
![eHwPIJ.png](https://s2.ax1x.com/2019/08/09/eHwPIJ.png)
Conventionally called <em><ins>mapDispatchToProps</ins></em>, this second parameter to <em><ins>connect()</ins></em> may either be an object, a function, or not supplied.

Your component will receive dispatch by <em><ins>default</ins></em>, i.e., when you do not supply a second parameter to <em><ins>connect()</ins></em>:
![eHwmqO.png](https://s2.ax1x.com/2019/08/09/eHwmqO.png)
If you define a <em><ins>mapDispatchToProps</ins></em> as a function, it will be called with a maximum of two parameters.

<strong>Parameters</strong><br/>
1. dispatch: Function
2. ownProps?: Object

&nbsp;&nbsp;&nbsp;&nbsp;1.dispatch
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your <em><ins>mapDispatchToProps</ins></em> is declared as a function taking one parameter, it will be given the <em><ins>dispatch</ins></em> of your <em><ins>store</ins></em>.
![eH0F0S.png](https://s2.ax1x.com/2019/08/09/eH0F0S.png)

&nbsp;&nbsp;&nbsp;&nbsp;2.ownProps
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If your <em><ins>mapDispatchToProps</ins></em> function is declared as taking two parameters, it will be called with <em><ins>dispatch</ins></em> as the first parameter and the props passed to the wrapper component as the second parameter, and will be re-invoked whenever the connected component receives new props.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second parameter is normally referred to as <em><ins>ownProps</ins></em> by convention.
![eH0u60.png](https://s2.ax1x.com/2019/08/09/eH0u60.png)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The number of declared function parameters of <em><ins>mapDispatchToProps</ins></em> determines whether they receive ownProps.

<strong>Returns</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Your <em><ins>mapDispatchToProps</ins></em> functions are expected to return an object. Each fields of the object should be a function, calling which is expected to dispatch an action to the store.

&nbsp;&nbsp;&nbsp;&nbsp;The return of your <em><ins>mapDispatchToProps</ins></em> functions are regarded as <em><ins>dispatchProps</ins></em>. It will be merged as props to your connected component. If you define <em><ins>mergeProps</ins></em>, it will be supplied as the second parameter to <em><ins>mergeProps</ins></em>.
![eHBg54.png](https://s2.ax1x.com/2019/08/09/eHBg54.png)
> You may define <em><ins>mapStateToProps</ins></em> and <em><ins>mapDispatchToProps</ins></em> as a factory function, i.e., you return a function instead of an object. In this case your returned function will be treated as the real <em><ins>mapStateToProps</ins></em> or <em><ins>mapDispatchToProps</ins></em>, and be called in subsequent calls.

<strong>Object Shorthand Form</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<em><ins>mapDispatchToProps</ins></em> may be an object where each field is an action creator.
![eHD8zR.png](https://s2.ax1x.com/2019/08/09/eHD8zR.png)
&nbsp;&nbsp;&nbsp;&nbsp;In this case, React-Redux binds the <em><ins>dispatch</ins></em> of your store to each of the action creators using <em><ins>bindActionCreators</ins></em>. The result will be regarded as <em><ins>dispatchProps</ins></em>, which will be either directly merged to your connected components, or supplied to <em><ins>mergeProps</ins></em> as the second argument.
![eHDRw8.png](https://s2.ax1x.com/2019/08/09/eHDRw8.png)

###### mergeProps
![eH2fud.png](https://s2.ax1x.com/2019/08/09/eH2fud.png)
If specified, defines how the final props for your own wrapped component are determined. If you do not provide <em><ins>mergeProps</ins></em>, your wrapped component receives <em><ins>{ ...ownProps, ...stateProps, ...dispatchProps }</ins></em> by default.

<strong>Parameters</strong><br/>
<em><ins>mergeProps</ins></em> should be specified with maximum of three parameters. They are the result of <em><ins>mapStateToProps()</ins></em>, <em><ins>mapDispatchToProps()</ins></em>, and the wrapper component's <em><ins>props</ins></em>, respectively:

1. stateProps
2. dispatchProps
3. ownProps

The fields in the plain object you return from it will be used as the props for the wrapped component. You may specify this function to select a slice of the state based on props, or to bind action creators to a particular variable from props.

<strong>Returns</strong><br/>
The return value of <em><ins>mergeProps</ins></em> is referred to as <em><ins>mergedProps</ins></em> and the fields will be used as the props for the wrapped component.

###### options
![eHRzsH.png](https://s2.ax1x.com/2019/08/09/eHRzsH.png)
![eHWFFP.png](https://s2.ax1x.com/2019/08/09/eHWFFP.png)

<strong>context</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;React-Redux v6 allows you to supply a custom context instance to be used by React-Redux. You need to pass the instance of your context to both <strong>&lt;Provider /&gt;</strong> and your connected component. You may pass the context to your connected component either by passing it here as a field of option, or as a prop to your connected component in rendering.
![eHfwuQ.png](https://s2.ax1x.com/2019/08/09/eHfwuQ.png)


<strong>pure</strong><br/>
- default value: true
Assumes that the wrapped component is a “pure” component and does not rely on any input or state other than its props and the selected Redux store’s state.

When <em><ins>&lt;options.pure&gt;</ins></em> is true, <em><ins>&lt;connect&gt;</ins></em> performs several equality checks that are used to avoid unnecessary calls to <em><ins>&lt;mapStateToProps&gt;</ins></em>, <em><ins>&lt;mapDispatchToProps&gt;</ins></em>, <em><ins>&lt;mergeProps&gt;</ins></em>, and ultimately to <em><ins>&lt;render&gt;</ins></em>. These include <em><ins>&lt;areStatesEqual&gt;</ins></em>, <em><ins>&lt;areOwnPropsEqual&gt;</ins></em>, <em><ins>&lt;areStatePropsEqual&gt;</ins></em>, and <em><ins>&lt;areMergedPropsEqual&gt;</ins></em>. While the defaults are probably appropriate 99% of the time, you may wish to override them with custom implementations for performance or other reasons.

<strong>areStatesEqual</strong><br/>
![eH5N36.png](https://s2.ax1x.com/2019/08/09/eH5N36.png)
- default value: <em><ins>strictEqual: (next, prev) => prev === next</ins></em>

When pure, compares incoming store state to its previous value.

Example 1
![eH5g8P.png](https://s2.ax1x.com/2019/08/09/eH5g8P.png)
You may wish to override <em><ins>areStatesEqual</ins></em> if your <em><ins>mapStateToProps</ins></em> function is computationally expensive and is also only concerned with a small slice of your state. The example above will effectively ignore state changes for everything but that slice of state.

Example 2

If you have impure reducers that mutate your store state, you may wish to override <em><ins>areStatesEqual</ins></em> to always return false:
![eH5hDg.png](https://s2.ax1x.com/2019/08/09/eH5hDg.png)
This would likely impact the other equality checks as well, depending on your <em><ins>mapStateToProps</ins></em> function.

<strong>areOwnPropsEqual</strong><br/>
![eH4spV.png](https://s2.ax1x.com/2019/08/09/eH4spV.png)
- default value: <em><ins>shallowEqual: (objA, objB) => boolean</ins></em> ( returns <em><ins>true</ins></em> when each field of the objects is equal )

When pure, compares incoming props to its previous value.

You may wish to override <em><ins>areOwnPropsEqual</ins></em> as a way to whitelist incoming props. You'd also have to implement <em><ins>mapStateToProps</ins></em>, <em><ins>mapDispatchToProps</ins></em> and <em><ins>mergeProps</ins></em> to also whitelist props.

<strong>areStatePropsEqual</strong><br/>
![eHhi28.png](https://s2.ax1x.com/2019/08/09/eHhi28.png)
- type: <em><ins>function</ins></em>
- default value: <em><ins>shallowEqual</ins></em>
When pure, compares the result of <em><ins>mapStateToProps</ins></em> to its previous value.

<strong>areMergedPropsEqual</strong><br/>
![eHhgII.png](https://s2.ax1x.com/2019/08/09/eHhgII.png)
- default value: <em><ins>shallowEqual</ins></em>
When pure, compares the result of <em><ins>mergeProps</ins></em> to its previous value.

You may wish to override <em><ins>areStatePropsEqual</ins></em> to use <em><ins>strictEqual</ins></em> if your <em><ins>mapStateToProps</ins></em> uses a memoized selector that will only return a new object if a relevant prop has changed. This would be a very slight performance improvement, since would avoid extra equality checks on individual props each time <em><ins>mapStateToProps</ins></em> is called.

You may wish to override <em><ins>areMergedPropsEqual</ins></em> to implement a <em><ins>deepEqual</ins></em> if your selectors produce complex props. ex: nested objects, new arrays, etc. (The deep equal check may be faster than just re-rendering.)

<strong>forwardRef</strong><br/>
If <em><ins>{forwardRef : true}</ins></em> has been passed to <em><ins>&lt;connect&gt;</ins></em>, adding a ref to the connected wrapper component will actually return the instance of the wrapped component.



#### connect() Returns
The return of <strong>connect()</strong> is a wrapper function that takes your component and returns a wrapper component with the additional props it injects.
![eH2SpD.png](https://s2.ax1x.com/2019/08/09/eH2SpD.png)
In most cases, the wrapper function will be called right away, without being saved in a temporary variable:
![eH2GNV.png](https://s2.ax1x.com/2019/08/09/eH2GNV.png)

#### Example Usage
Because <em><ins>connect</ins></em> is so flexible, it may help to see some additional examples of how it can be called:

<strong>Inject just <em><ins>dispatch</ins></em> and don't listen to store</strong><br/>
![eH6sN8.png](https://s2.ax1x.com/2019/08/09/eH6sN8.png)

<strong>Inject all action creators (addTodo, completeTodo, ...) without subscribing to the store</strong><br/>
![eH6HCF.png](https://s2.ax1x.com/2019/08/09/eH6HCF.png)

<strong>Inject dispatch and every field in the global state</strong><br/>
> Don’t do this! It kills any performance optimizations because TodoApp will rerender after every state change. It’s better to have more granular connect() on several components in your view hierarchy that each only listen to a relevant slice of the state.

![eH6HCF.png](https://s2.ax1x.com/2019/08/09/eH6HCF.png)

<strong>Inject dispatch and todos</strong><br/>
![eHceVP.png](https://s2.ax1x.com/2019/08/09/eHceVP.png)

<strong>Inject todos and all action creators</strong><br/>
![eHc3Ks.png](https://s2.ax1x.com/2019/08/09/eHc3Ks.png)

<strong>Inject todos and all action creators (addTodo, completeTodo, ...) as actions</strong><br/>
![eHcw24.png](https://s2.ax1x.com/2019/08/09/eHcw24.png)

<strong>Inject todos and a specific action creator (addTodo)</strong><br/>
![eHchxH.png](https://s2.ax1x.com/2019/08/09/eHchxH.png)

<strong>Inject todos and specific action creators (addTodo and deleteTodo) with shorthand syntax</strong><br/>
![eHcHdP.png](https://s2.ax1x.com/2019/08/09/eHcHdP.png)

<strong>Inject todos, todoActionCreators as todoActions, and counterActionCreators as counterActions</strong><br/>
![eHcXRg.png](https://s2.ax1x.com/2019/08/09/eHcXRg.png)

<strong>Inject todos, and todoActionCreators and counterActionCreators together as actions</strong><br/>
![eHgCd0.png](https://s2.ax1x.com/2019/08/09/eHgCd0.png)

<strong>Inject todos, and all todoActionCreators and counterActionCreators directly as props</strong><br/>
![eHgPoV.png](https://s2.ax1x.com/2019/08/09/eHgPoV.png)

<strong>Inject todos of a specific user depending on props</strong><br/>
![eHgAWF.png](https://s2.ax1x.com/2019/08/09/eHgAWF.png)

<strong>Inject todos of a specific user depending on props, and inject props.userId into the action</strong><br/>
![eHgue1.png](https://s2.ax1x.com/2019/08/09/eHgue1.png)

#### Notes
###### The Arity of mapToProps Functions
The number of declared function parameters of <strong>mapStateToProps</strong> and <strong>mapDispatchToProps</strong> determines whether they receive <strong>ownProps</strong>
> <strong>ownProps</strong> is not passed to <strong>mapStateToProps</strong> and <strong>mapDispatchToProps</strong> if the formal definition of the function contains one mandatory parameter (function has length 1). For example, functions defined like below won't receive <strong>ownProps</strong> as the second argument

![eHdDKK.png](https://s2.ax1x.com/2019/08/09/eHdDKK.png)
Functions with no mandatory parameters or two parameters*will receive <strong>ownProps</strong>.
![eHdf2t.png](https://s2.ax1x.com/2019/08/09/eHdf2t.png)

###### Factory Functions
If your <strong>mapStateToProps</strong> or <strong>mapDispatchToProps</strong> functions return a function, they will be called once when the component instantiates, and their returns will be used as the actual <strong>mapStateToProps</strong>, <strong>mapDispatchToProps</strong>, functions respectively, in their subsequent calls.

The factory functions are commonly used with memoized selectors. This gives you the ability to create component-instance-specific selectors inside the closure:
![eHazAH.png](https://s2.ax1x.com/2019/08/09/eHazAH.png)

## Provider
#### Overview

#### Props
###### store
Type: Redux Store

The single Redux <strong>store</strong> in your application.

###### children
ReactElement

The root of your component hierarchy.

###### context
You may provide a context instance. If you do so, you will need to provide the same context instance to all of your connected components as well. Failure to provide the correct context results in runtime error:  
> Could not find "store" in the context of "Connect(MyComponent)". Either wrap the root component in a <strong>&lt;Provider&gt;</strong>, or pass a custom React context provider to <strong>&lt;Provider&gt;</strong> and the corresponding React context consumer to Connect(Todo) in connect options.

> You do not need to provide custom context in order to access the store. React Redux exports the context instance it uses by default so that you can access the store by:
![ebtKrF.png](https://s2.ax1x.com/2019/08/09/ebtKrF.png)

#### Example Usage
In the example below, the <strong>&lt;App /&gt;</strong> component is our root-level component. This means it’s at the very top of our component hierarchy.

###### Vanilla React Example
![ebYVXD.png](https://s2.ax1x.com/2019/08/09/ebYVXD.png)

###### Usage with React Router
![ebY8c8.png](https://s2.ax1x.com/2019/08/09/ebY8c8.png)

## connectAdvanced()
- [Arguments](#arguments)
    - [selectorFactory](#selectorfactory)
    - [connectOptions](#connectoptions)
- [Returns](#returns)
    - [Static Properties](#static-properties)
    - [Static Methods](#static-methods)
- [Remarks](#remarks)
- [Examples](#examples)

![ebQJoV.png](https://s2.ax1x.com/2019/08/09/ebQJoV.png)
Connects a React component to a Redux store. It is the base for connect() but is less opinionated about how to combine state, props, and dispatch into your final props. It makes no assumptions about defaults or memoization of results, leaving those responsibilities to the caller.

It does not modify the component class passed to it; instead, it returns a new, connected component class for you to use.

Most applications will not need to use this, as the default behavior in connect is intended to work for most use cases.

#### Arguments
###### selectorFactory
![eblfhT.png](https://s2.ax1x.com/2019/08/09/eblfhT.png)
Type: <strong>Function</strong>

Initializes a selector function (during each instance's constructor). That selector function is called any time the connector component needs to compute new props, as a result of a store state change or receiving new props. The result of <strong>selector</strong> is expected to be a plain object, which is passed as the props to the wrapped component. If a consecutive call to <strong>selector</strong> returns the same object (<strong>===</strong>) as its previous call, the component will not be re-rendered. It's the responsibility of <strong>selector</strong> to return that previous object when appropriate.

###### connectOptions
Type: <strong>Object</strong>

If specified, further customizes the behavior of the connector.

&nbsp;&nbsp;<strong>getDisplayName</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>Function</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;computes the connector component's displayName property relative to that of the wrapped component. Usually overridden by wrapper functions. Default value: <em><ins>name => 'ConnectAdvanced('+name+')'</ins></em>

&nbsp;&nbsp;<strong>methodName</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>String</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;shown in error messages. Usually overridden by wrapper functions. Default value: <em><ins>'connectAdvanced'</ins></em>

&nbsp;&nbsp;<strong>renderCountProp</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>String</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;if defined, a property named this value will be added to the props passed to the wrapped component. Its value will be the number of times the component has been rendered, which can be useful for tracking down unnecessary re-renders. Default value: <em><ins>undefined</ins></em>

&nbsp;&nbsp;<strong>shouldHandleStateChanges</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>Boolean</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;controls whether the connector component subscribes to redux store state changes. If set to false, it will only re-render when parent component re-renders. Default value: <em><ins>true</ins></em>

&nbsp;&nbsp;<strong>forwardRef</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>Boolean</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;If true, adding a ref to the connected wrapper component will actually return the instance of the wrapped component.

&nbsp;&nbsp;Additionally, any extra options passed via <em><ins>connectOptions</ins></em> will be passed through to your <em><ins>selectorFactory</ins></em> in the <em><ins>factoryOptions</ins></em> argument.

#### Returns
A higher-order React component class that builds props from the store state and passes them to the wrapped component. A higher-order component is a function which accepts a component argument and returns a new component.

###### Static Properties
&nbsp;&nbsp;<strong>WrappedComponent</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Type: <em><ins>Component</ins></em><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The original component class passed to <em><ins>connectAdvanced(...)(Component)</ins></em>.

###### Static Methods
All the original static methods of the component are hoisted.

#### Remarks
Since <strong>connectAdvanced</strong> returns a higher-order component, it needs to be invoked two times. The first time with its arguments as described above, and a second time, with the component: <strong>connectAdvanced(selectorFactory)(MyComponent)</strong>.

<strong>connectAdvanced</strong> does not modify the passed React component. It returns a new, connected component, that you should use instead.

#### Examples
<strong>Inject todos of a specific user depending on props, and inject props.userId into the action</strong><br/>
![eblCkV.png](https://s2.ax1x.com/2019/08/09/eblCkV.png)

## batch()
![ebmCFg.png](https://s2.ax1x.com/2019/08/09/ebmCFg.png)
React's <strong>unstable_batchedUpdate()</strong> API allows any React updates in an event loop tick to be batched together into a single render pass. React already uses this internally for its own event handler callbacks. This API is actually part of the renderer packages like ReactDOM and React Native, not the React core itself.

Since React-Redux needs to work in both ReactDOM and React Native environments, we've taken care of importing this API from the correct renderer at build time for our own use. We also now re-export this function publicly ourselves, renamed to <strong>batch()</strong>. You can use it to ensure that multiple actions dispatched outside of React only result in a single render update, like this:
![ebmnTU.png](https://s2.ax1x.com/2019/08/09/ebmnTU.png)

## Hooks

- [Using Hooks in a React Redux App](#using hooks in a react redux app)
    - [useSelector()](#useselector)
    - [useDispatch()](#usedispatch)
    - [useStore()](#usestore)
- [Usage Warnings](#useselector)
    - [Stale Props and "Zombie Children"](#stale-props-and-zombie-children)
    - [Performance](#performance)

React's new "hooks" APIs give function components the ability to use local component state, execute side effects, and more.

React Redux now offers a set of hook APIs as an alternative to the existing <strong>connect()</strong> Higher Order Component. These APIs allow you to subscribe to the Redux store and dispatch actions, without having to wrap your components in <strong>connect()</strong>.

These hooks were first added in v7.1.0.

#### Using Hooks in a React Redux App
As with connect(), you should start by wrapping your entire application in a <Provider> component to make the store available throughout the component tree:
![eOnT6H.png](https://s2.ax1x.com/2019/08/10/eOnT6H.png)
From there, you may import any of the listed React Redux hooks APIs and use them within your function components.

###### useSelector()
![eOlzOe.png](https://s2.ax1x.com/2019/08/10/eOlzOe.png)
Allows you to extract data from the Redux store state, using a selector function.

The selector is approximately equivalent to the mapStateToProps argument to connect conceptually. The selector will be called with the entire Redux store state as its only argument. The selector will be run whenever the function component renders. <strong>useSelector()</strong> will also subscribe to the Redux store, and run your selector whenever an action is dispatched.

However, there are some differences between the selectors passed to <strong>useSelector()</strong> and a <strong>mapState</strong> function:
- The selector may return any value as a result, not just an object. The return value of the selector will be used as the return value of the <strong>useSelector()</strong> hook.
- When an action is dispatched, <strong>useSelector()</strong> will do a shallow comparison of the previous selector result value and the current result value. If they are different, the component will be forced to re-render. If they are the same, the component will not re-render.
- The selector function does not receive an <strong>ownProps</strong> argument. However, props can be used through closure (see the examples below) or by using a curried selector.
- Extra care must be taken when using memoizing selectors.
- <strong>useSelector()</strong> uses strict <strong>===</strong> reference equality checks by default, not shallow equality (see the following section for more details).

You may call <strong>useSelector()</strong> multiple times within a single function component. Each call to <strong>useSelector()</strong> creates an individual subscription to the Redux store. Because of the React update batching behavior used in React Redux v7, a dispatched action that causes multiple <strong>useSelector()</strong>s in the same component to return new values should only result in a single re-render.

<strong>Equality Comparisons and Updates</strong><br/>
When the function component renders, the provided selector function will be called and its result will be returned from the <strong>useSelector()</strong> hook. (A cached result may be returned if the selector has been run and hasn't changed.)

However, when an action is dispatched to the Redux store, <strong>useSelector()</strong> only forces a re-render if the selector result appears to be different than the last result. As of v7.1.0-alpha.5, the default comparison is a strict <strong>===</strong> reference comparison. This is different than <strong>connect()</strong>, which uses shallow equality checks on the results of <strong>mapState</strong> calls to determine if re-rendering is needed. This has several implications on how you should use <strong>useSelector()</strong>.

With <strong>mapState</strong>, all individual fields were returned in a combined object. It didn't matter if the return object was a new reference or not - <strong>connect()</strong> just compared the individual fields. With <strong>useSelector()</strong>, returning a new object every time will always force a re-render by default. If you want to retrieve multiple values from the store, you can:
- Call <strong>useSelector()</strong> multiple times, with each call returning a single field value
- Use Reselect or a similar library to create a memoized selector that returns multiple values in one object, but only returns a new object when one of the values has changed.
- Use the <strong>shallowEqual</strong> function from React-Redux as the <strong>equalityFn</strong> argument to <strong>useSelector()</strong>, like:
![eO39jU.png](https://s2.ax1x.com/2019/08/10/eO39jU.png)
The optional comparison function also enables using something like Lodash's <strong>_.isEqual()</strong> or Immutable.js's comparison capabilities.

<strong>useSelector Examples</strong><br/>
Basic usage:
![eO3ngK.png](https://s2.ax1x.com/2019/08/10/eO3ngK.png)
Using props via closure to determine what to extract:
![eO37P1.png](https://s2.ax1x.com/2019/08/10/eO37P1.png)

<strong>Using memoizing selectors</strong><br/>
When using <strong>useSelector</strong> with an inline selector as shown above, a new instance of the selector is created whenever the component is rendered. This works as long as the selector does not maintain any state. However, memoizing selectors (e.g. created via <strong>createSelector</strong> from <strong>reselect</strong>) do have internal state, and therefore care must be taken when using them. Below you can find typical usage scenarios for memoizing selectors.

When the selector does only depend on the state, simply ensure that it is declared outside of the component so that the same selector instance is used for each render:
![eOJng0.png](https://s2.ax1x.com/2019/08/10/eOJng0.png)
The same is true if the selector depends on the component's props, but will only ever be used in a single instance of a single component:
![eOJXrT.png](https://s2.ax1x.com/2019/08/10/eOJXrT.png)
However, when the selector is used in multiple component instances and depends on the component's props, you need to ensure that each component instance gets its own selector instance
![eOYyeU.png](https://s2.ax1x.com/2019/08/10/eOYyeU.png)
![eOYWWR.png](https://s2.ax1x.com/2019/08/10/eOYWWR.png)

###### useDispatch()
![eOYqFH.png](https://s2.ax1x.com/2019/08/10/eOYqFH.png)
This hook returns a reference to the <strong>dispatch</strong> function from the Redux store. You may use it to dispatch actions as needed.

Examples
![eOtQk4.png](https://s2.ax1x.com/2019/08/10/eOtQk4.png)
When passing a callback using <strong>dispatch</strong> to a child component, it is recommended to memoize it with <strong>useCallback</strong>, since otherwise child components may render unnecessarily due to the changed reference.
![eOtYX6.png](https://s2.ax1x.com/2019/08/10/eOtYX6.png)

###### useStore()
![eOtRHS.png](https://s2.ax1x.com/2019/08/10/eOtRHS.png)
This hook returns a reference to the same Redux store that was passed in to the <strong>&lt;Provider&gt;</strong> component.

This hook should probably not be used frequently. Prefer <strong>useSelector()</strong> as your primary choice. However, this may be useful for less common scenarios that do require access to the store, such as replacing reducers.

Examples
![eONiDK.png](https://s2.ax1x.com/2019/08/10/eONiDK.png)

#### Usage Warnings
###### Stale Props and "Zombie Children"
One of the most difficult aspects of React Redux's implementation is ensuring that if your <strong>mapStateToProps</strong> function is defined as <strong>(state, ownProps)</strong>, it will be called with the "latest" props every time. Up through version 4, there were recurring bugs reported involving edge case situations, such as errors thrown from a <strong>mapState</strong> function for a list item whose data had just been deleted.

Starting with version 5, React Redux has attempted to guarantee that consistency with <strong>ownProps</strong>. In version 7, that is implemented using a custom <strong>Subscription</strong> class internally in <strong>connect()</strong>, which forms a nested hierarchy. This ensures that connected components lower in the tree will only receive store update notifications once the nearest connected ancestor has been updated. However, this relies on each <strong>connect()</strong> instance overriding part of the internal React context, supplying its own unique <strong>Subscription</strong> instance to form that nesting, and rendering the <strong>&lt;ReactReduxContext.Provider&gt;</strong> with that new context value.

With hooks, there is no way to render a context provider, which means there's also no nested hierarchy of subscriptions. Because of this, the "stale props" and "zombie child" issues may potentially re-occur in an app that relies on using hooks instead of <strong>connect()</strong>.

Specifically, "stale props" means any case where:
- a selector function relies on this component's props to extract data
- a parent component would re-render and pass down new props as a result of an action
- but this component's selector function executes before this component has had a chance to re-render with those new props

Depending on what props were used and what the current store state is, this may result in incorrect data being returned from the selector, or even an error being thrown.

"Zombie child" refers specifically to the case where:

- Multiple nested connected components are mounted in a first pass, causing a child component to subscribe to the store before its parent
- An action is dispatched that deletes data from the store, such as a todo item
- The parent component would stop rendering that child as a result
- However, because the child subscribed first, its subscription runs before the parent stops rendering it. When it reads a value from the store based on props, that data no longer exists, and if the extraction logic is not careful, this may result in an error being thrown.

<strong>useSelector()</strong> tries to deal with this by catching all errors that are thrown when the selector is executed due to a store update (but not when it is executed during rendering). When an error occurs, the component will be forced to render, at which point the selector is executed again. This works as long as the selector is a pure function and you do not depend on the selector throwing errors.

If you prefer to deal with this issue yourself, here are some possible options for avoiding these problems altogether with <strong>useSelector()</strong>:

- Don't rely on props in your selector function for extracting data
- In cases where you do rely on props in your selector function and those props may change over time, or the data you're extracting may be based on items that can be deleted, try writing the selector functions defensively. Don't just reach straight into <strong>state.todos[props.id].name</strong> - read <strong>state.todos[props.id]</strong> first, and verify that it exists before trying to read <strong>todo.name</strong>.
- Because <strong>connect</strong> adds the necessary <strong>Subscription</strong> to the context provider and delays evaluating child subscriptions until the connected component has re-rendered, putting a connected component in the component tree just above the component using <strong>useSelector</strong> will prevent these issues as long as the connected component gets re-rendered due to the same store update as the hooks component.

###### Performance
As mentioned earlier, by default <strong>useSelector()</strong> will do a reference equality comparison of the selected value when running the selector function after an action is dispatched, and will only cause the component to re-render if the selected value changed. However, unlike <strong>connect()</strong>, <strong>useSelector()</strong> does not prevent the component from re-rendering due to its parent re-rendering, even if the component's props did not change.

If further performance optimizations are necessary, you may consider wrapping your function component in <strong>React.memo()</strong>:
![eOUAs0.png](https://s2.ax1x.com/2019/08/10/eOUAs0.png)
