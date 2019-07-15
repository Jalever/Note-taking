---
layout: post
title: React Context
subtitle: React Advanced Guides
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

`Context` provides a way to **_pass data through the component tree without having to pass props down manually at every level_**.

`Context` provides a way to share values between components without having to explicitly pass a prop through every level of the tree.

- [When to Use Context](#when-to-use-context)
- [Before You Use Context](#before-you-use-context)
- [API](#api)
    - [React.createContext](#reactcreatecontext)
    - [Context.Provider](#contextprovider)
    - [Class.contextType](#classcontexttype)
    - [Context.Consumer](#contextconsumer)
- [Usage](#usage)

## When to Use Context

`Context` is designed to **_share data that can be considered “global” for a tree of React components_**, such as the current authenticated user, theme, or preferred language.

## Before You Use Context

`Context` is primarily used when some data needs to be accessible by many components at different nesting levels. <br>
Apply it sparingly because it makes component reuse more difficult.

## API

#### React.createContext

```javascript
const MyContext = React.createContext(defaultValue);
```

Creates a `Context` object. <br>
When `React` renders a component that subscribes to this `Context` object it will read the current context value from the closest matching Provider above it in the tree.<br>
The `defaultValue` argument is only used when a component does not have a matching `Provider` above it in the tree. <br>
Note: passing undefined as a Provider value does not cause consuming components to use defaultValue.

#### Context.Provider

```javascript
<MyContext.Provider value={/* some value */}>
```

Every `Context` object comes with a `Provider` React component that allows consuming components to subscribe to context changes.
Accepts a value prop to be passed to consuming components that are descendants of this `Provider`.
One Provider can be connected to many consumers.
All consumers that are descendants of a Provider will re-render whenever the Provider’s value prop changes.

#### Class.contextType

The `contextType` property on a class can be assigned a `Context` object created by `React.createContext()`.

```javascript
class MyClass extends React.Component {
  componentDidMount() {
    let value = this.context;
    /* perform a side-effect at mount using the value of MyContext */
  }
  componentDidUpdate() {
    let value = this.context;
    /* ... */
  }
  componentWillUnmount() {
    let value = this.context;
    /* ... */
  }
  render() {
    let value = this.context;
    /* render something based on the value of MyContext */
  }
}
MyClass.contextType = MyContext;
```

#### Context.Consumer

```javascript
<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
```

A `React` component that subscribes to context changes. <br>
This lets you subscribe to a context within a function component.<br>
The value argument passed to the function will be equal to the value prop of the closest `Provider` for this context above in the tree.<br>
If there is no `Provider` for this context above, the value argument will be equal to the `defaultValue` that was passed to `createContext()`.<br>

## Usage

```javascript
const CustomContext = React.createContext();

class Parent extends React.Component {
	constructor(props) {
		super(props);
		this.state = {
			value: 1
		};
		this.handleContextChange = this.handleContextChange.bind(this);
	}

	handleContextChange(argu) {
		this.setState({
			value: argu
		});
	}

	render() {
		let contextValue = {
			data: this.state,
			handleChange: this.handleContextChange
		};

		return(
			<CustomContext.Provider value={contextValue}>
				<Child />
			</CustomContext.Provider>
		);
	}
}

const Child = props => (
	<div>
		<GrandChild />
	</div>
);

const Child2 = props => (
	<p>{ props.text }</p>
);

const GrandChild = props => (
	<CustomContext.Consumer>
		{
			({data, handleChange}) => (
				<React.Fragment>
					<button onClick={ () => handleChange(2) }>
						Change
					</button>
					<Child2 text={data.value} />
				</React.Fragment>
			)
		}
	</CustomContext.Consumer>

);
```

The State of `Parent component` is the value of `Context.Provider`. <br>
`Parent component` is also used as the storage of our storage of the state so that the context can pass it down the hierarchy.<br>
In the `component GrandChild`, we have used the `Context.Consumer` which receives a function via its children render prop.<br>
`component Child` and `Component Child2` which are between `Parent` and `GrandChild` is not aware about the whole context arrangement.