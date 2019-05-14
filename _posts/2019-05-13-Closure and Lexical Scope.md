---
layout:     post
title:      Closure and Lexical Scope
subtitle:   Web Development学习笔记系列
date:       2019-05-13
author:     Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
    - Web Development
---


## Closure
`Closure` is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

## Lexical scope
`Lexical scope` is the scope defined at lexing time.

#### Lexing time
This digs into the mechanics of how `JavaScript` engine works. <br/>

Despite commonly being referred to as an interpreted language, `JavaScript` compiles code immediately before executing it. <br/>

For example the statement: `var a = 2;` is split into two separate steps at lexing time:
- `var a` &nbsp;This declares the variable in the scope, before code execution.
- `a = 2` &nbsp;This assigns the value 2 to the variable a, if it is found in the available scope.

The `lexing phase` of compilation determines where and how all identifiers are declared, and thus how they will be looked up during execution. <br/>
This is the same mechanism which results in “hoisting” variables. <br/>
The variables are not actually moved within the source code, the declarations simply occur during the lexing phase and so the `JavaScript` engine is aware of these before execution.

```js
function foo() {  // 'scope of foo' aka lexical scope for bar
   var memory = 'hello closure';
   return function bar() {
      console.log(memory);
   }
}

// returns the bar function and assigns it to the identifier 'closure';
const closure = foo();

closure(); // hello closure
```
> function scope of outer function === lexical scope of inner function.
