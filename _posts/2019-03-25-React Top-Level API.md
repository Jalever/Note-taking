---
layout: post
title: React Top-Level API
subtitle: React API Reference
date: 2019-03-25
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [Components](#components)
    - [React.Component](#reactcomponent)
    - [React.PureComponent](#reactpurecomponent)
    - [React.memo](#reactmemo)
- [Creating React Elements](#creating-react-elements)
    - [React.createElement()](#reactcreateelement)
    - [React.createFactory()](#reactcreatefactory)
- [Transforming Elements](#transforming-elements)
    - [cloneElement()](#cloneelement)
    - [isValidElement()](#isvalidelement)
    - [React.Children](#reactchildren)
      - [React.Children.map](#reactchildrenmap)
      - [React.Children.forEach](#reactchildrenforeach)
      - [React.Children.count](#reactchildrencount)
      - [React.Children.only](#reactchildrenonly)
      - [React.Children.toArray](#reactchildrentoarray)
- [Fragments](#fragments)
    - [React.Fragment](#reactfragment)
- [Refs](#refs)
    - [React.CreateRef](#reactcreateref)
    - [React.forwardRef](#reactforwardref)
- [Suspense](#suspense)
    - [React.lazy](#reactlazy)
    - [React.Suspense](#reactsuspense)
- [Hooks](#hooks)

## Components
React components let you split the UI into independent, reusable pieces, and think about each piece in isolation. React components can be defined by subclassing `React.Component` or `React.PureComponent`.
- [React.Component](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactcomponent)
- [React.PureComponent](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactpurecomponent)

React components can also be defined as functions which can be wrapped:
- [React.memo](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactmemo)

#### React.Component
`React.Component` is the base class for React components when they are defined using ES6 classes:
![eM1ta9.png](https://s2.ax1x.com/2019/07/27/eM1ta9.png)

#### React.PureComponent
`React.PureComponent` is similar to `React.Component`. The difference between them is that `React.Component` doesn’t implement `shouldComponentUpdate()`, but `React.PureComponent` implements it with a shallow prop and state comparison.

If your React component’s `render()` function renders the same result given the same props and state, you can use `React.PureComponent` for a performance boost in some cases.

> `React.PureComponent`’s `shouldComponentUpdate()` only shallowly compares the objects. If these contain complex data structures, it may produce false-negatives for deeper differences. Only extend `PureComponent` when you expect to have simple props and state, or use `forceUpdate()` when you know deep data structures have changed. Or, consider using immutable objects to facilitate fast comparisons of nested data.<br/><br/>
> Furthermore, `React.PureComponent`’s `shouldComponentUpdate()` skips prop updates for the whole component subtree. Make sure all the children components are also “pure”.

#### React.memo
![eM3SLF.png](https://s2.ax1x.com/2019/07/27/eM3SLF.png)
`React.memo` is a Higher Order Component. It’s similar to `React.PureComponent` but for function components instead of classes.

If your function component renders the same result given the same props, you can wrap it in a call to `React.memo` for a performance boost in some cases by memoizing the result. This means that React will skip rendering the component, and reuse the last rendered result.

By default it will only shallowly compare complex objects in the props object. If you want control over the comparison, you can also provide a custom comparison function as the second argument.
![eM3doj.png](https://s2.ax1x.com/2019/07/27/eM3doj.png)
This method only exists as a Performance Optimization. Do not rely on it to “prevent” a render, as this can lead to bugs.
> Unlike the `shouldComponentUpdate()` method on class components, the `areEqual` function returns `true` if the props are equal and `false` if the props are not equal. This is the inverse from `shouldComponentUpdate`.

## Creating React Elements
We recommend using JSX to describe what your UI should look like. Each JSX element is just syntactic sugar for calling `React.createElement()`. You will not typically invoke the following methods directly if you are using JSX.
- [createElement()](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactcreateelement)
- [createFactory()](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactcreatefactory)

#### React.createElement()
![eMGp59.png](https://s2.ax1x.com/2019/07/27/eMGp59.png)
Create and return a new <strong>React element</strong> of the given type. The type argument can be either a tag name string (such as '`div`' or '`span`'), a <strong>React component</strong> type (a class or a function), or a <strong>React fragment</strong> type.

Code written with JSX will be converted to use `React.createElement()`. You will not typically invoke `React.createElement()` directly if you are using JSX.

#### React.createFactory()
![eMGVbD.png](https://s2.ax1x.com/2019/07/27/eMGVbD.png)

Return a function that produces React elements of a given type. Like <strong>React.createElement()</strong>, the type argument can be either a tag name string (such as '`div`' or '`span`'), a <strong>React component</strong> type (a class or a function), or a <strong>React fragment</strong> type.

This helper is considered legacy, and we encourage you to either use JSX or use `React.createElement()` directly instead.

You will not typically invoke `React.createFactory()` directly if you are using JSX.

## Transforming Elements
`React` provides several APIs for manipulating elements:
- [cloneElement() ](https://jalever.github.io/2019/03/25/React-Top-Level-API/#cloneelement)
- [isValidElement()](https://jalever.github.io/2019/03/25/React-Top-Level-API/#isvalidelement)
- [React.Children](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactchildren)
    - [React.Children.forEach](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactchildrenforeach)
    - [React.Children.count](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactchildrencount)
    - [React.Children.only](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactchildrenonly)
    - [React.Children.toArray](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactchildrentoarray)

#### cloneElement()
![eMGIsK.png](https://s2.ax1x.com/2019/07/27/eMGIsK.png)
Clone and return a new React element using `element` as the starting point. The resulting element will have the original element’s props with the new props merged in shallowly. New children will replace existing children. `key` and `ref` from the original element will be preserved.

`React.cloneElement()` is almost equivalent to:
![eMGbIH.png](https://s2.ax1x.com/2019/07/27/eMGbIH.png)
However, it also preserves `ref`s. This means that if you get a child with a `ref` on it, you won’t accidentally steal it from your ancestor. You will get the same `ref` attached to your new element.

#### isValidElement()
![eMJPoQ.png](https://s2.ax1x.com/2019/07/27/eMJPoQ.png)
Verifies the object is a React element. Returns `true` or `false`.

#### React.Children
`React.Children` provides utilities for dealing with the `this.props.children` opaque data structure.

###### React.Children.map
![eMJmLT.png](https://s2.ax1x.com/2019/07/27/eMJmLT.png)
Invokes a function on every immediate child contained within `children` with `this` set to `thisArg`. If `children` is an array it will be traversed and the function will be called for each child in the array. If children is `null` or `undefined`, this method will return `null` or `undefined` rather than an array.
> If `children` is a `Fragment` it will be treated as a single child and not traversed.

###### React.Children.forEach
![eMJawD.png](https://s2.ax1x.com/2019/07/27/eMJawD.png)
Like `React.Children.map()` but does not return an array.

###### React.Children.count
![eMJ0FH.png](https://s2.ax1x.com/2019/07/27/eMJ0FH.png)
Returns the total number of components in `children`, equal to the number of times that a callback passed to `map` or `forEach` would be invoked.

###### React.Children.only
![eMJ2m8.png](https://s2.ax1x.com/2019/07/27/eMJ2m8.png)
Verifies that `children` has only one child (a React element) and returns it. Otherwise this method throws an error.
> `React.Children.only()` does not accept the return value of `React.Children.map()` because it is an array rather than a `React` element.

###### React.Children.toArray
![eMJL0U.png](https://s2.ax1x.com/2019/07/27/eMJL0U.png)
Returns the `children` opaque data structure as a flat array with keys assigned to each child. Useful if you want to manipulate collections of children in your render methods, especially if you want to reorder or slice `this.props.children` before passing it down.
> `React.Children.toArray()` changes keys to preserve the semantics of nested arrays when flattening lists of children. That is, `toArray` prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.

## Fragments
React also provides a component for rendering multiple elements without a wrapper.
- [React.Fragment](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactfragment)

#### React.Fragment
The `React.Fragment` component lets you return multiple elements in a `render()` method without creating an additional DOM element
![eMYUcq.png](https://s2.ax1x.com/2019/07/27/eMYUcq.png)
You can also use it with the shorthand `<></>` syntax.

## Refs
- [React.createRef](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactcreateref)
- [React.forwardRef](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactforwardref)

#### React.CreateRef
`React.createRef` creates a `ref` that can be attached to `React` elements via the `ref` attribute.
![eMYsN4.png](https://s2.ax1x.com/2019/07/27/eMYsN4.png)

#### React.forwardRef
`React.forwardRef` creates a React component that forwards the `ref` attribute it receives to another component below in the tree.

`React.forwardRef` accepts a rendering function as an argument. React will call this function with `props` and `ref` as two arguments. This function should return a React node.
![eMY4HO.png](https://s2.ax1x.com/2019/07/27/eMY4HO.png)
This technique is not very common but is particularly useful in two scenarios:

###### Forwarding refs to DOM components
Consider a `FancyButton` component that renders the native button DOM element:
![eMYLvt.png](https://s2.ax1x.com/2019/07/27/eMYLvt.png)

React components hide their implementation details, including their rendered output. Other components using `FancyButton` usually will not need to obtain a ref to the inner `button` DOM element. This is good because it prevents components from relying on each other’s DOM structure too much.

Although such encapsulation is desirable for application-level components like `FeedStory` or `Comment`, it can be inconvenient for highly reusable “leaf” components like `FancyButton` or `MyTextInput`. These components tend to be used throughout the application in a similar manner as a regular DOM `button` and `input`, and accessing their DOM nodes may be unavoidable for managing focus, selection, or animations.

Ref forwarding is an opt-in feature that lets some components take a ref they receive, and pass it further down (in other words, “forward” it) to a child.

In the example below, `FancyButton` uses `React.forwardRef` to obtain the `ref` passed to it, and then forward it to the DOM `button` that it renders:
![eMYjDf.png](https://s2.ax1x.com/2019/07/27/eMYjDf.png)
This way, components using `FancyButton` can get a ref to the underlying `button` DOM node and access it if necessary—just like if they used a DOM `button` directly.

Here is a step-by-step explanation of what happens in the above example:

1. We create a React ref by calling `React.createRef` and assign it to a ref variable.
2. We pass our `ref` down to `<FancyButton ref={ref}>` by specifying it as a JSX attribute.
3. React passes the `ref` to the `(props, ref) => ...` function inside `forwardRef` as a second argument.
4. We forward this `ref` argument down to `<button ref={ref}>` by specifying it as a JSX attribute.
5. When the ref is attached, `ref.current` will point to the `<button>` DOM node.

> The second `ref` argument only exists when you define a component with `React.forwardRef` call. Regular function or class components don’t receive the `ref` argument, and ref is not available in props either.

> Ref forwarding is not limited to DOM components. You can forward refs to class component instances, too.

###### Forwarding refs in higher-order-components
This technique can also be particularly useful with higher-order components (also known as `HOC`s). Let’s start with an example HOC that logs component props to the console:
![eMti2n.png](https://s2.ax1x.com/2019/07/27/eMti2n.png)

The “logProps” HOC passes all `props` through to the component it wraps, so the rendered output will be the same. For example, we can use this HOC to log all props that get passed to our “fancy button” component:
![eMttaD.png](https://s2.ax1x.com/2019/07/27/eMttaD.png)

There is one caveat to the above example: refs will not get passed through. That’s because `ref` is not a prop. Like `key`, it’s handled differently by React. If you add a ref to a HOC, the ref will refer to the outermost container component, not the wrapped component.

This means that refs intended for our `FancyButton` component will actually be attached to the `LogProps` component:
![eMtcdS.png](https://s2.ax1x.com/2019/07/27/eMtcdS.png)

Fortunately, we can explicitly forward refs to the inner `FancyButton` component using the `React.forwardRef` API. `React.forwardRef` accepts a render function that receives `props` and `ref` parameters and returns a React node. For example:
![eMNVSA.png](https://s2.ax1x.com/2019/07/27/eMNVSA.png)
![eMNKw8.png](https://s2.ax1x.com/2019/07/27/eMNKw8.png)
![eMN1YQ.png](https://s2.ax1x.com/2019/07/27/eMN1YQ.png)

## Suspense
Suspense lets components “wait” for something before rendering. Today, Suspense only supports one use case: loading components dynamically with React.lazy. In the future, it will support other use cases like data fetching.
- [React.lazy](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactlazy)
- [React.Suspense](https://jalever.github.io/2019/03/25/React-Top-Level-API/#reactsuspense)

#### React.lazy
`React.lazy()` lets you define a component that is loaded dynamically. This helps reduce the bundle size to delay loading components that aren’t used during the initial render.
![eMNcOx.png](https://s2.ax1x.com/2019/07/27/eMNcOx.png)
Note that rendering `lazy` components requires that there’s a `<React.Suspense>` component higher in the rendering tree. This is how you specify a loading indicator.

<strong>Before: </strong>
![eMNopd.png](https://s2.ax1x.com/2019/07/27/eMNopd.png)

<strong>After: </strong>
![eMUCXq.png](https://s2.ax1x.com/2019/07/27/eMUCXq.png)
This will automatically load the bundle containing the `OtherComponent` when this component gets rendered.

`React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.

> `React.lazy` and Suspense are not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we recommend `Loadable Components`.

#### React.Suspense
`React.Suspense` let you specify the loading indicator in case some components in the tree below it are not yet ready to render. Today, lazy loading components is the <strong>only</strong> use case supported by `<React.Suspense>`:
![eMaErt.png](https://s2.ax1x.com/2019/07/27/eMaErt.png)
Note that `lazy` components can be deep inside the `Suspense` tree — it doesn’t have to wrap every one of them. The best practice is to place `<Suspense>` where you want to see a loading indicator, but to use `lazy()` wherever you want to do code splitting.

> `React.lazy()` and `<React.Suspense>` are not yet supported by `ReactDOMServer`. This is a known limitation that will be resolved in the future.

## Hooks
<i>Hooks</i> are a new addition in React 16.8. They let you use state and other React features without writing a class.
- Basic Hooks
    - [useState](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usestate)
    - [useEffect](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#useeffect)
    - [useContext](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usecontext)
- Additional Hooks
    - [useReducer](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usereducer)
    - [useCallback](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usecallback)
    - [useMemo](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usememo)
    - [useRef](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#useref)
    - [useImperativeHandle](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#useimperativehandle)
    - [useLayoutEffect](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#uselayouteffect)
    - [useDebugValue](https://jalever.github.io/2019/03/25/Hooks-API-Reference/#usedebugvalue)
