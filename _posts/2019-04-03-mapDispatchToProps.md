---
layout: post
title: mapDispatchToProps
subtitle: React Redux学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Redux
---

`mapDispatchToProps` is used for dispatching actions to the store.<br>
`dispatch` is a function of the `Redux` store.
You call `store.dispatch` to dispatch an action.
This is the only way to trigger a state change.<br>
With `React Redux`, your components never access the store directly - `connect` does it for you.

- By default, a connected component receives `props.dispatch` and can dispatch actions itself.
- `connect` can accept an argument called `mapDispatchToProps`, which lets you create functions that dispatch when called, and pass those functions as props to your component.

## Approaches for Dispatching

Providing a `mapDispatchToProps` allows you to specify which actions your component might need to dispatch.

#### Default: `dispatch` as a Prop

If you don't specify the second argument to `connect()`, your component will receive dispatch by default.
It lets you provide action dispatching functions as props.

#### Providing A `mapDispatchToProps` Parameter

###### More Declarative

if you define your own `mapDispatchToProps`, the connected component will no longer receive dispatch.

###### Pass Down Action Dispatching Logic to ( Unconnected ) Child Components

you also gain the ability to pass down the action dispatching functions to child ( likely unconnected ) components.

## Two Forms of `mapDispatchToProps`

The mapDispatchToProps parameter can be of two forms.
While the `function form` allows more customization, the `object form` is easy to use.

- Function form
  Allows more customization, gains access to `dispatch` and optionally `ownProps`
- Object shorthand form
  More declarative and easier to use

## Defining `mapDispatchToProps` As A Function

Defining mapDispatchToProps as a function gives you the most flexibility in customizing the functions your component receives, and how they dispatch actions.
You gain access to dispatch and ownProps.
You may use this chance to write customized functions to be called by your connected components.

#### Arguments

1. dispatch
   The `mapDispatchToProps` function will be called with dispatch as the first argument.

2. ownProps (optional)
   If your `mapDispatchToProps` function is declared as taking two parameters, it will be called with `dispatch` as the first parameter and the `props` passed to the connected component as the second parameter, and will be re-invoked whenever the connected component receives new props.

#### Return

Your `mapDispatchToProps` function should return a plain object:

- Each field in the object will become a separate prop for your own component, and the value should normally be a function that dispatches an action when called.
- If you use action creators ( as oppose to plain object actions ) inside `dispatch`, it is a convention to simply name the field key the same name as the action creator:

#### Defining the `mapDispatchToProps` Function with `bindActionCreators`
`bindActionCreators` turns an object whose values are `action creators`, into an object with the same keys, but with every action creator wrapped into a `dispatch` call so they may be invoked directly.

`bindActionCreators` accepts two parameters:
- A `function` (an action creator) or an `object` (each field an action creator)
- dispatch


## Defining `mapDispatchToProps` As An Object

## Usage

```javascript
import React from "react";
import { connect } from "react-redux";
import { addTodo } from "../redux/actions";

class AddTodo extends React.Component {
  constructor(props) {
    super(props);
    this.state = { input: "" };
  }

  updateInput = input => {
    this.setState({ input });
  };

  handleAddTodo = () => {
    this.props.addTodo(this.state.input);
    this.setState({ input: "" });
  };

  render() {
    return (
      <div>
        <input
          onChange={e => this.updateInput(e.target.value)}
          value={this.state.input}
        />
        <button className="add-todo" onClick={this.handleAddTodo}>
          Add Todo
        </button>
      </div>
    );
  }
}

export default connect(
  null,
  { addTodo }
)(AddTodo);
```

or

```javascript
import React from "react";
import { connect } from "react-redux";
import cx from "classnames";
import { toggleTodo } from "../redux/actions";

const Todo = ({ todo, toggleTodo }) => (
  <li className="todo-item" onClick={() => toggleTodo(todo.id)}>
    {todo && todo.completed ? "👌" : "👋"}{" "}
    <span
      className={cx(
        "todo-item__text",
        todo && todo.completed && "todo-item__text--completed"
      )}
    >
      {todo.content}
    </span>
  </li>
);

// export default Todo;
export default connect(
  null,
  { toggleTodo }
)(Todo);
```
