---
layout: post
title: Typescript Tutorial
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
- [Introduction]](#introduction)
- [Hello World of Generics]](#hello-world-of-generics)
- [Working with Generic Type Variables]](#working-with-generic-type-variables)
- [Generic Types]](#generic-types)
- [Generic Classes]](#generic-classes)
- [Generic Constraints]](#generic-constraints)
    - [Using Type Parameters in Generic Constraints]](#using-type-parameters-in-generic-constraints)
    - [Using Class Types in Generics]](#using-class-types-in-generics)
    - [Generic Constraints]](#generic-constraints)

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
