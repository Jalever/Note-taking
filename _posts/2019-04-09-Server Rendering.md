---
layout: post
title: Server Rendering
subtitle: React Router Guides学习笔记系列 2
date: 2019-04-09
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Router
---

## Preface
Rendering on the server is all **_stateless_**, which wrap the app in a stateless `<StaticRouter>`
```javascript
// client
<BrowserRouter>
  <App/>
</BrowserRouter>

// server (not the complete story)
<StaticRouter
  location={req.url}
  context={context}
>
  <App/>
</StaticRouter>

```
When you render a `<Redirect>` on the **_client_**, the browser history changes state and we get the new screen.<br>
In a static server environment we can’t change the app state. Instead, we use the `context prop` to find out what the result of rendering was.<br>
If we find a `context.url`, then we know the app redirected. This allows us to send a proper redirect from the server.
```javascript
const context = {};
const markup = ReactDOMServer.renderToString(
  <StaticRouter location={req.url} context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // Somewhere a `<Redirect>` was rendered
  redirect(301, context.url);
} else {
  // we're good, send the response
}

```

## Adding app specific context information
The router only ever adds `context.url`. <br>
But you may want some redirects to be `301` and others `302`. <br>
Or maybe you’d like to send a `404` response if some specific branch of `UI` is rendered, or a `401` if they aren’t authorized. <br>
The context prop is yours, so you can mutate it.
```javascript
function RedirectWithStatus({ from, to, status }) {
  return (
    <Route
      render={({ staticContext }) => {
        // there is no `staticContext` on the client, so
        // we need to guard against that here
        if (staticContext) staticContext.status = status;
        return <Redirect from={from} to={to} />;
      }}
    />
  );
}

// somewhere in your app
function App() {
  return (
    <Switch>
      {/* some other routes */}
      <RedirectWithStatus status={301} from="/users" to="/profiles" />
      <RedirectWithStatus status={302} from="/courses" to="/dashboard" />
    </Switch>
  );
}

// on the server
const context = {};

const markup = ReactDOMServer.renderToString(
  <StaticRouter context={context}>
    <App />
  </StaticRouter>
);

if (context.url) {
  // can use the `context.status` that
  // we added in RedirectWithStatus
  redirect(context.status, context.url);
}
```

## 404, 401, or any other status
Create a component that adds some context and render it anywhere in the app to get a different status code.<br>
Now We can render a `Status` anywhere in the app that you want to add the code to `staticContext`.<br>
```javascript
function Status({ code, children }) {
  return (
    <Route
      render={({ staticContext }) => {
        if (staticContext) staticContext.status = code;
        return children;
      }}
    />
  );
}

Now you can render a Status anywhere in the app that you want to add the code to staticContext.

function NotFound() {
  return (
    <Status code={404}>
      <div>
        <h1>Sorry, can’t find that.</h1>
      </div>
    </Status>
  );
}

// somewhere else
<Switch>
  <Route path="/about" component={About} />
  <Route path="/dashboard" component={Dashboard} />
  <Route component={NotFound} />
</Switch>;

```

## Putting it all together
#### Server
```javascript
import { createServer } from "http";
import React from "react";
import ReactDOMServer from "react-dom/server";
import { StaticRouter } from "react-router";
import App from "./App";

createServer((req, res) => {
  const context = {};

  const html = ReactDOMServer.renderToString(
    <StaticRouter location={req.url} context={context}>
      <App />
    </StaticRouter>
  );

  if (context.url) {
    res.writeHead(301, {
      Location: context.url
    });
    res.end();
  } else {
    res.write(`
      <!doctype html>
      <div id="app">${html}</div>
    `);
    res.end();
  }
}).listen(3000);

```
#### Server
```javascript
import ReactDOM from "react-dom";
import { BrowserRouter } from "react-router-dom";
import App from "./App";

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById("app")
);
```

## Data Loading
`React Router` exports the `matchPath` static function that it uses internally to match locations to routes. 
You can use this function on the server to help ***determine what your data dependencies will be before rendering***.

```javascript
const routes = [
  {
    path: "/",
    component: Root,
    loadData: () => getSomeData()
  }
  // etc.
];

Then use this config to render your routes in the app:

import { routes } from "./routes";

function App() {
  return (
    <Switch>
      {routes.map(route => (
        <Route {...route} />
      ))}
    </Switch>
  );
}
```

Then on the server you’d have something like:

```javascript
import { matchPath } from "react-router-dom";

// inside a request
const promises = [];
// use `some` to imitate `<Switch>` behavior of selecting only
// the first to match
routes.some(route => {
  // use `matchPath` here
  const match = matchPath(req.path, route);
  if (match) promises.push(route.loadData(match));
  return match;
});

Promise.all(promises).then(data => {
  // do something w/ the data so the client
  // can access it then render the app
});

```
