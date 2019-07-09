---
layout: post
title: Array
subtitle: Javascript Standard Built-in Object
date: 2019-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - JavaScript
---



## Title
1. [forEach](#forEach)
2. [map](#map)
3. [reduce](#reduce)
4. [from](#from)
5. [sort](#sort)

----------------------------------------------------------------------------
## forEach
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
## map
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

## reduce
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

## from
#### Definition
&ensp;&ensp;The <ins>***Array.from&#40;&#41;***</ins> method creates a new, shallow-copied <ins>***Array***</ins> instance from an array-like or iterable object.

Array.from() lets you create Arrays from:
* array-like objects (objects with a length property and indexed elements)
* iterable objects (objects where you can get its elements, such as Map and Set).

`Array.from()` has an optional parameter `mapFn`, which allows you to execute a `map` function on each element of the array (or subclass object) that is being created. More clearly, `Array.from(obj, mapFn, thisArg)` has the same result as `Array.from(obj).map(mapFn, thisArg)`, except that it does not create an intermediate array. This is especially important for certain array subclasses, like typed arrays, since the intermediate array would necessarily have values truncated to fit into the appropriate type.

The `length` property of the `from()` method is 1.

#### Syntax
`Array.from(arrayLike [, mapFn[, thisArg ] ] )`

##### Parameters
**arrayLike**<br/>
* Required.<br/>
* An array-like or iterable object to convert to an array.<br/>

**mapFn** <br/>
* Optional. <br/>
* Map function to call on every element of the array.<br/>

**thisArg** <br/>
* Optional.<br/>
* Value to use as `this` when executing `mapFn`.<br/>

##### Return value
A new `Array` instance.

#### Usage
#### Basic
```
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

#### Array from a String
```
Array.from('foo');
// [ "f", "o", "o" ]
```

#### Array from a Set
```
const set = new Set(['foo', 'bar', 'baz', 'foo']);
Array.from(set);
// [ "foo", "bar", "baz" ]
```

#### Array from a Map
```
const map = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(map);
// [[1, 2], [2, 4], [4, 8]]

const mapper = new Map([['1', 'a'], ['2', 'b']]);
Array.from(mapper.values());
// ['a', 'b'];

Array.from(mapper.keys());
// ['1', '2'];
```

#### Array from an Array-like object (arguments)
```
function f() {
  return Array.from(arguments);
}

f(1, 2, 3);

// [ 1, 2, 3 ]
```

#### Using arrow functions and Array.from
```
// Using an arrow function as the map function to
// manipulate the elements
Array.from([1, 2, 3], x => x + x);      
// [2, 4, 6]


// Generate a sequence of numbers
// Since the array is initialized with `undefined` on each position,
// the value of `v` below will be `undefined`
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

----------------------------------------------------------------------------

## sort
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
