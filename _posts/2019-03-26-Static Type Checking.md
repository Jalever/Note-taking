---
layout: post
title: Static Type Checking
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.jpg
catalog: true
tags:
  - React
---

Static type checkers like `Flow` and `TypeScript` identify certain types of problems before you even run your code.

- [Flow](#flow)
    - [Adding Flow to a Project](#adding-flow-to-a-project)
    - [Stripping Flow Syntax from the Compiled Code](#stripping-flow-syntax-from-the-compiled-code)
    - [Running Flow](#running-flow)
    - [Adding Flow Type Annotations](#adding-flow-type-annotations)
- [TypeScript](#typescript)
    - [Using TypeScript with Create React App](#using-typescript-with-create-react-app)
    - [Adding TypeScript to a Project](#adding-typescript-to-a-project)
    - [Configuring the TypeScript Compiler](#configuring-the-typescript-compiler)
    - [File extensions](#file-extensions)
    - [Running TypeScript](#running-typescript)
    - [Type Definitions](#type-definitions)
- [Reason](#reason)
- [Kotlin](#kotlin)
- [Other Languages](#other-languages)

## Flow
#### Adding Flow to a Project 
#### Stripping Flow Syntax from the Compiled Code  
#### Running Flow  
#### Adding Flow Type Annotations  
## TypeScript
It is a typed superset of `JavaScript`, and includes its own compiler. <br>
Being a typed language, `TypeScript` can catch errors and bugs at build time, long before your app goes live.

#### Using TypeScript with Create React App 
To create a new project with TypeScript support, run:
```javascript
npx create-react-app my-app --typescript
```

#### Adding TypeScript to a Project 
If you use `npm`, run:
```javascript
npm install --save-dev typescript
```
Installing `TypeScript` gives us access to the `tsc` command. 
Before configuration, let’s add `tsc` to the `scripts` section in our `package.json`:
```javascript
{
  // ...
  "scripts": {
    "build": "tsc",
    // ...
  },
  // ...
}
```

#### Configuring the TypeScript Compiler 
In TypeScript, these rules are defined in a special file called tsconfig.json. 
To generate this file:
```
npx tsc --init
```
Looking at the now generated `tsconfig.json`, you can see that there are many options you can use to configure the compiler. 

#### File extensions 
In `React`, you most likely write your components in a `.js` file. In `TypeScript` we have 2 file extensions:

`.ts` is the default file extension while `.tsx` is a special extension used for files which contain `JSX`.

#### Running TypeScript 

#### Type Definitions  

## Reason   
## Kotlin   
## Other Languages  