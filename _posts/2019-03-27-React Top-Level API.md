---
layout: post
title: Render Top-Level API
subtitle: React学习笔记系列
date: 2019-03-26
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

`React.memo` is a higher order component. It’s similar to `React.PureComponent`but for function components instead of classes.<br>
If your function component renders the same result given the same props, you can wrap it in a call to `React.memo` for a performance boost in some cases by memoizing the result.<br>
By default it will only shallowly compare complex objects in the props object.
React components can also be defined as functions which can be wrapped

```javascript
const MyComponent = React.memo(function MyComponent(props) {
  /* render using props */
});
```

If you want control over the comparison, you can also provide a custom comparison function as the second argument.

```javascript
function MyComponent(props) {
  /* render using props */
}
function areEqual(prevProps, nextProps) {
  /*
  return true if passing nextProps to render would return
  the same result as passing prevProps to render,
  otherwise return false
  */
}
export default React.memo(MyComponent, areEqual);
```

## Creating React Elements

#### React.createElement()

Create and return a new `React` element of the given type.<br>
The type argument can be either a <ins>**_tag name_**</ins> string (such as 'div' or 'span'), a <ins>**_React component_**</ins> type (a class or a function), or a <ins>**_React fragment_**</ins> type.<br>
Code written with JSX will be converted to use `React.createElement()`.<br>

```javascript
React.createElement(type, [props], [...children]);
```

#### React.createFactory()

```javascript
React.createFactory(type);
```

Return a function that produces `React` elements of a given type.<br/>
Like `React.createElement()`, the type argument can be either a **_tag name string_** (such as 'div' or 'span'), a **_React component type_** (a class or a function), or a **_React fragment type_**.<br/>
You will not typically invoke `React.createFactory()` directly if you are using JSX.

## Transforming Elements

#### cloneElement()

```javascript
React.cloneElement(
  element,
  [props],
  [...children]
)
```

Clone and return a new `React` element using `element` as the starting point. <br/>
The resulting element will have the original element’s props with the new props merged in shallowly. <br/>
New children will replace existing children. `key` and `ref` from the original element will be preserved.

#### isValidElement()

```javascript
React.isValidElement(object)
```

Verifies the object is a `React` element.<br/>
Returns `true` or `false`

#### React.Children

`React.Children` provides utilities for dealing with the `this.props.children` opaque data structure.

##### React.Children.map

```javascript
React.Children.map(children, function[(thisArg)])
```

Invokes a function on every immediate child contained within `children` with `this`set to `thisArg`.<br>
If children is an `array` it will be traversed and the function will be called for each child in the array.<br>
If children is `null` or `undefined`, this method will return `null` or `undefined` rather than an array.<br>
If children is a `Fragment` it will be treated as a single child and not traversed.

##### React.Children.forEach

```javascript
React.Children.forEach(children, function[(thisArg)])
```

Like `React.Children.map()` but does not return an array.

##### React.Children.count

```javascript
React.Children.count(children)
```

Returns the **_total number of components_** in children, equal to the number of times that a callback passed to `map` or `forEach` would be invoked.

##### React.Children.only

```javascript
React.Children.only(children)
```

Verifies that `children` has only one child (a React element) and returns it.<br> 
Otherwise this method throws an error.<br>

> `React.Children.only()` does not accept the return value of `React.Children.map()` because it is an array rather than a `React` element.

##### React.Children.toArray

```javascript
React.Children.toArray(children)
```

Returns the children opaque data structure as a flat array with keys assigned to each child.

> `React.Children.toArray()` changes keys to preserve the semantics of nested arrays when flattening lists of children. That is, `toArray` prefixes each key in the returned array so that each element’s key is scoped to the input array containing it.

## Fragments

#### React.Fragment

The `React.Fragment` component lets you return multiple elements in a `render()` method without creating an additional DOM element

```javascript
render() {
  return (
    <React.Fragment>
      Some text.
      <h2>A heading</h2>
    </React.Fragment>
  );
}
```

## Refs

#### React.CreateRef

`React.createRef` creates a `ref` that can be attached to `React` elements via the `ref` attribute.

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();
  }

  render() {
    return <input type="text" ref={this.inputRef} />;
  }

  componentDidMount() {
    this.inputRef.current.focus();
  }
}
```

#### React.forwardRef

`React.forwardRef` creates a `React` component that **_forwards the ref attribute it receives to another component below in the tree_**. This technique is not very common but is particularly useful in two scenarios:<br>

- Forwarding refs to DOM components
- Forwarding refs in higher-order-components

`React.forwardRef` accepts a rendering function as an argument.
`React` will call this function with `props` and `ref` as two arguments.
This function should return a `React` node.<br>

```javascript
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

In the above example, `React` passes a `ref` given to `<FancyButton ref={ref}>` element as a second argument to the rendering function inside the `React.forwardRef` call. This rendering function passes the `ref` to the `<button ref={ref}>` element.

As a result, after `React` attaches the `ref`, `ref.current` will point directly to the `<button>` DOM element instance.

## Suspense

#### React.lazy

`React.lazy()` lets you define a component that is loaded dynamically.
This helps **_reduce the bundle size to delay loading components that aren’t used during the initial render_**.

```javascript
// This component is loaded dynamically
const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

Note that rendering lazy components requires that there’s a `<React.Suspense>` component higher in the rendering tree. This is how you specify a loading indicator.

> NOTE: Using `React.lazy` with dynamic import requires `Promises` to be available in the JS environment. This requires a polyfill on IE11 and below.

#### React.Suspense

`React.Suspense` let you specify the loading indicator in case some components in the tree below it are not yet ready to render. <br>
Today, lazy loading components is the only use case supported by `<React.Suspense>`:

```javascript
// This component is loaded dynamically
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // Displays <Spinner> until OtherComponent loads
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```

Note that lazy components can be deep inside the `Suspense` tree — it doesn’t have to wrap every one of them.<br>
The best practice is to place `<Suspense>` where you want to see a loading indicator, but to use `lazy()` wherever you want to do code splitting.

> `React.lazy()` and `<React.Suspense>` are not yet supported by ReactDOMServer. This is a known limitation that will be resolved in the future.

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