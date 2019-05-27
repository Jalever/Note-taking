---
layout:     post
title:      React-Saga Handbook
subtitle:   React学习笔记系列
date:       2019-05-10
author:     Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - React Saga
---


## Saga Helpers

#### takeLatest
It allows only one "fetchData" task to run at any moment. <br/>
And it will be the latest started task. If a previous task is still running when another "fetchData" task is started, the previous task will be automatically cancelled.

#### fork
If you have multiple Sagas watching for different actions, you can create multiple watchers with those built-in helpers<br/>

When we fork a task, the task is started in the background and the caller can continue its flow without waiting for the forked task to terminate.


#### cancel
In order to cancel a forked task, we use a dedicated Effect `cancel`


#### race
Sometimes we start multiple tasks in parallel but we don't want to wait for all of them, we just need to get the winner: the first one that resolves (or rejects).<br/>
it automatically cancels the loser Effects.

## Effect
An "Effect" is an object that contains some information to be interpreted by the middleware.<br/>
You can view Effects like instructions to the middleware to perform some operation (e.g., invoke some asynchronous function, dispatch an action to the store, etc.).

To create Effects, you use the functions provided by the library in the `redux-saga/effects` package

#### call
`call` also supports invoking object methods, you can provide a this context to the invoked functions using the following form:
```jsx
yield call([obj, obj.method], arg1, arg2, ...) // as if we did obj.method(arg1, arg2 ...)
```

#### apply
`apply` is an alias for the method invocation form
```jsx
yield apply(obj, obj.method, [arg1, arg2, ...])
```

#### cps    
`cps` can be used to handle Node style functions (e.g. `fn(...args, callback)` where callback is of the form `(error, result) => ()`). <br />
`cps` stands for Continuation Passing Style.
