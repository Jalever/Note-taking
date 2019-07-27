---
layout: post
title: Controlled and Uncontrolled Components
subtitle: React Terminology
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [Overview](#overview)
- [Controlled Components](#controlled-components)
    - [The Reason Called Controlled](#the-reason-called-controlled)
- [Uncontrolled Components](#uncontrolled-components)
    - [Default Values](#default-values)
    - [The file input Tag](#the-file-input-Tag)


- [Conclusion](#conclusion)

## Overview
In most cases, we recommend using `controlled components` to implement forms. In a `controlled component`, form data is handled by a <ins>React component</ins>. The alternative is `uncontrolled components`, where form data is handled by the <ins>DOM</ins> itself.

## Controlled Components
`Controlled components` keep that state inside of `React` either in the component rendering the input, a parent component somewhere in the tree, or a flux store.

A `Controlled Component` is one that takes its current value through props and notifies changes through callbacks like `onChange`.

A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component.

![eMMIr4.png](https://s2.ax1x.com/2019/07/27/eMMIr4.png)

Every time you type a new character, `handleNameChange` is called. It takes in the new value of the input and sets it in the state.

![ZtKXU1.png](https://s2.ax1x.com/2019/07/03/ZtKXU1.png)

1. It starts out as an empty string — `''`.
2. You type `a` and `handleNameChange` gets an `a` and calls `setState`. The input is then re-rendered to have the value of `a`.
3. You type `b`. `handleNameChange` gets the value of `ab` and sets that to the state. The input is re-rendered once more, now with `value="ab"`.

This flow kind of ‘pushes’ the value changes to the form component, so the `Form` component always has the current value of the input, without needing to ask for it explicitly.

This means your data (state) and UI (inputs) are always in sync. The state gives the value to the input, and the input asks the Form to change the current value.

This also means that the form component can respond to input changes immediately; for example, by:
1. in-place feedback, like validations
2. disabling the button unless all fields have valid data
3. enforcing a specific input format, like credit card numbers

#### The Reason Called Controlled
There are other form elements, of course. You have `checkboxes` and `radios` and `selects` and `textareas`.

A form element becomes “controlled” if you set its value via a prop. That’s all.

Each of the form elements, though, has a different prop for setting that value, so here’s a little table to summarize:

![Zt8HKK.png](https://s2.ax1x.com/2019/07/03/Zt8HKK.png)


## Uncontrolled Components
In most cases, we recommend using Controlled Components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

To write an uncontrolled component, instead of writing an event handler for every state update, you can <b>use a ref</b> to get form values from the DOM.

For example, this code accepts a single name in an uncontrolled component:
![eMKN1U.png](https://s2.ax1x.com/2019/07/27/eMKN1U.png)

#### Default Values
In the React rendering lifecycle, the `value` attribute on form elements will override the value in the DOM. With an uncontrolled component, you often want React to specify the initial value, but leave subsequent updates uncontrolled. To handle this case, you can specify a `defaultValue` attribute instead of `value`.
![eMKfnH.png](https://s2.ax1x.com/2019/07/27/eMKfnH.png)
Likewise, `<input type="checkbox">` and `<input type="radio">` support `defaultChecked`, and `<select>` and `<textarea>` supports `defaultValue`.

#### The file input Tag
In HTML, an `<input type="file">` lets the user choose one or more files from their device storage to be uploaded to a server or manipulated by JavaScript via the File API.
![eMMSNq.png](https://s2.ax1x.com/2019/07/27/eMMSNq.png)
In React, an `<input type="file" />` is always an uncontrolled component because its value can only be set by a user, and not programmatically.

You should use the File API to interact with the files. The following example shows how to create a ref to the DOM node to access file(s) in a submit handler:
![eMM8DH.png](https://s2.ax1x.com/2019/07/27/eMM8DH.png)
![eMM6Vs.png](https://s2.ax1x.com/2019/07/27/eMM6Vs.png)



## Conclusion
Both the controlled and uncontrolled form fields have their merit. Evaluate your specific situation and pick the approach — what works for you is good enough.

If your form is incredibly simple in terms of UI feedback, uncontrolled with refs is entirely fine. You don’t have to listen to what the various articles are saying is “bad”.

![ZtG8IJ.png](https://s2.ax1x.com/2019/07/03/ZtG8IJ.png)
