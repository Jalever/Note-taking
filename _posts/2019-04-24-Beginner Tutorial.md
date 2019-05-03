---
layout: post
title: Beginner Tutorial
subtitle: React Saga学习笔记系列 1
date: 2019-04-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - React Saga
---

```jsx
import { put, takeEvery } from 'redux-saga/effects'

...

export function* incrementAsync() {
  yield delay(1000)
  yield put({ type: 'INCREMENT' })
}

// Our watcher Saga: spawn a new incrementAsync task on each INCREMENT_ASYNC
export function* watchIncrementAsync() {
  yield takeEvery('INCREMENT_ASYNC', incrementAsync)
}
```

`put` is one example of what we call an `Effect`. <br>
`Effects` are plain JavaScript objects which contain instructions to be fulfilled by the middleware.<br>
When a middleware retrieves an `Effect` yielded by a `Saga`, the `Saga` is paused until the `Effect` is fulfilled.
`takeEvery`, a helper function provided by `redux-saga`, to listen for dispatched `INCREMENT_ASYNC` actions and run `incrementAsync` each time.


If there are some sagas but you just want to start them both at once, add a `rootSaga` that is responsible for starting our other `Sagas`.
```jsx
import { put, takeEvery, all } from 'redux-saga/effects'

...

export default function* rootSaga() {
  yield all([
    helloSaga(),
    watchIncrementAsync()
  ])
}
```
This `Saga` yields an array with the results of calling our two sagas, `helloSaga` and `watchIncrementAsync`.

If the `Effect` type is a `PUT` then it will dispatch an action to the `Store`. If the `Effect` is a `CALL` then it'll call the given function.<br>


In fact, neither `put` nor `call` performs any <ins>dispatch</ins> or <ins>asynchronous call</ins> by themselves, they return ***plain JavaScript objects***.