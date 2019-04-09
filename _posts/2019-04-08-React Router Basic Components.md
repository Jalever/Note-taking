---
layout: post
title: Basic Components
subtitle: React Router Guides学习笔记系列 2
date: 2019-04-08
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Router
---

- [Routers](#routers)
- [Route Matching](#route-matching)
- [Route Rendering Props](#route-rendering-props)
- [Navigation](#navigation)

There are three types of components in `React Router`:

- **_router components_**
- **_route matching components_**
- **_navigation components_**

## Routers
`<BrowserRouter>` if you have a ***server that responds to requests*** <br>
`<HashRouter>` if you are using a ***static file server***.
```javascript
import { BrowserRouter } from "react-router-dom";
ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  holder
);

```

## Route Matching
There are two route matching components:
- `<Route>` <br>
- `<Switch>`<br>
`Route matching` is done by comparing a `<Route>`'s ***path*** prop to the current location’s pathname. <br>
When a `<Route>` matches it will render its content and when it does not match, it will render ***null***. <br>
A `<Switch>` will iterate over all of its children `<Route>` elements and only render the first one that matches the current location.
```javascript
<Switch>
  <Route exact path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
</Switch>
```

A `<Route>` with no path will always match.<br>

```javascript
<Switch>
  <Route exact path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
  {/* when none of the above match, <NoMatch> will be rendered */}
  <Route component={NoMatch} />
</Switch>
```

## Route Rendering Props
You have three prop choices for how you render a component for a given `<Route>`: 
- component
- render
- children

`component` should be used when you have an existing component (either a ***React.Component*** or a ***stateless functional component***) that you want to render.<br>
`render`, which takes an inline function, should only be used when you have to pass in-scope variables to the component you want to render. <br>
You should not use the `component` prop with an inline function to pass in-scope variables because you will get undesired component unmounts/remounts.
```javascript
const Home = () => <div>Home</div>;

const App = () => {
  const someVariable = true;

  return (
    <Switch>
      {/* these are good */}
      <Route exact path="/" component={Home} />
      <Route
        path="/about"
        render={props => <About {...props} extra={someVariable} />}
      />
      {/* do not do this */}
      <Route
        path="/contact"
        component={props => <Contact {...props} extra={someVariable} />}
      />
    </Switch>
  );
};

```

## Navigation
`React Router` provides a `<Link>` component to create links in your application.<br>
The `<NavLink>` is a special type of `<Link>` that can style itself as “active” when its <ins>to</ins> prop matches the current location.<br>
Any time that you want to force navigation, you can render a `<Redirect>`. When a `<Redirect>` renders, it will navigate using its <ins>to</ins> prop.

```javascript
<Link to="/">Home</Link>
// <a href='/'>Home</a>

The <NavLink> is a special type of <Link> that can style itself as “active” when its to prop matches the current location.

// location = { pathname: '/react' }
<NavLink to="/react" activeClassName="hurray">
  React
</NavLink>
// <a href='/react' className='hurray'>React</a>

// Any time that you want to force navigation, you can render a <Redirect>. When a <Redirect> renders, it will navigate using its to prop.

<Redirect to="/login" />

```
