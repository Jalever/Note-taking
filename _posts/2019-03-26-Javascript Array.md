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
<strong>arrayLike</strong><br/>
An array-like or iterable object to convert to an array.

<strong>mapFn</strong><br/>
Optional<br/>
Map function to call on every element of the array.

<strong>thisArg</strong><br/>
Optional<br/>
Value to use as `this` when executing `mapFn`.

###### Return Value
A new Array instance.

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
