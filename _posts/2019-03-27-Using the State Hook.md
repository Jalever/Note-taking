---
layout: post
title: Using the State Hook
subtitle: React Hooks学习笔记系列
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

- [Equivalent Class Example](#equivalent-class-example)
- [Hooks and Function Components](#hooks-and-function-components)
- [What’s a Hook?](#whats-a-hook)
    - [So what is a `Hook`?](#so-what-is-a-hook)
    - [When would I use a `Hook`?](#when-would-i-use-a-hook)
- [Declaring a State Variable](#declaring-a-state-variable)
    - [What does calling useState do?](#what-does-calling-usestate-do)
    - [What do we pass to useState as an argument?](#what-do-we-pass-to-usestate-as-an-argument)
    - [What does useState return?](#what-does-usestate-return)
- [Reading State](#reading-state)
- [Updating State](#updating-state)
- [Recap](#recap)
    - [What Do Square Brackets Mean?](#what-do-square-brackets-mean)
    - [Using Multiple State Variables](#using-multiple-state-variables)
- [Hooks Tutorial](#hooks-tutorial)

## Equivalent Class Example

```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

## Hooks and Function Components

function components in `React` look like this:

```javascript
const Example = props => {
  // You can use Hooks here!
  return <div />;
};
```

or this:

```javascript
function Example(props) {
  // You can use Hooks here!
  return <div />;
}
```

## What’s a Hook?

Our example starts by importing the `useState` Hook from React:

```javascript
import React, { useState } from "react";

function Example() {
  // ...
}
```

#### So what is a `Hook`?

- A `Hook` is a special function that lets you “hook into” `React` features.

#### When would I use a `Hook`?

- If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a `Hook` inside the existing function component.

## Declaring a State Variable

In a class, we initialize the `count` state to `0` by setting `this.state` to `{ count: 0 }` in the constructor:

```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
```

In a function component, we have no `this`, so we can’t assign or read `this.state`. Instead, we call the `useState` Hook directly inside our component:

```javascript
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

```

#### What does calling useState do?

It declares a “state variable”.<br>
Our variable is called `count` but we could call it anything else.<br>
This is a way to “preserve” some values between the function calls — `useState` is a new way to use the exact same capabilities that `this.state` provides in a class. <br>
Normally, variables “disappear” when the function exits but state variables are preserved by React.<br>

#### What do we pass to useState as an argument?

The only argument to the `useState()` Hook is the initial state.<br>
If we wanted to store two different values in state, we would call `useState()` twice.<br>

#### What does useState return?

It returns a pair of values: `the current state` and `a function` that updates it. <br>
This is why we write `const [count, setCount] = useState()`.

## Reading State

When we want to display the current count in a class, we read `this.state.count`:

```javascript
<p>You clicked {this.state.count} times</p>
```

In a function, we can use count directly:

```javascript
<p>You clicked {count} times</p>
```

## Updating State

In a class, we need to call `this.setState()` to update the `count` state:

```javascript
<button onClick={() => this.setState({ count: this.state.count + 1 })}>
  Click me
</button>
```

In a function, we already have `setCount` and `count` as variables so we don’t need this:

```javascript
<button onClick={() => setCount(count + 1)}>Click me</button>
```

## Recap

#### What Do Square Brackets Mean?
The names on the left aren’t a part of the `React API`. 
You can name your own state variables:
```javascript
  const [fruit, setFruit] = useState('banana');
```
This JavaScript syntax is called `array destructuring`. <br>
It means that we’re making two new variables `fruit` and `setFruit`, where `fruit` is set to the first value returned by `useState`, and `setFruit` is the second. <br>
It is equivalent to this code:
```javascript
  var fruitStateVariable = useState('banana'); // Returns a pair
  var fruit = fruitStateVariable[0]; // First item in a pair
  var setFruit = fruitStateVariable[1]; // Second item in a pair
```
When we declare a state variable with `useState`, it returns a pair — an array with two items. <br>
The first item is `the current value`, and the second is `a function` that lets us update it. 

#### Using Multiple State Variables
Declaring state variables as a pair of `[something, setSomething]` is also handy because it lets us give different names to different state variables if we want to use more than one:
```javascrit
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
```
In the above component, we have `age`, `fruit`, and `todos` as local variables, and we can update them individually:
```javascript
  function handleOrangeClick() {
    // Similar to this.setState({ fruit: 'orange' })
    setFruit('orange');
  }
```

## Hooks Tutorial
1. [Introducing Hooks](https://jalever.github.io/2019/03/27/Introducing-Hooks/)
2. [Hooks at a Glance](https://jalever.github.io/2019/03/27/Hooks-at-a-Glance/)
3. Using the State Hook