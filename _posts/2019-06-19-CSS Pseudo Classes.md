---
layout: post
title: CSS Pseudo Classes
subtitle: CSS
date: 2019-06-19
author: Jalever
header-img: img/css_bg_simple.png
catalog: true
tags:
  - CSS
---

## Anchor Pseudo Classes
<table>
    <thead>
        <tr>
            <td>Name</td>
            <td>:link</td>
            <td>:visited</td>
            <td>:hover</td>
            <td>:active</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Result</td>
            <td>unvisited link</td>
            <td>visited link</td>
            <td>mouse over link</td>
            <td>selected link</td>
        </tr>
    </tbody>
</table>

## All CSS Pseudo Classes
<table>
    <thead>
        <tr>
            <td>Selector</td>
            <td>Example</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>:link</td>
            <td>a:link</td>
            <td>Selects all unvisited links</td>
        </tr>
        <tr>
            <td>:visited</td>
            <td>a:visited</td>
            <td>Selects all visited links</td>
        </tr>
        <tr>
            <td>:hover</td>
            <td>a:hover</td>
            <td>Selects links on mouse over</td>
        </tr>
        <tr>
            <td>:active</td>
            <td>a:active</td>
            <td>Selects the active link</td>
        </tr>
        <tr>
            <td colspan="3"></td>
        </tr>
        <tr>
            <td>:first-child</td>
            <td>p:first-child</td>
            <td>Selects every &#60;p&#62; elements that is the first child of its parent</td>
        </tr>
        <tr>
            <td>:nth-child(n)</td>
            <td>p:nth-child(2)</td>
            <td>Selects every &#60;p&#62; element that is the second child of its parent</td>
        </tr>
        <tr>
            <td>:last-child</td>
            <td>p:last-child</td>
            <td>Selects every &#60;p&#62; elements that is the last child of its parent</td>
        </tr>
        <tr>
            <td>:nth-last-child(n)</td>
            <td>p:nth-last-child(2)</td>
            <td>Selects every &#60;p&#62; element that is the second child of its parent, counting from the last child</td>
        </tr>
        <tr>
            <td colspan="3"></td>
        </tr>
        <tr>
            <td>:first-of-type</td>
            <td>p:first-of-type</td>
            <td>Selects every &#60;p&#62; element that is the first &#60;p&#62; element of its parent</td>
        </tr>
        <tr>
            <td>:nth-of-type(n)</td>
            <td>p:nth-of-type(2)</td>
            <td>Selects every &#60;p&#62; element that is the second &#60;p&#62; element of its parent</td>
        </tr>
        <tr>
            <td>:last-of-type</td>
            <td>p:last-of-type</td>
            <td>Selects every &#60;p&#62; element that is the last &#60;p&#62; element of its parent</td>
        </tr>
        <tr>
            <td>:nth-last-of-type(n)</td>
            <td>p:nth-last-of-type(2)</td>
            <td>Selects every &#60;p&#62; element that is the second &#60;p&#62; element of its parent, counting from the last child</td>
        </tr>
        <tr>
            <td>:only-of-type</td>
            <td>p:only-of-type</td>
            <td>Selects every &#60;p&#62; element that is the only &#60;p&#62; element of its parent</td>
        </tr>

    </tbody>
</table>
