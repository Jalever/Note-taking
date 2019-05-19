---
layout: post
title: 前端路由原理实现
subtitle: React Router学习笔记系列
date: 2019-05-19
author: Jalever
header-img: img/post_2019_react_contextAPI_bg.png
catalog: true
tags:
  - React Router
---

## `hash`实现
`index.js`文件
```js
import BrowserRouter from "./BrowseRouter";
import Link from "./Link";
import Route from "./Route";

<BrowserRouter>
    <ul>
        <li>
            <Link to="/home">Home</Link>
        </li>
        <li>
            <Link to="/about">About</Link>
        </li>
    </ul>

    <hr/>

    <Route path="/home" render={() => <h1>Home</h1>} />
    <Route path="/about" render={() => <h1>About</h1>} />
</BrowserRouter>
```

`BrowseRouter.js`文件
```js
import React, { useState, useEffect } from "react";
import RouteContext from "./routeContext";


let BrowserRouter = props => {
    let [currentPath, setCurrentPath] = useState(window.location.hash);

    let handleHashChange = () => {
        let location = window.location;
        setCurrentPath(location.hash.substring(1));
    };

    useEffect(() => {

        let location = window.location;

        window.addEventListener("hashchange", handleHashChange);

        return () => window.removeEventListener("hashchange", handleHashChange);
    }, []);



    return(
        <RouteContext.Provider value={{ currentPath: currentPath }}>
            { props.children }
        </RouteContext.Provider>
    );
};


export default BrowserRouter;
```

`Route.js`文件
```js
import React from "react";
import RouteContext from "./routeContext";

export default ({ path, render }) => {
    return(
        <RouteContext.Consumer>
            {
                value => {
                    return (value.currentPath) === path && render();
                }
            }
        </RouteContext.Consumer>
    );
};
```

`Link.js`文件
```js
import React from "react";
import RouteContext from "./routeContext";

export default ({ to, ...props }) => {
    return(
        <a {...props} href={"#" + to} />
    );
};
```

`routeContext.js`文件
```js
import React,{ createContext } from "react";
const RouteContext = createContext();
export default RouteContext;
```
