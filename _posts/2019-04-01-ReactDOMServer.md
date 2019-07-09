---
layout: post
title: ReactDOMServer
subtitle: React API Reference
date: 2019-04-01
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

The `ReactDOMServer` object enables you to render components to static markup. Typically, it’s used on a **_Node server_**:

- [Overview](#overview)
    - [renderToString()](#rendertostring)
    - [renderToStaticMarkup()](#rendertostaticmarkup)
    - [renderToNodeStream()](#rendertonodestream)
    - [renderToStaticNodeStream()](#rendertostaticnodestream)

## Overview

The following methods can be used in both the `server` and `browser` environments:

#### renderToString()

```javascript
ReactDOMServer.renderToString(element);
```

Render a `React` element to its initial HTML.<br>
`React` will return an HTML string.<br>
You can use this method to generate `HTML` on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for SEO purposes.<br>
If you call `ReactDOM.hydrate()` on a node that already has this server-rendered markup, React will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.

#### renderToStaticMarkup()

```javascript
ReactDOMServer.renderToStaticMarkup(element);
```

Similar to `renderToString`, except this doesn’t create extra `DOM` attributes that `React` uses internally, such as `data-reactroot`.<br>
This is useful if you want to use `React` as a simple static page generator, as stripping away the extra attributes can save some bytes.<br>
If you plan to use `React` on the client to make the markup interactive, do not use this method. Instead, use `renderToString` on the server and `ReactDOM.hydrate()` on the client.

These additional methods depend on a package (stream) that is only available on the **_server_**, and won’t work in the browser.

#### renderToNodeStream()

```javascript
ReactDOMServer.renderToNodeStream(element);
```

Render a `React` element to its initial `HTML`.<br>
Returns a `Readable stream` that outputs an `HTML` string.<br>
The `HTML` output by this stream is exactly equal to what `ReactDOMServer.renderToString` would return.<br>
You can use this method to generate `HTML` on the server and send the markup down on the initial request for faster page loads and to allow search engines to crawl your pages for `SEO` purposes.<br>
If you call `ReactDOM.hydrate()` on a node that already has this server-rendered markup, `React` will preserve it and only attach event handlers, allowing you to have a very performant first-load experience.<br>
The stream returned from this method will return a byte stream encoded in `utf-8`.<br>

> Server-only

#### renderToStaticNodeStream()

Similar to `renderToNodeStream`, except this doesn’t create extra `DOM` attributes that `React` uses internally, such as `data-reactroot`. <br>
This is useful if you want to use `React` as a simple static page generator, as stripping away the extra attributes can save some bytes.<br>
The `HTML` output by this stream is exactly equal to what `ReactDOMServer.renderToStaticMarkup` would return.<br>
If you plan to use `React` on the client to make the markup interactive, do not use this method. Instead, use `renderToNodeStream` on the server and `ReactDOM.hydrate()` on the client.<br>
The stream returned from this method will return a byte stream encoded in `utf-8`.<br>

> Server-only
