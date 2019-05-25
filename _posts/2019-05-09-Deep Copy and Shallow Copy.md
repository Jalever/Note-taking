---
layout: post
title: Shallow Copy and Deep Copy
subtitle: Web Development学习笔记系列
date: 2019-05-09
author: Jalever
header-img: img/home_bg_black.png
catalog: true
tags:
  - Web Development
---

- [赋值](#%E8%B5%8B%E5%80%BC)
- [Shallow Copy](#shallow-copy)
- [Deep Copy](#deep-copy)
    - [自定义函数](#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%87%BD%E6%95%B0)
    - [JSON.parse() & JSON.stringify()](#jsonparse--jsonstringify)
- [总结](#%E6%80%BB%E7%BB%93)

## 赋值

```javascript
let obj = {
  name: "Jalever",
  age: 34,
  profession: "Software Engineer"
};

let copyObj = obj;

obj.name = "youtube";

console.log("obj");
console.log(obj); //{name: "youtube", age: 34, profession: "Software Engineer"}
console.log("\n");
console.log("copyObj");
console.log(copyObj); //{name: "youtube", age: 34, profession: "Software Engineer"}
console.log("\n");
```

## Shallow Copy

```javascript
let shallowCopy = obj => {
  if (!obj || typeof obj !== "object") {
    throw new Error("Error");
  }

  let targetObj = obj.constructor() === Array ? [] : {};
  for (let i in obj) {
    if (obj.hasOwnProperty(i)) {
      targetObj[i] = obj[i];
    }
  }
  return targetObj;
};

let obj = {
  name: "Jalever",
  age: 34,
  profession: "Software Engineer",
  friends: ["oo", "cc", "yy"]
};

let copyObj = deepCopy(obj);

obj.name = "youtube";
obj.friends.push("dd");

console.log("obj");
console.log(obj);
// age: 34
// friends: ["oo", "cc", "yy", "dd"]
// name: "youtube"
// profession: "Software Engineer"

console.log("copyObj");
console.log(copyObj);
// age: 34
// friends: ["oo", "cc", "yy", "dd"]
// name: "Jalever"
// profession: "Software Engineer"
```

## Deep Copy

#### 自定义函数

深拷贝函数：

```javascript
let deepCopy = obj => {
  if (!obj || typeof obj !== "object") {
    throw new Error("Error");
  }

  let target = obj.constructor === Array ? [] : {};
  for (let i in obj) {
    if (obj.hasOwnProperty(i)) {
      if (obj[i] && typeof obj[i] === "object") {
        target[i] = obj[i].constructor === Array ? [] : {};
        target[i] = deepCopy(obj[i]);
      } else {
        target[i] = obj[i];
      }
    }
  }
  return target;
};
```

示例：

```javascript
let deepCopy = obj => {
  if (!obj || typeof obj !== "object") {
    throw new Error("Error");
  }

  let target = obj.constructor === Array ? [] : {};
  for (let i in obj) {
    if (obj.hasOwnProperty(i)) {
      if (obj[i] && typeof obj[i] === "object") {
        target[i] = obj[i].constructor === Array ? [] : {};
        target[i] = deepCopy(obj[i]);
      } else {
        target[i] = obj[i];
      }
    }
  }
  return target;
};

let obj = {
  name: "Jalever",
  age: 34,
  profession: "Software Engineer",
  friends: ["oo", "cc", "yy"]
};

let copyObj = deepCopy(obj);

obj.name = "youtube";
obj.friends.push("dd");

console.log("obj");
console.log(obj);
// age: 34
// friends: ["oo", "cc", "yy", "dd"]
// name: "youtube"
// profession: "Software Engineer"

console.log("copyObj");
console.log(copyObj);
// age: 34
// friends: ["oo", "cc", "yy"]
// name: "Jalever"
// profession: "Software Engineer"
```

#### JSON.parse() & JSON.stringify()

```js
let deepCopy = obj => {
  return JSON.parse(JSON.stringify(obj));
};
```

## 总结

| --     | 和原数据是否指向同一对象 | 第一层数据为基本数据类型 | 原数据中包含子对象|
| --- | --- | --- | --- |
| 赋值   | 是      | 改变会使原数据一同改变   | 改变会使原数据一同改变 |
| 浅拷贝 | 否       | 改变不会使原数据一同改变 | 改变会使原数据一同改变 |
| 深拷贝 | 否       | 改变不会使原数据一同改变 | 改变不会使原数据一同改变 |
