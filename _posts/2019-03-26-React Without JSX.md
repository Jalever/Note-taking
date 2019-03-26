---
layout:     post
title:      React Without JSX
subtitle:   React学习笔记系列
date:       2019-03-26
author:     Jalever
header-img: img/post_2019_react_bg.png
catalog: true
tags:
    - React
---

`JSX` is not a requirement for using `React`.
Each `JSX` element is just syntactic sugar for calling `React.createElement(component, props, ...children)`. So, anything you can do with `JSX` can also be done with just `plain JavaScript`.<br>
For example, this code written with `JSX`:
```
class Hello extends React.Component {
  render() {
    return <div>Hello {this.props.toWhat}</div>;
  }
}

ReactDOM.render(
  <Hello toWhat="World" />,
  document.getElementById('root')
);
```
can be compiled to this code that does not use `JSX`:
```
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Hello ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, {toWhat: 'World'}, null),
  document.getElementById('root')
);
```

The component can either be provided as a `string`, or as `a subclass of React.Component`, or `a plain function for stateless components`.

If you get tired of typing React.createElement so much, one common pattern is to assign a shorthand:<br>
```
const e = React.createElement;

ReactDOM.render(
  e('div', null, 'Hello World'),
  document.getElementById('root')
);
```






