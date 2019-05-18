---
layout:     post
title:      AMD, CommonJS and UMD
subtitle:   Web Development学习笔记系列
date:       2019-05-18
author:     Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - Web Development
---


## AMD ( Asynchronous Module Definition )
Here’s module `foo` with a single dependency on `jquery`:
```js
//    filename: foo.js
define(['jquery'], function ($) {
    //    methods
    function myFunc(){};

    //    exposed public methods
    return myFunc;
});
```

And a little more complicated example with multiple dependencies and multiple exposed methods:
```js
//    filename: foo.js
define(['jquery', 'underscore'], function ($, _) {
    //    methods
    function a(){};    //    private because it's not returned (see below)
    function b(){};    //    public because it's returned
    function c(){};    //    public because it's returned

    //    exposed public methods
    return {
        b: b,
        c: c
    }
});
```



## CommonJS
`CommonJS` is a style you may be familiar with if you’re written anything in `Node` (which uses a slight variant).
```js
//    filename: foo.js

//    dependencies
var $ = require('jquery');

//    methods
function myFunc(){};

//    exposed public method (single)
module.exports = myFunc;

```

And our more complicate example, with multiple dependencies and multiple exposed methods:
```js
//    filename: foo.js
var $ = require('jquery');
var _ = require('underscore');

//    methods
function a(){};    //    private because it's omitted from module.exports (see below)
function b(){};    //    public because it's defined in module.exports
function c(){};    //    public because it's defined in module.exports

//    exposed public methods
module.exports = {
    b: b,
    c: c
};
```


## UMD ( Universal Module Definition )
Since `CommonJS` and `AMD` styles have both been equally popular, it seems there’s yet no consensus.<br/>
This has brought about the push for a “universal” pattern that supports both styles, which brings us to none other than the `Universal Module Definition`.
```js
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], factory);
    } else if (typeof exports === 'object') {
        // Node, CommonJS-like
        module.exports = factory(require('jquery'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.jQuery);
    }
}(this, function ($) {
    //    methods
    function myFunc(){};

    //    exposed public method
    return myFunc;
}));
```
