---
layout:     post
title:      React-Redux 浅显使用方法
subtitle:   React学习笔记系列
date:       2019-05-09
author:     Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - React
---

项目`store.js`文件中
```jsx
import { createStore, applyMiddleware } from "redux";

const store = createStore(
    reducers....
);
```
store.getState();<br/>
store.dipatch()

项目`index.html`文件中
```jsx
import { Provider } from "react-redux";

<Provider store={store}>
    <App />
</Provider>
```

然后创建`actions/xxx.js` <br/>
创建`reducers/xxx.js`

`reducers`过多的话，可以用`import { combineReducers } from "redux";`

页面中用`import { connect } from "react-redux";`




---

import {put, takeaway} from "redux-saga/effects";
