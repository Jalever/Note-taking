---
layout: post
title: Promise原理和实现(Class版)
subtitle: JavaScript系列
date: 2020-03-26
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---
## Promises的使用
`Promise` 必须为以下三种状态之一：等待态（`Pending`）、执行态（Fulfilled）和拒绝态（`Rejected`）。一旦`Promise` 被 `resolve` 或 `reject`，不能再迁移至其他任何状态（即状态 `immutable`）

基本过程：
1. 初始化 `Promise` 状态（`pending`）
2. 立即执行 `Promise` 中传入的 `fn` 函数，将`Promise` 内部 `resolve`、`reject` 函数作为参数传递给 `fn` ，按事件机制时机处理
3. 执行 `then(..)` 注册回调处理数组（`then` 方法可被同一个 `promise` 调用多次）
4. `Promise`里的关键是要保证，`then`方法传入的参数 `onFulfilled` 和 `onRejected`，必须在then方法被调用的那一轮事件循环之后的新执行栈中执行。

```js
const p1 = newPromise((resolve, reject) => {
    setTimeout(() => {
        resolve('result')
    },
    1000);
})

p1.then(res =>console.log(res), err => console.log(err))
```

符合Promise A+的状态控制
链式调用
值穿透 && 状态已变更的情况
兼顾同步任务
Promise.prototype.catch
Promise.prototype.finally
Promise.resolve
Promise.reject
Promise.all
Promise.race



## 引入状态控制
```js
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

export default class MyPromise{
    constructor(executor) {
        this._status = PENDING;
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            if(this._status !== PENDING) return;
            this._status = FULFILLED;

            while(this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };


        let _reject = reason => {
            if(this._status !== PENDING) return;
            this._status = REJECTED;
            while(this._rejectQueue.length) {
                let cb = this._rejectQueue.shift();
                cb(val);
            }
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        this._resolveQueue.push(resolveFn);
        this._rejectQueue.push(rejectFn);
    }
}
```
问题：
1. 只能是异步
2. 无法then链式调用

## 链式调用
```js
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

export default class MyPromise{
    constructor(executor) {
        this._status = PENDING;
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            if(this._status !== PENDING) return;
            this._status = FULFILLED;

            while(this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };

        let _reject = reason => {
            if(this._status !== PENDING) return;
            this._status = REJECTED;
            while(this._rejectQueue.length) {
                let cb = this._rejectQueue.shift();
                cb(reason);
            }
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        return new MyPromise((resolve, reject) => {
            const fulfilledFn = val => {
                try {
                    let x = resolveFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject): resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            const rejectedFn = val => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject): resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            this._resolveQueue.push(fulfilledFn);
            this._rejectQueue.push(rejectedFn);
        });
    }
}
```

使用：
```js
let p = new MyPromise((resolve, reject) => {
  setTimeout(() => {
    console.log('111');
    reject("222");
  }, 1000);
});

p.then(res => {
  console.log(res);

  return 333;
  // throw new Error('ee');
}, reason => {
  console.log('reason');
  console.log(reason);
  
  throw new Error('last');
}).then(res => {
  console.log(res);
  console.log('--- end ---');
  
  
}, reason => {
  console.log('end: reason => ', reason);
});

// 111
// reason
// 222
// end: reason =>  Error: last
```

问题
1. 值无法穿透
2. 处理状态已经resolve/rejecte的情况, 例如: Promise.resolve().then()

## 值穿透 && 状态已经是resolve/reject的情况
```js

const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

export default class MyPromise {
    constructor(executor) {
        this._value = undefined;
        this._status = PENDING;
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            if (this._status !== PENDING) return;
            this._status = FULFILLED;
            this._value = val;

            while (this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };

        let _reject = reason => {
            if (this._status !== PENDING) return;
            this._status = REJECTED;
            this._value = reason;

            while (this._rejectQueue.length) {
                let cb = this._rejectQueue.shift();
                cb(reason);
            }
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        typeof resolveFn !== 'function' ? resolveFn = value => value : null;
        typeof rejectFn !== 'function' ? rejectFn = reason => {
            throw new Error(reason instanceof Error ? reason.message : reason);
        } : null;

        return new MyPromise((resolve, reject) => {
            const fulfilledFn = val => {
                try {
                    let x = resolveFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            const rejectedFn = val => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            switch (this._status) {
                case PENDING:
                    this._resolveQueue.push(fulfilledFn);
                    this._rejectQueue.push(rejectedFn);
                    break;
                case FULFILLED:
                    fulfilledFn(this._value);
                case REJECTED:
                    rejectedFn(this._value);
                    break;
                default:
                    break;
            }
        });
    }
}
```

问题:
```js
let p = new MyPromise((resolve, reject) => {
  console.log('111');
  reject("222"); //状态已经是resolve/reject的情况
});

p.then(res => {
  console.log(res);

  return 333; 
}, reason => {
  console.log(reason);
  return '333';
})
  .then() //值穿透
  .then(res => {
    console.log(res);
    return '444';
  })
  .then(res => {
    console.log(res);
    console.log('--- end ---');


  }, reason => {
    console.log('end: reason => ', reason);
  });


// 111
// 222
// 333
// 444
// --- end ---
```

## 兼容同步任务
```js

const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

export default class MyPromise {
    constructor(executor) {
        this._value = undefined;
        this._status = PENDING;
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            const run = () => {
                if (this._status !== PENDING) return;
                this._status = FULFILLED;
                this._value = val;

                while (this._resolveQueue.length) {
                    let cb = this._resolveQueue.shift();
                    cb(val);
                }
            }

            setTimeout(run);
        };

        let _reject = reason => {
            const run = () => {
                if (this._status !== PENDING) return;
                this._status = REJECTED;
                this._value = reason;

                while (this._rejectQueue.length) {
                    let cb = this._rejectQueue.shift();
                    cb(reason);
                }
            }

            setTimeout(run);
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        typeof resolveFn !== 'function' ? resolveFn = value => value : null;
        typeof rejectFn !== 'function' ? rejectFn = reason => {
            throw new Error(reason instanceof Error ? reason.message : reason);
        } : null;

        return new MyPromise((resolve, reject) => {
            const fulfilledFn = val => {
                try {
                    let x = resolveFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            const rejectedFn = val => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            switch (this._status) {
                case PENDING:
                    this._resolveQueue.push(fulfilledFn);
                    this._rejectQueue.push(rejectedFn);
                    break;
                case FULFILLED:
                    fulfilledFn(this._value);
                case REJECTED:
                    rejectedFn(this._value);
                    break;
                default:
                    break;
            }
        });
    }
}
```

## Promise.prototype.catch()
```js
//catch方法其实就是执行一下then的第二个回调
catch(rejectFn) {
  return this.then(undefined, rejectFn)
}
```

## Promise.prototype.finally()
```js
//finally方法
finally(callback) {
  return this.then(
    value => MyPromise.resolve(callback()).then(() => value),             // MyPromise.resolve执行回调,并在then中return结果传递给后面的Promise
    reason => MyPromise.resolve(callback()).then(() => { throw reason })  // reject同理
  )
}
```

## 参考链接:
[文章](https://mp.weixin.qq.com/s?__biz=MzI4OTI0NDc2NQ==&mid=2247483861&idx=1&sn=0453a4fa5aa2956938138181ed30f64e&chksm=ec3352e7db44dbf12ee1118a2f0bf715a5f2e57ef74122c6a52b9125bedeb4953ede3826c8e6&scene=126&sessionid=1585146571&key=03b7e0e33e341fce7befb033476a930e790172eaaef162b83d083e34995f7316b8c921c890da4bbf8f109dc83037d7e5fa20b5801f9ebc2722e9b6f380a84e87ea635286b391e9f32c6fa650c82f76d8&ascene=1&uin=MTUyNTM3MDAyNg%3D%3D&devicetype=Windows+10&version=62080079&lang=en&exportkey=A2KvjAuUkA5WOxTHa%2F6O%2BJs%3D&pass_ticket=8C3g0RHiXRnElkMfuzVJPgjIpXKuEQ5pw2kLEkDRAtJsaFvRGdR1ZeWCwjM03JUa)