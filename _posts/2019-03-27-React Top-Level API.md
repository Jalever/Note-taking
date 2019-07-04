---
layout: post
title: React Top-Level API
subtitle: React API Reference
date: 2019-03-27
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

#### React.Component

<ins>**_React.Component_**</ins> is the base class for React components when they are defined using ES6 classes:

```javascript
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

#### React.PureComponent

<ins>**_React.PureComponent_**</ins> is similar to <ins>**_React.Component_**</ins>.<br>
The difference between them is that <ins>**_React.Component_**</ins> doesn’t implement <ins>**_shouldComponentUpdate()_**</ins>, but <ins>**_React.PureComponent_**</ins> implements it with a shallow prop and state comparison.<br>
If your React component’s <ins>**_render()_**</ins> function renders the same result given the same props and state, you can use <ins>**_React.PureComponent_**</ins> for a performance boost in some cases.<br>

> `React.PureComponent`’s `shouldComponentUpdate()` only shallowly compares the objects. If these contain complex data structures, it may produce false-negatives for deeper differences.<br>

#### React.memo

`React.memo` is a higher order component. It’s similar to `React.PureComponent`but for function components instead of classes.

If your function component renders the same result given the same props, you can wrap it in a call to `React.memo` for a performance boost in some cases by memoizing the result.

By default it will only shallowly compare complex objects in the props object.
React components can also be defined as functions which can be wrapped

![ZUS3ZD.png](https://s2.ax1x.com/2019/07/04/ZUS3ZD.png)

If you want control over the comparison, you can also provide a custom comparison function as the second argument.

![ZUpukQ.png](https://s2.ax1x.com/2019/07/04/ZUpukQ.png)

## Creating React Elements

#### React.createElement()

Create and return a new `React element` of the given type. The type argument can be either a tag name string (such as <strong>div</strong> or <strong>span</strong>), a `React component` type (a <strong>class</strong> or a <strong>function</strong>), or a `React fragment` type.

Code written with JSX will be converted to use `React.createElement()`. You will not typically invoke `React.createElement()` directly if you are using JSX.

![ZUpt7F.png](https://s2.ax1x.com/2019/07/04/ZUpt7F.png)

#### React.createFactory()

![ZU9puV.png](https://s2.ax1x.com/2019/07/04/ZU9puV.png)

Return a function that produces React elements of a given type. Like `React.createElement()`, the type argument can be either a `tag name string` (such as <strong>div</strong> or <strong>span</strong>), a `React component type` (a <strong>class</strong> or a <strong>function</strong>), or a `React fragment type`.

This helper is considered legacy, and we encourage you to either use `JSX` or use `React.createElement()` directly instead.

You will not typically invoke `React.createFactory()` directly if you are using JSX.

## Transforming Elements

#### cloneElement()

![ZU9zPH.png](https://s2.ax1x.com/2019/07/04/ZU9zPH.png)

Clone and return a new React element using `element` as the starting point. The resulting element will have the original element’s props with the new props merged in shallowly. New children will replace existing children. `key` and `ref` from the original element will be preserved.

`React.cloneElement()` is almost equivalent to:

![ZUCEdS.png](https://s2.ax1x.com/2019/07/04/ZUCEdS.png)

However, it also preserves `ref`s. This means that if you get a child with a `ref` on it, you won’t accidentally steal it from your ancestor. You will get the same `ref` attached to your new element.

#### isValidElement()

![ZUC0L6.png](https://s2.ax1x.com/2019/07/04/ZUC0L6.png)

Verifies the object is a React element. Returns `true` or `false`.

#### React.Children

`React.Children` provides utilities for dealing with the `this.props.children` opaque data structure.

###### React.Children.map
![ZUC5ef.png](https://s2.ax1x.com/2019/07/04/ZUC5ef.png)

Invokes a function on every immediate child contained within `children` with `this` set to `thisArg`. If `children` is an array it will be traversed and the function will be called for each child in the array. If children is `null` or `undefined`, this method will return `null` or `undefined` rather than an array.

> If `children` is a `Fragment` it will be treated as a single child and not traversed.

###### React.Children.forEach
![ZUCbWj.png](https://s2.ax1x.com/2019/07/04/ZUCbWj.png)

Like `React.Children.map()` but does not return an array.

###### React.Children.count
![ZUCXyq.png](https://s2.ax1x.com/2019/07/04/ZUCXyq.png)

Returns the total number of components in `children`, equal to the number of times that a callback passed to `map` or `forEach` would be invoked.

###### React.Children.only
![ZUCzwT.png](https://s2.ax1x.com/2019/07/04/ZUCzwT.png)

Verifies that `children` has only one child (a React element) and returns it. Otherwise this method throws an error.

> `React.Children.only()` does not accept the return value of `React.Children.map()` because it is an array rather than a `React` element.

###### React.Children.toArray
![ZUPCY4.png](https://s2.ax1x.com/2019/07/04/ZUPCY4.png)

Returns the `children` opaque data structure as a flat array with keys assigned to each child. Useful if you want to manipulate collections of children in your render methods, especially if you want to reorder or slice `this.props.children` before passing it down.

> `React.Children.toArray()` changes keys to preserve the semantics of nested arrays when flattening lists of children. That is, `toArray` prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.

## Fragments

#### React.Fragment

The `React.Fragment` component lets you return multiple elements in a `render()` method without creating an additional DOM element

![ZUi2rt.png](https://s2.ax1x.com/2019/07/04/ZUi2rt.png)

You can also use it with the shorthand `<></>` syntax.

## Refs

#### React.CreateRef

`React.createRef` creates a `ref` that can be attached to `React` elements via the `ref` attribute.

![ZUFFqx.png](https://s2.ax1x.com/2019/07/04/ZUFFqx.png)

#### React.forwardRef
`React.forwardRef` creates a React component that forwards the `ref` attribute it receives to another component below in the tree.

`React.forwardRef` accepts a rendering function as an argument. React will call this function with `props` and `ref` as two arguments. This function should return a React node.
![ZUFLSH.png](https://s2.ax1x.com/2019/07/04/ZUFLSH.png)

This technique is not very common but is particularly useful in two scenarios:

###### Forwarding refs to DOM components
Consider a `FancyButton` component that renders the native button DOM element:
![ZUkLNT.png](https://s2.ax1x.com/2019/07/04/ZUkLNT.png)

React components hide their implementation details, including their rendered output. Other components using `FancyButton` usually will not need to obtain a ref to the inner `button` DOM element. This is good because it prevents components from relying on each other’s DOM structure too much.

Although such encapsulation is desirable for application-level components like `FeedStory` or `Comment`, it can be inconvenient for highly reusable “leaf” components like `FancyButton` or `MyTextInput`. These components tend to be used throughout the application in a similar manner as a regular DOM `button` and `input`, and accessing their DOM nodes may be unavoidable for managing focus, selection, or animations.

Ref forwarding is an opt-in feature that lets some components take a ref they receive, and pass it further down (in other words, “forward” it) to a child.

In the example below, `FancyButton` uses `React.forwardRef` to obtain the `ref` passed to it, and then forward it to the DOM `button` that it renders:

![ZUAiE6.png](https://s2.ax1x.com/2019/07/04/ZUAiE6.png)

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

![ZUESJS.png](https://s2.ax1x.com/2019/07/04/ZUESJS.png)

The “logProps” HOC passes all `props` through to the component it wraps, so the rendered output will be the same. For example, we can use this HOC to log all props that get passed to our “fancy button” component:

![ZUEQy9.png](https://s2.ax1x.com/2019/07/04/ZUEQy9.png)

There is one caveat to the above example: refs will not get passed through. That’s because `ref` is not a prop. Like `key`, it’s handled differently by React. If you add a ref to a HOC, the ref will refer to the outermost container component, not the wrapped component.

This means that refs intended for our `FancyButton` component will actually be attached to the `LogProps` component:

![ZUEwyd.png](https://s2.ax1x.com/2019/07/04/ZUEwyd.png)

Fortunately, we can explicitly forward refs to the inner `FancyButton` component using the `React.forwardRef` API. `React.forwardRef` accepts a render function that receives `props` and `ref` parameters and returns a React node. For example:

![ZUEsTP.png](https://s2.ax1x.com/2019/07/04/ZUEsTP.png)

## Suspense
Suspense lets components “wait” for something before rendering. Today, Suspense only supports one use case: loading components dynamically with React.lazy. In the future, it will support other use cases like data fetching.

#### React.lazy
> `React.lazy` and Suspense are not yet available for server-side rendering. If you want to do code-splitting in a server rendered app, we recommend `Loadable Components`.

The `React.lazy` function lets you render a dynamic import as a regular component.

<strong>Before: </strong>
![ZUVSTx.png](https://s2.ax1x.com/2019/07/04/ZUVSTx.png)

<strong>After: </strong>
![ZUVFpD.png](https://s2.ax1x.com/2019/07/04/ZUVFpD.png)

This will automatically load the bundle containing the `OtherComponent` when this component gets rendered.

`React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.

#### React.Suspense
If the module containing the `OtherComponent` is not yet loaded by the time `MyComponent` renders, we must show some fallback content while we’re waiting for it to load - such as a loading indicator. This is done using the `Suspense` component.
![ZUV8Xj.png](https://s2.ax1x.com/2019/07/04/ZUV8Xj.png)

The `fallback` prop accepts any React elements that you want to render while waiting for the component to load. You can place the `Suspense` component anywhere above the lazy component. You can even wrap multiple lazy components with a single `Suspense` component.

![ZUVRN6.png](https://s2.ax1x.com/2019/07/04/ZUVRN6.png)

## Hooks
Hooks let you use `state` and `other React features` without writing a `class`.
```javascript
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
[Hooks API Reference](https://jalever.github.io/2019/03/27/Hooks-API-Reference/)
