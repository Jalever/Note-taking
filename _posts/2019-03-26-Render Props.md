---
layout: post
title: Render Props
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.png
catalog: true
tags:
  - React
---

The term `render prop` refers to a technique for sharing code between `React components` using a prop whose value is a function.<br>
A component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.<br>
```javascript
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```

- [Use Render Props for Cross-Cutting Concerns](#use-render-props-for-cross-cutting-concerns)
- [Using Props Other Than render](#using-props-other-than-render)
- [Caveats](#caveats)
    - [Be careful when using Render Props with React.PureComponent](#be-careful-when-using-render-props-with-reactpurecomponent)

## Use Render Props for Cross-Cutting Concerns
> Cross-Cutting Concerns: It is a concern which is applicable throughout the application and it affects the entire application.For example: logging, security and data transfer are the concerns which are needed in almost every module of an application, hence they are cross-cutting concerns.

Components are the primary unit of code reuse in React, but it’s not always obvious how to share the state or behavior that one component encapsulates to other components that need that same state.
For example:
```javascript
// The <Mouse> component encapsulates the behavior we need...
class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>

        {/* ...but how do we render something other than a <p>? */}
        <p>The current mouse position is ({this.state.x}, {this.state.y})</p>
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse />
      </div>
    );
  }
}
```
Now the `<Mouse>` component encapsulates all behavior associated with listening for `mousemove` events and storing the `(x, y)` position of the cursor, but it’s not yet truly reusable.<br>
As a first pass, you might try rendering the `<Cat>` inside `<Mouse>`’s render method, like this:
```javascript
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class MouseWithCat extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>

        {/*
          We could just swap out the <p> for a <Cat> here ... but then
          we would need to create a separate <MouseWithSomethingElse>
          component every time we need to use it, so <MouseWithCat>
          isn't really reusable yet.
        */}
        <Cat mouse={this.state} />
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <MouseWithCat />
      </div>
    );
  }
}
```
This approach will work for our specific use case, but we haven’t achieved the objective of truly encapsulating the behavior in a reusable way. Now, every time we want the mouse position for a different use case, we have to create a new component (i.e. essentially another `<MouseWithCat>`) that renders something specifically for that use case.<br>
Here’s where the `render prop` comes in: Instead of hard-coding a <Cat> inside a <Mouse> component, and effectively changing its rendered output, we can provide <Mouse> with a function prop that it uses to dynamically determine what to render–a render prop.
```javascript
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>Move the mouse around!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```

## Using Props Other Than render
Any prop that is a function that a component uses to know what to render is technically a `render prop`
you have to explicitly state that children should be a function in your propTypes when designing an API like this.
```javascript
Mouse.propTypes = {
  children: PropTypes.func.isRequired
};
```

## Caveats 

#### Be careful when using Render Props with React.PureComponent 
Using a `render prop` can negate the advantage that comes from using `React.PureComponent` if you create the function inside a `render` method.<br>
This is because the shallow prop comparison will always return `false` for new props, and each `render` in this case will generate a new value for the render prop.

