---
layout: post
title: Controlled / Uncontrolled Components
subtitle: React Terminology
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

- [Overview](#overview)
- [Uncontrolled Components](#uncontrolled-components)
- [Controlled Components](#controlled-components)
    - [The Reason Called Controlled](#the-reason-called-controlled)
- [Conclusion](#conclusion)

## Overview
In most cases, we recommend using `controlled components` to implement forms. In a `controlled component`, form data is handled by a <ins>React component</ins>. The alternative is `uncontrolled components`, where form data is handled by the <ins>DOM</ins> itself.


## Uncontrolled Components
Certain `DOM` elements such as `<input>`, `<textarea>`, and `<select>` that by default maintain state (***user input***) within the `DOM` layer.

A `Uncontrolled Component` is one that stores its own state internally, and you query the `DOM` using a `ref` to find its current value when you need it.

This is a bit more like traditional HTML.

To write an uncontrolled component, instead of writing an event handler for every state update, you can use a ref to get form values from the DOM.

For example, this code accepts a single name in an uncontrolled component:

![ZtnzIx.png](https://s2.ax1x.com/2019/07/03/ZtnzIx.png)

## Controlled Components
`Controlled components` keep that state inside of `React` either in the component rendering the input, a parent component somewhere in the tree, or a flux store.

A `Controlled Component` is one that takes its current value through props and notifies changes through callbacks like `onChange`.

A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component.

![ZtKVcF.png](https://s2.ax1x.com/2019/07/03/ZtKVcF.png)

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

## Conclusion
Both the controlled and uncontrolled form fields have their merit. Evaluate your specific situation and pick the approach — what works for you is good enough.

If your form is incredibly simple in terms of UI feedback, uncontrolled with refs is entirely fine. You don’t have to listen to what the various articles are saying is “bad”.

![ZtG8IJ.png](https://s2.ax1x.com/2019/07/03/ZtG8IJ.png)
