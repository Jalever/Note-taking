---
layout: post
title: Hooks at a Glance
subtitle: React Hooks学习笔记系列 2
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

- [State Hook](#state-hook)
    - [Declaring multiple state variables](#declaring-multiple-state-variables)
    - [But what is a Hook?](#but-what-is-a-hook)
- [Effect Hook](#effect-hook)
- [Rules of Hooks](#rules-of-hooks)
- [Building Your Own Hooks](#building-your-own-hooks)
- [Hooks Tutorial](#hooks-tutorial)

## State Hook

```javascript
import React, { useState } from "react";

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

`useState` is a `Hook`.<br>
We call it inside a function component to add some local state to it.<br>
`useState` returns a pair: the `current state value` and a `function` that lets you update it.<br>
You can call this function from an event handler or somewhere else.<br>
The only argument to `useState` is the initial state.<br>
In the example above, it is `0` because our counter starts from zero.<br>

> Note that unlike `this.state`, the state here doesn’t have to be an object — although it can be if you want.
> The initial state argument is only used during the first render.

#### Declaring multiple state variables
You can use the `State Hook` more than once in a single component:
```javascript
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```
The `array destructuring` syntax lets us give different names to the state variables we declared by calling `useState`.

#### But what is a Hook? 
`Hooks` are ***functions*** that let you “hook into” `React state` and `lifecycle features` from function components.<br>
`Hooks` don’t work inside classes — they let you use `React` without classes.

## Effect Hook
The Effect Hook, `useEffect`, adds the ability to perform `side effects` from a function component. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in `React` classes, but unified into a single `API`. <br>
For example, this component sets the document title after `React` updates the `DOM`:
```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

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
When you call `useEffect`, you’re telling `React` to run your “effect” function after flushing changes to the DOM. <br>
Effects are declared inside the component so they have access to its `props` and `state`. <br>
By default, `React` runs the effects after every render — including the first render. 

Effects may also optionally specify how to “clean up” after them by returning a function. <br>
For example, this component uses an effect to subscribe to a friend’s online status, and cleans up by unsubscribing from it:
```javascript
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
In this example, `React` would ***unsubscribe*** from our `ChatAPI` when ***the component unmounts***, as well as before ***re-running the effect*** due to ***a subsequent render***.

like with `useState`, you can use more than a single effect in a component:
```javascript
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

## Rules of Hooks
`Hooks` are `JavaScript` functions, but they impose two additional rules:
- Only call `Hooks` at the top level.
  - Don’t call `Hooks` inside ***loops***, ***conditions***, or ***nested functions***.
- Only call `Hooks` from `React` function components.
  - Don’t call `Hooks` from regular `JavaScript` functions.

## Building Your Own Hooks
Sometimes, we want to reuse some stateful logic between components.<br>
Traditionally, there were two popular solutions to this problem: `higher-order components` and `render props`. <br>
Custom `Hooks` let you do this, but without adding more components to your tree.
For example,we’ll extract this logic into a custom Hook called `useFriendStatus`:
```javascript
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```
Now we can use it from both components:
```javascript
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
and
```javascript
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```
The state of these components is completely independent.<br>
`Hooks` are a way to reuse stateful logic, not state itself.<br>
In fact, each call to a `Hook` has a completely isolated state — so you can even use the same custom `Hook` twice in one component.<br>
If a function’s name starts with ”use” and it calls other Hooks, we say it is a `custom Hook`. <br>
The `useSomething` naming convention is how our linter plugin is able to find bugs in the code using Hooks.

## Hooks Tutorial
1. [Introducing Hooks](https://jalever.github.io/2019/03/27/Introducing-Hooks/)
2. Hooks at a Glance
