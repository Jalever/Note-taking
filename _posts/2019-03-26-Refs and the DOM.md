---
layout: post
title: Refs and the DOM
subtitle: React Advanced Guides
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

&ensp;&ensp;**_Refs_** provide a way to `access DOM nodes` or `React elements` created in the render method.

&ensp;&ensp;In the typical React dataflow, props are the only way that parent components interact with their children. To modify a child, you re-render it with new props.

&ensp;&ensp;There are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child to be modified could be an instance of a React component, or it could be a DOM element.

- [When to Use Refs](#when-to-use-refs)
- [Creating Refs](#creating-refs)
- [Accessing Refs](#accessing-refs)
    - [Adding a Ref to a DOM Element](#adding-a-ref-to-a-dom-element)
    - [Adding a Ref to a Class Component](#adding-a-ref-to-a-class-component)
    - [Refs and Function Components](#refs-and-function-components)
- [Exposing DOM Refs to Parent Components](#exposing-dom-refs-to-parent-components)
    - [Forwarding refs to DOM components](#forwarding-refs-to-dom-components)
- [Callback Refs](#callback-refs)
- [Legacy API: String Refs](#legacy-api-string-refs)
- [Caveats with callback refs](#caveats-with-callback-refs)

## When to Use Refs
There are a few good use cases for refs:
- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.

Avoid using refs for anything that can be done declaratively.

For example, instead of exposing `open()` and `close()` methods on a `Dialog` component, pass an `isOpen` prop to it.

> The examples below have been updated to use the `React.createRef()` API introduced in React 16.3. If you are using an earlier release of React, we recommend using callback refs instead.

## Creating Refs
Refs are created using `React.createRef()` and attached to React elements via the `ref` attribute. Refs are commonly assigned to an instance property when a component is constructed so they can be referenced throughout the component.
![elVel4.png](https://s2.ax1x.com/2019/07/28/elVel4.png)

## Accessing Refs
When a ref is passed to an element in `render`, a reference to the node becomes accessible at the `current` attribute of the ref.
![elVM01.png](https://s2.ax1x.com/2019/07/28/elVM01.png)
The value of the ref differs depending on the type of the node:
- When the `ref` attribute is used on an HTML element, the `ref` created in the constructor with `React.createRef()` receives the underlying DOM element as its `current` property.
- When the `ref` attribute is used on a custom class component, the `ref` object receives the mounted instance of the component as its `current`.
- <strong>You may not use the ref attribute on function components</strong> because they don’t have instances.

The examples below demonstrate the differences.

#### Adding a Ref to a DOM Element
This code uses a `ref` to store a reference to a DOM node:
![ele2oq.png](https://s2.ax1x.com/2019/07/28/ele2oq.png)
![eleoy4.png](https://s2.ax1x.com/2019/07/28/eleoy4.png)
React will assign the `current` property with the DOM element when the component mounts, and assign it back to `null` when it unmounts. `ref` updates happen before `componentDidMount` or `componentDidUpdate` lifecycle methods.

#### Adding a Ref to a Class Component
If we wanted to wrap the `CustomTextInput` above to simulate it being clicked immediately after mounting, we could use a ref to get access to the custom input and call its `focusTextInput` method manually:
![eleOFx.png](https://s2.ax1x.com/2019/07/28/eleOFx.png)
Note that this only works if `CustomTextInput` is declared as a class:
![elejfK.png](https://s2.ax1x.com/2019/07/28/elejfK.png)

#### Refs and Function Components
You may not use the ref attribute on function components because they don’t have instances:
![elmrh6.png](https://s2.ax1x.com/2019/07/28/elmrh6.png)
You should convert the component to a class if you need a ref to it, just like you do when you need lifecycle methods or state.

You can, however, <strong>use the ref attribute inside a function component</strong> as long as you refer to a DOM element or a class component:
![elmvEn.png](https://s2.ax1x.com/2019/07/28/elmvEn.png)

## Exposing DOM Refs to Parent Components
In rare cases, you might want to have access to a child’s DOM node from a parent component. This is generally not recommended because it breaks component encapsulation, but it can occasionally be useful for triggering focus or measuring the size or position of a child DOM node.

While you could add a ref to the child component, this is not an ideal solution, as you would only get a component instance rather than a DOM node. Additionally, this wouldn’t work with function components.

#### Forwarding refs to DOM components
If you use React 16.3 or higher, we recommend to use ref forwarding for these cases. <strong>Ref forwarding lets components opt into exposing any child component’s ref as their own</strong>.

Consider a `FancyButton` component that renders the native `button` DOM element:
![elu1zT.png](https://s2.ax1x.com/2019/07/28/elu1zT.png)
React components hide their implementation details, including their rendered output. Other components using `FancyButton` usually will not need to obtain a ref to the inner `button` DOM element. This is good because it prevents components from relying on each other’s DOM structure too much.

Although such encapsulation is desirable for application-level components like `FeedStory` or `Comment`, it can be inconvenient for highly reusable “leaf” components like `FancyButton` or `MyTextInput`. These components tend to be used throughout the application in a similar manner as a regular DOM `button` and `input`, and accessing their DOM nodes may be unavoidable for managing focus, selection, or animations.

<strong>Ref forwarding is an opt-in feature that lets some components take a ref they receive, and pass it further down (in other words, “forward” it) to a child</strong>.

In the example below, `FancyButton` uses `React.forwardRef` to obtain the `ref` passed to it, and then forward it to the DOM `button` that it renders:
 ![eluGyF.png](https://s2.ax1x.com/2019/07/28/eluGyF.png)
This way, components using `FancyButton` can get a ref to the underlying `button` DOM node and access it if necessary—just like if they used a DOM `button` directly.

Here is a step-by-step explanation of what happens in the above example:

1. We create a React ref by calling `React.createRef` and assign it to a `ref` variable.
2. We pass our `ref` down to `<FancyButton ref={ref}>` by specifying it as a JSX attribute.
3. React passes the `ref` to the `(props, ref) => ...` function inside `forwardRef` as a second argument.
4. We forward this `ref` argument down to `<button ref={ref}>` by specifying it as a JSX attribute.
5. When the ref is attached, `ref.current` will point to the `<button>` DOM node.
> The second `ref` argument only exists when you define a component with `React.forwardRef` call. Regular function or class components don’t receive the `ref` argument, and ref is not available in props either.<br/><br/>
> Ref forwarding is not limited to DOM components. You can forward refs to class component instances, too.

## Callback Refs
React also supports another way to set refs called “callback refs”, which gives more fine-grain control over when refs are set and unset.

Instead of passing a `ref` attribute created by `createRef()`, you pass a function. The function receives the React component instance or HTML DOM element as its argument, which can be stored and accessed elsewhere.

The example below implements a common pattern: using the `ref` callback to store a reference to a DOM node in an instance property.
![elKdBQ.png](https://s2.ax1x.com/2019/07/28/elKdBQ.png)
![elKw7j.png](https://s2.ax1x.com/2019/07/28/elKw7j.png)
![elKBAs.png](https://s2.ax1x.com/2019/07/28/elKBAs.png)
React will call the `ref` callback with the DOM element when the component mounts, and call it with `null` when it unmounts. Refs are guaranteed to be up-to-date before `componentDidMount` or `componentDidUpdate` fires.

You can pass callback refs between components like you can with object refs that were created with `React.createRef()`.
![elKI41.png](https://s2.ax1x.com/2019/07/28/elKI41.png)
In the example above, `Parent` passes its ref callback as an `inputRef` prop to the `CustomTextInput`, and the `CustomTextInput` passes the same function as a special `ref` attribute to the `<input>`. As a result, `this.inputElement` in `Parent` will be set to the DOM node corresponding to the `<input>` element in the `CustomTextInput`.

## Legacy API: String Refs
If you worked with React before, you might be familiar with an older API where the `ref` attribute is a string, like "`textInput`", and the DOM node is accessed as `this.refs.textInput`. We advise against it because string refs have some issues, are considered legacy, and <strong>are likely to be removed in one of the future releases</strong>.

## Caveats with callback refs
If the `ref` callback is defined as an inline function, it will get called twice during updates, first with `null` and then again with the DOM element. This is because a new instance of the function is created with each render, so React needs to clear the old ref and set up the new one. You can avoid this by defining the `ref` callback as a bound method on the class, but note that it shouldn’t matter in most cases.
