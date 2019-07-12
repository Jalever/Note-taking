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
![Zc6ow9.png](https://s2.ax1x.com/2019/07/10/Zc6ow9.png)

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
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to start copying elements from. If negative, <strong>start</strong> will be counted from the end.
&nbsp;&nbsp;&nbsp;&nbsp;If <strong>start</strong> is omitted, <strong>copyWithin</strong> will copy from index 0.


&nbsp;&nbsp;<strong>end</strong><br/>
&nbsp;&nbsp;&nbsp;&nbsp;Optional<br/>
&nbsp;&nbsp;&nbsp;&nbsp;Zero-based index at which to end copying elements from. <strong>copyWithin</strong> copies up to but not including <strong>end</strong>. If negative, <strong>end</strong> will be counted from the end.
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
## Array.prototype.forEach()
#### Definition
&ensp;&ensp;The forEach() method calls a provided function once for each element in an array, in order.
> Note: forEach() does not execute the function for array elements without values.

#### Syntax
`array.forEach( function( currentValue, index, arr ), thisValue )`

**currentValue**<br/>
* Required.<br/>
* The value of the current element<br/>

**index** <br/>
* Optional. <br/>
* The array index of the current element<br/>

**arr** <br/>
* Optional.<br/>
* The array object the current element belongs to<br/>

**function( currentValue, index, arr )**<br/>
* Required. <br/>
* A function to be run for each element in the array.<br/>

**thisValue**<br/>
* Optional. <br/>
* A value to be passed to the function to be used as its "this" value.
* If this parameter is empty, the value "undefined" will be passed as its "this" value<br/>

#### Usage
```
const numbers = [4, 9, 16, 25];
numbers.forEach( (currentValue, index, arr) => {
	console.log("index[" + index + "]: " + currentValue);
} );
//expected output:
// index[0]: 4
// index[1]: 9
// index[2]: 16
// index[3]: 25
```
----------------------------------------------------------------------------
## Array.prototype.map()
#### Definition
&ensp;&ensp;The map() method creates a new array with the results of calling a function for every array element.<br/>
&ensp;&ensp;The map() method calls the provided function once for each element in an array, in order.<br/>
> Note: map() does not execute the function for array elements without values.<br/>
> Note: map() does not change the original array.

#### Syntax
`array.forEach( function( currentValue, index, arr ), thisValue )`

**currentValue**<br/>
* Required.<br/>
* The value of the current element<br/>

**index** <br/>
* Optional. <br/>
* The array index of the current element<br/>

**arr** <br/>
* Optional.<br/>
* The array object the current element belongs to<br/>

**function( currentValue, index, arr )**<br/>
* Required. <br/>
* A function to be run for each element in the array.<br/>

**thisValue**<br/>
* Optional. <br/>
* A value to be passed to the function to be used as its "this" value.
* If this parameter is empty, the value "undefined" will be passed as its "this" value<br/>

#### Usage
```
const numbers = [43,222,32,1];
numbers.forEach( (currentValue, index, arr) => {
	console.log("index[" + index + "]: " + currentValue);
} );
//expected output:
// index[0]: 43
// index[1]: 222
// index[2]: 32
// index[3]: 1
```

----------------------------------------------------------------------------

## Array.prototype.reduce()
#### Definition
&ensp;&ensp;The reduce() method reduces the array to a single value.
&ensp;&ensp;The reduce() method executes a provided function for each value of the array (from left-to-right).
&ensp;&ensp;The return value of the function is stored in an accumulator (result/total).
> Note: reduce() does not execute the function for array elements without values.

#### Syntax
`array.reduce( function( total, currentValue, currentIndex, arr ), initialValue )`

**total**<br/>
* Required.<br/>
* The initialValue, or the previously returned value of the function<br/>

**currentValue** <br/>
* Required. <br/>
* The value of the current element<br/>

**currentIndex** <br/>
* Optional.<br/>
* The array index of the current element<br/>

**arr**<br/>
* Optional. <br/>
* The array object the current element belongs to.<br/>

**function( total, currentValue, currentIndex, arr )**<br/>
* Required. <br/>
* A function to be run for each element in the array.<br/>

**initialValue**<br/>
* Optional.<br/>
* A value to be passed to the function as the initial value.<br/>

#### Usage
```
const numbers = [33,54,6,7,42,58];

var sum = numbers.reduce( (total, currentValue, currentIndex, arr) => {
	return total + currentValue;
} );

console.log("Sum: " + sum);
//expected output:
//Sum: 200
```

----------------------------------------------------------------------------

## Array.prototype.sort()
#### Definition
&ensp;&ensp;The sort() method sorts the elements of an array in place and returns the array.<br/>

&ensp;&ensp;The default sort order is built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.
If compareFunction is not supplied, all non-undefined array elements are sorted by converting them to strings and comparing strings in UTF-16 code units order. <br/>

For example, "banana" comes before "cherry". In a numeric sort, 9 comes before 80, but because numbers are converted to strings, "80" comes before "9" in Unicode order.<br/>

All `undefined` elements are sorted to the end of the array.<br/>

If `compareFunction` is supplied, all `non-undefined` array elements are sorted according to the return value of the compare function (all `undefined` elements are sorted to the end of the array, with no call to `compareFunction`).

If `a` and `b` are two elements being compared, then:

* If `compareFunction(a, b)` is less than 0, sort `a` to an index lower than `b` (i.e. a comes first).
	* ( a, b ) &#60; 0 =>  a, b

* If `compareFunction(a, b)` returns 0, leave `a` and `b` unchanged with respect to each other, but sorted with respect to all different elements.

* If `compareFunction(a, b)` is greater than 0, sort `b` to an index lower than `a` (i.e. b comes first).
	* ( a, b ) &#62; 0 =>  b, a

#### Syntax
##### Parameters
* compareFunction
Specifies a function that defines the sort order.<br/>
If omitted, the array is sorted according to each character's Unicode code point value, according to the string conversion of each element.  <br/>
	* firstEl
		* The first element for comparison.
	* secondEl
		* The second element for comparison.

##### Return value
The sorted array.
> Note that the array is sorted in place, and no copy is made.

#### Usage
```
var months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

var array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```
---
