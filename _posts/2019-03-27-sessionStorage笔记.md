---
layout: post
title: localStorage and SessionStorage
subtitle: Web API
date: 2019-03-27
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---
## LocalStorage
#### Definition

- The `localStorage` and `sessionStorage` properties allow to save key/value pairs in a web browser.<br>
- The `localStorage` object stores data with no expiration date. The data will not be deleted when the browser is closed, and will be available the next day, week, or year.<br/>
- The `localStorage` property is read-only.<br/>
- `sessionStorage` property which stores data for one session (data is lost when the browser tab is closed).

#### Syntax

> window.localStorage

###### Syntax for SAVING data to sessionStorage:

> localStorage.setItem("key", "value");

###### Syntax for READING data from sessionStorage:

> var lastname = localStorage.getItem("key");

###### Syntax for REMOVING saved data from sessionStorage:

> localStorage.removeItem("key");

#### Usage

```
localStorage.setItem("firstName","Jalever");
localStorage.getItem("lastName","Chen");

let firstName = localStorage.getItem("firstName");
console.log(firstName);
```

#### Browser Support

<table>
    <thead>
        <tr>
            <td>Property</td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/chrome.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/edge.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/firefox.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/safari.png" /></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>sessionStorage</td>
            <td>4.0</td>
            <td>8.0</td>
            <td>3.5</td>
            <td>4.0</td>
        </tr>
    </tbody>
</table>



## Session Storage
#### Definition
The `localStorage` and `sessionStorage` properties allow to save key/value pairs in a web browser.<br>
The `sessionStorage` object stores data for only one session (the data is deleted when the browser tab is closed).<br/>
the `localStorage` property which stores data with no expiration date. The data will not be deleted when the browser is closed, and will be available the next day, week, or year.

#### Syntax
> window.sessionStorage

###### Syntax for SAVING data to sessionStorage:
> sessionStorage.setItem("key", "value");

###### Syntax for READING data from sessionStorage:
> var lastname = sessionStorage.getItem("key");

###### Syntax for REMOVING saved data from sessionStorage:
> sessionStorage.removeItem("key");

###### Syntax for REMOVING ALL saved data from sessionStorage:
> sessionStorage.clear();

#### Usage
```
sessionStorage.setItem("firstName","Jalever");
sessionStorage.getItem("lastName","Chen");

let firstName = sessionStorage.getItem("firstName");
console.log(firstName);
```

#### Browser Support
<table>
    <thead>
        <tr>
            <td>Property</td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/chrome.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/edge.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/firefox.png" /></td>
            <td><img src="https://github.com/Jalever/Note-taking/blob/master/images/safari.png" /></td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>sessionStorage</td>
            <td>4.0</td>
            <td>8.0</td>
            <td>3.5</td>
            <td>4.0</td>
        </tr>
    </tbody>
</table>
