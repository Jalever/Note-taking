---
layout: post
title: dva
subtitle: Web Development学习笔记系列
date: 2019-04-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - dva
---

## Data Flow

## Models

#### State

The state tree of your models.<br>
Usually, the state is a `Javascript` object(Technically it can be any type), which is a immutable data.

#### Action

`Actions` are the only way to get data into the store.<br>
Any data, whether from <ins>UI events</ins>, <ins>network callbacks</ins>, or other sources such as <ins>WebSockets</ins> needs to eventually be dispatched as `actions.action`.

```jsx
dispatch({
  type: "add"
});
```

#### dispatch function

`Dispatching function` is a function for triggering action<br>
`action` is the only way to change state<br>
`Dispatch` can be regarded as a way to trigger this action<br>
`Reducer` is to describe how to change state<br>

```jsx
dispatch({
  type: "user/add", // if in model outside, need to add namespace
  payload: {}
});
```

#### Reducer

`Reducer` (also called a `reducing function`) is a function that accepts an accumulation and a value and returns a new accumulation. They are used to reduce a collection of values down to a single value
In `dva`, `Reducers` accumulate current model's state.<br>

#### Effect

In `dva`, we use `redux-sagas` to control asynchronous flow

#### Subscription

`Subscriptions` is a way to get data from source, it is come from `elm`.
Data source can be: <ins>the current time</ins>, <ins>the websocket connection of server</ins>, <ins>keyboard input</ins>, <ins>geolocation change</ins>, <ins>history router change</ins>, etc..

## Router

Because our current app is `SPA`, frontend codes are required to control the router logics.<br>
Through `History API` provided by the browser, we can monitor the change of the browser's url, so as to control the router.

## Route Components
