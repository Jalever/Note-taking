---
layout: post
title: history
subtitle: React Router API学习笔记系列
date: 2019-04-08
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Router
---

- [Preface](#preface)
    - [browser history](#browser-history)
    - [hash history](#hash-history)
    - [memory history](#memory-history)
- [`history` objects typically have the following **_properties_** and **_methods_**:](#history-objects-typically-have-the-following-properties-and-methods)
    - [length - (number)](#length---number)
    - [action - (string)](#action---string)
    - [location - (object)](#location---object)
        - [pathname - (string)](#pathname---string)
        - [search - (string)](#search---string)
        - [hash - (string)](#hash---string)
        - [state - (object)](#state---object)
    - [push(path, [state]) - (function)](#pushpath-state---function)
    - [replace(path, [state]) - (function)](#replacepath-state---function)
    - [go(n) - (function)](#gon---function)
    - [goBack() - (function)](#goback---function)
    - [goForward() - (function)](#goforward---function)
    - [block(prompt) - (function)](#blockprompt---function)
- [`history` is mutable](#history-is-mutable)

## Preface

History provides several different implementations for managing session history in `JavaScript` in various environments.

#### browser history

A `DOM-specific` implementation, useful in **_web browsers_** that support the `HTML5 history API`

#### hash history

A `DOM-specific` implementation for legacy web browsers

#### memory history

An in-memory history implementation, useful in **_testing_** and **_non-DOM environments_** like `React Native`

## `history` objects typically have the following **_properties_** and **_methods_**:

#### length - (number)

The number of entries in the history stack

#### action - (string)

The current action (PUSH, REPLACE, or POP)

#### location - (object)

The current location.<br>
May have the following properties:

###### pathname - (string)

The path of the `URL`

###### search - (string)

The `URL` query string

###### hash - (string)

The `URL` hash fragment

###### state - (object)

location-specific state that was provided to e.g. `push`(path, state) when this location was pushed onto the stack. <br>
Only available in **_browser_** and **_memory_** history.

#### push(path, [state]) - (function) 
Pushes a new entry onto the history stack
#### replace(path, [state]) - (function) 
Replaces the current entry on the history stack
#### go(n) - (function) 
Moves the pointer in the history stack by n entries
#### goBack() - (function) 
Equivalent to go(-1)
#### goForward() - (function) 
Equivalent to go(1)
#### block(prompt) - (function) 
Prevents navigation


## `history` is mutable
The `history` object is mutable. <br>
Therefore it is recommended to access the location from the render props of `<Route>`, not from `history.location`. <br>
This ensures your assumptions about `React` are correct in lifecycle hooks.
