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

- [Approaches for Dispatching](#approaches-for-dispatching)
    - [Default: `dispatch` as a Prop](#default-dispatch-as-a-prop)
    - [Providing A `mapDispatchToProps` Parameter](#providing-a-mapdispatchtoprops-parameter)
        - [More Declarative](#more-declarative)
        - [Pass Down Action Dispatching Logic to ( Unconnected ) Child Components](#pass-down-action-dispatching-logic-to--unconnected--child-components)
- [Two Forms of `mapDispatchToProps`](#two-forms-of-mapdispatchtoprops)
- [Defining `mapDispatchToProps` As A Function](#defining-mapdispatchtoprops-as-a-function)
    - [Arguments](#arguments)
    - [Return](#return)
    - [Defining the `mapDispatchToProps` Function with `bindActionCreators`](#defining-the-mapdispatchtoprops-function-with-bindactioncreators)
    - [Manually Injecting `dispatch`](#manually-injecting-dispatch)
- [Defining `mapDispatchToProps` As An Object](#defining-mapdispatchtoprops-as-an-object)
- [Common Problems](#common-problems)
    - [Why is my component not receiving `dispatch`](#why-is-my-component-not-receiving-dispatch)
    - [Can I `mapDispatchToProps` without `mapStateToProps` in `Redux`](#can-i-mapdispatchtoprops-without-mapstatetoprops-in-redux)
- [Usage](#usage)

`mapDispatchToProps` is used for **_dispatching actions to the store_**.<br>
`dispatch` is a function of the `Redux` store.<br>
You call `store.dispatch` to dispatch an action.<br>
This is the only way to trigger a state change.<br>
With `React Redux`, your components never access the store directly - `connect` does it for you.

- By default, a connected component receives `props.dispatch` and can dispatch actions itself.
- `connect` can accept an argument called `mapDispatchToProps`, which lets you create functions that dispatch when called, and pass those functions as `props` to your component.

## Approaches for Dispatching

Providing a `mapDispatchToProps` allows you to specify which actions your component might need to dispatch.

#### Default: `dispatch` as a Prop

If you don't specify the second argument to `connect()`, your component will receive `dispatch` by default.

```javascript
connect()(MyComponent);
// which is equivalent with
connect(
  null,
  null
)(MyComponent);

// or
connect(mapStateToProps /** no second argument */)(MyComponent);
```

Once you have connected your component in this way, your component receives `props.dispatch`.<br>
You may use it to dispatch actions to the store.

```javascript
function Counter({ count, dispatch }) {
  return (
    <div>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      <span>{count}</span>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "RESET" })}>reset</button>
    </div>
  );
}
```

#### Providing A `mapDispatchToProps` Parameter

Providing a `mapDispatchToProps` allows you to specify which actions your component might need to dispatch.<br>
It lets you provide action dispatching functions as props.<br>
Therefore, instead of calling `props.dispatch(() => increment())`, you may call `props.increment()` directly.

###### More Declarative

if you define your own `mapDispatchToProps`, the connected component will no longer receive dispatch.

```javascript
// button needs to be aware of "dispatch"
<button onClick={() => dispatch({ type: "SOMETHING" })} />

// button unaware of "dispatch",
<button onClick={doSomething} />
```

###### Pass Down Action Dispatching Logic to ( Unconnected ) Child Components

you can pass down the action dispatching functions to child ( likely `unconnected` ) components. <br>
This allows more components to dispatch actions, while keeping them "unaware" of `Redux`.

```javascript
// pass down toggleTodo to child component
// making Todo able to dispatch the toggleTodo action
const TodoList = ({ todos, toggleTodo }) => (
  <div>
    {todos.map(todo => (
      <Todo todo={todo} onClick={toggleTodo} />
    ))}
  </div>
);
```

## Two Forms of `mapDispatchToProps`

The mapDispatchToProps parameter can be of two forms.
While the `function form` allows more customization, the `object form` is easy to use.

- Function form<br>
  Allows more customization, gains access to `dispatch` and optionally `ownProps`
- Object shorthand form<br>
  More declarative and easier to use

## Defining `mapDispatchToProps` As A Function

Defining `mapDispatchToProps` as a function gives you the most flexibility in customizing the functions your component receives, and how they dispatch actions.<br>
You gain access to `dispatch` and `ownProps`.<br>
You may use this chance to write customized functions to be called by your connected components.<br>

#### Arguments

1. dispatch<br>
   The `mapDispatchToProps` function will be called with `dispatch` as the first argument. <br>
   You will normally make use of this by returning **_new functions that call `dispatch()` inside themselves_**, and either pass in a **_plain action object_** directly or pass in the **_result of an action creator_**.

2. ownProps (optional)<br>
   If your `mapDispatchToProps` function is declared as taking two parameters, it will be called with `dispatch` as the first parameter and the `props` passed to the connected component as the second parameter, and will be re-invoked whenever the connected component receives new props.

```javascript
// binds on component re-rendering
<button onClick={() => this.props.toggleTodo(this.props.todoId)} />;

// binds on `props` change
const mapDispatchToProps = (dispatch, ownProps) => {
  toggleTodo: () => dispatch(toggleTodo(ownProps.todoId));
};
```

#### Return

Your `mapDispatchToProps` function should return a plain object:

- Each field in the object will become a separate prop for your own component, and the value should normally be a function that dispatches an action when called.
- If you use action creators ( as oppose to plain object actions ) inside `dispatch`, it is a convention to simply name the field key the same name as the action creator:

```javascript
const increment = () => ({ type: "INCREMENT" });
const decrement = () => ({ type: "DECREMENT" });
const reset = () => ({ type: "RESET" });

const mapDispatchToProps = dispatch => {
  return {
    // dispatching actions returned by action creators
    increment: () => dispatch(increment()),
    decrement: () => dispatch(decrement()),
    reset: () => dispatch(reset())
  };
};
```

The return of the `mapDispatchToProps` function will be merged to your connected component as props.<br>
You may call them directly to dispatch its action.

```javascript
function Counter({ count, increment, decrement, reset }) {
  return (
    <div>
      <button onClick={decrement}>-</button>
      <span>{count}</span>
      <button onClick={increment}>+</button>
      <button onClick={reset}>reset</button>
    </div>
  );
}
```

#### Defining the `mapDispatchToProps` Function with `bindActionCreators`

`bindActionCreators` turns an object whose values are `action creators`, into an object with the same keys, but with every action creator wrapped into a `dispatch` call so they may be invoked directly.<br>

`bindActionCreators` accepts two parameters:

- A `function` (an action creator) or an `object` (each field an action creator)
- `dispatch`

```javascript
import { bindActionCreators } from "redux";

const increment = () => ({ type: "INCREMENT" });
const decrement = () => ({ type: "DECREMENT" });
const reset = () => ({ type: "RESET" });

// binding an action creator
// returns (...args) => dispatch(increment(...args))
const boundIncrement = bindActionCreators(increment, dispatch);

// binding an object full of action creators
const boundActionCreators = bindActionCreators(
  { increment, decrement, reset },
  dispatch
);
// returns
// {
//   increment: (...args) => dispatch(increment(...args)),
//   decrement: (...args) => dispatch(decrement(...args)),
//   reset: (...args) => dispatch(reset(...args)),
// }
```

To use `bindActionCreators` in our `mapDispatchToProps` function:

```javascript
import { bindActionCreators } from "redux";
// ...

function mapDispatchToProps(dispatch) {
  return bindActionCreators({ increment, decrement, reset }, dispatch);
}

// component receives props.increment, props.decrement, props.reset
connect(
  null,
  mapDispatchToProps
)(Counter);
```

#### Manually Injecting `dispatch`

If the `mapDispatchToProps` argument is supplied, the component will no longer receive the default `dispatch`.

```javascript
import { bindActionCreators } from "redux";
// ...

function mapDispatchToProps(dispatch) {
  return {
    dispatch,
    ...bindActionCreators({ increment, decrement, reset }, dispatch)
  };
}
```

## Defining `mapDispatchToProps` As An Object

Note that:

- Each field of the `mapDispatchToProps` object is assumed to be an action creator
- Your component will no longer receive `dispatch` as a prop

```javascript
const mapDispatchToProps = {
  increment,
  decrement,
  reset
};
```

Since the actual name of the variable is up to you, you might want to give it a name like `actionCreators`, or even define the object inline in the call to connect:

```javascript
import { increment, decrement, reset } from "./counterActions";

const actionCreators = {
  increment,
  decrement,
  reset
};

export default connect(
  mapState,
  actionCreators
)(Counter);
```

or

```javascript
export default connect(
  mapState,
  { increment, decrement, reset }
)(Counter);
```

## Common Problems

#### Why is my component not receiving `dispatch`
1. You do not provide `mapDispatchToProps`
2. Your customized `mapDispatchToProps` function return specifically contains dispatch
```javascript
const mapDispatchToProps = dispatch => {
  return {
    increment: () => dispatch(increment()),
    decrement: () => dispatch(decrement()),
    reset: () => dispatch(reset()),
    dispatch
  }
}
```

#### Can I `mapDispatchToProps` without `mapStateToProps` in `Redux`
Yes


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
