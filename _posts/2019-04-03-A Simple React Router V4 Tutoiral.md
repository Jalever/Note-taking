---
layout: post
title: A Simple React Router V4 Tutorial
subtitle: React-Router学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React-Router
---
- [Installation](#installation)
- [Determining which type of router to use](#determining-which-type-of-router-to-use)
- [History](#history)
- [Rendering a <Router>](#rendering-a-router)
- [The <App>](#the-app)
- [Routes](#routes)
    - [<Route>](#route)
    - [path](#path)
    - [`<Switch>`](#switch)
    - [What does the <Route> render?](#what-does-the-route-render)
        - [component](#component)
        - [render](#render)
        - [children](#children)

## Installation
`React Router` has been broken into three packages: 
- `react-router`
That package provides the core routing components and functions for `React Router` applications.
- `react-router-dom`
This provides environment specific `browser` components, but it also re-export all of `react-router`'s exports.
- `react-router-native`
This  provide environment specific `React Native` components, but it also re-export all of `react-router`'s exports.

## Determining which type of router to use
`<BrowserRouter>` should be used when you have a server that will handle dynamic requests (knows how to respond to any possible `URI`)<br>
`<HashRouter>` should be used for static websites (where the `server` can only respond to requests for files that it knows about)

## History
Each router creates a `history` object, which it uses to keep track of the current location and re-render the website whenever that changes.<br>
The other components provided by `React Router` rely on having that history object available through `React`’s context, so they must be rendered as descendants of a router component.<br>
A `React Router` component that does not have a router as one of its ancestors will fail to work.

## Rendering a <Router>
`Router` components only expect to receive a single child element. <br>
To work within this limitation, it is useful to create an `<App>` component that renders the rest of your application.
```javascript
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render((
  <BrowserRouter>
    <App />
  </BrowserRouter>
), document.getElementById('root'));
```

## The <App>
Our application is defined within the `<App>` component.<br>
The `<Header>` component will contain links to navigate throughout the website.<br>
The `<Main>` component is where the rest of the content will be rendered.
```javascript
function App() {
  return (
    <div>
      <Header />
      <Main />
    </div>
  );
}
```

## Routes
```javascript
import { Switch, Route } from 'react-router-dom'
function Main() {
  return (
    <main>
      <Switch>
        <Route exact path='/' component={Home}/>
        <Route path='/roster' component={Roster}/>
        <Route path='/schedule' component={Schedule}/>
      </Switch>
    </main>
  );
}
```

#### <Route>
The `<Route>` component is the main building block of `React Router`. <br>
Anywhere that you want to only render content based on the location’s pathname, you should use a `<Route>` element.

#### path
A `<Route>` expects a ***path prop***, which is a string that describes the pathname that the route matches<br>
for example, `<Route path='/roster'/>` should match a pathname that begins with `/roster`<br>
When the current location’s pathname is matched by the path, the route will render a `React` element.
When the path does not match, the route will not render anything

#### `<Switch>`
The `<Switch>` will iterate over its children elements (the routes) and only render the first one that matches the current pathname.<br>
For this website, the paths that we want to match are:
| /               | the homepage                                      |
| --------------- | ------------------------------------------------- |
| /roster         | the team's roster                                 |
| /roster/:number | a profile for a player, using the player's number |
| /schedule       | the team's schedule of games                      |
```javascript
<Switch>
  <Route exact path='/' component={Home}/>
  {/* both /roster and /roster/:number begin with /roster */}
  <Route path='/roster' component={Roster}/>
  <Route path='/schedule' component={Schedule}/>
</Switch>
```

#### What does the <Route> render?
`Routes` have three props that can be used to define what should be rendered when the route’s path matches. 
Only one should be provided to a `<Route>` element.

The element rendered by the `<route>` will be passed a number of props.


###### component 
- A React component
- When a route with a component prop matches, the route will return a new element whose type is the provided `React` component (created using `React.createElement`)
```javascript
<Route path='/page' component={Page} />
```
###### render 
- A function that returns a `React` element
- It will be called when the path matches
- This is similar to component, but is useful for inline rendering and passing extra props to the element
```javascript
const extraProps = { color: 'red' }
<Route path='/page' render={(props) => (
  <Page {...props} data={extraProps}/>
)}/>`
```
###### children 
- A function that returns a React element
- Unlike the prior two props, this will always be rendered, regardless of whether the route’s path matches the current location.
```javascript
<Route path='/page' children={(props) => (
  props.match
    ? <Page {...props}/>
    : <EmptyPage {...props}/>
)}/>
```


