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

<strong>Primitives will be wrapped to objects</strong><br/>
![eAn1aj.png](https://s2.ax1x.com/2019/07/23/eAn1aj.png)

<strong>Exceptions will interrupt the ongoing copying task</strong><br/>
![eQnrmd.png](https://s2.ax1x.com/2019/07/28/eQnrmd.png)
![eQns0A.png](https://s2.ax1x.com/2019/07/28/eQns0A.png)

<strong>Copying accessors</strong><br/>
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
The static method <strong>Object.defineProperty()</strong> defines a new property directly on an object, or modifies an existing property on an object, and returns the object.
> You call this method directly on the `Object` constructor rather than on an instance of type `Object`.

![eVgCIU.png](https://s2.ax1x.com/2019/07/24/eVgCIU.png)
- Syntax
- Description
- Examples
    - Creating a property
    - Modifying a property
        - Writable attribute
        - Enumerable attribute
        - Configurable attribute
    - Adding properties and default values
    - Custom Setters and Getters
    - Custom Setters and Getters

###### Syntax
![eVglJe.png](https://s2.ax1x.com/2019/07/24/eVglJe.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;obj<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object on which to define the property.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;prop<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The name or `Symbol` of the property to be defined or modified.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;descriptor<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The descriptor for the property being defined or modified.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The object that was passed to the function.<br/>

###### Description
This method allows a precise addition to or modification of a property on an object. <strong>Normal property addition through assignment</strong> creates properties which show up during property enumeration (`for...in` loop or `Object.keys` method), whose values may be <ins>changed</ins>, and which may be <ins>deleted</ins>. This method allows these extra details to be changed from their defaults. By default, values added using <strong>Object.defineProperty()</strong> are immutable.

Property descriptors present in objects come in two main flavors: <strong>Data Descriptors</strong> and <strong>Accessor Descriptors</strong>. A <ins>data descriptor</ins> is a property that has a value, which may or may not be writable. An <ins>accessor descriptor</ins> is a property described by a getter-setter pair of functions. A descriptor must be one of these two flavors; it cannot be both.

Both data and accessor descriptors are <strong>object</strong>s. They share the following optional keys(The default value is in the case of defining properties using <strong>Object.defineProperty&#40;&#41;</strong>):

&nbsp;&nbsp;<b>configurable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- `true` if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `false`.<br/>
&nbsp;&nbsp;<b>enumerable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- `true` if and only if this property shows up during enumeration of the properties on the corresponding object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `false`.<br/>

A data descriptor also has the following optional keys:

&nbsp;&nbsp;<b>value</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- The value associated with the property. Can be any valid JavaScript value (number, object, function, etc).<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `undefined`.<br/>
&nbsp;&nbsp;<b>writable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- true if and only if the value associated with the property may be changed with an assignment operator.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `false`.<br/>

An accessor descriptor also has the following optional keys:

&nbsp;&nbsp;<b>get</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- A function which serves as a getter for the property, or `undefined` if there is no getter. When the property is accessed, this function is called without arguments and with `this` set to the object through which the property is accessed (this may not be the object on which the property is defined due to inheritance). The return value will be used as the value of the property.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `undefined`.<br/>
&nbsp;&nbsp;<b>set</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;- A function which serves as a setter for the property, or `undefined` if there is no setter. When the property is assigned to, this function is called with one argument (the value being assigned to the property) and with `this` set to the object through which the property is assigned.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;- Defaults to `undefined`.<br/>

If a descriptor has neither of `value`, `writable`, `get` and `set` keys, it is treated as a data descriptor. If a descriptor has both `value` or `writable` and `get` or `set` keys, an exception is thrown.
![eVdrHH.png](https://s2.ax1x.com/2019/07/24/eVdrHH.png)

Bear in mind that these attributes are not necessarily the descriptor's own properties. Inherited properties will be considered as well. In order to ensure these defaults are preserved, you might freeze the <strong>Object.prototype</strong> upfront, specify all options explicitly, or point to null with <strong>Object.create(null)</strong>.
![eVfAk6.png](https://s2.ax1x.com/2019/07/24/eVfAk6.png)
![eVfEtK.png](https://s2.ax1x.com/2019/07/24/eVfEtK.png)
![eVfVfO.png](https://s2.ax1x.com/2019/07/24/eVfVfO.png)
![eVfepD.png](https://s2.ax1x.com/2019/07/24/eVfepD.png)

###### Examples
<strong>Creating a property</strong><br/>
When the property specified doesn't exist in the object, <strong>Object.defineProperty()</strong> creates a new property as described. Fields may be omitted from the descriptor, and default values for those fields are inputted.
![eVhLGT.png](https://s2.ax1x.com/2019/07/24/eVhLGT.png)
![eVhvM4.png](https://s2.ax1x.com/2019/07/24/eVhvM4.png)
![eVhxsJ.png](https://s2.ax1x.com/2019/07/24/eVhxsJ.png)
![eVhzL9.png](https://s2.ax1x.com/2019/07/24/eVhzL9.png)

<strong>Modifying a property</strong><br/>
When the property already exists, `Object.defineProperty()` attempts to modify the property according to the values in the descriptor and the object's current configuration. If the old descriptor had its `configurable` attribute set to `false` the property is said to be “non-configurable”. It is not possible to change any attribute of a non-configurable accessor property. For data properties, it is possible to modify the value if the property is writable, and it is possible to change `writable` attribute from `true` to `false`. It is not possible to switch between data and accessor property types when the property is non-configurable.

A `TypeError` is thrown when attempts are made to change non-configurable property attributes (except `value` and `writable`, if permitted) unless the current and new values are the same.

1.Writable attribute<br/>
When the `writable` property attribute is set to `false`, the property is said to be “non-writable”. It cannot be reassigned.
![eQK7WV.png](https://s2.ax1x.com/2019/07/28/eQK7WV.png)
![eQKHzT.png](https://s2.ax1x.com/2019/07/28/eQKHzT.png)
As seen in the example, trying to write into the non-writable property doesn't change it but doesn't throw an error either.

2.Enumerable attribute<br/>
The `enumerable` property attribute defines whether the property is picked by `Object.assign()` or `spread` operator. For non-`Symbols` properties it also defines whether it shows up in a `for...in` loop and `Object.keys()` or not.
![eQMNYq.png](https://s2.ax1x.com/2019/07/28/eQMNYq.png)
![eQMUf0.png](https://s2.ax1x.com/2019/07/28/eQMUf0.png)
![eQMdpV.png](https://s2.ax1x.com/2019/07/28/eQMdpV.png)
![eQMwlT.png](https://s2.ax1x.com/2019/07/28/eQMwlT.png)

3.Configurable attribute<br/>
The `configurable` attribute controls at the same time whether the property can be deleted from the object and whether its attributes (other than `value` and `writable`) can be changed.
![eQMvjS.png](https://s2.ax1x.com/2019/07/28/eQMvjS.png)
![eQQp7j.png](https://s2.ax1x.com/2019/07/28/eQQp7j.png)
If the `configurable` attribute of `o.a` had been `true`, none of the errors would be thrown and the property would be deleted at the end.

<strong>Adding properties and default values</strong><br/>
It is important to consider the way default values of attributes are applied. There is often a difference between simply using dot notation to assign a value and using `Object.defineProperty()`, as shown in the example below.
![eQQ4Cq.png](https://s2.ax1x.com/2019/07/28/eQQ4Cq.png)
![eQQ580.png](https://s2.ax1x.com/2019/07/28/eQQ580.png)
![eQQovT.png](https://s2.ax1x.com/2019/07/28/eQQovT.png)

<strong>Custom Setters and Getters</strong><br/>
The example below shows how to implement a self-archiving object. When `temperature` property is set, the `archive` array gets a log entry.
![eQluM8.png](https://s2.ax1x.com/2019/07/28/eQluM8.png)
![eQlKsS.png](https://s2.ax1x.com/2019/07/28/eQlKsS.png)
In this example, a getter always returns the same value.
![eQl1aj.png](https://s2.ax1x.com/2019/07/28/eQl1aj.png)

<strong>Custom Setters and Getters</strong><br/>
If an accessor property is inherited, its `get` and `set` methods will be called when the property is accessed and modified on descendant objects. If these methods use a variable to store the value, this value will be shared by all objects.
![eQ1UfI.png](https://s2.ax1x.com/2019/07/28/eQ1UfI.png)
This can be fixed by storing the value in another property. In `get` and `set` methods, `this` points to the object which is used to access or modify the property.
![eQ1y7Q.png](https://s2.ax1x.com/2019/07/28/eQ1y7Q.png)
Unlike accessor properties, value properties are always set on the object itself, not on a prototype. However, if a non-writable value property is inherited, it still prevents from modifying the property on the object.
![eQ1hcV.png](https://s2.ax1x.com/2019/07/28/eQ1hcV.png)







#### Object.defineProperties()
The <strong>Object.defineProperties()</strong> method defines new or modifies existing properties directly on an object, returning the object.
![eVJrH1.png](https://s2.ax1x.com/2019/07/24/eVJrH1.png)

###### Syntax
![eVtg6e.png](https://s2.ax1x.com/2019/07/24/eVtg6e.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object on which to define or modify properties.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>props</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;An object whose keys represent the names of properties to be defined or modified and whose values are objects describing those properties. Each value in `props` must be either a data descriptor or an accessor descriptor; it cannot be both (see `Object.defineProperty()` for more details).<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Data descriptors and accessor descriptors may optionally contain the following keys:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>configurable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`true` if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `false`.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>enumerable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`true` if and only if this property shows up during enumeration of the properties on the corresponding object.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `false`.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A data descriptor also has the following optional keys:<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>value</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The value associated with the property. Can be any valid JavaScript value (number, object, function, etc).<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `undefined`.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>writable</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`true` if and only if the value associated with the property may be changed with an assignment operator.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `false`.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;An accessor descriptor also has the following optional keys:<br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>get</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A function which serves as a getter for the property, or `undefined` if there is no getter. The function's return value will be used as the value of the property.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `undefined`.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>set</b><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A function which serves as a setter for the property, or `undefined` if there is no setter. The function will receive as its only argument the new value being assigned to the property.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Defaults to `undefined`.<br/>

If a descriptor has neither of `value`, `writable`, `get` and `set` keys, it is treated as a data descriptor. If a descriptor has both `value` or `writable` and `get` or `set` keys, an exception is thrown.
![eVdrHH.png](https://s2.ax1x.com/2019/07/24/eVdrHH.png)

&nbsp;&nbsp;<strong>Return value</strong><br/>
The object that was passed to the function.

###### Description
<strong>Object.defineProperties</strong>, in essence, defines all properties corresponding to the enumerable own properties of <strong>props</strong> on the object <strong>obj</strong> object.

###### Example
![eVdMcT.png](https://s2.ax1x.com/2019/07/24/eVdMcT.png)

#### Object.entries()
The `Object.entries()` method returns an array of a given object's own enumerable string-keyed property `[key, value]` pairs, in the same order as that provided by a `for...in` loop (the difference being that a for-in loop enumerates properties in the prototype chain as well). The order of the array returned by <strong>Object.entries()</strong> does not depend on how an object is defined. If there is a need for certain ordering then the array should be sorted first like `Object.entries(obj).sort((a, b) => b[0].localeCompare(a[0]))`;.
![e1Tm5V.png](https://s2.ax1x.com/2019/07/29/e1Tm5V.png)

###### Syntax
![e1TQv4.png](https://s2.ax1x.com/2019/07/29/e1TQv4.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object whose own enumerable string-keyed property `[key, value]` pairs are to be returned.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;An array of the given object's own enumerable string-keyed property `[key, value]` pairs.<br/>

###### Description
`Object.entries()` returns an array whose elements are arrays corresponding to the enumerable string-keyed property `[key, value]` pairs found directly upon `object`. The ordering of the properties is the same as that given by looping over the property values of the object manually.

###### Examples
![e1TDrd.png](https://s2.ax1x.com/2019/07/29/e1TDrd.png)
![e1TrqA.png](https://s2.ax1x.com/2019/07/29/e1TrqA.png)
![e1TyVI.png](https://s2.ax1x.com/2019/07/29/e1TyVI.png)
![e1T6at.png](https://s2.ax1x.com/2019/07/29/e1T6at.png)
![e1T2Pf.png](https://s2.ax1x.com/2019/07/29/e1T2Pf.png)
![e1TWRS.png](https://s2.ax1x.com/2019/07/29/e1TWRS.png)
![e1Tfxg.png](https://s2.ax1x.com/2019/07/29/e1Tfxg.png)
![e1T4MQ.png](https://s2.ax1x.com/2019/07/29/e1T4MQ.png)

<strong>Converting an Object to a Map</strong><br/>
The `new Map()` constructor accepts an iterable of `entries`. With `Object.entries`, you can easily convert from `Object` to `Map`:
![e1TLGT.png](https://s2.ax1x.com/2019/07/29/e1TLGT.png)

<strong>Iterating through an Object</strong><br/>
Using `Array Destructuring`, you can iterate through objects easily.
![e1TvM4.png](https://s2.ax1x.com/2019/07/29/e1TvM4.png)

#### Object.freeze()
The `Object.freeze()` method <strong>freezes</strong> an object. A frozen object can no longer be changed; freezing an object prevents new properties from being added to it, existing properties from being removed, prevents changing the enumerability, configurability, or writability of existing properties, and prevents the values of existing properties from being changed. In addition, freezing an object also prevents its prototype from being changed. `freeze()` returns the same object that was passed in.
![e1H8tx.png](https://s2.ax1x.com/2019/07/29/e1H8tx.png)

###### Syntax
![e1Ht1O.png](https://s2.ax1x.com/2019/07/29/e1Ht1O.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object to freeze.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The object that was passed to the function.<br/>

###### Description
Nothing can be added to or removed from the properties set of a frozen object. Any attempt to do so will fail, either silently or by throwing a `TypeError` exception (most commonly, but not exclusively, when in strict mode).

For data properties of a frozen object, values cannot be changed, the writable and configurable attributes are set to false. Accessor properties (getters and setters) work the same (and still give the illusion that you are changing the value). Note that values that are objects can still be modified, unless they are also frozen. As an object, an array can be frozen; after doing so, its elements cannot be altered and no elements can be added to or removed from the array.

`freeze()` returns the same object that was passed into the function. It does not create a frozen copy.

###### Examples
<strong>Freezing objects</strong><br/>
![e1qhYq.png](https://s2.ax1x.com/2019/07/29/e1qhYq.png)
![e1q7XF.png](https://s2.ax1x.com/2019/07/29/e1q7XF.png)

<strong>Freezing arrays</strong><br/>
![e1L3As.png](https://s2.ax1x.com/2019/07/29/e1L3As.png)
The object being frozen is immutable. However, it is not necessarily constant. The following example shows that a frozen object is not constant (freeze is shallow).
![e1LzUs.png](https://s2.ax1x.com/2019/07/29/e1LzUs.png)
To be a constant object, the entire reference graph (direct and indirect references to other objects) must reference only immutable frozen objects. The object being frozen is said to be immutable because the entire object state (values and references to other objects) within the whole object is fixed. Note that strings, numbers, and booleans are always immutable and that Functions and Arrays are objects.

1.What is "shallow freeze"?<br/>
The result of calling `Object.freeze(object)` only applies to the immediate properties of `object` itself and will prevent future property addition, removal or value re-assignment operations only on `object`. If the value of those properties are objects themselves, those objects are not frozen and may be the target of property addition, removal or value re-assignment operations.
![e1XkWt.png](https://s2.ax1x.com/2019/07/29/e1XkWt.png)
To make an object immutable, recursively freeze each property which is of type object (deep freeze). Use the pattern on a case-by-case basis based on your design when you know the object contains no Cycles in the reference graph, otherwise an endless loop will be triggered. An enhancement to `deepFreeze()` would be to have an internal function that receives a path (e.g. an Array) argument so you can suppress calling `deepFreeze()` recursively when an object is in the process of being made immutable. You still run a risk of freezing an object that shouldn't be frozen, such as [window].
![e1XYOU.png](https://s2.ax1x.com/2019/07/29/e1XYOU.png)
![e1XUw4.png](https://s2.ax1x.com/2019/07/29/e1XUw4.png)

###### Usage notes
In ES5, if the argument to this method is not an object (a primitive), then it will cause a `TypeError`. In ES2015, a non-object argument will be treated as if it were a frozen ordinary object, and be simply returned.
![e1Xo1P.png](https://s2.ax1x.com/2019/07/29/e1Xo1P.png)

<strong>Comparison to Object.seal()</strong><br/>
Objects sealed with `Object.seal()` can have their existing properties changed. Existing properties in objects frozen with `Object.freeze()` are made immutable.

#### Object.fromEntries()
The `Object.fromEntries()` method transforms a list of key-value pairs into an object.
![e1jdu8.png](https://s2.ax1x.com/2019/07/29/e1jdu8.png)

###### Syntax
![e1jwDS.png](https://s2.ax1x.com/2019/07/29/e1jwDS.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>iterable</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;An iterable such as Array or Map or other objects implementing the iterable protocol.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A new object whose properties are given by the entries of the iterable.<br/>

###### Description
The `Object.fromEntries()` method takes a list of key-value pairs and returns a new object whose properties are given by those entries. The iterable argument is expected to be an object that implements an `@@iterator` method, that returns an iterator object, that produces a two element array-like object, whose first element is a value that will be used as a property key, and whose second element is the value to associate with that property key.

`Object.fromEntries()` performs the reverse of `Object.entries()`.

###### Examples
<strong>Converting a Map to an Object</strong><br/>
With `Object.fromEntries`, you can convert from `Map` to `Object`:
![e1jH81.png](https://s2.ax1x.com/2019/07/29/e1jH81.png)

<strong>Converting an Array to an Object</strong><br/>
With `Object.fromEntries`, you can convert from `Array` to `Object`:
![e1vuPs.png](https://s2.ax1x.com/2019/07/29/e1vuPs.png)

<strong>Object transformations</strong><br/>
With `Object.fromEntries`, its reverse method `Object.entries()`, and Array Manipulation Methods, you are able to transform objects like this:
![e1vUi9.png](https://s2.ax1x.com/2019/07/29/e1vUi9.png)

#### Object.getOwnPropertyDescriptor()
The `Object.getOwnPropertyDescriptor()` method returns a property descriptor for an own property (that is, one directly present on an object and not in the object's prototype chain) of a given object.
![eQ8asf.png](https://s2.ax1x.com/2019/07/28/eQ8asf.png)

###### Syntax
![eQ8czq.png](https://s2.ax1x.com/2019/07/28/eQ8czq.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object in which to look for the property.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>prop</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The name or Symbol of the property whose description is to be retrieved.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A property descriptor of the given property if it exists on the object, undefined otherwise.<br/>

###### Description
This method permits examination of the precise description of a property. A property in JavaScript consists of either a string-valued name or a `Symbol` and a property descriptor.

A property descriptor is a record with some of the following attributes:

<strong>value</strong><br/>
&nbsp;&nbsp;The value associated with the property (data descriptors only).

<strong>writable</strong><br/>
&nbsp;&nbsp;`true` if and only if the value associated with the property may be changed (data descriptors only).

<strong>get</strong><br/>
&nbsp;&nbsp;A function which serves as a getter for the property, or undefined if there is no getter (accessor descriptors only).

<strong>set</strong><br/>
&nbsp;&nbsp;A function which serves as a setter for the property, or `undefined` if there is no setter (accessor descriptors only).

<strong>configurable</strong><br/>
&nbsp;&nbsp;`true` if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.

<strong>enumerable</strong><br/>
&nbsp;&nbsp;`true` if and only if this property shows up during enumeration of the properties on the corresponding object.

###### Examples
![eQJGvt.png](https://s2.ax1x.com/2019/07/28/eQJGvt.png)
![eQJtDf.png](https://s2.ax1x.com/2019/07/28/eQJtDf.png)
![eQJaVS.png](https://s2.ax1x.com/2019/07/28/eQJaVS.png)
![eQJdUg.png](https://s2.ax1x.com/2019/07/28/eQJdUg.png)
![eQJw5Q.png](https://s2.ax1x.com/2019/07/28/eQJw5Q.png)

#### Object.getOwnPropertyDescriptors()
The `Object.getOwnPropertyDescriptors()` method returns all own property descriptors of a given object.
![eQY7Wj.png](https://s2.ax1x.com/2019/07/28/eQY7Wj.png)

###### Syntax
![eQYvwT.png](https://s2.ax1x.com/2019/07/28/eQYvwT.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object for which to get all own property descriptors.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;An object containing all own property descriptors of an object. Might be an empty object, if there are no properties.<br/>

###### Description
This method permits examination of the precise description of all own properties of an object. A property in JavaScript consists of either a string-valued name or a `Symbol` and a property descriptor.

A property descriptor is a record with some of the following attributes:

<strong>value</strong><br/>
&nbsp;&nbsp;The value associated with the property (data descriptors only).

<strong>writable</strong><br/>
&nbsp;&nbsp;`true` if and only if the value associated with the property may be changed (data descriptors only).

<strong>get</strong><br/>
&nbsp;&nbsp;A function which serves as a getter for the property, or `undefined` if there is no getter (accessor descriptors only).

<strong>set</strong><br/>
&nbsp;&nbsp;A function which serves as a setter for the property, or `undefined` if there is no setter (accessor descriptors only).

<strong>configurable</strong><br/>
&nbsp;&nbsp;`true` if and only if the type of this property descriptor may be changed and if the property may be deleted from the corresponding object.

<strong>enumerable</strong><br/>
&nbsp;&nbsp;`true` if and only if this property shows up during enumeration of the properties on the corresponding object.

###### Examples
<strong>Creating a shallow clone</strong><br/>
Whereas the `Object.assign()` method will only copy enumerable and own properties from a source object to a target object, you are able to use this method and `Object.create()` for a shallow copy between two unknown objects:
![eQtrn0.png](https://s2.ax1x.com/2019/07/28/eQtrn0.png)

<strong>Creating a subclass</strong><br/>
A typical way of creating a subclass is to define the subclass, set its prototype to an instance of the superclass, and then define properties on that instance. This can get awkward especially for getters and setters. Instead, you can use this code to set the prototype:
![eQthcR.png](https://s2.ax1x.com/2019/07/28/eQthcR.png)

#### Object.getOwnPropertyNames()
The `Object.getOwnPropertyNames()` method returns an array of all properties (including non-enumerable properties except for those which use Symbol) found directly in a given object.
![eQUAIO.png](https://s2.ax1x.com/2019/07/28/eQUAIO.png)

###### Syntax
![eQauhF.png](https://s2.ax1x.com/2019/07/28/eQauhF.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object whose enumerable and non-enumerable properties are to be returned.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;An array of strings that corresponds to the properties found directly in the given object.<br/>

###### Description
`Object.getOwnPropertyNames()` returns an array whose elements are strings corresponding to the enumerable and non-enumerable properties found directly in a given object `obj`. The ordering of the enumerable properties in the array is consistent with the ordering exposed by a `for...in` loop (or by `Object.keys()`) over the properties of the object. The ordering of the non-enumerable properties in the array and the ordering among the enumerable properties is not defined.

###### Examples
<strong>Using Object.getOwnPropertyNames()</strong><br/>
![eQ2sDU.png](https://s2.ax1x.com/2019/07/28/eQ2sDU.png)
![eQ2gUJ.png](https://s2.ax1x.com/2019/07/28/eQ2gUJ.png)
![eQ2WCR.png](https://s2.ax1x.com/2019/07/28/eQ2WCR.png)
![eQ2f81.png](https://s2.ax1x.com/2019/07/28/eQ2f81.png)
![eQ2hgx.png](https://s2.ax1x.com/2019/07/28/eQ2hgx.png)
If you want only the enumerable properties, see `Object.keys()` or use a `for...in` loop &#40;note that this will also return enumerable properties found along the prototype chain for the object unless the latter is filtered with `hasOwnProperty()`&#41;.

Items on the prototype chain are not listed:
![eQ2IKK.png](https://s2.ax1x.com/2019/07/28/eQ2IKK.png)

<strong>Get non-enumerable properties only</strong><br/>
This uses the `Array.prototype.filter()` function to remove the enumerable keys &#40;obtained with `Object.keys()`&#41; from a list of all keys &#40;obtained with `Object.getOwnPropertyNames()`&#41; thus giving only the non-enumerable keys as output.
![eQ2bUH.png](https://s2.ax1x.com/2019/07/28/eQ2bUH.png)

#### Object.getOwnPropertySymbols()
The `Object.getOwnPropertySymbols()` method returns an array of all symbol properties found directly upon a given object.
![e1xFY9.png](https://s2.ax1x.com/2019/07/29/e1xFY9.png)

###### Syntax
![e1xQFH.png](https://s2.ax1x.com/2019/07/29/e1xQFH.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object whose symbol properties are to be returned.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;An array of all symbol properties found directly upon the given object.<br/>

###### Description
Similar to `Object.getOwnPropertyNames()`, you can get all symbol properties of a given object as an array of symbols. Note that `Object.getOwnPropertyNames()` itself does not contain the symbol properties of an object and only the string properties.

As all objects have no own symbol properties initially, `Object.getOwnPropertySymbols()` returns an empty array unless you have set symbol properties on your object.

###### Examples
![e1zPnf.png](https://s2.ax1x.com/2019/07/29/e1zPnf.png)

#### Object.getPrototypeOf()
The `Object.getPrototypeOf()` method returns the prototype (i.e. the value of the internal <strong>&lsqb;&lsqb;Prototype&rsqb;&rsqb;</strong> property) of the specified object.
![e3SeaD.png](https://s2.ax1x.com/2019/07/29/e3SeaD.png)

###### Syntax
![e3SQxI.png](https://s2.ax1x.com/2019/07/29/e3SQxI.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>obj</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The object whose prototype is to be returned.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The prototype of the given object. If there are no inherited properties, `null` is returned.<br/>

###### Examples
![e3StIg.png](https://s2.ax1x.com/2019/07/29/e3StIg.png)

###### Notes
In ES5, it will throw a `TypeError` exception if the obj parameter isn't an object. In ES2015, the parameter will be coerced to an `Object`.
![e3SDs0.png](https://s2.ax1x.com/2019/07/29/e3SDs0.png)

#### Object.is()
The `Object.is()` method determines whether two values are the same value.

###### Syntax
![e3SHoD.png](https://s2.ax1x.com/2019/07/29/e3SHoD.png)
&nbsp;&nbsp;<strong>Parameters</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>value1</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first value to compare.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong><ins>value2</ins></strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second value to compare.<br/>
&nbsp;&nbsp;<strong>Return value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A `Boolean` indicating whether or not the two arguments are the same value.<br/>

###### Description
`Object.is()` determines whether two values are the same value. Two values are the same if one of the following holds:

- both `undefined`
- both `null`
- both `true` or both `false`
- both strings of the same length with the same characters in the same order
- both the same object (means both object have same reference)
- both numbers and
    - both `+0`
    - both `-0`
    - both `NaN`
    - or both non-zero and both not `NaN` and both have the same value
This is not the same as being equal according to the `==` operator. The `==` operator applies various coercions to both sides (if they are not the same Type) before testing for equality (resulting in such behavior as `"" == false` being `true`), but `Object.is` doesn't coerce either value.

This is also not the same as being equal according to the `===` operator. The `===` operator (and the `==` operator as well) treats the number values `-0` and `+0` as equal and treats `Number.NaN` as not equal to `NaN`.

###### Examples
![e3ks1g.png](https://s2.ax1x.com/2019/07/29/e3ks1g.png)

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
