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
If <em><ins>&lt;{forwardRef : true}&gt;</ins></em> has been passed to <em><ins>&lt;connect&gt;</ins></em>, adding a ref to the connected wrapper component will actually return the instance of the wrapped component.



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
