---
layout: post
title: Inheritance and the Prototype Chain
subtitle: Web Development
date: 2019-06-17
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---
## Overview

<strong>JavaScript</strong> is a bit confusing for developers experienced in class-based languages (like <strong>Java</strong> or <strong>C++</strong>), as it is dynamic and does not provide a class implementation per se (the <strong>class</strong> keyword is introduced in ES2015, but is syntactical sugar, <strong>JavaScript</strong> remains prototype-based).

When it comes to inheritance, <strong>JavaScript</strong> only has one construct: objects. Each object has a private property which holds a link to another object called its `prototype`. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. By definition, null has no prototype, and acts as the final link in this `prototype chain`.

Nearly all objects in <strong>JavaScript</strong> are instances of <strong>Object</strong> which sits on the top of a prototype chain.

While this confusion is often considered to be one of <strong>JavaScript</strong>'s weaknesses, the prototypal inheritance model itself is, in fact, more powerful than the classic model. It is, for example, fairly trivial to build a classic model on top of a prototypal model.

[![V75w5T.md.png](https://s2.ax1x.com/2019/06/17/V75w5T.md.png)](https://imgchr.com/i/V75w5T)

## Inheritance with the prototype chain
#### Inheriting Properties
JavaScript objects are dynamic "bags" of properties (referred to as own properties). JavaScript objects have a link to a prototype object. When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.

Here is what happens when trying to access a property:



#### Inheriting Methods
