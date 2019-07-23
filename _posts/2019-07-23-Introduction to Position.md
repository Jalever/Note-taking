---
layout: post
title: CSS position Property
subtitle: CSS Properties
date: 2019-07-23
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---
- [Definition and Usage](#definition-and-usage)
- [Browser Support](#browser-support)
- [CSS Syntax](#css-syntax)
- [Property Values](#property-values)
            
## Definition and Usage
The <strong>position</strong> property specifies the type of positioning method used for an element (static, relative, absolute, fixed, or sticky).
![eFnwse.png](https://s2.ax1x.com/2019/07/23/eFnwse.png)

## Browser Support
The numbers in the table specify the first browser version that fully supports the property.
![eFnsII.png](https://s2.ax1x.com/2019/07/23/eFnsII.png)
> Note: The `sticky` value is not supported in Internet Explorer or Edge 15 and earlier versions.

## CSS Syntax
![eFncJP.png](https://s2.ax1x.com/2019/07/23/eFncJP.png)

## Property Values
<table>
    <thead>
        <tr>
            <td>Value</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>static</td>
            <td>Default value. Elements render in order, as they appear in the document flow</td>
        </tr>
        <tr>
            <td>absolute</td>
            <td>The element is positioned relative to its first positioned (not static) ancestor element</td>
        </tr>
        <tr>
            <td>fixed</td>
            <td>The element is positioned relative to the browser window</td>
        </tr>
        <tr>
            <td>relative</td>
            <td>The element is positioned relative to its normal position, so "left:20px" adds 20 pixels to the element's LEFT position</td>
        </tr>
        <tr>
            <td>sticky</td>
            <td>The element is positioned based on the user's scroll position<br/>A sticky element toggles between relative and fixed, depending on the scroll position. It is positioned relative until a given offset position is met in the viewport - then it "sticks" in place (like position:fixed).<br/>Note: Not supported in IE/Edge 15 or earlier. Supported in Safari from version 6.1 with a -webkit- prefix.</td>
        </tr>
        <tr>
            <td>initial</td>
            <td>Sets this property to its default value.</td>
        </tr>
        <tr>
            <td>inherit</td>
            <td>Inherits this property from its parent element.</td>
        </tr>
    </tbody>
</table>
