---
layout:     post
title:      React Without ES6
subtitle:   React学习笔记系列
date:       2019-03-26
author:     Jalever
header-img: img/post_2019_react_bg.jpg
catalog: true
tags:
    - React
---

- [Declaring Default Props](#declaring-default-props)
- [Setting the Initial State](#setting-the-initial-state)
- [Autobinding](#autobinding)
- [Mixins](#mixins)

Normally you would define a React component as a plain JavaScript class:
```
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
If you don’t use ES6 yet, you may use the `create-react-class` module instead:
```
var createReactClass = require('create-react-class');
var Greeting = createReactClass({
  render: function() {
    return <h1>Hello, {this.props.name}</h1>;
  }
});
```
The API of ES6 classes is similar to `createReactClass()` with a few exceptions.

## Declaring Default Props
With functions and ES6 classes `defaultProps` is defined as a property on the component itself:
```
class Greeting extends React.Component {
  // ...
}

Greeting.defaultProps = {
  name: 'Mary'
};
```
With `createReactClass()`, you need to define `getDefaultProps()` as a function on the passed object:
```
var Greeting = createReactClass({
  getDefaultProps: function() {
    return {
      name: 'Mary'
    };
  },

  // ...

});
```

## Setting the Initial State
In ES6 classes, you can define the initial state by assigning `this.state` in the constructor:
```
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  // ...
}
```
With `createReactClass()`, you have to provide a separate `getInitialState` method that returns the initial state:
```
var Counter = createReactClass({
  getInitialState: function() {
    return {count: this.props.initialCount};
  },
  // ...
});
```

## Autobinding
In React components declared as ES6 classes, methods follow the same semantics as regular ES6 classes.<br>
This means that they don’t automatically bind this to the instance.<br> 
You’ll have to explicitly use `.bind(this)` in the constructor:
```
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Hello!'};
    // This line is important!
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    alert(this.state.message);
  }

  render() {
    // Because `this.handleClick` is bound, we can use it as an event handler.
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
}
```
With `createReactClass()`, this is not necessary because it binds all methods:
```
var SayHello = createReactClass({
  getInitialState: function() {
    return {message: 'Hello!'};
  },

  handleClick: function() {
    alert(this.state.message);
  },

  render: function() {
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
});
```
If the boilerplate code for event handlers is too unattractive to you, you may enable the `experimental Class Properties` syntax proposal with `Babel`:
```
class SayHello extends React.Component {
  constructor(props) {
    super(props);
    this.state = {message: 'Hello!'};
  }
  // WARNING: this syntax is experimental!
  // Using an arrow here binds the method:
  handleClick = () => {
    alert(this.state.message);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Say hello
      </button>
    );
  }
}
```
> Please note that the syntax above is experimental and the syntax may change, or the proposal might not make it into the language.

## Mixins
We also found numerous issues in codebases using mixins, and don’t recommend using them in the new code.