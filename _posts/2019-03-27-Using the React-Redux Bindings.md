---
layout: post
title: Using the React-Redux Binding
subtitle: React Hooks学习笔记系列
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Redux
---

- [Using the React-Redux Bindings](#using-the-react-redux-bindings)
  - [Using Redux with React](#using-redux-with-react)
  - [What Does <ins>***connect***</ins> Do?](#what-does-insconnectins-do)
  - [Why Use <ins>***React-Redux***</ins>?](#why-use-insreact-reduxins)
  - [<ins>***connect***</ins> Basics](#insconnectins-basics)
  - [App Setup with <ins>Provider</ins>](#app-setup-with-insproviderins)
  - [Writing <ins>***mapState***</ins> Functions](#writing-insmapstateins-functions)
  - [Writing <ins>***mapDispatch***</ins> Functions](#writing-insmapdispatchins-functions)
  - [Tips for Using <ins>***connect***</ins>](#tips-for-using-insconnectins)
  - [Inside <ins>***connect***</ins>](#inside-insconnectins)
  - [Inside <ins><b>&#60;Provider&#62;</b></ins>](#inside-insb60provider62bins)
  - [Links](#links)

## Using the React-Redux Bindings

### Using Redux with React
&ensp;&ensp;Redux can be used with any UI layer (such as Angular, Vue, or plain JS), but is most commonly used with React.<br/>

&ensp;&ensp;The official <ins>***React-Redux***</ins> package provides bindings between <ins>***React***</ins> and <ins>***Redux***</ins>.<br/>

&ensp;&ensp;The connect function generates wrapper "container" components that subscribe to the store, so you don't have to write store subscription code for every component that needs to talk to the store.<br/>

&ensp;&ensp;Any component in your application can be wrapped with connect and "connected" to the store. <br/>

&ensp;&ensp;Connecting more components is usually better for performance.<br/>

&ensp;&ensp;Finally, putting a <ins><b>&#60;Provider&#62;</b></ins>; component around your root component makes the store accessible to all connected components.<br/>

![react-redux-provider](https://github.com/Jalever/Note-taking/blob/master/images/react-redux-provider.png)

### What Does <ins>***connect***</ins> Do?
* Automatically handles subscribing to the store, and helps dispatch actions.<br/>

* Performance optimizations - automatically implements shouldComponentUpdate, and only re-renders your component when the data it needs changes.<br/>

* Separates "subscribing to the store" from "what store am I subscribing to, and where did it come from?"<br/>

* Helps keep your <ins>***React***</ins> components "unaware" of Redux.<br/>

### Why Use <ins>***React-Redux***</ins>?
* There's no reason to write repetitive store subscription logic in every component. connect handles that for you automatically.

* connect does a lot of work to ensure your real component only re-renders when it actually needs to. If you hand-write subscription code, your component will probably re-render too often.

* Manually importing the store ties your components to that specific store instance, making it harder to test them. React-Redux's <Provider> acts as a lightweight dependency injection approach, which lets you reuse Redux-connected components and test them with a fake store if needed.

* Your components will receive data and callback functions as props, same as any other React component would. This makes the more reusable.

* Effectively all React+Redux apps use React-Redux, so that's what the documentation, articles, and community all refer to.

### <ins>***connect***</ins> Basics
The connect function takes two arguments, both optional:
* <ins>***mapStateToProps***</ins>: called every time the store state changes. It receives the entire store state, and should return an object of data this component needs.

* <ins>***mapDispatchToProps***</ins>: called once on component creation. It receives the dispatch method, and should return an object full of functions that use dispatch.

&ensp;&ensp;For both functions, each field in the returned object becomes a prop for the wrapped component.<br/>
&ensp;&ensp;<ins>***connect***</ins> returns a new function that accepts the component to wrap, and that function returns the wrapper component.

```
import {connect} from "react-redux";
import {increment} from "./counterActions";

function mapStateToProps(state) {
    return {
        // The "counter" field in this object becomes props.counter
        counter : state.counter
    };
}

function mapDispatchToProps(dispatch, ownProps) {
    return {
        // The "increment" field in this object becomes props.increment
        increment : () => dispatch(increment())
    };
}

const Counter = (props) => (
    <div>
        <div>Counter value: {props.counter}</div>,
        <button onClick={props.increment}>Increment</button>
    </div>
);

export default connect(mapStateToProps, mapDispatchToProps)(Counter);
// Expanded:
// const generateWrapperComponent = connect(mapState, mapDispatch);
// const ConnectedCounter = generateWrapperComponent(Counter);
```
### App Setup with <ins>Provider</ins>
&ensp;&ensp;Wrapping your root application component in <ins><b>&#60;Provider&#62;</b></ins> and passing it the store reference makes that store available to all connected components in the component tree.

```
import React from "react";
import ReactDOM from "react-dom";
import {Provider} from "react-redux";

import {store} from "./store";

// App may be connected itself, and have connected
// components deep inside its tree
import App from "./App";

ReactDOM.render(
    // Wrap your top-level component in <Provider>,
    // and pass in the store reference
    <Provider store={store}>
        <App />
    </Provider>,
    document.getElementById("root")
);
```

### Writing <ins>***mapState***</ins> Functions
* connect will re-run your <ins>***mapState***</ins> function every time the store state changes. It does a **shallow equality** comparison between the last and current result objects, and re-renders your component if any fields are ***===*** different than the last result.

* If your function is written with two parameters, it will get the wrapper component's props as the second argument, and it will also be called whenever the props passed to the wrapper component change.

* Similar to reducers, a <ins>***mapState***</ins> function should be pure and have no side effects - just state ( + wrapper props) in, new component props out.

```
// Also commonly known as "mapState" for short
function mapStateToProps(state) {
    return {
        counter : state.counter
    };
}

// Same thing, just with lots of ES6 shorthand
const mapState = ({counter}) => ({counter});

// If declared with two arguments, will be called whenever
// the state changes _and_ when incoming props change
const mapState = (state, ownProps) => ({
    todo : state.todos[ownProps.todoIndex]
});

// can contain whatever logic and data preparation
// steps you need, not just "return state.whatever"
const mapState = (state) => {
    const {basicData, otherItem} = state;
    const transformedData = transformStuff(basicData);
    const filteredData = filterStuff(transformedData);

    return {
        data : filteredData,
        otherItem,
    };
}
```

### Writing <ins>***mapDispatch***</ins> Functions
* By default, <ins>***connect***</ins> gives your components <ins>***props.dispatch***</ins>.

* If you want to "bind" action creators instead, you can provide a <ins>***mapDispatch***</ins> function as the second argument to <ins>***connect***</ins>. It gets <ins>***dispatch***</ins> as an argument, and you can return functions that will dispatch automatically when called.

* Declaring <ins>***mapDispatch***</ins> with two arguments works the same way as <ins>***mapState***</ins> - will be given <ins>***ownProps***</ins>, and re-run when they change

* ***Better choice***: pass an object full of action creators as the second argument to connect (the "object shorthand")

### Tips for Using <ins>***connect***</ins>
* You can connect as many of your app's components as you want, not just the root component. In fact, connecting more components is usually better for performance!

* Feel free to connect any component that needs to access store state or dispatch actions, or where passing props down multiple levels would be a pain.

* Only declare your <ins><b>map&#42;</b></ins> functions with two arguments if you really need to reference the props, otherwise it's a waste.

* Useful pattern: connected list components rendering connected list item components. 
Usually requires passing an item ID, like <ListItem itemId={123} />. (This works best if your state uses a "normalized" structure, so you can look up items by ID easily.)

* Both <ins><b>map&#42;</b></ins> functions are optional. If you only need data, use <ins><b>connect(mapState)(MyComponent)</b></ins>. If you only need to dispatch, use <ins><b>connect(null, mapDispatch)(MyComponent)</b></ins>.

* My advice: never write an actual <ins>***mapDispatch***</ins> function yourself - use the "object shorthand" form with action creators instead!

### Inside <ins>***connect***</ins>
```
// connect() is a function that injects Redux-related props into your component.
// You can inject data and callbacks that change that data by dispatching actions.

function connect(mapStateToProps, mapDispatchToProps) {
    // It lets us inject component as the last step so people can use it as
    // a decorator, or reuse the connection definition with multiple components.
    // Generally you don't need to worry about it.
    return function (WrappedComponent) {
        // It returns a component
        return class ConnectWrapper extends React.Component {
            render() {
                return (
                    // that renders your component
                    <WrappedComponent
                        {/* with its props  */}
                        {...this.props}
                        {/* and additional props calculated from Redux store */}
                        {...mapStateToProps(store.getState(), this.props)}
                        {...mapDispatchToProps(store.dispatch, this.props)}
                    />
                )
            }

            componentDidMount() {
                // Subscribes to the store so it doesn't miss updates
                this.unsubscribe = store.subscribe(this.handleChange.bind(this))
            }

            componentWillUnmount() {
                // Unsubscribes when the component unmounts
                this.unsubscribe()
            }

            handleChange() {
                // Re-renders when the store state changes
                this.forceUpdate()
            }
        }
    }
}

// Not the real implementation but a mental model.
// It skips the question of where we get the "store"
// from (answer: <Provider> puts it in React context)
// and it skips any performance optimizations (real
//  connect() makes sure we don't re-render in vain).

// The purpose of connect() is that you don't have to
// think about subscribing to the store or perf
```

### Inside <ins><b>&#60;Provider&#62;</b></ins>
```
import {Children, Component} from "react";

export function createProvider(storeKey = 'store', subKey) {
    const subscriptionKey = subKey || `${storeKey}Subscription`

    class Provider extends Component {
        getChildContext() {
            return { [storeKey]: this[storeKey], [subscriptionKey]: null }
        }

        constructor(props, context) {
            super(props, context)
            this[storeKey] = props.store;
        }

        render() {
            return Children.only(this.props.children)
        }
    }

    Provider.childContextTypes = {
        [storeKey]: storeShape.isRequired,
        [subscriptionKey]: subscriptionShape,
    }

    return Provider
}
```

### Links
[Using the React-Redux Bindings](https://blog.isquaredsoftware.com/presentations/workshops/redux-fundamentals/react-redux.html#/)












