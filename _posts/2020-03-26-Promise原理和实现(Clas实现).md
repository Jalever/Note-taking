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

- [Promises的使用](#promises%e7%9a%84%e4%bd%bf%e7%94%a8)
- [Promise A+ 规范](#promise-a-%e8%a7%84%e8%8c%83)
- [简易版Promise实现](#%e7%ae%80%e6%98%93%e7%89%88promise%e5%ae%9e%e7%8e%b0)
- [引入状态控制](#%e5%bc%95%e5%85%a5%e7%8a%b6%e6%80%81%e6%8e%a7%e5%88%b6)
- [`then`的链式调用](#then%e7%9a%84%e9%93%be%e5%bc%8f%e8%b0%83%e7%94%a8)
- [值穿透 && 状态已经是resolve/reject的情况](#%e5%80%bc%e7%a9%bf%e9%80%8f--%e7%8a%b6%e6%80%81%e5%b7%b2%e7%bb%8f%e6%98%afresolvereject%e7%9a%84%e6%83%85%e5%86%b5)
- [兼容同步任务](#%e5%85%bc%e5%ae%b9%e5%90%8c%e6%ad%a5%e4%bb%bb%e5%8a%a1)
- [Promise.prototype.catch()](#promiseprototypecatch)
- [Promise.prototype.finally()](#promiseprototypefinally)
- [Promise.prototype.resolve()](#promiseprototyperesolve)
- [Promise.prototype.reject()](#promiseprototypereject)
- [Promise.all()](#promiseall)
- [Promise.race()](#promiserace)
- [完整代码](#%e5%ae%8c%e6%95%b4%e4%bb%a3%e7%a0%81)
- [参考链接:](#%e5%8f%82%e8%80%83%e9%93%be%e6%8e%a5)


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


## Promise A+ 规范
`ES6` 的 `Promise` 实现需要遵循`Promise/A+`规范，是规范对 `Promise` 的状态控制做了要求。`Promise/A+`的规范比较长，这里只总结两条核心规则:

- `Promise` 本质是一个状态机，且状态只能为以下三种：`Pending`（等待态）、`Fulfilled`（执行态）、`Rejected`（拒绝态），状态的变更是单向的，只能从 `Pending -> Fulfilled` 或 `Pending -> Rejected`，状态变更不可逆
- `then`方法接收两个可选参数，分别对应状态改变时触发的回调。`then` 方法返回一个 `promise`。`then` 方法可以被同一个 `promise` 调用多次
![GPCKIO.png](https://s1.ax1x.com/2020/03/27/GPCKIO.png)


## 简易版Promise实现
```js
export default class MyPromise {
    constructor(executor) {
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            while(this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };

        let _reject = val => {
            while(this._rejectQueue.length){
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

使用情况:
![GP9R8H.png](https://s1.ax1x.com/2020/03/27/GP9R8H.png)

控制台输出:
![GPCiiF.png](https://s1.ax1x.com/2020/03/27/GPCiiF.png)

问题:
1. 无法链式调用

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
2. 无法`then`链式调用

## `then`的链式调用

```js

const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

export default class MyPromise {
    constructor(executor) {
        this._status = PENDING;
        this._resolveQueue = [];
        this._rejectQueue = [];

        let _resolve = val => {
            if (this._status !== PENDING) return;
            this._status = FULFILLED;

            while (this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };

        let _reject = val => {
            if (this._status !== PENDING) return;
            this._status = REJECTED;

            while (this._rejectQueue.length) {
                let cb = this._rejectQueue.shift();
                cb(val);
            }
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        return new MyPromise((resolve, reject) => {

            const fulfilledFn = val => {
                try {
                    let x = resolveFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            const rejectedFn = () => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
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
    console.log(111);
    resolve(2222);
  }, 1000);
});
p.then(res => {
  console.log(res);
  return '333';
}).then(res => {
  console.log(res);
  return '444';
  
}).then(res => {
  console.log(res);
});

// 111
// 2222
// 333
// 444
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
            this._value = val;
            this._status = FULFILLED;

            while (this._resolveQueue.length) {
                let cb = this._resolveQueue.shift();
                cb(val);
            }
        };

        let _reject = val => {
            if (this._status !== PENDING) return;
            this._value = val;
            this._status = REJECTED;

            while (this._rejectQueue.length) {
                let cb = this._rejectQueue.shift();
                cb(val);
            }
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        //值穿透
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

            const rejectedFn = () => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            //解决值已是resolve/reject状态的情况
            switch (this._status) {
                case PENDING:
                    this._resolveQueue.push(fulfilledFn);
                    this._rejectQueue.push(rejectedFn);
                    break;
                case FULFILLED:
                    fulfilledFn(this._value);
                    break;
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
上面的代码有一个问题,如下:
![GPELTI.png](https://s1.ax1x.com/2020/03/27/GPELTI.png)

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
                this._value = val;
                this._status = FULFILLED;

                while (this._resolveQueue.length) {
                    let cb = this._resolveQueue.shift();
                    cb(val);
                }
            };

            setTimeout(run);
        };

        let _reject = val => {
            const run = () => {
                if (this._status !== PENDING) return;
                this._value = val;
                this._status = REJECTED;

                while (this._rejectQueue.length) {
                    let cb = this._rejectQueue.shift();
                    cb(val);
                }
            };

            setTimeout(run);
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        //值穿透
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

            const rejectedFn = () => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            //解决值已是resolve/reject状态的情况
            switch (this._status) {
                case PENDING:
                    this._resolveQueue.push(fulfilledFn);
                    this._rejectQueue.push(rejectedFn);
                    break;
                case FULFILLED:
                    fulfilledFn(this._value);
                    break;
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

## Promise.prototype.resolve()
`Promise.resolve(value)`方法返回一个以给定值解析后的 Promise 对象。<br/>
如果该值为 `promise`, 返回这个 `promise`;<br/>
如果这个值是 `thenable`(即带有`then` 方法),返回的 `promise` 会“跟随”这个 thenable 的对象，采用它的最终状态；<br/>
否则返回的 `promise` 将以此值完成。此函数将类 `promise` 对象的多层嵌套展平<br/>
```js
//静态的resolve方法
static resolve(value) {
    // 根据规范, 如果参数是Promise实例, 直接return这个实例
  if(value instanceof MyPromise) return value;
  return new MyPromise(resolve => resolve(value))
}
```

## Promise.prototype.reject()
`Promise.reject()`方法返回一个带有拒绝原因的 `Promise` 对象
```js
//静态的reject方法
static reject(reason) {
  return new MyPromise((resolve, reject) => reject(reason))
}
```

## Promise.all()
`Promise.all(iterable)`方法返回一个 `Promise` 实例, 此实例在 `iterable` 参数内所有的 `promise` 都"完成`(resolved)`"或参数中不包含 `promise` 时回调完成`(resolve)`; 如果参数中 `promise` 有一个失败`(rejected)`，此实例回调失败`(reject)`, 失败原因的是第一个失败 `promise` 的结果
```js
static all(promiseArr) {
    return new MyPromise((resolve, reject) => {
        let index = 0;
        let result = [];

        promiseArr.forEach((pro, idx) => {
            MyPromise.resolve(pro).then(value => {
                index++;
                result[idx] = value;

                if(index === promiseArr.length) resolve(result);
            }, reason => {
                reject(reason);
            });

        });
    });
}
```

使用:
```js
let fun1 = MyPromise.resolve('all - 111');

let fun2 = 'all - 222';

let fun3 = new MyPromise((resolve, reject) => setTimeout(resolve, 1000, 'result - 333'));

let promiseArr = [fun1, fun2, fun3];

MyPromise.all(promiseArr).then(res => {
  console.log(res);
});

//返回:
// ["all - 111", "all - 222", "result - 333"]
```

## Promise.race()
`Promise.race(iterable)`方法返回一个 `promise`, 一旦迭代器中的某个 `promise` 解决或拒绝，返回的 `promise` 就会解决或拒绝

```js
    static race(promiseArr) {
        return new MyPromise((resolve, reject) => {
            for (let pro of promiseArr) {
                MyPromise.resolve(pro).then(val => resolve(val), reason => reject(reason))
            }
        });
    }
```

使用：
```js
let fun1 = new MyPromise((resolve, reject) => {
  setTimeout(resolve, 500, 'race - 111');
});

let fun2 = new MyPromise((resolve, reject) => {
  setTimeout(resolve, 100, 'race - 222');
});

let fun3 = new MyPromise((resolve, reject) => setTimeout(resolve, 1000, 'result - 333'));

let promiseArr = [fun1, fun2, fun3];

MyPromise.race(promiseArr).then(res => {
  console.log(res);
});

//返回:
//race - 222
```

## 完整代码
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
                this._value = val;
                this._status = FULFILLED;

                while (this._resolveQueue.length) {
                    let cb = this._resolveQueue.shift();
                    cb(val);
                }
            };

            setTimeout(run);
        };

        let _reject = val => {
            const run = () => {
                if (this._status !== PENDING) return;
                this._value = val;
                this._status = REJECTED;

                while (this._rejectQueue.length) {
                    let cb = this._rejectQueue.shift();
                    cb(val);
                }
            };

            setTimeout(run);
        };

        executor(_resolve, _reject);
    }

    then(resolveFn, rejectFn) {
        //值穿透
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

            const rejectedFn = () => {
                try {
                    let x = rejectFn(val);
                    x instanceof MyPromise ? x.then(resolve, reject) : resolve(x)
                } catch (error) {
                    reject(error);
                }
            };

            //解决值已是resolve/reject状态的情况
            switch (this._status) {
                case PENDING:
                    this._resolveQueue.push(fulfilledFn);
                    this._rejectQueue.push(rejectedFn);
                    break;
                case FULFILLED:
                    fulfilledFn(this._value);
                    break;
                case REJECTED:
                    rejectedFn(this._value);
                    break;

                default:
                    break;
            }
        });
    }

    catch(resolveFn, rejectFn) {
        return this.then(undefined, rejectFn);
    }

    finally(cb) {
        return this.then(
            val => MyPromise.resolve(cb()).then(() => val),
            reason => MyPromise.resolve(cb()).then(() => { throw reason })
        );
    }

    static resolve(value) {

        if (value instanceof MyPromise) return value;
        return new MyPromise(resolve => resolve(value));
    }

    static reject(reason) {
        return new Promise((resolve, reject) => reject(reason));
    }

    static all(promiseArr) {
        return new MyPromise((resolve, reject) => {
            let result = [];
            let index = 0;

            promiseArr.forEach((pro, idx) => {
                MyPromise.resolve(pro).then(val => {
                    index++;
                    result[idx] = val;

                    if (index === promiseArr.length) resolve(result);
                }, reason => {
                    reject(reason);
                })
            });
        });
    }

    static race(promiseArr) {
        return new MyPromise((resolve, reject) => {
            for (let pro of promiseArr) {
                MyPromise.resolve(pro).then(val => resolve(val), reason => reject(reason))
            }
        });
    }
}
```

## 参考链接:
<a href="https://mp.weixin.qq.com/s?__biz=MzI4OTI0NDc2NQ==&mid=2247483861&idx=1&sn=0453a4fa5aa2956938138181ed30f64e&chksm=ec3352e7db44dbf12ee1118a2f0bf715a5f2e57ef74122c6a52b9125bedeb4953ede3826c8e6&scene=126&sessionid=1585146571&key=03b7e0e33e341fce7befb033476a930e790172eaaef162b83d083e34995f7316b8c921c890da4bbf8f109dc83037d7e5fa20b5801f9ebc2722e9b6f380a84e87ea635286b391e9f32c6fa650c82f76d8&ascene=1&uin=MTUyNTM3MDAyNg%3D%3D&devicetype=Windows+10&version=62080079&lang=en&exportkey=A2KvjAuUkA5WOxTHa%2F6O%2BJs%3D&pass_ticket=8C3g0RHiXRnElkMfuzVJPgjIpXKuEQ5pw2kLEkDRAtJsaFvRGdR1ZeWCwjM03JUa" target="_blank">参考文章</a>