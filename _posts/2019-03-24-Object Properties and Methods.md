---
layout: post
title: Object Properties and Methods
subtitle: Javascript Standard Built-in Object
date: 2019-03-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---

- [Overview](#overview)
- [Syntax](#syntax)
- [Description](#description)
- [Properties of the Object constructor](#properties-of-the-object-constructor)
    - [Object.length](#objectlength)
    - [Object.prototype](#objectprototype)
- [Methods of the Object constructor](#methods-of-the-object-constructor)
    - [Object.assign()](#objectassign)
    - [Object.create()](#object.create())
    - [Object.defineProperty()](#objectdefineproperty)
    - [Object.defineProperties()](#objectdefineproperties)
    - [Object.entries()](#object.entries)
    - [Object.freeze()](#object.freeze)
    - [Object.fromEntries()](#objectfromentries)
    - [Object.getOwnPropertyDescriptor()](#objectgetownpropertydescriptor)
    - [Object.getOwnPropertyDescriptors()](#objectgetownpropertydescriptors)
    - [Object.getOwnPropertyNames()](#objectgetOwnPropertyNames)
    - [Object.getOwnPropertySymbols()](#objectgetOwnPropertySymbols)
    - [Object.getPrototypeOf()](#objectgetprototypeof)
    - [Object.is()](#objectis)
    - [Object.isExtensible()](#objectisextensible)
    - [Object.isFrozen()](#objectisfrozen)
    - [Object.isSealed()](#objectissealed)
    - [Object.keys()](#objectkeys)
    - [Object.preventExtensions()](#objectpreventextensions)
    - [Object.seal()](#objectseal)
    - [Object.setPrototypeOf()](#objectsetprototypeof)
    - [Object.values()](#objectvalues)
- [Object instances and Object prototype object](#object-instances-and-object-prototype-object)
    - [Properties](#properties)
        - [Object.prototype.constructor](#objectprototypeconstructor)
    - [Methods](#methods)
        - [Object.prototype.hasOwnProperty()](#objectprototypehasownproperty)
        - [Object.prototype.isPrototypeOf()](#objectprototypeisprototypeof)
        - [Object.prototype.propertyIsEnumerable()](#objectprototypepropertyisenumerable)
        - [Object.prototype.toLocaleString()](#objectprototypetolocalestring)
        - [Object.prototype.toString()](#objectprototypetostring)
        - [Object.prototype.valueOf()](#objectprototypevalueof)

## Overview
The <strong>Object</strong> constructor creates an object wrapper.

## Syntax
![eAFVdx.png](https://s2.ax1x.com/2019/07/23/eAFVdx.png)

#### Parameters
###### nameValuePair1, nameValuePair2, ... nameValuePairN
Pairs of names (strings) and values (any value) where the name is separated from the value by a colon.

###### value
Any value.

## Description
The <strong>Object</strong> constructor creates an object wrapper for the given value. If the value is <strong>null</strong> or <strong>undefined</strong>, it will create and return an empty object, otherwise, it will return an object of a Type that corresponds to the given value. If the value is an object already, it will return the value.

When called in a non-constructor context, <strong>Object</strong> behaves identically to <strong>new Object()</strong>.

## Properties of the Object constructor
#### Object.length
Has a value of 1.

#### Object.prototype
The <strong>Object.prototype</strong> is a property of the <strong>Object</strong> constructor. It is also the end of a prototype chain.
![eAFVdx.png](https://s2.ax1x.com/2019/07/23/eAFVdx.png)

## Methods of the Object constructor
#### Object.assign()
The <strong>Object.assign()</strong> method is used to copy the values of all enumerable own properties from one or more source objects to a target object. It will return the target object.
![eAePSK.png](https://s2.ax1x.com/2019/07/23/eAePSK.png)

###### Syntax
![eAel6S.png](https://s2.ax1x.com/2019/07/23/eAel6S.png)

&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>target</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The target object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>sources</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The source object(s).<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>The target object.</strong><br/>

###### Description
Properties in the target object will be overwritten by properties in the sources if they have the same key. Later sources' properties will similarly overwrite earlier ones.

The <strong>Object.assign()</strong> method only copies enumerable and own properties from a source object to a target object. It uses <strong>[&#91;Get&#93;]</strong> on the source and <strong>[&#91;Set&#93;]</strong> on the target, so it will invoke getters and setters. Therefore it assigns properties versus just copying or defining new properties. This may make it unsuitable for merging new properties into a prototype if the merge sources contain getters. For copying property definitions, including their enumerability, into prototypes <strong>Object.getOwnPropertyDescriptor()</strong> and <strong>Object.defineProperty()</strong> should be used instead.

Both <strong>String</strong> and <strong>Symbol</strong> properties are copied.

In case of an error, for example if a property is non-writable, a <strong>TypeError</strong> will be raised, and the <strong>target</strong> object can be changed if any properties are added before error is raised.

Note that <strong>Object.assign()</strong> does not throw on <strong>null</strong> or <strong>undefined</strong> source values.

###### Examples
<strong>Cloning an object</strong><br/>
![eAmsv8.png](https://s2.ax1x.com/2019/07/23/eAmsv8.png)

<strong>Warning for Deep Clone</strong><br/>
For deep cloning, we need to use other alternatives because <strong>Object.assign()</strong> copies property values. If the source value is a reference to an object, it only copies that reference value.
![eAmf5n.png](https://s2.ax1x.com/2019/07/23/eAmf5n.png)

<strong>Merging objects</strong><br/>
![eAm580.png](https://s2.ax1x.com/2019/07/23/eAm580.png)

<strong>Merging objects with same properties</strong><br/>
![eAm7KU.png](https://s2.ax1x.com/2019/07/23/eAm7KU.png)
The properties are overwritten by other objects that have the same properties later in the parameters order.

<strong>Copying symbol-typed properties</strong><br/>
![eAmvP1.png](https://s2.ax1x.com/2019/07/23/eAmvP1.png)

<strong>Properties on the prototype chain and non-enumerable properties cannot be copied</strong><br/>
![eAnmxf.png](https://s2.ax1x.com/2019/07/23/eAnmxf.png)

<strong>Primitives will be wrapped to objects</strong></strong><br/>
![eAn1aj.png](https://s2.ax1x.com/2019/07/23/eAn1aj.png)

<strong>Exceptions will interrupt the ongoing copying task</strong></strong><br/>
![eAnsiR.png](https://s2.ax1x.com/2019/07/23/eAnsiR.png)

<strong>Copying accessors</strong></strong><br/>
![eAuckj.png](https://s2.ax1x.com/2019/07/23/eAuckj.png)
![eAuf10.png](https://s2.ax1x.com/2019/07/23/eAuf10.png)

#### Object.create()
Creates a new object with the specified prototype object and properties.

#### Object.defineProperty()
Adds the named property described by a given descriptor to an object.

#### Object.defineProperties()
Adds the named properties described by the given descriptors to an object.

#### Object.entries()
Returns an array containing all of the [key, value] pairs of a given object's own enumerable string properties.

#### Object.freeze()
Freezes an object: other code can't delete or change any properties.

#### Object.fromEntries()
Returns a new object from an iterable of key-value pairs (reverses Object.entries).

#### Object.getOwnPropertyDescriptor()
Returns a property descriptor for a named property on an object.

#### Object.getOwnPropertyDescriptors()
Returns an object containing all own property descriptors for an object.

#### Object.getOwnPropertyNames()
Returns an array containing the names of all of the given object's own enumerable and non-enumerable properties.

#### Object.getOwnPropertySymbols()
Returns an array of all symbol properties found directly upon a given object.

#### Object.getPrototypeOf()
Returns the prototype of the specified object.

#### Object.is()
Compares if two values are the same value. Equates all NaN values (which differs from both Abstract Equality Comparison and Strict Equality Comparison).

#### Object.isExtensible()
Determines if extending of an object is allowed.

#### Object.isFrozen()
Determines if an object was frozen.

#### Object.isSealed()
Determines if an object is sealed.

#### Object.keys()
Returns an array containing the names of all of the given object's own enumerable string properties.

#### Object.preventExtensions()
Prevents any extensions of an object.

#### Object.seal()
Prevents other code from deleting properties of an object.

#### Object.setPrototypeOf()
Sets the prototype (i.e., the internal [[Prototype]] property).

#### Object.values()
Returns an array containing the values that correspond to all of a given object's own enumerable string properties.

## Object instances and Object prototype object
All objects in JavaScript are descended from <strong>Object</strong>; all objects inherit methods and properties from <strong>Object.prototype</strong>, although they may be overridden. For example, other constructors' prototypes override the <strong>constructor</strong> property and provide their own <strong>toString()</strong> methods. Changes to the <strong>Object</strong> prototype object are propagated to all objects unless the properties and methods subject to those changes are overridden further along the prototype chain.


#### Properties
###### Object.prototype.constructor
Specifies the function that creates an object's prototype.

#### Methods
###### Object.prototype.hasOwnProperty()
Returns a boolean indicating whether an object contains the specified property as a direct property of that object and not inherited through the prototype chain.

###### Object.prototype.isPrototypeOf()
Returns a boolean indicating whether the object this method is called upon is in the prototype chain of the specified object.

###### Object.prototype.propertyIsEnumerable()
Returns a boolean indicating if the internal ECMAScript [[Enumerable]] attribute is set.

###### Object.prototype.toLocaleString()
Calls toString().

###### Object.prototype.toString()
Returns a string representation of the object.

###### Object.prototype.valueOf()
Returns the primitive value of the specified object.
