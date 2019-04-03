---
layout: post
title: mapStateToProps
subtitle: React Redux学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Redux
---

first argument passed in to `connect`<br>
`mapStateToProps` is used for selecting the part of the data from the store that the connected component needs.
 It’s frequently referred to as just `mapState` for short

- It is called every time the store state changes.
- It receives the entire store state, and should return an object of data this component needs.

- [Defining `mapStateToProps`](#defining-mapstatetoprops)
- [Arguments](#arguments)
- [Return](#return)
- [Usage](#usage)

## Defining `mapStateToProps`
mapStateToProps should be defined as a function:
```javascript
function mapStateToProps(state, ownProps?)
```
It should take a first argument called `state`, optionally a second argument called `ownProps`, and return a plain object containing the data that the connected component needs.<br>

This function should be passed as the first argument to connect, and will be called every time when the `Redux` store state changes. If you do not wish to subscribe to the store, pass null or undefined to connect in place of mapStateToProps.<br>

It does not matter if a `mapStateToProps` function is written using the function keyword (`function mapState(state) { }` ) or as an arrow function (`const mapState = (state) => { }` )- it will work the same either way.

## Arguments
1. state
The first argument to a `mapStateToProps` function is the entire `Redux` store state (the same value returned by a call to `store.getState()`)
2. ownProps (optional)
if your component needs the data from its own `props` to retrieve data from the store.

## Return
Your `mapStateToProps` function should return a plain object that contains the data the component needs:
- Each field in the object will become a prop for your actual component
- The values in the fields will be used to determine if your component needs to re-render

## Usage
```javascript
const TodoList = ({ todos }) => (
  <ul className="todo-list">
    {todos && todos.length
      ? todos.map((todo, index) => {
          return <Todo key={`todo-${todo.id}`} todo={todo} />;
        })
      : "No todos, yay!"}
  </ul>
);

// const mapStateToProps = state => {
//   const { byIds, allIds } = state.todos || {};
//   const todos =
//     allIds && state.todos.allIds.length
//       ? allIds.map(id => (byIds ? { ...byIds[id], id } : null))
//       : null;
//   return { todos };
// };

const mapStateToProps = state => {
const { visibilityFilter } = state;
const todos = getTodosByVisibilityFilter(state, visibilityFilter);
return { todos };

export default connect(mapStateToProps)(TodoList);
```
