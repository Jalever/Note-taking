---
layout: post
title: Array Properties and Methods
subtitle: Javascript Standard Built-in Object
date: 2019-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - JavaScript
---
- [Properties](#properties)
    - [Array.length](#arraylength)
    - [Array.prototype](#arrayprototype)
- [Methods](#methods)
    - [Array.from()](#arrayfrom)
    - [Array.isArray()](#arrayisarray)
    - [Array.of()](#arrayof)
    - [Array.prototype.concat()](#arrayprototypeconcat)
    - [Array.prototype.copyWithin()](#arrayprototypecopywithin)
    - [Array.prototype.entries()](#arrayprototypeentries)
    - [Array.prototype.every()](#arrayprototypeevery)
    - [Array.prototype.fill()](#arrayprototypefill)
    - [Array.prototype.filter()](#arrayprototypefilter)
    - [Array.prototype.find()](#arrayprototypefind)
    - [Array.prototype.findIndex()](#arrayprototypefindindex)
    - [Array.prototype.flat()](#arrayprototypeflat)
    - [Array.prototype.flatMap()](#arrayprototypeflatmap)
    - [Array.prototype.forEach()](#arrayprototypeforeach)
    - [Array.prototype.includes()](#arrayprototypeincludes)
    - [Array.prototype.indexOf()](#arrayprototypeindexof)
    - [Array.prototype.join()](#arrayprototypejoin)
    - [Array.prototype.keys()](#arrayprototypekeys)
    - [Array.prototype.lastIndexOf()](#arrayprototypelastindexof)
    - [Array.prototype.map()](#arrayprototypemap)
    - [Array.prototype.pop()](#arrayprototypepop)
    - [Array.prototype.push()](#arrayprototypepush)
    - [Array.prototype.reduce()](#arrayprototypereduce)
    - [Array.prototype.reduceRight()](#arrayprototypereduceright)
    - [Array.prototype.reverse()](#arrayprototypereverse)
    - [Array.prototype.shift()](#arrayprototypeshift)
    - [Array.prototype.slice()](#arrayprototypeslice)
    - [Array.prototype.some()](#arrayprototypesome)
    - [Array.prototype.sort()](#arrayprototypesort)
    - [Array.prototype.splice()](#arrayprototypesplice)
    - [Array.prototype.toLocaleString()](#arrayprototypetoLocalestring)
    - [Array.prototype.toString()](#arrayprototypetostring)
    - [Array.prototype.unshift()](#arrayprototypeunshift)
    - [Array.prototype.values()](#arrayprototypevalues)

----------------------------------------------------------------------------
## Array.from()
The `Array.from()` method creates a new, shallow-copied `Array` instance from an array-like or iterable object.

#### Syntax
![ZcrFrd.png](https://s2.ax1x.com/2019/07/10/ZcrFrd.png)

###### Parameters
&nbsp;&nbsp;<strong>arrayLike</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;An array-like or iterable object to convert to an array.

&nbsp;&nbsp;<strong>mapFn</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Map function to call on every element of the array.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as `this` when executing `mapFn`.

###### Return Value
&nbsp;&nbsp;A new Array instance.

#### Description
`Array.from()` lets you create Arrays from:

- array-like objects (objects with a `length` property and indexed elements) or
- iterable objects (objects where you can get its elements, such as `Map` and `Set`).

`Array.from()` has an optional parameter `mapFn`, which allows you to execute a map function on each element of the array (or subclass object) that is being created. More clearly, `Array.from(obj, mapFn, thisArg)` has the same result as `Array.from(obj).map(mapFn, thisArg)`, except that it does not create an intermediate array. This is especially important for certain array subclasses, like `typed arrays`, since the intermediate array would necessarily have values truncated to fit into the appropriate type.

The `length` property of the `from()` method is 1.

In ES2015, the class syntax allows for sub-classing of both built-in and user defined classes; as a result, static methods such as `Array.from` are "inherited" by subclasses of Array and create new instances of the subclass, not Array.

#### Examples
###### Array from a String
![Zcsb7R.png](https://s2.ax1x.com/2019/07/10/Zcsb7R.png)

###### Array from a Set
![ZcsXh6.png](https://s2.ax1x.com/2019/07/10/ZcsXh6.png)

###### Array from a Map
![ZcylEn.png](https://s2.ax1x.com/2019/07/10/ZcylEn.png)

###### Array from an Array-like object (arguments)
![ZcyRDH.png](https://s2.ax1x.com/2019/07/10/ZcyRDH.png)

###### Using arrow functions and Array.from()
![Zcy728.png](https://s2.ax1x.com/2019/07/10/Zcy728.png)

###### Sequence generator (range)
![ebCVUI.png](https://s2.ax1x.com/2019/08/09/ebCVUI.png)
![ebCrZ9.png](https://s2.ax1x.com/2019/08/09/ebCrZ9.png)

----------------------------------------------------------------------------
## Array.isArray()
The `Array.isArray()` method determines whether the passed value is an Array.
![ZcRx3t.png](https://s2.ax1x.com/2019/07/10/ZcRx3t.png)

#### Syntax
![Zcflsf.png](https://s2.ax1x.com/2019/07/10/Zcflsf.png)

###### Parameters
&nbsp;&nbsp;<strong>value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The value to be checked.

###### Return Value
&nbsp;&nbsp;`true` if the value is an `Array`; otherwise, `false`.

#### Description
If the value is an `Array`, `true` is returned; otherwise, `false` is.

#### Examples
![Zc4oPH.png](https://s2.ax1x.com/2019/07/10/Zc4oPH.png)

----------------------------------------------------------------------------
## Array.of()
The `Array.of()` method creates a new Array instance from a variable number of arguments, regardless of number or type of the arguments.

The difference between `Array.of()` and the Array constructor is in the handling of integer arguments: `Array.of(7)` creates an array with a single element, 7, whereas `Array(7)` creates an empty array with a length property of 7

> this implies an array of 7 empty slots, not slots with actual undefined values.

![Zc21LF.png](https://s2.ax1x.com/2019/07/10/Zc21LF.png)

#### Syntax
![Zc2cFA.png](https://s2.ax1x.com/2019/07/10/Zc2cFA.png)
###### Parameters
&nbsp;&nbsp;<strong>elementN</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Elements of which to create the array.

###### Return Value
&nbsp;&nbsp;A new `Array` instance.

#### Description
This function is part of the ECMAScript 2015 standard.

#### Examples
![ZcR1pt.png](https://s2.ax1x.com/2019/07/10/ZcR1pt.png)

----------------------------------------------------------------------------
## Array.prototype.concat()
The `concat()` method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
![ZgVr24.png](https://s2.ax1x.com/2019/07/10/ZgVr24.png)

#### Syntax
![ZgVgq1.png](https://s2.ax1x.com/2019/07/10/ZgVgq1.png)

###### Parameters
&nbsp;&nbsp;<strong>valueN</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;An Arrays and/or values to concatenate into a new array. If all `valueN` parameters are omitted, `concat` returns a shallow copy of the existing array on which it is called. See the description below for more details.

###### Return Value
&nbsp;&nbsp;A new `Array` instance.

#### Description
The `concat` method creates a new array consisting of the elements in the object on which it is called, followed in order by, for each argument, the elements of that argument (if the argument is an array) or the argument itself (if the argument is not an array). It does not recurse into nested array arguments.

The `concat` method does not alter `this` or any of the arrays provided as arguments but instead returns a shallow copy that contains copies of the same elements combined from the original arrays. Elements of the original arrays are copied into the new array as follows:

- Object references (and not the actual object): `concat` copies object references into the new array. Both the original and new array refer to the same object. That is, if a referenced object is modified, the changes are visible to both the new and original arrays. This includes elements of array arguments that are also arrays.
- Data types such as strings, numbers and booleans (not `String`, `Number`, and `Boolean` objects): `concat` copies the values of strings and numbers into the new array.

> Concatenating array(s)/value(s) will leave the originals untouched. Furthermore, any operation on the new array (except operations on elements which are object references) will have no effect on the original arrays, and vice versa.

#### Examples
###### Concatenating two arrays
The following code concatenates two arrays:
![ZgeyH1.png](https://s2.ax1x.com/2019/07/10/ZgeyH1.png)

###### Concatenating three arrays
The following code concatenates three arrays:
![Zge24K.png](https://s2.ax1x.com/2019/07/10/Zge24K.png)

###### Concatenating values to an array
The following code concatenates three values to an array:
![ZgeIud.png](https://s2.ax1x.com/2019/07/10/ZgeIud.png)

###### Concatenating nested arrays
The following code concatenates nested arrays and demonstrates retention of references:
![ZgmeKJ.png](https://s2.ax1x.com/2019/07/10/ZgmeKJ.png)


----------------------------------------------------------------------------
## Array.prototype.copyWithin()
The `copyWithin()` method shallow copies part of an array to another location in the same array and returns it without modifying its length.
![ZWfVJg.png](https://s2.ax1x.com/2019/07/12/ZWfVJg.png)

#### Syntax
![ZWfGYF.png](https://s2.ax1x.com/2019/07/12/ZWfGYF.png)

###### Parameters
&nbsp;&nbsp;<strong>target</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to copy the sequence to. If negative, <strong>target</strong> will be counted from the end.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>target</strong> is at or greater than <strong>arr.length</strong>, nothing will be copied. If <strong>target</strong> is positioned after <strong>start</strong>, the copied sequence will be trimmed to fit <strong>arr.length</strong>.

&nbsp;&nbsp;<strong>start</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to start copying elements from. If negative, <strong>start</strong> will be counted from the end.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>start</strong> is omitted, <strong>copyWithin</strong> will copy from index 0.


&nbsp;&nbsp;<strong>end</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to end copying elements from. <strong>copyWithin</strong> copies up to but not including <strong>end</strong>. If negative, <strong>end</strong> will be counted from the end.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>end</strong> is omitted, <strong>copyWithin</strong> will copy until the last index (default to <strong>arr.length</strong>).

###### Return Value
&nbsp;&nbsp;The modified array.

#### Description
The <strong>copyWithin</strong> works like C and C++'s <strong>memmove</strong>, and is a high-performance method to shift the data of an <strong>Array</strong>. This especially applies to the <strong>TypedArray</strong> method of the same name. The sequence is copied and pasted as one operation; pasted sequence will have the copied values even when the copy and paste region overlap.

The <strong>copyWithin</strong> function is intentionally generic, it does not require that its <strong>this</strong> value be an <strong>Array</strong> object.

The <strong>copyWithin</strong> method is a mutable method. It does not alter the length of <strong>this</strong>, but it will change its content and create new properties, if necessary.

#### Examples
![ZW4aa6.png](https://s2.ax1x.com/2019/07/12/ZW4aa6.png)

----------------------------------------------------------------------------
## Array.prototype.entries()
The `entries()` method returns a new <strong>Array Iterator</strong> object that contains the key/value pairs for each index in the array.

![ZW5Ik6.png](https://s2.ax1x.com/2019/07/12/ZW5Ik6.png)

#### Syntax
![ZWIGH1.png](https://s2.ax1x.com/2019/07/12/ZWIGH1.png)

###### Return Value
&nbsp;&nbsp;A new <strong>Array</strong> iterator object.

#### Examples
###### Iterating with index and element
![ZWoqeA.png](https://s2.ax1x.com/2019/07/12/ZWoqeA.png)

###### Using a for…of loop
![ZWTpQg.png](https://s2.ax1x.com/2019/07/12/ZWTpQg.png)


----------------------------------------------------------------------------
## Array.prototype.every()
The `every()` method tests whether all elements in the array pass the test implemented by the provided function. It returns a <strong>Boolean</strong> value.
> This method returns true for any condition put on an empty array.

![ZWHcLQ.png](https://s2.ax1x.com/2019/07/12/ZWHcLQ.png)


#### Syntax
![ZWHOoR.png](https://s2.ax1x.com/2019/07/12/ZWHOoR.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A function to test for each element, taking three arguments:<br/>

&nbsp;&nbsp;&nbsp;&nbsp;<strong>element</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.<br/>

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The <strong>array</strong> every was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A value to use as this when executing callback.<br/>

###### Return Value
&nbsp;&nbsp;<strong>true</strong> if the callback function returns a truthy value for every array element. Otherwise, <strong>false</strong>.

#### Description
The <strong>every</strong> method executes the provided <strong>callback</strong> function once for each element present in the array until it finds the one where <strong>callback</strong> returns a `falsy` value. If such an element is found, the <strong>every</strong> method immediately returns <strong>false</strong>. Otherwise, if <strong>callback</strong> returns a `truthy` value for all elements, <strong>every</strong> returns <strong>true</strong>. <strong>callback</strong> is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values.

<strong>callback</strong> is invoked with three arguments: the value of the element, the index of the element, and the Array object being traversed.

If a <strong>thisArg</strong> parameter is provided to <strong>every</strong>, it will be used as callback's <strong>this</strong> value. Otherwise, the value <strong>undefined</strong> will be used as its <strong>this</strong> value.  The <strong>this</strong> value ultimately observable by <strong>callback</strong> is determined according to the usual rules for determining the this seen by a function.

<strong>every</strong> does not mutate the array on which it is called.

The range of elements processed by <strong>every</strong> is set before the first invocation of <strong>callback</strong>. Therefore, <strong>callback</strong> will not run on elements that are appended to the array after the call to <strong>every</strong> begins. If existing elements of the array are changed, their value as passed to <strong>callback</strong> will be the value at the time <strong>every</strong> visits them. Elements that are deleted are not visited.

<strong>every</strong> acts like the "for all" quantifier in mathematics. In particular, for an empty array, it returns true.

#### Examples
###### Testing size of all array elements
The following example tests whether all elements in the array are bigger than 10.
![ZWL8zV.png](https://s2.ax1x.com/2019/07/12/ZWL8zV.png)

###### Using arrow functions
Arrow functions provide a shorter syntax for the same test.
![ZWL0iR.png](https://s2.ax1x.com/2019/07/12/ZWL0iR.png)

----------------------------------------------------------------------------
## Array.prototype.fill()
The `fill()` method fills (modifies) all the elements of an array from a start index (default zero) to an end index (default array length) with a static value. It returns the modified array.
![ZWLOoj.png](https://s2.ax1x.com/2019/07/12/ZWLOoj.png)

#### Syntax
![ZWOSS0.png](https://s2.ax1x.com/2019/07/12/ZWOSS0.png)

###### Parameters
&nbsp;&nbsp;<strong>value</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to fill an array.

&nbsp;&nbsp;<strong>start</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Start index, defaults to 0.

&nbsp;&nbsp;<strong>end</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;End index, defaults to <strong>this.length</strong>.

###### Return Value
&nbsp;&nbsp;The modified array.

#### Description
The <strong>fill</strong> method takes up to three arguments <strong>value</strong>, <strong>start</strong> and <strong>end</strong>. The <strong>start</strong> and <strong>end</strong> arguments are optional with default values of <strong>0</strong> and the <strong>length</strong> of the <strong>this</strong> object.

If <strong>start</strong> is negative, it is treated as <strong>length+start</strong> where <strong>length</strong> is the length of the array. If <strong>end</strong> is negative, it is treated as <strong>length+end</strong>.

<strong>fill</strong> is intentionally generic, it does not require that its <strong>this</strong> value be an Array object.

<strong>fill</strong> is a mutable method, it will change <strong>this</strong> object itself, and return it, not just return a copy of it.

When <strong>fill</strong> gets passed an object, it will copy the reference and fill the array with references to that object.

#### Examples
![ZWXM3q.png](https://s2.ax1x.com/2019/07/12/ZWXM3q.png)

----------------------------------------------------------------------------
## Array.prototype.filter()
The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.
![ZojdSg.png](https://s2.ax1x.com/2019/07/15/ZojdSg.png)

#### Syntax
![ZovYu9.png](https://s2.ax1x.com/2019/07/15/ZovYu9.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function is a predicate, to test each element of the array. Return `true` to keep the element, `false` otherwise. It accepts three arguments:

&nbsp;&nbsp;&nbsp;&nbsp;<strong>element</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array filter was called upon.


&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;A new array with the elements that pass the test. If no elements pass the test, an empty array will be returned.

#### Description
`filter()` calls a provided `callback` function once for each element in an array, and constructs a new array of all the values for which `callback` returns a value that coerces to true. `callback` is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values. Array elements which do not pass the `callback` test are simply skipped, and are not included in the new array.

`callback` is invoked with three arguments:

1. the value of the element
2. the index of the element
3. the Array object being traversed

If a `thisArg` parameter is provided to `filter`, it will be used as the callback's `this` value.  Otherwise, the value `undefined` will be used as its `this` value. The `this` value ultimately observable by `callback` is determined according to the usual rules for determining the `this` seen by a function.

`filter()` does not mutate the array on which it is called.

The range of elements processed by `filter()` is set before the first invocation of `callback`. Elements which are appended to the array after the call to `filter()` begins will not be visited by `callback`. If existing elements of the array are changed, or deleted, their value as passed to `callback` will be the value at the time `filter()` visits them; elements that are deleted are not visited.

#### Examples
###### Filtering out all small values
The following example uses `filter()` to create a filtered array that has all elements with values less than 10 removed.
![eLSRMD.png](https://s2.ax1x.com/2019/08/10/eLSRMD.png)

###### Filtering invalid entries from JSON
The following example uses `filter()` to create a filtered json of all elements with non-zero, numeric `id`.
![eLS4Zd.png](https://s2.ax1x.com/2019/08/10/eLS4Zd.png)
![eLS5dA.png](https://s2.ax1x.com/2019/08/10/eLS5dA.png)

###### Searching in array
Following example uses `filter()` to filter array content based on search criteria
![eLS7JP.png](https://s2.ax1x.com/2019/08/10/eLS7JP.png)

###### Searching in array
![eLSbz8.png](https://s2.ax1x.com/2019/08/10/eLSbz8.png)

----------------------------------------------------------------------------
## Array.prototype.find()
The `find()` method returns the <strong>value</strong> of the <strong>first element</strong> in the array that satisfies the provided testing function. Otherwise `undefined` is returned.
![ZoxqQe.png](https://s2.ax1x.com/2019/07/15/ZoxqQe.png)

See also the `findIndex()` method, which returns the index of a found element in the array instead of its value.

#### Syntax
![ZozQlF.png](https://s2.ax1x.com/2019/07/15/ZozQlF.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function to execute on each value in the array, taking three arguments:

&nbsp;&nbsp;&nbsp;&nbsp;<strong>element</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array find was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional object to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;The <strong>value</strong> of the <strong>first element</strong> in the array that satisfies the provided testing function. Otherwise, `undefined` is returned.

#### Description
The `find` method executes the `callback` function once for each index of the array until it finds one where `callback` returns a true value. If such element is found, `find` immediately returns the value of that element. Otherwise, `find` returns `undefined`. `callback` is invoked for every index of the array from `0` to `length - 1` and it is invoked for all indexes, not just those that have been assigned values. This indicates that it may be less efficient for sparse arrays compared to other methods that only visit indexes with assigned value.

`callback` is invoked with three arguments: the value of the element, the index of the element, and the Array object being traversed.

If a `thisArg` parameter is provided to `find`, it will be used as the `this` value for each invocation of the `callback`. If it is not provided, then `undefined` is used.

The `find` method does not mutate the array on which it is called.

The range of elements processed by `find` is set before the first invocation of `callback`. Therefore, `callback` will not visit the elements that are appended to the array after the call to `find` begins. If an existing, unvisited element of the array is changed by `callback`, its value passed to the `callback` will be the given value at the time `find` visits that element's index. Elements that are deleted are still visited.

#### Examples
###### Find an object in an array by one of its properties
![eLppiq.png](https://s2.ax1x.com/2019/08/10/eLppiq.png)

###### Using ES2015 arrow function
![eLpPzT.png](https://s2.ax1x.com/2019/08/10/eLpPzT.png)

###### Find a prime number in an array
The following example finds an element in the array that is a prime number (or returns `undefined` if there is no prime number).
![eLpVeJ.png](https://s2.ax1x.com/2019/08/10/eLpVeJ.png)

The following examples show that non-existent and deleted elements are visited and that the value passed to the callback is their value when visited.
![eLpnF1.png](https://s2.ax1x.com/2019/08/10/eLpnF1.png)
![eLpKW6.png](https://s2.ax1x.com/2019/08/10/eLpKW6.png)

----------------------------------------------------------------------------
## Array.prototype.findIndex()
The `findIndex()` method returns the <strong>index</strong> of the first element in the array <strong>that satisfies the provided testing function</strong>. Otherwise, it returns <strong>-1</strong>, indicating that no element passed the test.
![ZTCNHH.png](https://s2.ax1x.com/2019/07/15/ZTCNHH.png)

#### Syntax
![ZTCrgf.png](https://s2.ax1x.com/2019/07/15/ZTCrgf.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A function to execute on each value in the array until the function returns `true`, indicating that the satisfying element was found. It takes three arguments:

&nbsp;&nbsp;&nbsp;&nbsp;<strong>element</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array `findIndex` was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional object to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;The index of the first element in the array that passes the test. Otherwise, `-1`.

#### Description
The `findIndex` method executes the `callback` function once for every index `0..length-1` (inclusive) in the array until it finds the one where `callback` returns a truthy value (a value that coerces to `true`).

If such an element is found, `findIndex` immediately returns the element's index. If the callback never returns a truthy value (or the array's `length` is 0), `findIndex` returns -1. Unlike other array methods such as `Array.some`, the `callback` is called even for indexes with unassigned values.

`callback` is invoked with three arguments:

1. The value of the element
2. The index of the element
3. The Array object being traversed

If a `thisArg` parameter is passed to `findIndex`, it will be used as the `this` inside each invocation of the `callback`. If it is not provided, then `undefined` is used.

The range of elements processed by `findIndex` is set before the first invocation of `callback`. `callback` will not process the elements appended to the array after the call to `findIndex` begins. If an existing, unvisited element of the array is changed by `callback`, its value passed to the `callback` will be the value at the time `findIndex` visits the element's index. Elements that are deleted are still visited.

#### Examples
###### Find the index of a prime number in an array
The following example returns the index of the first element in the array that is a prime number, or -1 if there is no prime number.
![eLp3Oe.png](https://s2.ax1x.com/2019/08/10/eLp3Oe.png)

###### Find index using arrow function
The following example finds the index of a fruit using an arrow function:
![eLpJwd.png](https://s2.ax1x.com/2019/08/10/eLpJwd.png)

----------------------------------------------------------------------------
## Array.prototype.flat()
The `flat()` method creates a new array with all sub-array elements concatenated into it recursively up to the specified depth.

#### Syntax
![ZHmuLR.png](https://s2.ax1x.com/2019/07/16/ZHmuLR.png)

###### Parameters
&nbsp;&nbsp;<strong>depth</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;The depth level specifying how deep a nested array structure should be flattened. Defaults to 1.

###### Return Value
&nbsp;&nbsp;A new array with the sub-array elements concatenated into it.

#### Examples
###### Flattening nested arrays
![eXv2ng.png](https://s2.ax1x.com/2019/08/11/eXv2ng.png)

###### Flattening and array holes
The flat method removes empty slots in arrays:
![eXvW7j.png](https://s2.ax1x.com/2019/08/11/eXvW7j.png)

#### Alternative
###### reduce and concat
![eXvhAs.png](https://s2.ax1x.com/2019/08/11/eXvhAs.png)

###### Deep level flatten use recursion with reduce and concat
![eXvo90.png](https://s2.ax1x.com/2019/08/11/eXvo90.png)

###### Non Recursive flatten deep using a stack
![eXvx41.png](https://s2.ax1x.com/2019/08/11/eXvx41.png)

###### recursive flatten deep
![eXxFDe.png](https://s2.ax1x.com/2019/08/11/eXxFDe.png)

----------------------------------------------------------------------------
## Array.prototype.flatMap()
The `flatMap()` method first maps each element using a mapping function, then flattens the result into a new array. It is identical to a `map()` followed by a `flat()` of depth 1, but `flatMap()` is often quite useful, as merging both into one method is slightly more efficient.

#### Syntax
![ZHnTEt.png](https://s2.ax1x.com/2019/07/16/ZHnTEt.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function that produces an element of the new Array, taking three arguments:

&nbsp;&nbsp;&nbsp;&nbsp;<strong>currentValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array `map` was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;A new array with each element being the result of the callback function and flattened to a depth of 1.

#### Description
See `Array.prototype.map()` for a detailed description of the callback function. The `flatMap` method is identical to a `map` followed by a call to `flat` of depth 1.

#### Examples
###### map() and flatMap()
![eXxfKO.png](https://s2.ax1x.com/2019/08/11/eXxfKO.png)
While the above could have been achieved by using map itself, here is an example that better showcases the use of `flatMap`.

Let's generate a list of words from a list of sentences.
![eXxhrD.png](https://s2.ax1x.com/2019/08/11/eXxhrD.png)
Notice, the output list length can be different from the input list length.

###### For adding and removing items during a map()
`flatMap` can be used as a way to add and remove items (modify the number of items) during a `map`. In other words, it allows you to map many items to many items (by handling each input item separately), rather than always one-to-one. In this sense, it works like the opposite of filter. Simply return a 1-element array to keep the item, a multiple-element array to add items, or a 0-element array to remove the item.
![eXxTIA.png](https://s2.ax1x.com/2019/08/11/eXxTIA.png)

#### Alternative
###### reduce() and concat()
![eXxqRP.png](https://s2.ax1x.com/2019/08/11/eXxqRP.png)

Note, however, that this is inefficient and should be avoided for large arrays: in each iteration, it creates a new temporary array that must be garbage-collected, and it copies elements from the current accumulator array into a new array instead of just adding the new elements to the existing array.

----------------------------------------------------------------------------
## Array.prototype.forEach()
The `forEach()` method executes a provided function once for each array element.
![ZH35z6.png](https://s2.ax1x.com/2019/07/16/ZH35z6.png)

#### Syntax
![ZH3XFA.png](https://s2.ax1x.com/2019/07/16/ZH3XFA.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function to execute on each element, taking three arguments:

&nbsp;&nbsp;&nbsp;&nbsp;<strong>currentValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.

&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array `forEach()` was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;undefined.

#### Description
`forEach()` calls a provided `callback` function once for each element in an array in ascending order. It is not invoked for index properties that have been deleted or are uninitialized (i.e. on Sparse Arrays).
> <strong>Sparse Array</strong>: an array of data in which many elements have a value of zero. This is in contrast to a dense array, where most of the elements have non-zero values or are “full” of numbers.

`callback` is invoked with three arguments:
1. the value of the element
2. the index of the element
3. the Array object being traversed

If a `thisArg` parameter is provided to `forEach()`, it will be used as callback's `this` value. Otherwise, the value `undefined` will be used as its `this` value. The `this` value ultimately observable by `callback` is determined according to the usual rules for determining the `this` seen by a function.

The range of elements processed by `forEach()` is set before the first invocation of `callback`. Elements which are appended to the array after the call to `forEach()` begins will not be visited by `callback`. If existing elements of the array are changed, or deleted, their value as passed to `callback` will be the value at the time `forEach()` visits them; elements that are deleted before being visited are not visited. If elements that are already visited are removed (e.g. using `shift()`) during the iteration, later elements will be skipped - see example below.

`forEach()` executes the `callback` function once for each array element; unlike `map()` or `reduce()` it always returns the value `undefined` and is not chainable. The typical use case is to execute side effects at the end of a chain.

`forEach()` does not mutate the array on which it is called (although `callback`, if invoked, may do so).

> There is no way to stop or break a `forEach()` loop other than by throwing an exception. If you need such behavior, the `forEach()` method is the wrong tool.
> Early termination may be accomplished with:
> - A simple loop
> - A for...of loop
> - Array.prototype.every()
> - Array.prototype.some()
> - Array.prototype.find()
> - Array.prototype.findIndex()<br/>
> The other Array methods: `every()`, `some()`, `find()`, and `findIndex()` test the array elements with a predicate returning a truthy value to determine if further iteration is required.

#### Examples
###### Converting a for loop to forEach
![exJJxA.png](https://s2.ax1x.com/2019/08/12/exJJxA.png)

###### Printing the contents of an array
> Note: In order to display the content of an array in the console, you can use `console.table()` which will print a formated version of the array. The following example illustrates another way of doing so, using forEach().

The following code logs a line for each element in an array:
![exJs2j.png](https://s2.ax1x.com/2019/08/12/exJs2j.png)

###### Using thisArg
The following (contrived) example updates an object's properties from each entry in the array:
![exJgrq.png](https://s2.ax1x.com/2019/08/12/exJgrq.png)

Since the `thisArg` parameter (`this`) is provided to `forEach()`, it is passed to `callback` each time it's invoked, for use as its `this` value.
> If passing the function argument using an arrow function expression the <strong>thisArg</strong> parameter can be omitted as arrow functions lexically bind the this value.

###### An object copy function
The following code creates a copy of a given object. There are different ways to create a copy of an object; the following is just one way and is presented to explain how `Array.prototype.forEach()` works by using ECMAScript 5 `Object.*` meta property functions.
![exJfaT.png](https://s2.ax1x.com/2019/08/12/exJfaT.png)

###### If the array is modified during iteration, other elements might be skipped.
The following example logs "one", "two", "four". When the entry containing the value "two" is reached, the first entry of the whole array is shifted off, which results in all remaining entries moving up one position. Because element "four" is now at an earlier position in the array, "three" will be skipped. `forEach()` does not make a copy of the array before iterating.
![exYAdf.png](https://s2.ax1x.com/2019/08/12/exYAdf.png)
![exYeJg.png](https://s2.ax1x.com/2019/08/12/exYeJg.png)

###### Flatten an array
The following example is only here for learning purpose. If you want to flatten an array using built-in methods you can use `Array.prototype.flat()` (expected to be part of ES2019 and already implemented in some browsers).
![exYmWQ.png](https://s2.ax1x.com/2019/08/12/exYmWQ.png)

----------------------------------------------------------------------------
## Array.prototype.includes()
The `includes()` method determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate.
![ZHbqFf.png](https://s2.ax1x.com/2019/07/16/ZHbqFf.png)


#### Syntax
![ZHq9wq.png](https://s2.ax1x.com/2019/07/16/ZHq9wq.png)

###### Parameters
&nbsp;&nbsp;<strong>valueToFind</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The value to search for.    
> When comparing strings and characters, `includes()` is case-sensitive.

&nbsp;&nbsp;<strong>fromIndex</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;The position in this array at which to begin searching for `valueToFind`; the first character to be searched is found at `fromIndex` for positive values of `fromIndex`, or at `array.length + fromIndex` for negative values of `fromIndex` (using the absolute value of `fromIndex` as the number of characters from the end of the array at which to start the search). Defaults to 0.

###### Return Value
&nbsp;&nbsp;A `Boolean` which is `true` if the value `valueToFind` is found within the array (or the part of the array indicated by the index `fromIndex`, if specified). Values of zero are all considered to be equal regardless of sign (that is, `-0` is considered to be equal to both `0` and `+0`), but `false` is not considered to be the same as 0.

> Technically speaking, `includes()` uses the sameValueZero algorithm to determine whether the given element is found.

#### Examples
![mpTzuD.png](https://s2.ax1x.com/2019/08/13/mpTzuD.png)

###### fromIndex is greater than or equal to the array length
If `fromIndex` is greater than or equal to the length of the array, `false` is returned. The array will not be searched.
![mp7PUA.png](https://s2.ax1x.com/2019/08/13/mp7PUA.png)

###### Computed index is less than 0
If `fromIndex` is negative, the computed index is calculated to be used as a position in the array at which to begin searching for `valueToFind`. If the computed index is less or equal than `-1 * array.length`, the entire array will be searched.
![mp7i4I.png](https://s2.ax1x.com/2019/08/13/mp7i4I.png)

###### includes() used as a generic method
`includes()` method is intentionally generic. It does not require `this` value to be an Array object, so it can be applied to other kinds of objects (e.g. array-like objects). The example below illustrates `includes()` method called on the function's arguments object.
![mp7kCt.png](https://s2.ax1x.com/2019/08/13/mp7kCt.png)

----------------------------------------------------------------------------
## Array.prototype.indexOf()
The `indexOf()` method returns the first index at which a given element can be found in the array, or `-1` if it is not present.
![ZLdgU0.png](https://s2.ax1x.com/2019/07/17/ZLdgU0.png)

#### Syntax
![ZLdTbR.png](https://s2.ax1x.com/2019/07/17/ZLdTbR.png)

###### Parameters
&nbsp;&nbsp;<strong>searchElement</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Element to locate in the array.

&nbsp;&nbsp;<strong>fromIndex</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;The index to start the search at. If the index is greater than or equal to the array's length, `-1` is returned, which means the array will not be searched. If the provided index value is a negative number, it is taken as the offset from the end of the array. Note: if the provided index is negative, the array is still searched from front to back. If the provided index is `0`, then the whole array will be searched. Default: `0` (entire array is searched).

###### Return Value
&nbsp;&nbsp;The first index of the element in the array; `-1` if not found.

#### Description
`indexOf()` compares `searchElement` to elements of the Array using strict equality (the same method used by the `===` or triple-equals operator).

#### Examples
###### Using indexOf()
The following example uses `indexOf()` to locate values in an array.
![ZLw3GT.png](https://s2.ax1x.com/2019/07/17/ZLw3GT.png)

###### Finding all the occurrences of an element
![ZLwNL9.png](https://s2.ax1x.com/2019/07/17/ZLwNL9.png)

###### Finding if an element exists in the array or not and updating the array
![ZLwdd1.png](https://s2.ax1x.com/2019/07/17/ZLwdd1.png)

----------------------------------------------------------------------------
## Array.prototype.join()
The `join()` method creates and returns a new string by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string. If the array has only one item, then that item will be returned without using the separator.
![ZLBGDJ.png](https://s2.ax1x.com/2019/07/17/ZLBGDJ.png)

#### Syntax
![ZLBBvD.png](https://s2.ax1x.com/2019/07/17/ZLBBvD.png)

###### Parameters
&nbsp;&nbsp;<strong>separator</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Specifies a string to separate each pair of adjacent elements of the array. The separator is converted to a string if necessary. If omitted, the array elements are separated with a comma (","). If `separator` is an empty string, all elements are joined without any characters in between them.

###### Return Value
&nbsp;&nbsp;A string with all array elements joined. If `arr.length` is `0`, the empty string is returned.

#### Description
The string conversions of all array elements are joined into one string.
> If an element is `undefined` or `null`, it is converted to the empty string.

#### Examples
###### Joining an array four different ways
The following example creates an array, `a`, with three elements, then joins the array four times: using the default separator, then a comma and a space, then a plus and an empty string.
![ZLBzMF.png](https://s2.ax1x.com/2019/07/17/ZLBzMF.png)

###### Joining an array-like object
The following example joins array-like object (`arguments`), by calling `Function.prototype.call` on `Array.prototype.join`.

![ZLD8Rf.png](https://s2.ax1x.com/2019/07/17/ZLD8Rf.png)

----------------------------------------------------------------------------
## Array.prototype.keys()
The `keys()` method returns a new <strong>Array Iterator</strong> object that contains the keys for each index in the array.
![ZLrvB4.png](https://s2.ax1x.com/2019/07/17/ZLrvB4.png)

#### Syntax
![ZLsEuD.png](https://s2.ax1x.com/2019/07/17/ZLsEuD.png)

###### Return Value
&nbsp;&nbsp;A new <strong>Array</strong> iterator object.

#### Examples
###### Key iterator doesn't ignore holes
![ZLsnUA.png](https://s2.ax1x.com/2019/07/17/ZLsnUA.png)

----------------------------------------------------------------------------
## Array.prototype.lastIndexOf()
The `lastIndexOf()` method returns the last index at which a given element can be found in the array, or `-1` if it is not present. The array is searched backwards, starting at `fromIndex`.
![ZL6Rc6.png](https://s2.ax1x.com/2019/07/17/ZL6Rc6.png)

#### Syntax
![ZL6b9I.png](https://s2.ax1x.com/2019/07/17/ZL6b9I.png)

###### Parameters
&nbsp;&nbsp;<strong>searchElement</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Element to locate in the array.

&nbsp;&nbsp;<strong>fromIndex</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;The index at which to start searching backwards. Defaults to the array's length minus one (`arr.length - 1`), i.e. the whole array will be searched. If the index is greater than or equal to the length of the array, the whole array will be searched. If negative, it is taken as the offset from the end of the array. Note that even when the index is negative, the array is still searched from back to front. If the calculated index is less than `0`, `-1` is returned, i.e. the array will not be searched.

###### Return Value
&nbsp;&nbsp;The last index of the element in the array; `-1` if not found.

#### Description
`lastIndexOf` compares `searchElement` to elements of the Array using <strong>Strict Equality</strong> (the same method used by the `===`, or triple-equals, operator).

#### Examples
###### Using lastIndexOf
The following example uses `lastIndexOf` to locate values in an array.
![ZLcJbD.png](https://s2.ax1x.com/2019/07/17/ZLcJbD.png)

###### Finding all the occurrences of an element
The following example uses `lastIndexOf` to find all the indices of an element in a given array, using `push` to add them to another array as they are found.

![ZLgIfA.png](https://s2.ax1x.com/2019/07/17/ZLgIfA.png)

Note that we have to handle the case `idx == 0` separately here because the element will always be found regardless of the `fromIndex` parameter if it is the first element of the array. This is different from the `indexOf` method.

----------------------------------------------------------------------------
## Array.prototype.map()
The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.
![ZXnAiR.png](https://s2.ax1x.com/2019/07/18/ZXnAiR.png)

#### Syntax
![ZXnwwQ.png](https://s2.ax1x.com/2019/07/18/ZXnwwQ.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function that produces an element of the new Array, taking three arguments:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>currentValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array `map` was called upon.

&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as `this` when executing `callback`.

###### Return Value
&nbsp;&nbsp;A new array with each element being the result of the callback function.

#### Description
<strong>map</strong> calls a provided <strong>callback</strong> function once for each element in an array, in order, and constructs a new array from the results. <strong>callback</strong> is invoked only for indexes of the array which have assigned values, including <ins>undefined</ins>. It is not called for missing elements of the array (that is, indexes that have never been set, which have been deleted or which have never been assigned a value).

Since <strong>map</strong> builds a new array, using it when you aren't using the returned array is an anti-pattern; use <ins>forEach</ins> or <ins>for-of</ins> instead. Signs you shouldn't be using map:
1. You're not using the array it returns
2. You're not returning a value from the callback.

<strong>callback</strong> is invoked with three arguments: the value of the element, the index of the element, and the Array object being traversed.

If a <strong>thisArg</strong> parameter is provided to <strong>map</strong>, it will be used as callback's <strong>this</strong> value. Otherwise, the value <strong>undefined</strong> will be used as its <strong>this</strong> value. The <strong>this</strong> value ultimately observable by <strong>callback</strong> is determined according to The Usual Rules For Determining The This Seen By A Function.

<strong>map</strong> does not mutate the array on which it is called (although <strong>callback</strong>, if invoked, may do so).

The range of elements processed by <strong>map</strong> is set before the first invocation of <strong>callback</strong>. Elements which are appended to the array after the call to <strong>map</strong> begins will not be visited by <strong>callback</strong>. If existing elements of the array are changed, their value as passed to <strong>callback</strong> will be the value at the time <strong>map</strong> visits them. Elements that are deleted after the call to <strong>map</strong> begins and before being visited are not visited.

Due to the algorithm defined in the specification if the array which map was called upon is sparse, resulting array will also be sparse keeping same indices blank.

#### Examples
###### Mapping an array of numbers to an array of square roots
The following code takes an array of numbers and creates a new array containing the square roots of the numbers in the first array.
![ZXlnVU.png](https://s2.ax1x.com/2019/07/18/ZXlnVU.png)

###### Using map to reformat objects in an array
The following code takes an array of objects and creates a new array containing the newly reformatted objects.
![ZXlhGj.png](https://s2.ax1x.com/2019/07/18/ZXlhGj.png)

###### Mapping an array of numbers using a function containing an argument
The following code shows how map works when a function requiring one argument is used with it. The argument will automatically be assigned from each element of the array as map loops through the original array.
![ZX1FoD.png](https://s2.ax1x.com/2019/07/18/ZX1FoD.png)

###### Using map generically
This example shows how to use map on a <strong>String</strong> to get an array of bytes in the ASCII encoding representing the character values:
![ZX1dmV.png](https://s2.ax1x.com/2019/07/18/ZX1dmV.png)

###### Using map generically querySelectorAll
This example shows how to iterate through a collection of objects collected by <strong>querySelectorAll</strong>. This is because <strong>querySelectorAll</strong> returns a <strong>NodeList</strong> which is a collection of objects.

In this case we return all the selected options' values on the screen:
![ZX3mh4.png](https://s2.ax1x.com/2019/07/18/ZX3mh4.png)

###### Tricky use case
It is common to use the callback with one argument (the element being traversed). Certain functions are also commonly used with one argument, even though they take additional optional arguments. These habits may lead to confusing behaviors.
![ZX84RH.png](https://s2.ax1x.com/2019/07/18/ZX84RH.png)
![ZX8TsI.png](https://s2.ax1x.com/2019/07/18/ZX8TsI.png)

One alternative output of the map method being called with parseInt as a parameter runs as follows:
![ZXGSQs.png](https://s2.ax1x.com/2019/07/18/ZXGSQs.png)

----------------------------------------------------------------------------
## Array.prototype.pop()
The <strong>pop()</strong> method removes the <ins>last</ins> element from an array and returns that element. This method changes the length of the array.
![ZXth7t.png](https://s2.ax1x.com/2019/07/18/ZXth7t.png)

#### Syntax
![ZXt79S.png](https://s2.ax1x.com/2019/07/18/ZXt79S.png)

###### Return Value
&nbsp;&nbsp;The removed element from the array; undefined if the array is empty.

#### Description
The <strong>pop</strong> method removes the last element from an array and returns that value to the caller.

<strong>pop</strong> is intentionally generic; this method can be called or applied to objects resembling arrays. Objects which do not contain a <strong>length</strong> property reflecting the last in a series of consecutive, zero-based numerical properties may not behave in any meaningful manner.

If you call <strong>pop()</strong> on an empty array, it returns <strong>undefined</strong>.

<strong>Array.prototype.shift()</strong> has similar behavior to <strong>pop</strong>, but applied to the first element in an array.

#### Examples
###### Removing the last element of an array
The following code creates the <strong>myFish</strong> array containing four elements, then removes its last element.
![ZXtj7q.png](https://s2.ax1x.com/2019/07/18/ZXtj7q.png)

###### Using apply( ) or call ( ) on array-like objects
The following code creates the <strong>myFish</strong> array-like object containing four elements and a length parameter, then removes its last element and decrements the length parameter.
![ZXNShT.png](https://s2.ax1x.com/2019/07/18/ZXNShT.png)

----------------------------------------------------------------------------
## Array.prototype.push()
The <strong>push()</strong> method adds one or more elements to the end of an array and returns the new length of the array.
![ZXN3DA.png](https://s2.ax1x.com/2019/07/18/ZXN3DA.png)

#### Syntax
![ZXNYUP.png](https://s2.ax1x.com/2019/07/18/ZXNYUP.png)

###### Parameters
&nbsp;&nbsp;<strong>elementN</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The elements to add to the end of the array.

###### Return Value
&nbsp;&nbsp;The new <strong>length</strong> property of the object upon which the method was called.

#### Description
The <strong>push</strong> method appends values to an array.

<strong>push</strong> is intentionally generic. This method can be used with <strong>call()</strong> or <strong>apply()</strong> on objects resembling arrays. The <strong>push</strong> method relies on a <strong>length</strong> property to determine where to start inserting the given values. If the <strong>length</strong> property cannot be converted into a number, the index used is 0. This includes the possibility of <strong>length</strong> being nonexistent, in which case <strong>length</strong> will also be created.

Although <strong>String</strong>s are native, Array-like objects, they are not suitable in applications of this method, as strings are immutable.  Similarly for the native, Array-like object arguments.


#### Examples
###### Adding elements to an array
The following code creates the <strong>sports</strong> array containing two elements, then appends two elements to it. The <strong>total</strong> variable contains the new length of the array.
![ZXNO2D.png](https://s2.ax1x.com/2019/07/18/ZXNO2D.png)

###### Merging two arrays
This example uses <strong>apply()</strong> to push all elements from a second array.

Do not use this method if the second array (<strong>moreVegs</strong> in the example) is very large, because the maximum number of parameters that one function can take is limited in practice.
![ZXUCIP.png](https://s2.ax1x.com/2019/07/18/ZXUCIP.png)

###### Using an object in an array-like fashion
As mentioned above, <strong>push</strong> is intentionally generic, and we can use that to our advantage. <strong>Array.prototype.push</strong> can work on an object just fine, as this example shows. Note that we don't create an array to store a collection of objects. Instead, we store the collection on the object itself and use <strong>call</strong> on <strong>Array.prototype.push</strong> to trick the method into thinking we are dealing with an array, and it just works, thanks to the way JavaScript allows us to establish the execution context however we please.
![ZXUYL9.png](https://s2.ax1x.com/2019/07/18/ZXUYL9.png)
Note that although <strong>obj</strong> is not an array, the method <strong>push</strong> successfully incremented <strong>obj</strong>'s <strong>length</strong> property just like if we were dealing with an actual array.

----------------------------------------------------------------------------
## Array.prototype.reduce()
The <strong>reduce()</strong> method executes a <strong>reducer</strong> function (that you provide) on each element of the array, resulting in a single output value.
![ZXUYL9.png](https://s2.ax1x.com/2019/07/18/ZXUYL9.png)
Your <strong>reducer</strong> function's returned value is assigned to the accumulator, whose value is remembered across each iteration throughout the array and ultimately becomes the final, single resulting value.


#### Syntax
![ZX2c3d.png](https://s2.ax1x.com/2019/07/18/ZX2c3d.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A function to execute on each element in the array (except for the first, if no initialValue is supplied), taking four arguments:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>accumulator</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The accumulator accumulates the callback's return values. It is the accumulated value previously returned in the last invocation of the callback, or <strong>initialValue</strong>, if supplied.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>currentValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array. Starts from index 0 if an <strong>initialValue</strong> is provided. Otherwise, starts from index 1.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array <strong>reduce()</strong> was called upon.<br/>
&nbsp;&nbsp;<strong>initialValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A value to use as the first argument to the first call of the <strong>callback</strong>. If no <strong>initialValue</strong> is supplied, the first element in the array will be used and skipped. Calling <strong>reduce()</strong> on an empty array without an <strong>initialValue</strong> will throw a <strong>TypeError</strong>.<br/>

###### Return Value
&nbsp;&nbsp;The single value that results from the reduction.

#### Description
The <strong>reduce()</strong> method executes the <strong>callback</strong> once for each assigned value present in the array, taking four arguments:
- accumulator
- currentValue
- currentIndex
- array
The first time the callback is called, <strong>accumulator</strong> and <strong>currentValue</strong> can be one of two values. If <strong>initialValue</strong> is provided in the call to <strong>reduce()</strong>, then <strong>accumulator</strong> will be equal to <strong>initialValue</strong>, and <strong>currentValue</strong> will be equal to the first value in the array. If no <strong>initialValue</strong> is provided, then <strong>accumulator</strong> will be equal to the first value in the array, and <strong>currentValue</strong> will be equal to the second.
> Note: If initialValue is not provided, reduce() will execute the callback function starting at index 1, skipping the first index. If initialValue is provided, it will start at index 0.

If the array is empty and no <strong>initialValue</strong> is provided, <strong>TypeError</strong> will be thrown. If the array only has one element (regardless of position) and no <strong>initialValue</strong> is provided, or if <strong>initialValue</strong> is provided but the array is empty, the solo value will be returned without calling <strong>callback</strong>.

It is usually safer to provide an <strong>initialValue</strong> because there are three possible outputs without <strong>initialValue</strong>, as shown in the following example.
![ZXfPn1.png](https://s2.ax1x.com/2019/07/18/ZXfPn1.png)

#### Examples
###### Sum all the values of an array
![ZX4fk6.png](https://s2.ax1x.com/2019/07/18/ZX4fk6.png)
Alternatively written with an arrow function:
![ZX44fO.png](https://s2.ax1x.com/2019/07/18/ZX44fO.png)

###### Sum of values in an object array
To sum up the values contained in an array of objects, you must supply an <strong>initialValue</strong>, so that each item passes through your function.
![ZX4vh8.png](https://s2.ax1x.com/2019/07/18/ZX4vh8.png)
Alternatively written with an arrow function:
![ZX5S1g.png](https://s2.ax1x.com/2019/07/18/ZX5S1g.png)

###### Flatten an array of arrays
![ZX59Xj.png](https://s2.ax1x.com/2019/07/18/ZX59Xj.png)
Alternatively written with an arrow function:
![ZX5iBn.png](https://s2.ax1x.com/2019/07/18/ZX5iBn.png)

###### Counting instances of values in an object
![ZX5VhT.png](https://s2.ax1x.com/2019/07/18/ZX5VhT.png)

###### Grouping objects by a property
![ZX5Wuj.png](https://s2.ax1x.com/2019/07/18/ZX5Wuj.png)
![ZX5hbn.png](https://s2.ax1x.com/2019/07/18/ZX5hbn.png)

###### Bonding arrays contained in an array of objects using the spread operator and initialValue
![ZXIaGT.png](https://s2.ax1x.com/2019/07/18/ZXIaGT.png)
![ZXIRJK.png](https://s2.ax1x.com/2019/07/18/ZXIRJK.png)

###### Remove duplicate items in array
> If you are using an environment compatible with `Set` and `Array.from()`, you could use `let orderedArray = Array.from(new Set(myArray));` to get an array where duplicate items have been removed.

![ZXoQFx.png](https://s2.ax1x.com/2019/07/18/ZXoQFx.png)

###### Running Promises in Sequence
![ZXoy6g.png](https://s2.ax1x.com/2019/07/18/ZXoy6g.png)
![ZXoR7n.png](https://s2.ax1x.com/2019/07/18/ZXoR7n.png)
![ZXofkq.png](https://s2.ax1x.com/2019/07/18/ZXofkq.png)

###### Function composition enabling piping
![ZXoz9K.png](https://s2.ax1x.com/2019/07/18/ZXoz9K.png)

###### write map using reduce
![ZXTlHs.png](https://s2.ax1x.com/2019/07/18/ZXTlHs.png)

----------------------------------------------------------------------------
## Array.prototype.reduceRight()
The <strong>reduceRight()</strong> method applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value.
![ZvNkHs.png](https://s2.ax1x.com/2019/07/19/ZvNkHs.png)

#### Syntax
![ZvUFxO.png](https://s2.ax1x.com/2019/07/19/ZvUFxO.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Function to execute on each value in the array, taking four arguments:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>accumulator</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The value previously returned in the last invocation of the callback, or <strong>initialValue</strong>, if supplied.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>currentValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array <strong>reduceRight()</strong> was called upon.<br/>
&nbsp;&nbsp;<strong>initialValue</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Value to use as accumulator to the first call of the <strong>callback</strong>. If no initial value is supplied, the last element in the array will be used and skipped. Calling reduce or reduceRight on an empty array without an initial value creates a <strong>TypeError</strong>.<br/>

###### Return Value
&nbsp;&nbsp;The value that results from the reduction.

#### Description
<strong>reduceRight</strong> executes the callback function once for each element present in the array, excluding holes in the array, receiving four arguments: the initial value (or value from the previous callback call), the value of the current element, the current index, and the array over which iteration is occurring.

The call to the <strong>reduceRight</strong> callback would look something like this:
![ZvdN80.png](https://s2.ax1x.com/2019/07/19/ZvdN80.png)

The first time the function is called, the <strong>accumulator</strong> and <strong>currentValue</strong> can be one of two values. If an <strong>initialValue</strong> was provided in the call to <strong>reduceRight</strong>, then <strong>accumulator</strong> will be equal to <strong>initialValue</strong> and <strong>currentValue</strong> will be equal to the last value in the array. If no <strong>initialValue</strong> was provided, then <strong>accumulator</strong> will be equal to the last value in the array and <strong>currentValue</strong> will be equal to the second-to-last value.

If the array is empty and no <strong>initialValue</strong> was provided, <strong>TypeError</strong> would be thrown. If the array has only one element (regardless of position) and no <strong>initialValue</strong> was provided, or if <strong>initialValue</strong> is provided but the array is empty, the solo value would be returned without calling <strong>callback</strong>.

#### Examples
###### Sum up all values within an array
![ZvweZ4.png](https://s2.ax1x.com/2019/07/19/ZvweZ4.png)

###### Flatten an array of arrays
![ZvwsOS.png](https://s2.ax1x.com/2019/07/19/ZvwsOS.png)

###### Run a list of asynchronous functions with callbacks in series each passing their results to the next
![ZvBp3q.png](https://s2.ax1x.com/2019/07/19/ZvBp3q.png)
![ZvB9g0.png](https://s2.ax1x.com/2019/07/19/ZvB9g0.png)

###### ​​​​​​Difference between reduce and reduceRight
![ZvBiuT.png](https://s2.ax1x.com/2019/07/19/ZvBiuT.png)

###### Defining Composible Function
The concept of compose function is simple it combines n functions. It’s a flowing right-to-left, calling each function with the output of the last one.
![ZvB8Ve.png](https://s2.ax1x.com/2019/07/19/ZvB8Ve.png)

----------------------------------------------------------------------------
## Array.prototype.reverse()
The <strong>reverse()</strong> method reverses an array in place. The first array element becomes the last, and the last array element becomes the first.
![ZvBzZD.png](https://s2.ax1x.com/2019/07/19/ZvBzZD.png)

#### Syntax
![ZvDAQP.png](https://s2.ax1x.com/2019/07/19/ZvDAQP.png)

###### Return Value
&nbsp;&nbsp;The reversed array.

#### Description
The <strong>reverse</strong> method transposes the elements of the calling array object in place, mutating the array, and returning a reference to the array.

<strong>reverse</strong> is intentionally generic; this method can be called or applied to objects resembling arrays. Objects which do not contain a <strong>length</strong> property reflecting the last in a series of consecutive, zero-based numerical properties may not behave in any meaningful manner.

#### Examples
###### Reversing the elements in an array
The following example creates an array <strong>a</strong>, containing three elements, then reverses the array. The call to <strong>reverse()</strong> returns a reference to the reversed array <strong>a</strong>.
![ZvD3Q0.png](https://s2.ax1x.com/2019/07/19/ZvD3Q0.png)

###### Reversing the elements in an array-like object
The following example creates an array-like object <strong>a</strong>, containing three elements and a length property, then reverses the array-like object. The call to <strong>reverse()</strong> returns a reference to the reversed array-like object <strong>a</strong>.
![ZvDtwF.png](https://s2.ax1x.com/2019/07/19/ZvDtwF.png)

----------------------------------------------------------------------------
## Array.prototype.shift()
The <strong>shift()</strong> method removes the <strong>first</strong> element from an array and returns that removed element. This method changes the length of the array.
![ZvDH0S.png](https://s2.ax1x.com/2019/07/19/ZvDH0S.png)

#### Syntax
![ZvrmX6.png](https://s2.ax1x.com/2019/07/19/ZvrmX6.png)

###### Return Value
&nbsp;&nbsp;The removed element from the array; undefined if the array is empty.

#### Description
The <strong>shift</strong> method removes the element at the zeroeth index and shifts the values at consecutive indexes down, then returns the removed value. If the <strong>length</strong> property is 0, <strong>undefined</strong> is returned.

<strong>shift</strong> is intentionally generic; this method can be called or applied to objects resembling arrays. Objects which do not contain a <strong>length</strong> property reflecting the last in a series of consecutive, zero-based numerical properties may not behave in any meaningful manner.

<strong>Array.prototype.pop()</strong> has similar behavior to <strong>shift</strong>, but applied to the last element in an array.

#### Examples
###### Removing an element from an array
The following code displays the <strong>myFish</strong> array before and after removing its first element. It also displays the removed element:
![ZvsKvq.png](https://s2.ax1x.com/2019/07/19/ZvsKvq.png)

###### Using shift() method in while loop
The shift() method is often used in condition inside while loop. In the following example every iteration will remove the next element from an array, until it is empty:
![ZvsGaF.png](https://s2.ax1x.com/2019/07/19/ZvsGaF.png)

----------------------------------------------------------------------------
## Array.prototype.slice()
The <strong>slice()</strong> method returns a shallow copy of a portion of an array into a new array object selected from <strong>begin</strong> to <strong>end</strong>(<strong>end</strong> not included). The original array will not be modified.
![Zvy8yt.png](https://s2.ax1x.com/2019/07/19/Zvy8yt.png)

#### Syntax
![Zvy6mV.png](https://s2.ax1x.com/2019/07/19/Zvy6mV.png)

###### Parameters
&nbsp;&nbsp;<strong>begin</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to begin extraction.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A negative index can be used, indicating an offset from the end of the sequence. <strong>slice(-2)</strong> extracts the last two elements in the sequence.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>begin</strong> is undefined, <strong>slice</strong> begins from index <strong>0</strong>.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>begin</strong> is greater than the length of the sequence, an empty array is returned.<br/>
&nbsp;&nbsp;<strong>end</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index before which to end extraction. <strong>slice</strong> extracts up to but not including <strong>end</strong>.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;For example, <strong>slice(1,4)</strong> extracts the second element through the fourth element (elements indexed 1, 2, and 3).<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A negative index can be used, indicating an offset from the end of the sequence. <strong>slice(2,-1)</strong> extracts the third element through the second-to-last element in the sequence.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>end</strong> is omitted, <strong>slice</strong> extracts through the end of the sequence(<strong>arr.length</strong>).<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>end</strong> is greater than the length of the sequence, <strong>slice</strong> extracts through to the end of the sequence (<strong>arr.length</strong>).<br/>

###### Return Value
&nbsp;&nbsp;A new array containing the extracted elements.

#### Description
<strong>slice</strong> does not alter the original array. It returns a shallow copy of elements from the original array. Elements of the original array are copied into the returned array as follows:
- For object references (and not the actual object), <strong>slice</strong> copies object references into the new array. Both the original and new array refer to the same object. If a referenced object changes, the changes are visible to both the new and original arrays.
- For strings, numbers and booleans (not <strong>String</strong>, <strong>Number</strong> and <strong>Boolean</strong> objects), <strong>slice</strong> copies the values into the new array. Changes to the string, number or boolean in one array do not affect the other array.

If a new element is added to either array, the other array is not affected.

#### Examples
###### Return a portion of an existing array
![Zvgr6A.png](https://s2.ax1x.com/2019/07/19/Zvgr6A.png)

###### Using slice
In the following example, <strong>slice</strong> creates a new array, <strong>newCar</strong>, from <strong>myCar</strong>. Both include a reference to the object <strong>myHonda</strong>. When the color of <strong>myHonda</strong> is changed to purple, both arrays reflect the change.
![ZvgCFS.png](https://s2.ax1x.com/2019/07/19/ZvgCFS.png)
![Zvgwfe.png](https://s2.ax1x.com/2019/07/19/Zvgwfe.png)

###### Array-like objects
<strong>slice</strong> method can also be called to convert Array-like objects / collections to a new Array. You just bind the method to the object. The <strong>arguments</strong> inside a function is an example of an 'array-like object'.
![Zv2SXR.png](https://s2.ax1x.com/2019/07/19/Zv2SXR.png)
Binding can be done with the .<strong>call</strong> function of <strong>Function.prototype</strong> and it can also be reduced using <strong>[].slice.call(arguments)</strong> instead of <strong>Array.prototype.slice.call</strong>. Anyway, it can be simplified using <strong>bind</strong>.
![Zv2P76.png](https://s2.ax1x.com/2019/07/19/Zv2P76.png)

----------------------------------------------------------------------------
## Array.prototype.some()
The <strong>some()</strong> method tests whether at least one element in the array passes the test implemented by the provided function. It returns a <strong>Boolean</strong> value.
> This method returns false for any condition put on an empty array.

![epfZuD.png](https://s2.ax1x.com/2019/07/21/epfZuD.png)

#### Syntax
![epfKUA.png](https://s2.ax1x.com/2019/07/21/epfKUA.png)

###### Parameters
&nbsp;&nbsp;<strong>callback</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;A function to test for each element, taking three arguments:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>element</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>index</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The index of the current element being processed in the array.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<strong>array</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The array <strong>some()</strong> was called upon.<br/>
&nbsp;&nbsp;<strong>thisArg</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A value to use as <strong>this</strong> when executing <strong>callback</strong>.<br/>

###### Return Value
&nbsp;&nbsp;<strong>true</strong> if the callback function returns a <ins>truthy</ins> value for at least one element in the array. Otherwise, <strong>false</strong>.

#### Description
The <strong>some()</strong> method executes the <strong>callback</strong> function once for each element present in the array until it finds the one where <strong>callback</strong> returns a truthy value (a value that becomes true when converted to a Boolean). If such an element is found, <strong>some()</strong> immediately returns <strong>true</strong>. Otherwise, <strong>some()</strong> returns <strong>false</strong>. <strong>callback</strong> is invoked only for indexes of the array with assigned values. It is not invoked for indexes which have been deleted or which have never been assigned values.

<strong>callback</strong> is invoked with three arguments: the value of the element, the index of the element, and the Array object being traversed.

If a <strong>thisArg</strong> parameter is provided to <strong>some()</strong>, it will be used as the callback's <strong>this</strong> value. Otherwise, the value <strong>undefined</strong> will be used as its <strong>this</strong> value. The <strong>this</strong> value ultimately observable by <strong>callback</strong> is determined according to the usual rules for determining the <strong>this</strong> seen by a function.

<strong>some()</strong> does not mutate the array on which it is called.

The range of elements processed by <strong>some()</strong> is set before the first invocation of <strong>callback</strong>. Elements appended to the array after the call to <strong>some()</strong> begins will not be visited by <strong>callback</strong>. If an existing, unvisited element of the array is changed by <strong>callback</strong>, its value passed to the visiting <strong>callback</strong> will be the value at the time that <strong>some()</strong> visits that element's index. Elements that are deleted are not visited.

#### Examples
###### Testing value of array elements
The following example tests whether any element in the array is bigger than 10.
![ep4jjf.png](https://s2.ax1x.com/2019/07/21/ep4jjf.png)

###### Testing array elements using arrow functions
Arrow functions provide a shorter syntax for the same test.
![ep59EQ.png](https://s2.ax1x.com/2019/07/21/ep59EQ.png)

###### Checking whether a value exists in an array
To mimic the function of the <strong>includes()</strong> method, this custom function returns <strong>true</strong> if the element exists in the array:
![ep5CNj.png](https://s2.ax1x.com/2019/07/21/ep5CNj.png)

###### Checking whether a value exists using an arrow function
![ep5P4s.png](https://s2.ax1x.com/2019/07/21/ep5P4s.png)

###### Converting any value to Boolean
![ep4XgP.png](https://s2.ax1x.com/2019/07/21/ep4XgP.png)

----------------------------------------------------------------------------
## Array.prototype.sort()
The <strong>sort()</strong> method sorts the elements of an array in place and returns the sorted array. The default sort order is built upon converting the elements into strings, then comparing their sequences of <strong>UTF-16</strong> code units values.

The time and space complexity of the sort cannot be guaranteed as it depends on the implementation.
![epTzzn.png](https://s2.ax1x.com/2019/07/21/epTzzn.png)

#### Syntax
![ep7yWj.png](https://s2.ax1x.com/2019/07/21/ep7yWj.png)

###### Parameters
&nbsp;&nbsp;<strong>compareFunction</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Specifies a function that defines the sort order. If omitted, the array elements are converted to strings, then sorted according to each character's Unicode code point value.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong>firstEl</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The first element for comparison.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<strong>secondEl</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The second element for comparison.<br/>

###### Return Value
&nbsp;&nbsp;The sorted array.
> Note that the array is sorted in place, and no copy is made.

#### Description
If <strong>compareFunction</strong> is not supplied, all non-<strong>undefined</strong> array elements are sorted by converting them to strings and comparing strings in UTF-16 code units order. For example, "banana" comes before "cherry". In a numeric sort, 9 comes before 80, but because numbers are converted to strings, "80" comes before "9" in the Unicode order. All <strong>undefined</strong> elements are sorted to the end of the array.

If <strong>compareFunction</strong> is supplied, all non-<strong>undefined</strong> array elements are sorted according to the return value of the compare function (all <strong>undefined</strong> elements are sorted to the end of the array, with no call to <strong>compareFunction</strong>). If <strong>a</strong> and <strong>b</strong> are two elements being compared, then:
- If <strong>compareFunction(a, b)</strong> is less than 0, sort <strong>a</strong> to an index lower than <strong>b</strong> (i.e. <strong>a</strong> comes first).
- If <strong>compareFunction(a, b)</strong> returns 0, leave <strong>a</strong> and <strong>b</strong> unchanged with respect to each other, but sorted with respect to all different elements. Note: the ECMAscript standard does not guarantee this behavior, thus, not all browsers (e.g. Mozilla versions dating back to at least 2003) respect this.
- If <strong>compareFunction(a, b)</strong> is greater than 0, sort <strong>b</strong> to an index lower than <strong>a</strong> (i.e. <strong>b</strong> comes first).
- <strong>compareFunction(a, b)</strong> must always return the same value when given a specific pair of elements <strong>a</strong> and <strong>b</strong> as its two arguments. If inconsistent results are returned, then the sort order is undefined.

So, the compare function has the following form:
![epXBT0.png](https://s2.ax1x.com/2019/07/21/epXBT0.png)

To compare numbers instead of strings, the compare function can simply subtract <strong>b</strong> from <strong>a</strong>. The following function will sort the array in ascending order (if it doesn't contain <strong>Infinity</strong> and <strong>NaN</strong>):
![epjC9S.png](https://s2.ax1x.com/2019/07/21/epjC9S.png)

The <strong>sort</strong> method can be conveniently used with function expressions:
![epjP1g.png](https://s2.ax1x.com/2019/07/21/epjP1g.png)

ES2015 provides arrow function expressions with even shorter syntax.
![epjEBn.png](https://s2.ax1x.com/2019/07/21/epjEBn.png)

Objects can be sorted, given the value of one of their properties.
![epvlPf.png](https://s2.ax1x.com/2019/07/21/epvlPf.png)
![epv8xg.png](https://s2.ax1x.com/2019/07/21/epv8xg.png)

#### Description
###### Creating, displaying, and sorting an array
The following example creates four arrays and displays the original array, then the sorted arrays. The numeric arrays are sorted without a compare function, then sorted using one.
![epx9yQ.png](https://s2.ax1x.com/2019/07/21/epx9yQ.png)
![epxies.png](https://s2.ax1x.com/2019/07/21/epxies.png)
This example produces the following output. As the output shows, when a compare function is used, numbers sort correctly whether they are numbers or numeric strings.
![epzEBd.png](https://s2.ax1x.com/2019/07/21/epzEBd.png)

###### Sorting non-ASCII characters
For sorting strings with non-ASCII characters, i.e. strings with accented characters(e, é, è, a, ä, etc.), strings from languages other than English, use <strong>String.localeCompare</strong>. This function can compare those characters so they appear in the right order.
![e9p9yD.png](https://s2.ax1x.com/2019/07/21/e9p9yD.png)

----------------------------------------------------------------------------
## Array.prototype.splice()
The <strong>splice()</strong> method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
![ek0rVA.png](https://s2.ax1x.com/2019/07/23/ek0rVA.png)

#### Syntax
![ekBlz8.png](https://s2.ax1x.com/2019/07/23/ekBlz8.png)

###### Parameters
&nbsp;&nbsp;<strong>start</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The index at which to start changing the array. If greater than the length of the array, `start` will be set to the length of the array. If negative, it will begin that many elements from the end of the array (with origin -1, meaning -n is the index of the nth last element and is therefore equivalent to the index of `array.length - n`). If the absolute value of `start` is greater than the length of the array, it will begin from index 0. <br/>
&nbsp;&nbsp;<strong>deleteCount</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;An integer indicating the number of elements in the array to remove from `start`.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If `deleteCount` is omitted, or if its value is equal to or larger than `array.length - start` (that is, if it is equal to or greater than the number of elements left in the array, starting at `start`), then all the elements from `start` to the end of the array will be deleted.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;If `deleteCount` is 0 or negative, no elements are removed. In this case, you should specify at least one new element.<br/>
&nbsp;&nbsp;<strong>item1, item2, ...</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;The elements to add to the array, beginning from `start`. If you do not specify any elements, `splice()` will only remove elements from the array.

###### Return Value
&nbsp;&nbsp;An array containing the deleted elements. If only one element is removed, an array of one element is returned. If no elements are removed, an empty array is returned.

#### Description
If the specified number of elements to insert differs from the number of elements being removed, the array's length will be different at the end of the call.

#### Examples
###### Remove 0 (zero) elements from index 2, and insert "drum"
![eks5lV.png](https://s2.ax1x.com/2019/07/23/eks5lV.png)

###### Remove 0 (zero) elements from index 2, and insert "drum" and "guitar"
![ekyqu8.png](https://s2.ax1x.com/2019/07/23/ekyqu8.png)

###### Remove 1 element from index 3
![ek6tPA.png](https://s2.ax1x.com/2019/07/23/ek6tPA.png)

###### Remove 1 element from index 2, and insert "trumpet"
![ek6qR1.png](https://s2.ax1x.com/2019/07/23/ek6qR1.png)

###### Remove 2 elements from index 0, and insert "parrot", "anemone" and "blue"
![ekcYeU.png](https://s2.ax1x.com/2019/07/23/ekcYeU.png)

###### Remove 2 elements from index 2
![ekc6eO.png](https://s2.ax1x.com/2019/07/23/ekc6eO.png)

###### Remove 1 element from index -2
![ekc5lt.png](https://s2.ax1x.com/2019/07/23/ekc5lt.png)

###### Remove all elements after index 2 (incl.)
![ekc7m8.png](https://s2.ax1x.com/2019/07/23/ekc7m8.png)

----------------------------------------------------------------------------
## Array.prototype.toLocaleString()
The <strong>toLocaleString()</strong> method returns a string representing the elements of the array. The elements are converted to Strings using their <strong>toLocaleString</strong> methods and these Strings are separated by a locale-specific String (such as a comma “,”).
![ek4cv9.png](https://s2.ax1x.com/2019/07/23/ek4cv9.png)

#### Syntax
![ek5axH.png](https://s2.ax1x.com/2019/07/23/ek5axH.png)

###### Parameters
&nbsp;&nbsp;<strong>locales</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;A string with a BCP 47 language tag, or an array of such strings. For the general form and interpretation of the `locales` argument, see the `Intl` page.<br/>
&nbsp;&nbsp;<strong>options</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;An object with configuration properties, for numbers see `Number.prototype.toLocaleString()`, and for dates see `Date.prototype.toLocaleString()`.<br/>

###### Return Value
&nbsp;&nbsp;A string representing the elements of the array.

#### Examples
#### Using locales and options
The elements of the array are converted to strings using their `toLocaleString` methods.
- Object: Object.prototype.toLocaleString()
- Number: Number.prototype.toLocaleString()
- Date: Date.prototype.toLocaleString()

Always display the currency for the strings and numbers in the `prices` array:
![ekI3lQ.png](https://s2.ax1x.com/2019/07/23/ekI3lQ.png)

----------------------------------------------------------------------------
## Array.prototype.toString()
The `toString()` method returns a string representing the specified array and its elements.
![ekIwfU.png](https://s2.ax1x.com/2019/07/23/ekIwfU.png)

#### Syntax
![ekIr6J.png](https://s2.ax1x.com/2019/07/23/ekIr6J.png)
###### Return Value
A string representing the elements of the array.

#### Description
The `Array` object overrides the `toString` method of `Object`. For Array objects, the `toString` method joins the array and returns one string containing each array element separated by commas.

JavaScript calls the `toString` method automatically when an array is to be represented as a text value or when an array is referred to in a string concatenation.

----------------------------------------------------------------------------
## Array.prototype.toString()
The <strong>unshift()</strong> method adds one or more elements to the beginning of an array and returns the new length of the array.
![ekLjVH.png](https://s2.ax1x.com/2019/07/23/ekLjVH.png)

#### Syntax
![ekO9RP.png](https://s2.ax1x.com/2019/07/23/ekO9RP.png)

###### Parameters
&nbsp;&nbsp;<strong>elementN</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;The elements to add to the front of the array.<br/>

###### Return Value
&nbsp;&nbsp;The new length property of the object upon which the method was called.

#### Description
The <strong>unshift</strong> method inserts the given values to the beginning of an array-like object.

<strong>unshift</strong> is intentionally generic; this method can be called or applied to objects resembling arrays. Objects which do not contain a <strong>length</strong> property reflecting the last in a series of consecutive, zero-based numerical properties may not behave in any meaningful manner.

Please note that, if multiple elements are passed as parameters, they're inserted in chunk at the beginning of the object, in the exact same order they were passed as parameters. Hence, calling unshift with <strong>n</strong> arguments <strong>once</strong>, or calling it <strong>n</strong> times with <strong>1</strong> argument (with a loop, for example), don't yield the same results. See example:
![ekOree.png](https://s2.ax1x.com/2019/07/23/ekOree.png)

#### Examples
![ekOsdH.png](https://s2.ax1x.com/2019/07/23/ekOsdH.png)

----------------------------------------------------------------------------
## Array.prototype.toString()
