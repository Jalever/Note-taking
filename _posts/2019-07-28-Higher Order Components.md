---
layout: post
title: Higher Order Components
subtitle: React Advanced Guides
date: 2019-07-28
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---
- [Overview](#overview)
- [Use HOCs For Cross-Cutting Concerns](#use-hocs-for-cross-cutting-concerns)
- [Don’t Mutate the Original Component. Use Composition.](#dont-mutate-the-original-component-use-composition)
- [Convention](#convention)
    - [Pass Unrelated Props Through to the Wrapped Component](#pass-unrelated-props-through-to-the-wrapped-component)
    - [Maximizing Composability](#maximizing-composability)
    - [Wrap the Display Name for Easy Debugging](#wrap-the-display-name-for-easy-debugging)
- [Caveats](#caveats)
    - [Don’t Use HOCs Inside the render Method](#dont-use-hocs-inside-the-render-method)
    - [Static Methods Must Be Copied Over](#static-methods-must-be-copied-over)
    - [Refs Aren’t Passed Through](#refs-arent-passed-through)

## Overview
A higher-order component (HOC) is an advanced technique in React for reusing component logic. HOCs are not part of the React API, per se. They are a pattern that emerges from React’s compositional nature.

Concretely, a higher-order component is a function that takes a component and returns a new component.
![elw1Et.png](https://s2.ax1x.com/2019/07/28/elw1Et.png)
Whereas a component transforms props into UI, a higher-order component transforms a component into another component.

HOCs are common in third-party React libraries, such as Redux’s `connect` and Relay’s `createFragmentContainer`.

## Use HOCs For Cross-Cutting Concerns
Components are the primary unit of code reuse in React. However, you’ll find that some patterns aren’t a straightforward fit for traditional components.

For example, say you have a `CommentList` component that subscribes to an external data source to render a list of comments:
![elBASO.png](https://s2.ax1x.com/2019/07/28/elBASO.png)
![elBV6e.png](https://s2.ax1x.com/2019/07/28/elBV6e.png)
Later, you write a component for subscribing to a single blog post, which follows a similar pattern:
![elD3U1.png](https://s2.ax1x.com/2019/07/28/elD3U1.png)
`CommentList` and `BlogPost` aren’t identical — they call different methods on `DataSource`, and they render different output. But much of their implementation is the same:
- On mount, add a change listener to `DataSource`.
- Inside the listener, call `setState` whenever the data source changes.
- On unmount, remove the change listener.

You can imagine that in a large app, this same pattern of subscribing to `DataSource` and calling `setState` will occur over and over again. We want an abstraction that allows us to define this logic in a single place and share it across many components. This is where higher-order components excel.

We can write a function that creates components, like `CommentList` and `BlogPost`, that subscribe to `DataSource`. The function will accept as one of its arguments a child component that receives the subscribed data as a prop. Let’s call the function `withSubscription`:
![elsWAs.png](https://s2.ax1x.com/2019/07/28/elsWAs.png)
The first parameter is the wrapped component. The second parameter retrieves the data we’re interested in, given a `DataSource` and the current props.

When `CommentListWithSubscription` and `BlogPostWithSubscription` are rendered, `CommentList` and `BlogPost` will be passed a `data` prop with the most current data retrieved from `DataSource`:
![el6ywQ.png](https://s2.ax1x.com/2019/07/28/el6ywQ.png)
![el66oj.png](https://s2.ax1x.com/2019/07/28/el66oj.png)
Note that a HOC doesn’t modify the input component, nor does it use inheritance to copy its behavior. Rather, a HOC composes the original component by wrapping it in a container component. A HOC is a pure function with zero side-effects.

And that’s it! The wrapped component receives all the props of the container, along with a new prop, `data`, which it uses to render its output. The HOC isn’t concerned with how or why the data is used, and the wrapped component isn’t concerned with where the data came from.

Because `withSubscription` is a normal function, you can add as many or as few arguments as you like. For example, you may want to make the name of the `data` prop configurable, to further isolate the HOC from the wrapped component. Or you could accept an argument that configures `shouldComponentUpdate`, or one that configures the data source. These are all possible because the HOC has full control over how the component is defined.

Like components, the contract between `withSubscription` and the wrapped component is entirely props-based. This makes it easy to swap one HOC for a different one, as long as they provide the same props to the wrapped component. This may be useful if you change data-fetching libraries, for example.

## Don’t Mutate the Original Component. Use Composition.
Resist the temptation to modify a component’s prototype (or otherwise mutate it) inside a HOC.
![elctnU.png](https://s2.ax1x.com/2019/07/28/elctnU.png)
There are a few problems with this. One is that the input component cannot be reused separately from the enhanced component. More crucially, if you apply another HOC to EnhancedComponent that also mutates componentWillReceiveProps, the first HOC’s functionality will be overridden! This HOC also won’t work with function components, which do not have lifecycle methods.

Mutating HOCs are a leaky abstraction—the consumer must know how they are implemented in order to avoid conflicts with other HOCs.

Instead of mutation, HOCs should use composition, by wrapping the input component in a container component:
![elc59I.png](https://s2.ax1x.com/2019/07/28/elc59I.png)
This HOC has the same functionality as the mutating version while avoiding the potential for clashes. It works equally well with class and function components. And because it’s a pure function, it’s composable with other HOCs, or even with itself.

You may have noticed similarities between HOCs and a pattern called <strong>Container Components</strong>. Container components are part of a strategy of separating responsibility between high-level and low-level concerns. Containers manage things like subscriptions and state, and pass props to components that handle things like rendering UI. HOCs use containers as part of their implementation. You can think of HOCs as parameterized container component definitions.

## Convention
#### Pass Unrelated Props Through to the Wrapped Component
HOCs add features to a component. They shouldn’t drastically alter its contract. It’s expected that the component returned from a HOC has a similar interface to the wrapped component.

HOCs should pass through props that are unrelated to its specific concern. Most HOCs contain a render method that looks something like this:
![elgBVg.png](https://s2.ax1x.com/2019/07/28/elgBVg.png)
This convention helps ensure that HOCs are as flexible and reusable as possible.

#### Maximizing Composability
Not all HOCs look the same. Sometimes they accept only a single argument, the wrapped component:
![elgWrT.png](https://s2.ax1x.com/2019/07/28/elgWrT.png)
Usually, HOCs accept additional arguments. In this example from Relay, a config object is used to specify a component’s data dependencies:
![elg4ZF.png](https://s2.ax1x.com/2019/07/28/elg4ZF.png)
The most common signature for HOCs looks like this:
![elgTi9.png](https://s2.ax1x.com/2019/07/28/elgTi9.png)
What?! If you break it apart, it’s easier to see what’s going on.
![elg7GR.png](https://s2.ax1x.com/2019/07/28/elg7GR.png)
In other words, `connect` is a higher-order function that returns a higher-order component!

This form may seem confusing or unnecessary, but it has a useful property. Single-argument HOCs like the one returned by the `connect` function have the signature `Component => Component`. Functions whose output type is the same as its input type are really easy to compose together.
![el2eoQ.png](https://s2.ax1x.com/2019/07/28/el2eoQ.png)
(This same property also allows `connect` and other enhancer-style HOCs to be used as decorators, an experimental JavaScript proposal.)

The `compose` utility function is provided by many third-party libraries including lodash (as `lodash.flowRight`), `Redux`, and `Ramda`.

#### Wrap the Display Name for Easy Debugging
The container components created by HOCs show up in the React Developer Tools like any other component. To ease debugging, choose a display name that communicates that it’s the result of a HOC.

The most common technique is to wrap the display name of the wrapped component. So if your higher-order component is named `withSubscription`, and the wrapped component’s display name is `CommentList`, use the display name `WithSubscription(CommentList)`:
![el2gFH.png](https://s2.ax1x.com/2019/07/28/el2gFH.png)

## Caveats
Higher-order components come with a few caveats that aren’t immediately obvious if you’re new to React.

#### Don’t Use HOCs Inside the render Method
React’s diffing algorithm (called reconciliation) uses component identity to determine whether it should update the existing subtree or throw it away and mount a new one. If the component returned from `render` is identical (`===`) to the component from the previous render, React recursively updates the subtree by diffing it with the new one. If they’re not equal, the previous subtree is unmounted completely.

Normally, you shouldn’t need to think about this. But it matters for HOCs because it means you can’t apply a HOC to a component within the render method of a component:
![elRtnf.png](https://s2.ax1x.com/2019/07/28/elRtnf.png)
The problem here isn’t just about performance — remounting a component causes the state of that component and all of its children to be lost.

Instead, apply HOCs outside the component definition so that the resulting component is created only once. Then, its identity will be consistent across renders. This is usually what you want, anyway.

In those rare cases where you need to apply a HOC dynamically, you can also do it inside a component’s lifecycle methods or its constructor.

#### Static Methods Must Be Copied Over
Sometimes it’s useful to define a static method on a React component. For example, Relay containers expose a static method getFragment to facilitate the composition of GraphQL fragments.

When you apply a HOC to a component, though, the original component is wrapped with a container component. That means the new component does not have any of the static methods of the original component.
![elRfN4.png](https://s2.ax1x.com/2019/07/28/elRfN4.png)
To solve this, you could copy the methods onto the container before returning it:
![elRog1.png](https://s2.ax1x.com/2019/07/28/elRog1.png)
However, this requires you to know exactly which methods need to be copied. You can use [hoist-non-react-statics](https://github.com/mridgway/hoist-non-react-statics) to automatically copy all non-React static methods:
![elWSgI.png](https://s2.ax1x.com/2019/07/28/elWSgI.png)
Another possible solution is to export the static method separately from the component itself.
![elWAUg.png](https://s2.ax1x.com/2019/07/28/elWAUg.png)

#### Refs Aren’t Passed Through
While the convention for higher-order components is to pass through all props to the wrapped component, this does not work for refs. That’s because `ref` is not really a prop — like `key`, it’s handled specially by React. If you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.

The solution for this problem is to use the `React.forwardRef` API.

Let’s start with an example HOC that logs component props to the console:
![elWcRA.png](https://s2.ax1x.com/2019/07/28/elWcRA.png)
The “logProps” HOC passes all `props` through to the component it wraps, so the rendered output will be the same. For example, we can use this HOC to log all props that get passed to our “fancy button” component:
![elW5dS.png](https://s2.ax1x.com/2019/07/28/elW5dS.png)
There is one caveat to the above example: refs will not get passed through. That’s because `ref` is not a prop. Like `key`, it’s handled differently by React. If you add a ref to a HOC, the ref will refer to the outermost container component, not the wrapped component.

This means that refs intended for our `FancyButton` component will actually be attached to the `LogProps` component:
![elWHRs.png](https://s2.ax1x.com/2019/07/28/elWHRs.png)
Fortunately, we can explicitly forward refs to the inner `FancyButton` component using the `React.forwardRef` API. `React.forwardRef` accepts a render function that receives `props` and `ref` parameters and returns a React node. For example:
![elfpi4.png](https://s2.ax1x.com/2019/07/28/elfpi4.png)
