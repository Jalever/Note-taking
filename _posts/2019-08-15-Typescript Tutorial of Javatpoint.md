---
layout: post
title: Typescript Handbook
subtitle: Wrap up of Typescript Handbook
date: 2019-08-15
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Typescript
---

- [Typescript Type](#typescript-type)
- [Generic](#generic)
- [Functions](#functions)
- [Enum](#enum)
- [Type Inference](#type-inference)
- [Type Compatibility](#type-compatibility)

## Typescript Type
The TypeScript language supports different types of values. It provides data types for the JavaScript to transform it into a strongly typed programing language. JavaScript doesn't support data types, but with the help of TypeScript, we can use the data types feature in JavaScript. TypeScript plays an important role when the object-oriented programmer wants to use the type feature in any scripting language or object-oriented programming language. The Type System checks the validity of the given values before the program uses them. It ensures that the code behaves as expected.

TypeScript provides data types as an optional Type System. We can classify the TypeScript data type as following.
![mEmHI0.png](https://s2.ax1x.com/2019/08/15/mEmHI0.png)

#### Static Types
In the context of type systems, static types mean "at compile time" or "without running a program." In a statically typed language, variables, parameters, and objects have types that the compiler knows at compile time. The compiler used this information to perform the type checking.

Static types can be further divided into two sub-categories:

###### Built-in or Primitive Type
The TypeScript has five built-in data types, which are given below.
![mEnneA.png](https://s2.ax1x.com/2019/08/15/mEnneA.png)

<strong>Number</strong><br/>
Like JavaScript, all the numbers in TypeScript are stored as floating-point values. These numeric values are treated like a number data type. The numeric data type can be used to represents both integers and fractions. TypeScript also supports Binary(Base 2), Octal(Base 8), Decimal(Base 10), and Hexadecimal(Base 16) literals.
![mEKZVA.png](https://s2.ax1x.com/2019/08/15/mEKZVA.png)

<strong>String</strong><br/>
We will use the string data type to represents the text in TypeScript. String type work with textual data. We include string literals in our scripts by enclosing them in single or double quotation marks. It also represents a sequence of Unicode characters. It embedded the expressions in the form of <strong>$&#123;expr&#125;</strong>.
![mEMneJ.png](https://s2.ax1x.com/2019/08/15/mEMneJ.png)

<strong>Boolean</strong><br/>
The string and numeric data types can have an unlimited number of different values, whereas the Boolean data type can have only two values. They are "true" and "false." A Boolean value is a truth value which specifies whether the condition is true or not.
![mEMbm4.png](https://s2.ax1x.com/2019/08/15/mEMbm4.png)

<strong>Void</strong><br/>
A void is a return type of the functions which do not return any type of value. It is used where no data type is available. A variable of type void is not useful because we can only assign undefined or null to them. An undefined data type denotes uninitialized variable, whereas null represents a variable whose value is undefined.
![mEl1KO.png](https://s2.ax1x.com/2019/08/15/mEl1KO.png)

<strong>Null</strong><br/>
Null represents a variable whose value is undefined. Much like the void, it is not extremely useful on its own. The Null accepts the only one value, which is null. The Null keyword is used to define the Null type in TypeScript, but it is not useful because we can only assign a null value to it.
![mElqiR.png](https://s2.ax1x.com/2019/08/15/mElqiR.png)

###### Undefined
The Undefined primitive type denotes all uninitialized variables in TypeScript and JavaScript. It has only one value, which is undefined. The undefined keyword defines the undefined type in TypeScript, but it is not useful because we can only assign an undefined value to it.
![mE1wk9.png](https://s2.ax1x.com/2019/08/15/mE1wk9.png)

###### Any Type
It is the "super type" of all data type in TypeScript. It is used to represents any JavaScript value. It allows us to opt-in and opt-out of type-checking during compilation. If a variable cannot be represented in any of the basic data types, then it can be declared using "<strong>Any</strong>" data type. Any type is useful when we do not know about the type of value (which might come from an API or 3rd party library), and we want to skip the type-checking on compile time.
![mE3F74.png](https://s2.ax1x.com/2019/08/15/mE3F74.png)

###### User-Defined DataType
TypeScript supports the following user-defined data types:
![mE8C8I.png](https://s2.ax1x.com/2019/08/15/mE8C8I.png)

<strong>Array</strong><br/>
An array is a collection of elements of the same data type. Like JavaScript, TypeScript also allows us to work with arrays of values. An array can be written in two ways:

1.Use the type of the elements followed by [] to denote an array of that element type:
![mEGuwD.png](https://s2.ax1x.com/2019/08/15/mEGuwD.png)
2.The second way uses a generic array type:
![mEGaTg.png](https://s2.ax1x.com/2019/08/15/mEGaTg.png)

<strong>Touple</strong><br/>
The Tuple is a data type which includes two sets of values of different data types. It allows us to express an array where the type of a fixed number of elements is known, but they are not the same. For example, if we want to represent a value as a pair of a number and a string, then it can be written as:
![mEGvhd.png](https://s2.ax1x.com/2019/08/15/mEGvhd.png)

<strong>Interface</strong><br/>
An Interface is a structure which acts as a contract in our application. It defines the syntax for classes to follow, means a class which implements an interface is bound to implement all its members. It cannot be instantiated but can be referenced by the class which implements it. The TypeScript compiler uses interface for type-checking that is also known as "duck typing" or "structural subtyping."
![mEJjbT.png](https://s2.ax1x.com/2019/08/15/mEJjbT.png)

<strong>Class</strong><br/>
Classes are used to create reusable components and acts as a template for creating objects. It is a logical entity which store variables and functions to perform operations. TypeScript gets support for classes from ES6. It is different from the interface which has an implementation inside it, whereas an interface does not have any implementation inside it.
![mEYMRA.png](https://s2.ax1x.com/2019/08/15/mEYMRA.png)

<strong>Enums</strong><br/>
Enums define a set of named constant. TypeScript provides both string-based and numeric-based enums. By default, enums begin numbering their elements starting from 0, but we can also change this by manually setting the value to one of its elements. TypeScript gets support for enums from ES6.
![mEY7dO.png](https://s2.ax1x.com/2019/08/15/mEY7dO.png)

<strong>Functions</strong><br/>
A function is the logical blocks of code to organize the program. Like JavaScript, TypeScript can also be used to create functions either as a <strong>named function</strong> or as an <strong>anonymous function</strong>. Functions ensure that our program is readable, maintainable, and reusable. A function declaration has a function's name, return type, and parameters.
![mEtVln.png](https://s2.ax1x.com/2019/08/15/mEtVln.png)

#### Generics
Generic is used to create a component which can work with a variety of data type rather than a single one. It allows a way to create reusable components. It ensures that the program is flexible as well as scalable in the long term. TypeScript uses generics with the type variable &lt;T&gt; that denotes types. The type of generic functions is just like non-generic functions, with the type parameters listed first, similarly to function declarations.
![mEtU0K.png](https://s2.ax1x.com/2019/08/15/mEtU0K.png)

#### Decorators
A decorator is a special of data type which can be attached to a <strong>class declaration</strong>, <strong>method</strong>, <strong>property</strong>, <strong>accessor</strong>, and <strong>parameter</strong>. It provides a way to add both annotations and a meta-programing syntax for classes and functions. It is used with "@" symbol.

A decorator is an experimental feature which may change in future releases. To enable support for the decorator, we must enable the <strong>experimentalDecorators</strong> compiler option either on the <strong>command line</strong> or in our <strong>tsconfig.json</strong>.

## Generics
- [Introduction](#introduction)
- [Hello World of Generics](#hello-world-of-generics)
- [Working with Generic Type Variables](#working-with-generic-type-variables)
- [Generic Types](#generic-types)
- [Generic Classes](#generic-classes)
- [Generic Constraints](#generic-constraints)
    - [Using Type Parameters in Generic Constraints](#using-type-parameters-in-generic-constraints)
    - [Using Class Types in Generics](#using-class-types-in-generics)
    - [Generic Constraints](#generic-constraints)

#### Introduction
A major part of software engineering is building components that not only have well-defined and consistent APIs, but are also reusable. Components that are capable of working on the data of today as well as the data of tomorrow will give you the most flexible capabilities for building up large software systems.

In languages like C# and Java, one of the main tools in the toolbox for creating reusable components is generics, that is, being able to create a component that can work over a variety of types rather than a single one. This allows users to consume these components and use their own types

#### Hello World of Generics
To start off, let’s do the “hello world” of generics: the identity function. The identity function is a function that will return back whatever is passed in. You can think of this in a similar way to the <em><ins>echo</ins></em> command.

Without generics, we would either have to give the identity function a specific type:
![mE2G1x.png](https://s2.ax1x.com/2019/08/15/mE2G1x.png)
Or, we could describe the identity function using the <em><ins>any</ins></em> type:
![mE2gu8.png](https://s2.ax1x.com/2019/08/15/mE2gu8.png)
While using <em><ins>any</ins></em> is certainly generic in that it will cause the function to accept any and all types for the type of <em><ins>arg</ins></em>, we actually are losing the information about what that type was when the function returns. If we passed in a number, the only information we have is that any type could be returned.

Instead, we need a way of capturing the type of the argument in such a way that we can also use it to denote what is being returned. Here, we will use a <em><ins>type variable</ins></em>, a special kind of variable that works on types rather than values.
![mERQr8.png](https://s2.ax1x.com/2019/08/15/mERQr8.png)
We’ve now added a type variable <em><ins>T</ins></em> to the identity function. This <em><ins>T</ins></em> allows us to capture the type the user provides (e.g. <em><ins>number</ins></em>), so that we can use that information later. Here, we use <em><ins>T</ins></em> again as the return type. On inspection, we can now see the same type is used for the argument and the return type. This allows us to traffic that type information in one side of the function and out the other.

We say that this version of the <em><ins>identity</ins></em> function is generic, as it works over a range of types. Unlike using <em><ins>any</ins></em>, it’s also just as precise (ie, it doesn’t lose any information) as the first <em><ins>identity</ins></em> function that used numbers for the argument and return type.

Once we’ve written the generic identity function, we can call it in one of two ways. The first way is to pass all of the arguments, including the type argument, to the function:
![mEfICd.png](https://s2.ax1x.com/2019/08/15/mEfICd.png)
Here we explicitly set <em><ins>T</ins></em> to be <em><ins>string</ins></em> as one of the arguments to the function call, denoted using the &lt;&gt; around the arguments rather than <em><ins>()</ins></em>.

The second way is also perhaps the most common. Here we use type <em><ins>argument inference</ins></em> – that is, we want the compiler to set the value of <em><ins>T</ins></em> for us automatically based on the type of the argument we pass in:
![mEhMKx.png](https://s2.ax1x.com/2019/08/15/mEhMKx.png)
Notice that we didn’t have to explicitly pass the type in the angle brackets (<em><ins>&lt;&gt;</ins></em>); the compiler just looked at the value "<em><ins>myString</ins></em>", and set <em><ins>T</ins></em> to its type. While type argument inference can be a helpful tool to keep code shorter and more readable, you may need to explicitly pass in the type arguments as we did in the previous example when the compiler fails to infer the type, as may happen in more complex examples

#### Working with Generic Type Variables
When you begin to use generics, you’ll notice that when you create generic functions like <em><ins>identity</ins></em>, the compiler will enforce that you use any generically typed parameters in the body of the function correctly. That is, that you actually treat these parameters as if they could be any and all types.

Let’s take our <em><ins>identity</ins></em> function from earlier:
![mETLbq.png](https://s2.ax1x.com/2019/08/15/mETLbq.png)
What if we want to also log the length of the argument <em><ins>arg</ins></em> to the console with each call? We might be tempted to write this:
![mE76iT.png](https://s2.ax1x.com/2019/08/15/mE76iT.png)
When we do, the compiler will give us an error that we’re using the <em><ins>.length</ins></em> member of <em><ins>arg</ins></em>, but nowhere have we said that <em><ins>arg</ins></em> has this member. Remember, we said earlier that these type variables stand in for any and all types, so someone using this function could have passed in a <em><ins>number</ins></em> instead, which does not have a <em><ins>.length</ins></em> member.

Let’s say that we’ve actually intended this function to work on arrays of <em><ins>T</ins></em> rather than <em><ins>T</ins></em> directly. Since we’re working with arrays, the <em><ins>.length</ins></em> member should be available. We can describe this just like we would create arrays of other types:
![mE7hLR.png](https://s2.ax1x.com/2019/08/15/mE7hLR.png)
You can read the type of <em><ins>loggingIdentity</ins></em> as “the generic function <em><ins>loggingIdentity</ins></em> takes a type parameter <em><ins>T</ins></em>, and an argument <em><ins>arg</ins></em> which is an array of <em><ins>T</ins></em>s, and returns an array of <em><ins>T</ins></em>s.” If we passed in an array of numbers, we’d get an array of numbers back out, as <em><ins>T</ins></em> would bind to <em><ins>number</ins></em>. This allows us to use our generic type variable <em><ins>T</ins></em> as part of the types we’re working with, rather than the whole type, giving us greater flexibility.

We can alternatively write the sample example this way:
![mE7HJO.png](https://s2.ax1x.com/2019/08/15/mE7HJO.png)

#### Generic Types
In previous sections, we created generic identity functions that worked over a range of types. In this section, we’ll explore the type of the functions themselves and how to create generic interfaces.

The type of generic functions is just like those of non-generic functions, with the type parameters listed first, similarly to function declarations:
![mEqooq.png](https://s2.ax1x.com/2019/08/15/mEqooq.png)
We could also have used a different name for the generic type parameter in the type, so long as the number of type variables and how the type variables are used line up.
![mELynJ.png](https://s2.ax1x.com/2019/08/15/mELynJ.png)
We can also write the generic type as a call signature of an object literal type:
![mEL6B9.png](https://s2.ax1x.com/2019/08/15/mEL6B9.png)
Which leads us to writing our first generic interface. Let’s take the object literal from the previous example and move it to an interface:
![mEO8C6.png](https://s2.ax1x.com/2019/08/15/mEO8C6.png)
In a similar example, we may want to move the generic parameter to be a parameter of the whole interface. This lets us see what type(s) we’re generic over (e.g. <strong>Dictionary&lt;string&gt;</strong> rather than just <strong>Dictionary</strong>). This makes the type parameter visible to all the other members of the interface.
![mEXRSK.png](https://s2.ax1x.com/2019/08/15/mEXRSK.png)
Notice that our example has changed to be something slightly different. Instead of describing a generic function, we now have a non-generic function signature that is a part of a generic type. When we use <strong>GenericIdentityFn</strong>, we now will also need to specify the corresponding type argument (here: <strong>number</strong>), effectively locking in what the underlying call signature will use. Understanding when to put the type parameter directly on the call signature and when to put it on the interface itself will be helpful in describing what aspects of a type are generic.

In addition to generic interfaces, we can also create generic classes. Note that it is not possible to create generic enums and namespaces

#### Generic Classes
A generic class has a similar shape to a generic interface. Generic classes have a generic type parameter list in angle brackets (&lt;&gt;) following the name of the class.
![mZpEEF.png](https://s2.ax1x.com/2019/08/16/mZpEEF.png)
This is a pretty literal use of the <strong>GenericNumber</strong> class, but you may have noticed that nothing is restricting it to only use the <strong>number</strong> type. We could have instead used <strong>string</strong> or even more complex objects.
![mZpn3R.png](https://s2.ax1x.com/2019/08/16/mZpn3R.png)
Just as with interface, putting the type parameter on the class itself lets us make sure all of the properties of the class are working with the same type.

As we covered in our section on classes, a class has two sides to its type: the static side and the instance side. Generic classes are only generic over their instance side rather than their static side, so when working with classes, static members can not use the class’s type parameter

#### Generic Constraints
###### Using Type Parameters in Generic Constraints
If you remember from an earlier example, you may sometimes want to write a generic function that works on a set of types where you have some knowledge about what capabilities that set of types will have. In our <strong>loggingIdentity</strong> example, we wanted to be able to access the <strong>.length</strong> property of <strong>arg</strong>, but the compiler could not prove that every type had a <strong>.length</strong> property, so it warns us that we can’t make this assumption.
![mZpzVO.png](https://s2.ax1x.com/2019/08/16/mZpzVO.png)
Instead of working with any and all types, we’d like to constrain this function to work with any and all types that also have the <strong>.length</strong> property. As long as the type has this member, we’ll allow it, but it’s required to have at least this member. To do so, we must list our requirement as a constraint on what T can be.

To do so, we’ll create an interface that describes our constraint. Here, we’ll create an interface that has a single <strong>.length</strong> property and then we’ll use this interface and the <strong>extends</strong> keyword to denote our constraint:
![mZ9SaD.png](https://s2.ax1x.com/2019/08/16/mZ9SaD.png)
Because the generic function is now constrained, it will no longer work over any and all types:
![mZ9AMt.png](https://s2.ax1x.com/2019/08/16/mZ9AMt.png)
Instead, we need to pass in values whose type has all the required properties:
![mZ9Vqf.png](https://s2.ax1x.com/2019/08/16/mZ9Vqf.png)

###### Using Class Types in Generics
You can declare a type parameter that is constrained by another type parameter. For example, here we’d like to get a property from an object given its name. We’d like to ensure that we’re not accidentally grabbing a property that does not exist on the <strong>obj</strong>, so we’ll place a constraint between the two types:
![mZPavR.png](https://s2.ax1x.com/2019/08/16/mZPavR.png)

#### Generic Constraints
When creating factories in TypeScript using generics, it is necessary to refer to class types by their constructor functions. For example,
![mZinIO.png](https://s2.ax1x.com/2019/08/16/mZinIO.png)
A more advanced example uses the prototype property to infer and constrain relationships between the constructor function and the instance side of class types.
![mZilzd.png](https://s2.ax1x.com/2019/08/16/mZilzd.png)

## Functions

- [Introduction](#introduction)
- [Functions](#functions)
- [Function Types](#function-types)
    - [Typing the function](#typing-the-function)
    - [Writing the function type](#writing-the-function-type)
    - [Inferring the types](#inferring-the-types)
- [Optional and Default Parameters](#optional-and-default-parameters)
- [Rest Parameters](#rest-parameters)
- [this](#this)
    - [this and arrow functions](#this-and-arrow-functions)
    - [this parameters](#this-parameters)
    - [this parameters in callbacks](#this-parameters-in-callbacks)
- [Overloads](#overloads)

#### Introduction
Functions are the fundamental building block of any application in JavaScript. They’re how you build up layers of abstraction, mimicking classes, information hiding, and modules. In TypeScript, while there are classes, namespaces, and modules, functions still play the key role in describing how to <strong><ins>do</ins></strong> things. TypeScript also adds some new capabilities to the standard JavaScript functions to make them easier to work with.

#### Functions
To begin, just as in JavaScript, TypeScript functions can be created both as a named function or as an anonymous function. This allows you to choose the most appropriate approach for your application, whether you’re building a list of functions in an API or a one-off function to hand off to another function.

To quickly recap what these two approaches look like in JavaScript:
![mepL6I.png](https://s2.ax1x.com/2019/08/16/mepL6I.png)
Just as in JavaScript, functions can refer to variables outside of the function body. When they do so, they’re said to <strong><ins>capture</ins></strong> these variables. While understanding how this works (and the trade-offs when using this technique) is outside of the scope of this article, having a firm understanding how this mechanic works is an important piece of working with JavaScript and TypeScript.
![me9En0.png](https://s2.ax1x.com/2019/08/16/me9En0.png)

#### Function Types
###### Typing the function
Let’s add types to our simple examples from earlier:
![me91j1.png](https://s2.ax1x.com/2019/08/16/me91j1.png)
We can add types to each of the parameters and then to the function itself to add a return type. TypeScript can figure the return type out by looking at the return statements, so we can also optionally leave this off in many cases.

###### Writing the function type
Now that we’ve typed the function, let’s write the full type of the function out by looking at each piece of the function type.
![meCMa8.png](https://s2.ax1x.com/2019/08/16/meCMa8.png)
A function’s type has the same two parts: the type of the arguments and the return type. When writing out the whole function type, both parts are required. We write out the parameter types just like a parameter list, giving each parameter a name and a type. This name is just to help with readability. We could have instead written:
![meCYMn.png](https://s2.ax1x.com/2019/08/16/meCYMn.png)
As long as the parameter types line up, it’s considered a valid type for the function, regardless of the names you give the parameters in the function type.

The second part is the return type. We make it clear which is the return type by using a fat arrow (<strong>=></strong>) between the parameters and the return type. As mentioned before, this is a required part of the function type, so if the function doesn’t return a value, you would use <strong>void</strong> instead of leaving it off.

Of note, only the parameters and the return type make up the function type. Captured variables are not reflected in the type. In effect, captured variables are part of the “hidden state” of any function and do not make up its API

###### Inferring the types
In playing with the example, you may notice that the TypeScript compiler can figure out the type even if you only have types on one side of the equation:
![meCrRJ.png](https://s2.ax1x.com/2019/08/16/meCrRJ.png)
This is called “contextual typing”, a form of type inference. This helps cut down on the amount of effort to keep your program typed.

#### Optional and Default Parameters
In TypeScript, every parameter is assumed to be required by the function. This doesn’t mean that it can’t be given <strong>null</strong> or <strong>undefined</strong>, but rather, when the function is called, the compiler will check that the user has provided a value for each parameter. The compiler also assumes that these parameters are the only parameters that will be passed to the function. In short, the number of arguments given to a function has to match the number of parameters the function expects.
![mei0gJ.png](https://s2.ax1x.com/2019/08/16/mei0gJ.png)
In JavaScript, every parameter is optional, and users may leave them off as they see fit. When they do, their value is <strong>undefined</strong>. We can get this functionality in TypeScript by adding a <strong>?</strong> to the end of parameters we want to be optional. For example, let’s say we want the last name parameter from above to be optional:
![meivvj.png](https://s2.ax1x.com/2019/08/16/meivvj.png)
Any optional parameters must follow required parameters. Had we wanted to make the first name optional, rather than the last name, we would need to change the order of parameters in the function, putting the first name last in the list.

In TypeScript, we can also set a value that a parameter will be assigned if the user does not provide one, or if the user passes <strong>undefined</strong> in its place. These are called default-initialized parameters. Let’s take the previous example and default the last name to "<strong>Smith</strong>".
![meFPaV.png](https://s2.ax1x.com/2019/08/16/meFPaV.png)
Default-initialized parameters that come after all required parameters are treated as optional, and just like optional parameters, can be omitted when calling their respective function. This means optional parameters and trailing default parameters will share commonality in their types, so both
![meFeM9.png](https://s2.ax1x.com/2019/08/16/meFeM9.png)
and
![meFQIK.png](https://s2.ax1x.com/2019/08/16/meFQIK.png)
share the same type <strong>(firstName: string, lastName?: string) => string</strong>. The default value of <strong>lastName</strong> disappears in the type, only leaving behind the fact that the parameter is optional.

Unlike plain optional parameters, default-initialized parameters don’t need to occur after required parameters. If a default-initialized parameter comes before a required parameter, users need to explicitly pass <strong>undefined</strong> to get the default initialized value. For example, we could write our last example with only a default initializer on <strong>firstName</strong>:
![meFYMd.png](https://s2.ax1x.com/2019/08/16/meFYMd.png)

#### Rest Parameters
Required, optional, and default parameters all have one thing in common: they talk about one parameter at a time. Sometimes, you want to work with multiple parameters as a group, or you may not know how many parameters a function will ultimately take. In JavaScript, you can work with the arguments directly using the <strong>arguments</strong> variable that is visible inside every function body.

In TypeScript, you can gather these arguments together into a variable:
![mekoAP.png](https://s2.ax1x.com/2019/08/16/mekoAP.png)
<strong><ins>Rest parameters</ins></strong> are treated as a boundless number of optional parameters. When passing arguments for a rest parameter, you can use as many as you want; you can even pass none. The compiler will build an array of the arguments passed in with the name given after the ellipsis(...), allowing you to use it in your function.

The ellipsis is also used in the type of the function with rest parameters:
![mekvBn.png](https://s2.ax1x.com/2019/08/16/mekvBn.png)

#### this
Learning how to use <strong>this</strong> in JavaScript is something of a rite of passage. Since TypeScript is a superset of JavaScript, TypeScript developers also need to learn how to use <strong>this</strong> and how to spot when it’s not being used correctly. Fortunately, TypeScript lets you catch incorrect uses of <strong>this</strong> with a couple of techniques.

###### this and arrow functions
In JavaScript, <strong>this</strong> is a variable that’s set when a function is called. This makes it a very powerful and flexible feature, but it comes at the cost of always having to know about the context that a function is executing in. This is notoriously confusing, especially when returning a function or passing a function as an argument.

Let’s look at an example:
![menu4I.png](https://s2.ax1x.com/2019/08/16/menu4I.png)
Notice that <strong>createCardPicker</strong> is a function that itself returns a function. If we tried to run the example, we would get an error instead of the expected alert box. This is because the <strong>this</strong> being used in the function created by <strong>createCardPicker</strong> will be set to <strong>window</strong> instead of our <strong>deck</strong> object. That’s because we call <strong>cardPicker()</strong> on its own. A top-level non-method syntax call like this will use <strong>window</strong> for <strong>this</strong>. (Note: under strict mode, this will be <strong>undefined</strong> rather than <strong>window</strong>).

We can fix this by making sure the function is bound to the correct <strong>this</strong> before we return the function to be used later. This way, regardless of how it’s later used, it will still be able to see the original <strong>deck</strong> object. To do this, we change the function expression to use the ECMAScript 6 arrow syntax. Arrow functions capture the <strong>this</strong> where the function is created rather than where it is invoked:
![men25R.png](https://s2.ax1x.com/2019/08/16/men25R.png)
Even better, TypeScript will warn you when you make this mistake if you pass the <strong>--noImplicitThis</strong> flag to the compiler. It will point out that <strong>this</strong> in <strong>this.suits&#91;pickedSuit&#93;</strong> is of type <strong>any</strong>.

###### this parameters
Unfortunately, the type of <strong>this.suits&#91;pickedSuit&#93;</strong> is still <strong>any</strong>. That’s because <strong>this</strong> comes from the function expression inside the object literal. To fix this, you can provide an explicit <strong>this</strong> parameter. <strong>this</strong> parameters are fake parameters that come first in the parameter list of a function:
![meKju8.png](https://s2.ax1x.com/2019/08/16/meKju8.png)
Let’s add a couple of interfaces to our example above, <strong>Card</strong> and <strong>Deck</strong>, to make the types clearer and easier to reuse:
![meM1v6.png](https://s2.ax1x.com/2019/08/16/meM1v6.png)
![meM8KK.png](https://s2.ax1x.com/2019/08/16/meM8KK.png)
Now TypeScript knows that <strong>createCardPicker</strong> expects to be called on a <strong>Deck</strong> object. That means that <strong>this</strong> is of type <strong>Deck</strong> now, not <strong>any</strong>, so <strong>--noImplicitThis</strong> will not cause any errors.

###### this parameters in callbacks
You can also run into errors with <strong>this</strong> in callbacks, when you pass functions to a library that will later call them. Because the library that calls your callback will call it like a normal function, <strong>this</strong> will be <strong>undefined</strong>. With some work you can use <strong>this</strong> parameters to prevent errors with callbacks too. First, the library author needs to annotate the callback type with <strong>this</strong>:
![mes1kd.png](https://s2.ax1x.com/2019/08/16/mes1kd.png)
<strong>this: void</strong> means that <strong>addClickListener</strong> expects <strong>onclick</strong> to be a function that does not require a <strong>this</strong> type. Second, annotate your calling code with <strong>this</strong>:
![me6WFJ.png](https://s2.ax1x.com/2019/08/16/me6WFJ.png)
With <strong>this</strong> annotated, you make it explicit that <strong>onClickBad</strong> must be called on an instance of <strong>Handler</strong>. Then TypeScript will detect that <strong>addClickListener</strong> requires a function that has <strong>this: void</strong>. To fix the error, change the type of <strong>this</strong>:
![me6XYd.png](https://s2.ax1x.com/2019/08/16/me6XYd.png)
Because <strong>onClickGood</strong> specifies its <strong>this</strong> type as <strong>void</strong>, it is legal to pass to <strong>addClickListener</strong>. Of course, this also means that it can’t use <strong>this.info</strong>. If you want both then you’ll have to use an arrow function:
![mecEfs.png](https://s2.ax1x.com/2019/08/16/mecEfs.png)
This works because arrow functions use the outer <strong>this</strong>, so you can always pass them to something that expects <strong>this: void</strong>. The downside is that one arrow function is created per object of type Handler. Methods, on the other hand, are only created once and attached to Handler’s prototype. They are shared between all objects of type Handler.

#### Overloads  
JavaScript is inherently a very dynamic language. It’s not uncommon for a single JavaScript function to return different types of objects based on the shape of the arguments passed in.
![megjMt.png](https://s2.ax1x.com/2019/08/16/megjMt.png)
![megxqf.png](https://s2.ax1x.com/2019/08/16/megxqf.png)
Here, the <strong>pickCard</strong> function will return two different things based on what the user has passed in. If the users passes in an object that represents the deck, the function will pick the card. If the user picks the card, we tell them which card they’ve picked. But how do we describe this to the type system?

The answer is to supply multiple function types for the same function as a list of overloads. This list is what the compiler will use to resolve function calls. Let’s create a list of overloads that describe what our <strong>pickCard</strong> accepts and what it returns.
![me21zR.png](https://s2.ax1x.com/2019/08/16/me21zR.png)
![me2NdO.png](https://s2.ax1x.com/2019/08/16/me2NdO.png)
With this change, the overloads now give us type checked calls to the <strong>pickCard</strong> function.

In order for the compiler to pick the correct type check, it follows a similar process to the underlying JavaScript. It looks at the overload list and, proceeding with the first overload, attempts to call the function with the provided parameters. If it finds a match, it picks this overload as the correct overload. For this reason, it’s customary to order overloads from most specific to least specific.

Note that the <strong>function pickCard(x): any</strong> piece is not part of the overload list, so it only has two overloads: one that takes an object and one that takes a number. Calling <strong>pickCard</strong> with any other parameter types would cause an error.

## Enum
Enums allow us to define a set of named constants. Using enums can make it easier to document intent, or create a set of distinct cases. TypeScript provides both numeric and string-based enums.

#### Numeric enums
We’ll first start off with numeric enums, which are probably more familiar if you’re coming from other languages. An enum can be defined using the <strong>enum</strong> keyword.
![mudlP1.png](https://s2.ax1x.com/2019/08/17/mudlP1.png)
Above, we have a numeric enum where <strong>Up</strong> is initialized with <strong>1</strong>. All of the following members are auto-incremented from that point on. In other words, <strong>Direction.Up</strong> has the value <strong>1</strong>, <strong>Down</strong> has <strong>2</strong>, <strong>Left</strong> has <strong>3</strong>, and <strong>Right</strong> has <strong>4</strong>.

If we wanted, we could leave off the initializers entirely:
![mud18x.png](https://s2.ax1x.com/2019/08/17/mud18x.png)
Here, <strong>Up</strong> would have the value <strong>0</strong>, <strong>Down</strong> would have <strong>1</strong>, etc. This auto-incrementing behavior is useful for cases where we might not care about the member values themselves, but do care that each value is distinct from other values in the same enum.

Using an enum is simple: just access any member as a property off of the enum itself, and declare types using the name of the enum:
![mu0phn.png](https://s2.ax1x.com/2019/08/17/mu0phn.png)
Numeric enums can be mixed in computed and constant members (see below). The short story is, enums without initializers either need to be first, or have to come after numeric enums initialized with numeric constants or other constant enum members. In other words, the following isn’t allowed:
![muDQeO.png](https://s2.ax1x.com/2019/08/17/muDQeO.png)

#### String enums
String enums are a similar concept, but have some subtle runtime differences as documented below. In a string enum, each member has to be constant-initialized with a string literal, or with another string enum member.
![murN4J.png](https://s2.ax1x.com/2019/08/17/murN4J.png)
While string enums don’t have auto-incrementing behavior, string enums have the benefit that they “serialize” well. In other words, if you were debugging and had to read the runtime value of a numeric enum, the value is often opaque - it doesn’t convey any useful meaning on its own (though Reverse Mapping can often help), string enums allow you to give a meaningful and readable value when your code runs, independent of the name of the enum member itself.

#### Heterogeneous enums
Technically enums can be mixed with string and numeric members, but it’s not clear why you would ever want to do so:
![mur7VS.png](https://s2.ax1x.com/2019/08/17/mur7VS.png)
Unless you’re really trying to take advantage of JavaScript’s runtime behavior in a clever way, it’s advised that you don’t do this.

#### Computed and constant members
Each enum member has a value associated with it which can be either constant or computed. An enum member is considered constant if:

- It is the first member in the enum and it has no initializer, in which case it’s assigned the value <strong>0</strong>:
![mus0iQ.png](https://s2.ax1x.com/2019/08/17/mus0iQ.png)
- It does not have an initializer and the preceding enum member was a numeric constant. In this case the value of the current enum member will be the value of the preceding enum member plus one.
![musDRs.png](https://s2.ax1x.com/2019/08/17/musDRs.png)
- The enum member is initialized with a constant enum expression. A constant enum expression is a subset of TypeScript expressions that can be fully evaluated at compile time. An expression is a constant enum expression if it is:

1. a literal enum expression (basically a string literal or a numeric literal)
2. a reference to previously defined constant enum member (which can originate from a different enum)
3. a parenthesized constant enum expression
4. one of the <strong><ins>&plus;</ins></strong>, <strong><ins>&minus;</ins></strong>, <strong><ins>&sim;</ins></strong> unary operators applied to constant enum expression
5. <strong><ins>&sol;</ins></strong>, <strong><ins>&minus;</ins></strong>, <strong><ins>&ast;</ins></strong>, <strong><ins>&sol;</ins></strong>, <strong><ins>&percnt;</ins></strong>, <strong><ins>&lt;&lt;</ins></strong>, <strong><ins>&gt;&gt;</ins></strong>, <strong><ins>&gt;&gt;&gt;</ins></strong>, <strong><ins>&amp;</ins></strong>, <strong><ins>&verbar;</ins></strong>, <strong><ins>&Hat;</ins></strong> binary operators with constant enum expressions as operands

&npsp;&npsp;It is a compile time error for constant enum expressions to be evaluated to NaN or Infinity.

In all other cases enum member is considered computed.
![muyg1A.png](https://s2.ax1x.com/2019/08/17/muyg1A.png)

#### Union enums and enum member types
There is a special subset of constant enum members that aren’t calculated: literal enum members. A literal enum member is a constant enum member with no initialized value, or with values that are initialized to
- any string literal (e.g. "<strong>foo</strong>", <strong>"bar"</strong>, <strong>"baz"</strong>)
- any numeric literal (e.g. <strong>1</strong>, <strong>100</strong>)
- a unary minus applied to any numeric literal (e.g. <strong>-1</strong>, <strong>-100</strong>)
When all members in an enum have literal enum values, some special semantics come to play.

The first is that enum members also become types as well! For example, we can say that certain members can only have the value of an enum member:
![mu6hvR.png](https://s2.ax1x.com/2019/08/17/mu6hvR.png)
The other change is that enum types themselves effectively become a union of each enum member. While we haven’t discussed union types yet, all that you need to know is that with union enums, the type system is able to leverage the fact that it knows the exact set of values that exist in the enum itself. Because of that, TypeScript can catch silly bugs where we might be comparing values incorrectly. For example:
![mu6b5D.png](https://s2.ax1x.com/2019/08/17/mu6b5D.png)
In that example, we first checked whether <strong>x</strong> was not <strong>E.Foo</strong>. If that check succeeds, then our <strong>&#124;&#124;</strong> will short-circuit, and the body of the ‘if’ will run. However, if the check didn’t succeed, then x can only be <strong>E.Foo</strong>, so it doesn’t make sense to see whether it’s equal to <strong>E.Bar</strong>.

#### Enums at runtime
Enums are real objects that exist at runtime. For example, the following enum
![mucUZ6.png](https://s2.ax1x.com/2019/08/17/mucUZ6.png)
can actually be passed around to functions
![mugu6A.png](https://s2.ax1x.com/2019/08/17/mugu6A.png)

#### Enums at compile time
Even though Enums are real objects that exist at runtime, the <strong>keyof</strong> keyword works differently than you might expect for typical objects. Instead, use <strong>keyof</strong> <strong>typeof</strong> to get a Type that represents all Enum keys as strings.
![mu2zrR.png](https://s2.ax1x.com/2019/08/17/mu2zrR.png)

#### Reverse mappings
In addition to creating an object with property names for members, numeric enums members also get a reverse mapping from enum values to enum names. For example, in this example:
![muRJMj.png](https://s2.ax1x.com/2019/08/17/muRJMj.png)
TypeScript might compile this down to something like the the following JavaScript:
![muRrz4.png](https://s2.ax1x.com/2019/08/17/muRrz4.png)
In this generated code, an enum is compiled into an object that stores both forward (`name -> value`) and reverse (`value -> name`) mappings. References to other enum members are always emitted as property accesses and never inlined.

Keep in mind that string enum members do not get a reverse mapping generated at all.

#### const enums
In most cases, enums are a perfectly valid solution. However sometimes requirements are tighter. To avoid paying the cost of extra generated code and additional indirection when accessing enum values, it’s possible to use <strong>const</strong> enums. Const enums are defined using the const modifier on our enums:
![muRRdx.png](https://s2.ax1x.com/2019/08/17/muRRdx.png)
Const enums can only use constant enum expressions and unlike regular enums they are completely removed during compilation. Const enum members are inlined at use sites. This is possible since const enums cannot have computed members.
![muR5WD.png](https://s2.ax1x.com/2019/08/17/muR5WD.png)
in generated code will become
![muRTQH.png](https://s2.ax1x.com/2019/08/17/muRTQH.png)

#### Ambient enums
Ambient enums are used to describe the shape of already existing enum types.
![muRxfS.png](https://s2.ax1x.com/2019/08/17/muRxfS.png)
One important difference between ambient and non-ambient enums is that, in regular enums, members that don’t have an initializer will be considered constant if its preceding enum member is considered constant. In contrast, an ambient (and non-const) enum member that does not have initializer is always considered computed.

## Type Inference
#### Introduction
In this section, we will cover type inference in TypeScript. Namely, we’ll discuss where and how types are inferred.

#### Basics  
In TypeScript, there are several places where type inference is used to provide type information when there is no explicit type annotation. For example, in this code
![mMvdzQ.png](https://s2.ax1x.com/2019/08/18/mMvdzQ.png)
The type of the <strong>x</strong> variable is inferred to be <strong>number</strong>. This kind of inference takes place when initializing variables and members, setting parameter default values, and determining function return types.

In most cases, type inference is straightforward. In the following sections, we’ll explore some of the nuances in how types are inferred.

#### Best common type
When a type inference is made from several expressions, the types of those expressions are used to calculate a “best common type”. For example,
![mQpFfK.png](https://s2.ax1x.com/2019/08/18/mQpFfK.png)
To infer the type of `x` in the example above, we must consider the type of each array element. Here we are given two choices for the type of the array: `number` and `null`. The best common type algorithm considers each candidate type, and picks the type that is compatible with all the other candidates.

Because the best common type has to be chosen from the provided candidate types, there are some cases where types share a common structure, but no one type is the super type of all candidate types. For example:
![mQiSgK.png](https://s2.ax1x.com/2019/08/18/mQiSgK.png)
Ideally, we may want `zoo` to be inferred as an `Animal[]`, but because there is no object that is strictly of type `Animal` in the array, we make no inference about the array element type. To correct this, instead explicitly provide the type when no one type is a super type of all other candidates:
![mQVxCd.png](https://s2.ax1x.com/2019/08/18/mQVxCd.png)
When no best common type is found, the resulting inference is the union array type, `(Rhino | Elephant | Snake)[]`.

#### Contextual Typing
Type inference also works in “the other direction” in some cases in TypeScript. This is known as “contextual typing”. Contextual typing occurs when the type of an expression is implied by its location. For example:
![mQZRMt.png](https://s2.ax1x.com/2019/08/18/mQZRMt.png)
Here, the Typescript type checker used the type of the `Window.onmousedown` function to infer the type of the function expression on the right hand side of the assignment. When it did so, it was able to infer the type of the `mouseEvent` parameter, which does contain a `button` property, but not a `kangaroo` property.

Typescript is smart enough to infer the type of things in other contexts as well:
![mQZfqf.png](https://s2.ax1x.com/2019/08/18/mQZfqf.png)
Based on the fact that the above function is being assigned to `Window.onscroll`, Typescript knows that `uiEvent` is a `UIEvent`, and not a `MouseEvent` like the previous example. `UIEvent` objects contain no `button` property, and so Typescript will throw an error.

If this function were not in a contextually typed position, the function’s argument would implicitly have type `any`, and no error would be issued (unless you are using the `--noImplicitAny` option):
![mQZHRs.png](https://s2.ax1x.com/2019/08/18/mQZHRs.png)
We can also explicitly give type information to the function’s argument to override any contextual type:
![mQeCW9.png](https://s2.ax1x.com/2019/08/18/mQeCW9.png)
However, this code will log `undefined`, since `uiEvent` has no property called `button`.

Contextual typing applies in many cases. Common cases include arguments to function calls, right hand sides of assignments, type assertions, members of object and array literals, and return statements. The contextual type also acts as a candidate type in best common type. For example:
![mQeksx.png](https://s2.ax1x.com/2019/08/18/mQeksx.png)
In this example, best common type has a set of four candidates: `Animal`, `Rhino`, `Elephant`, and `Snake`. Of these, `Animal` can be chosen by the best common type algorithm.

## Type Compatibility
#### Introduction
Type compatibility in TypeScript is based on structural subtyping. Structural typing is a way of relating types based solely on their members. This is in contrast with nominal typing. Consider the following code:
![mQmyjI.png](https://s2.ax1x.com/2019/08/18/mQmyjI.png)
In nominally-typed languages like C# or Java, the equivalent code would be an error because the Person class does not explicitly describe itself as being an implementer of the `Named` interface.

TypeScript’s structural type system was designed based on how JavaScript code is typically written. Because JavaScript widely uses anonymous objects like function expressions and object literals, it’s much more natural to represent the kinds of relationships found in JavaScript libraries with a structural type system instead of a nominal one

###### A Note on Soundness
TypeScript’s type system allows certain operations that can’t be known at compile-time to be safe. When a type system has this property, it is said to not be “sound”. The places where TypeScript allows unsound behavior were carefully considered, and throughout this document we’ll explain where these happen and the motivating scenarios behind them.

#### Starting out
The basic rule for TypeScript’s structural type system is that `x` is compatible with `y` if `y` has at least the same members as `x`. For example:
![mQuCWQ.png](https://s2.ax1x.com/2019/08/18/mQuCWQ.png)
To check whether `y` can be assigned to `x`, the compiler checks each property of `x` to find a corresponding compatible property in `y`. In this case, `y` must have a member called `name` that is a string. It does, so the assignment is allowed.

The same rule for assignment is used when checking function call arguments:
![mQuQSJ.png](https://s2.ax1x.com/2019/08/18/mQuQSJ.png)
Note that `y` has an extra `location` property, but this does not create an error. Only members of the target type (`Named` in this case) are considered when checking for compatibility.

This comparison process proceeds recursively, exploring the type of each member and sub-member.

#### Comparing two functions
While comparing primitive types and object types is relatively straightforward, the question of what kinds of functions should be considered compatible is a bit more involved. Let’s start with a basic example of two functions that differ only in their parameter lists:
![mQKdEV.png](https://s2.ax1x.com/2019/08/18/mQKdEV.png)
To check if `x` is assignable to `y`, we first look at the parameter list. Each parameter in `x` must have a corresponding parameter in `y` with a compatible type. Note that the names of the parameters are not considered, only their types. In this case, every parameter of `x` has a corresponding compatible parameter in `y`, so the assignment is allowed.

The second assignment is an error, because `y` has a required second parameter that `x` does not have, so the assignment is disallowed.

You may be wondering why we allow ‘discarding’ parameters like in the example `y = x`. The reason for this assignment to be allowed is that ignoring extra function parameters is actually quite common in JavaScript. For example, `Array.forEach` provides three parameters to the callback function: the array element, its index, and the containing array. Nevertheless, it’s very useful to provide a callback that only uses the first parameter:
![mQKyv9.png](https://s2.ax1x.com/2019/08/18/mQKyv9.png)
Now let’s look at how return types are treated, using two functions that differ only by their return type:
![mQKgD1.png](https://s2.ax1x.com/2019/08/18/mQKgD1.png)
The type system enforces that the source function’s return type be a subtype of the target type’s return type.

###### Function Parameter Bivariance
When comparing the types of function parameters, assignment succeeds if either the source parameter is assignable to the target parameter, or vice versa. This is unsound because a caller might end up being given a function that takes a more specialized type, but invokes the function with a less specialized type. In practice, this sort of error is rare, and allowing this enables many common JavaScript patterns. A brief example:
![mQQvcQ.png](https://s2.ax1x.com/2019/08/18/mQQvcQ.png)
![mQlSns.png](https://s2.ax1x.com/2019/08/18/mQlSns.png)

###### Optional Parameters and Rest Parameters
When comparing functions for compatibility, optional and required parameters are interchangeable. Extra optional parameters of the source type are not an error, and optional parameters of the target type without corresponding parameters in the source type are not an error.

When a function has a rest parameter, it is treated as if it were an infinite series of optional parameters.

This is unsound from a type system perspective, but from a runtime point of view the idea of an optional parameter is generally not well-enforced since passing `undefined` in that position is equivalent for most functions.

The motivating example is the common pattern of a function that takes a callback and invokes it with some predictable (to the programmer) but unknown (to the type system) number of arguments:
![mQlj56.png](https://s2.ax1x.com/2019/08/18/mQlj56.png)

###### Functions with overloads
When a function has overloads, each overload in the source type must be matched by a compatible signature on the target type. This ensures that the target function can be called in all the same situations as the source function.

#### Enums
Enums are compatible with numbers, and numbers are compatible with enums. Enum values from different enum types are considered incompatible. For example,
![mQ11Zn.png](https://s2.ax1x.com/2019/08/18/mQ11Zn.png)

#### Classes
Classes work similarly to object literal types and interfaces with one exception: they have both a static and an instance type. When comparing two objects of a class type, only members of the instance are compared. Static members and constructors do not affect compatibility.
![mQ1gzD.png](https://s2.ax1x.com/2019/08/18/mQ1gzD.png)

###### Private and protected members in classes
Private and protected members in a class affect their compatibility. When an instance of a class is checked for compatibility, if the target type contains a private member, then the source type must also contain a private member that originated from the same class. Likewise, the same applies for an instance with a protected member. This allows a class to be assignment compatible with its super class, but not with classes from a different inheritance hierarchy which otherwise have the same shape.

#### Generics  
Because TypeScript is a structural type system, type parameters only affect the resulting type when consumed as part of the type of a member. For example,
![mQ3X9K.png](https://s2.ax1x.com/2019/08/18/mQ3X9K.png)
In the above, x and y are compatible because their structures do not use the type argument in a differentiating way. Changing this example by adding a member to Empty<T> shows how this works:
![mQ8pBd.png](https://s2.ax1x.com/2019/08/18/mQ8pBd.png)
In this way, a generic type that has its type arguments specified acts just like a non-generic type.

For generic types that do not have their type arguments specified, compatibility is checked by specifying any in place of all unspecified type arguments. The resulting types are then checked for compatibility, just as in the non-generic case.

For example,
![mQ83CV.png](https://s2.ax1x.com/2019/08/18/mQ83CV.png)

#### Advanced Topics
###### Subtype vs Assignment
So far, we’ve used “compatible”, which is not a term defined in the language spec. In TypeScript, there are two kinds of compatibility: subtype and assignment. These differ only in that assignment extends subtype compatibility with rules to allow assignment to and from `any`, and to and from `enum` with corresponding numeric values.

Different places in the language use one of the two compatibility mechanisms, depending on the situation. For practical purposes, type compatibility is dictated by assignment compatibility, even in the cases of the `implements` and `extends` clauses.
