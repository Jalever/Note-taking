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
    - [Object.create()](#objectcreate)
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
The <strong>Object.create()</strong> method creates a new object, using an existing object as the prototype of the newly created object.
![eEIj1O.png](https://s2.ax1x.com/2019/07/24/eEIj1O.png)

###### Syntax
![eEoF4P.png](https://s2.ax1x.com/2019/07/24/eEoF4P.png)

&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>proto</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object which should be the prototype of the newly-created object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>propertiesObject</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional. If specified and not `undefined`, an object whose enumerable own properties (that is, those properties defined upon itself and not enumerable properties along its prototype chain) specify property descriptors to be added to the newly-created object, with the corresponding property names. These properties correspond to the second argument of `Object.defineProperties()`.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A new object with the specified prototype object and properties.<br/>
&nbsp;&nbsp;<strong>Exceptions</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A `TypeError` exception if the `propertiesObject` parameter is `null` or a non-primitive-wrapper object.<br/>

###### Examples
&nbsp;&nbsp;<strong>Classical inheritance with Object.create()</strong><br/>
Below is an example of how to use <strong>Object.create()</strong> to achieve classical inheritance. This is for single inheritance, which is all that JavaScript supports.
![eEqFl6.png](https://s2.ax1x.com/2019/07/24/eEqFl6.png)
![eEqGnS.png](https://s2.ax1x.com/2019/07/24/eEqGnS.png)

`rect` take <strong>prototype.constructor</strong> of Shape
![eELZvV.png](https://s2.ax1x.com/2019/07/24/eELZvV.png)

set <strong>Object.prototype.constructor</strong> to Rectangle
![eEL3CR.png](https://s2.ax1x.com/2019/07/24/eEL3CR.png)

If you wish to inherit from multiple objects, then mixins are a possibility.
![eELUbD.png](https://s2.ax1x.com/2019/07/24/eELUbD.png)
<strong>Object.assign()</strong> copies properties from the <strong>OtherSuperClass</strong> prototype to the <strong>MyClass</strong> prototype, making them available to all instances of <strong>MyClass</strong>.

&nbsp;&nbsp;<strong>Using propertiesObject argument with Object.create()</strong><br/>
![eEj054.png](https://s2.ax1x.com/2019/07/24/eEj054.png)
![eEjs2R.png](https://s2.ax1x.com/2019/07/24/eEjs2R.png)
![eEjcKx.png](https://s2.ax1x.com/2019/07/24/eEjcKx.png)
![eEjWVO.png](https://s2.ax1x.com/2019/07/24/eEjWVO.png)
![eEjhIe.png](https://s2.ax1x.com/2019/07/24/eEjhIe.png)
![eEjIGd.png](https://s2.ax1x.com/2019/07/24/eEjIGd.png)
![eEjoRA.png](https://s2.ax1x.com/2019/07/24/eEjoRA.png)

###### Custom and Null objects
A new object created from a completely custom object (especially one created from the <strong>null</strong> object, which is basically a custom object with NO members) can behave in unexpected ways. This is especially true when debugging, since common object-property converting/detecting utility functions may generate errors, or simply lose information (especially if using silent error-traps that ignore errors). For example, here are two objects:
![eEzG2d.png](https://s2.ax1x.com/2019/07/24/eEzG2d.png)
As shown above, all seems normal so far. However, when attempting to actually use these objects, their differences quickly become apparent:
![eEzDPg.png](https://s2.ax1x.com/2019/07/24/eEzDPg.png)
Testing just a few of the many most basic built-in functions shows the magnitude of the problem more clearly:
![eVSSRH.png](https://s2.ax1x.com/2019/07/24/eVSSRH.png)
As said, these differences can make debugging even simple-seeming problems quickly go astray. For example:

A simple common debugging function:
![eVSPsI.png](https://s2.ax1x.com/2019/07/24/eVSPsI.png)
Not such simple results: (especially if silent error-trapping had hidden the error messages)
![eVS1e0.png](https://s2.ax1x.com/2019/07/24/eVS1e0.png)
(But if same object is created simply in different order -- at least in some implementations...)
![eVSwO1.png](https://s2.ax1x.com/2019/07/24/eVSwO1.png)
Note that such a different order may arise statically via disparate fixed codings such as here, but also dynamically via whatever the order any such property-adding code-branches actually get executed at runtime as depends on inputs and/or random-variables. Then again, the actual iteration order is not guaranteed no matter what the order members are added.

<strong>Some NON-solutions</strong><br/>
A good solution for the missing object-methods is not immediately apparent.

Adding the missing object-method directly from the standard-object does NOT work:
![eVSITf.png](https://s2.ax1x.com/2019/07/24/eVSITf.png)
Adding the missing object-method directly to new object's "prototype" does not work either, since new object does not have a real prototype (which is really the cause of ALL these problems) and one cannot be directly added:
![eVSqpQ.png](https://s2.ax1x.com/2019/07/24/eVSqpQ.png)
Adding the missing object-method by using the standard-object as new object's prototype does not work either:
![eVSx00.png](https://s2.ax1x.com/2019/07/24/eVSx00.png)

<strong>Some OK solutions</strong><br/>
Again, adding the missing object-method directly from the <strong>standard-object</strong> does NOT work. However, adding the <strong>generic</strong> method directly, DOES:
![eVp3jA.png](https://s2.ax1x.com/2019/07/24/eVp3jA.png)
However, setting the generic <strong>prototype</strong> as the new object's prototype works even better:
![eVpw9g.png](https://s2.ax1x.com/2019/07/24/eVpw9g.png)
(In addition to all the string-related functions shown above, this also adds:)
![eVpouR.png](https://s2.ax1x.com/2019/07/24/eVpouR.png)

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
