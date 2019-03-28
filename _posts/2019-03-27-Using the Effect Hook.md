---
layout: post
title: Using the Effect Hook
subtitle: React Hooks学习笔记系列 4
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

- [Effects Without Cleanup](#effects-without-cleanup)
    - [Example Using Classes](#example-using-classes)
    - [Example Using Hooks](#example-using-hooks)
        - [What does useEffect do?](#what-does-useeffect-do)
        - [Why is useEffect called inside a component?](#why-is-useeffect-called-inside-a-component)
        - [Does useEffect run after every render?](#does-useeffect-run-after-every-render)
    - [Detailed Explanation](#detailed-explanation)
- [Effects with Cleanup](#effects-with-cleanup)
    - [Example Using Classes](#example-using-classes-1)
    - [Example Using Hooks](#example-using-hooks-1)
        - [Why did we return a function from our effect?](#why-did-we-return-a-function-from-our-effect)
        - [When exactly does React clean up an effect?](#when-exactly-does-react-clean-up-an-effect)
- [Recap](#recap)
- [Tips for Using Effects](#tips-for-using-effects)
    - [Use Multiple Effects to Separate Concerns](#use-multiple-effects-to-separate-concerns)
    - [Why Effects Run on Each Update](#why-effects-run-on-each-update)
    - [Optimizing Performance by Skipping Effects](#optimizing-performance-by-skipping-effects)
- [Hooks Tutorial](#hooks-tutorial)

## Effects Without Cleanup
`Network requests`, `manual DOM mutations`, and `logging` are common examples of effects that don’t require a cleanup. 

#### Example Using Classes
In `React` class components, the render method itself shouldn’t cause side effects.<br>
It would be too early — we typically want to perform our effects after `React` has updated the `DOM`.<br>
This is why in `React` classes, we put side effects into `componentDidMount` and `componentDidUpdate`.
Coming back to our example, here is a `React` counter class component that updates the document title right after `React` makes changes to the `DOM`:
```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
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
Note how we have to duplicate the code between these two lifecycle methods in class.

#### Example Using Hooks
```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
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

###### What does useEffect do?
By using this `Hook`, you tell `React` that your component needs to do something after render.<br>
`React` will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the `DOM` updates.

###### Why is useEffect called inside a component?
Placing useEffect inside the component lets us access the count state variable (or any props) right from the effect.<br>
We don’t need a special `API` to read it — it’s already in the function scope.

###### Does useEffect run after every render?
By default, it runs both after the ***first render*** and ***after every update***.<br>
`React` guarantees the `DOM` has been updated by the time it runs the effects.

#### Detailed Explanation
Every time we re-render, we schedule a different effect, replacing the previous one.<br>
In a way, this makes the effects behave more like a part of the render result — each effect “belongs” to a particular render. 

## Effects with Cleanup
For example, we might want to set up a ***subscription*** to some external data source. In that case, it is important to clean up so that we don’t introduce a memory leak!

#### Example Using Classes
In a `React` class, you would typically set up a subscription in `componentDidMount`, and clean it up in `componentWillUnmount`.
```javascript
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

#### Example Using Hooks
If your effect returns a function, `React` will run it when it is time to clean up:
```javascript
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

###### Why did we return a function from our effect?
This is the optional cleanup mechanism for effects.
Every effect may return a function that cleans up after it. 

###### When exactly does React clean up an effect?
`React` performs the cleanup when the component unmounts.<br>
Effects run for every render and not just once. This is why `React` also cleans up effects from the previous render before running the effects next time. 

## Recap
Some effects might require cleanup so they return a function:
```javascript
 useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```
Other effects might not have a cleanup phase, and don’t return anything.
```javascript
useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

## Tips for Using Effects

#### Use Multiple Effects to Separate Concerns
Here is a component that combines the counter and the friend status indicator logic from the previous examples:
```javascript
class FriendStatusWithCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0, isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }
  // ...
```
How can `Hooks` solve this problem?<br>
You can also use several effects.<br>
This lets us separate unrelated logic into different effects:<br>
```javascript
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
  // ...
}
```
`Hooks` lets us split the code based on what it is doing rather than a lifecycle method name.<br>
`React` will apply every effect used by the component, in the order they were specified.

#### Why Effects Run on Each Update
Our class reads `friend.id` from `this.props`, subscribes to the friend status after the component mounts, and unsubscribes during unmounting:
```javascript
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```
But what happens if the friend prop changes while the component is on the screen? Our component would continue displaying the online status of a different friend.<br>
In a class component, we would need to add `componentDidUpdate` to handle this case:
```javascript
 componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // Unsubscribe from the previous friend.id
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // Subscribe to the next friend.id
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```
Now consider the version of this component that uses `Hooks`:
```javascript
function FriendStatus(props) {
  // ...
  useEffect(() => {
    // ...
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```
There is no special code for handling updates because `useEffect` handles them by `default`.<br>
It cleans up the previous effects before applying the next effects. <br>
To illustrate this, here is a sequence of subscribe and unsubscribe calls that this component could produce over time:
```javascript
// Mount with { friend: { id: 100 } } props
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // Run first effect

// Update with { friend: { id: 200 } } props
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Run next effect

// Update with { friend: { id: 300 } } props
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Run next effect

// Unmount
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Clean up last effect
```

#### Optimizing Performance by Skipping Effects
In some cases, cleaning up or applying the effect after every render might create a performance problem.<br>
In class components, we can solve this by writing an extra comparison with `prevProps` or `prevState` inside `componentDidUpdate`:
```javascript
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```
You can tell `React` to skip applying an effect if certain values haven’t changed between re-renders.<br>
To do so, pass an array as an optional second argument to `useEffect`:
```javascript
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```
This also works for effects that have a cleanup phase:
```javascript
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Only re-subscribe if props.friend.id changes
```
> If you use this optimization, make sure the array includes all values from the component scope (such as `props` and `state`) that change over time and that are used by the effect. Otherwise, your code will reference stale values from previous renders.
> If you want to run an effect and clean it up only once (on `mount` and `unmount`), you can pass an empty array (`[]`) as a second argument. This tells `React` that your effect doesn’t depend on any values from `props` or `state`, so it never needs to re-run.
> If you pass an empty array (`[]`), the `props` and `state` inside the effect will always have their initial values. 

## Hooks Tutorial
1. [Introducing Hooks](https://jalever.github.io/2019/03/27/Introducing-Hooks/)
2. [Hooks at a Glance](https://jalever.github.io/2019/03/27/Hooks-at-a-Glance/)
3. [Using the State Hook](https://jalever.github.io/2019/03/27/Using-the-State-Hook/)
4.  Using the Effect Hook
5. [Rules of Hooks](https://jalever.github.io/2019/03/27/Rules-of-Hooks/)
6. [Building Your Own Hooks](https://jalever.github.io/2019/03/27/Building-Your-Own-Hooks/)
7. [Hooks API Reference](https://jalever.github.io/2019/03/27/Hooks-API-Reference/)