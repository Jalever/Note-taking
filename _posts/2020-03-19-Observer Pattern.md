---
layout: post
title: 观察者模式
subtitle: Behavioral Pattern
date: 2020-03-19
author: Jalever
header-img: img/design_pattern_bg_simple.png
catalog: true
tags:
  - Design Pattern
---
## 定义
观察者模式(Observer Pattern)： 定义对象间一种一对多的依赖关系，使得当每一个对象改变状态，则所有依赖于它的对象都会得到通知并自动更新。

观察者模式是一种对象行为型模式。

观察者模式的别名包括发布-订阅（Publish/Subscribe）模式、模型-视图（Model/View）模式、源-监听器（Source/Listener）模式或从属者（Dependents）模式。

![NxTMtK.png](https://s1.ax1x.com/2020/07/04/NxTMtK.png)

## 实例
Observer的创建:
```js
<template>
  <div class="exception-test-wrapper">
    <p>消息: {{ msgItemNum }}</p>
    <ul id="msgItems"></ul>
    <input v-model="user_input" />
    <button @click="onUserSubmit">add</button>
  </div>
</template>
<script>

const Observer = (function () {
  let _messages = [];
  return {
    _messages,
    regist: function (type, fn) {
      if (!_messages[type]) {
        _messages[type] = [fn];
      } else {
        _messages[type].push(fn);
      }
    },
    fire: function (type, args) {
      if (!_messages[type]) return;

      var events = {
        type,
        args: args || {},
      };

      let len = _messages[type]["length"];
      for (let i = 0; i < len; i++) {
        _messages[type][i].call(this, events);
      }
    },
    remove: function (type, fn) {
      if (_messages[type] instanceof Array) {
        let len = _messages[type]["length"];
        for (let i = len; i >= 0; i--) {
          _messages[type][i] === fn && _messages[type].splice(i, 1);
        }
      }
    },
  };
})();

export default {
  props: {},
  components: {  },
  data() {
    return {
      msgItemNum: 0,
      user_input: "",
    };
  },
  computed: {},
  mounted() {
    Observer.regist("addCommentMessage", this.addMessageItem);
    Observer.regist("addCommentMessage", this.changeMsgNum);
    Observer.regist("removeCommentMessage", this.changeMsgNum);
  },
  filters: {},
  watch: {},
  methods: {
    addMessageItem(e) {
      let text = e.args.text,
        ul = document.getElementById("msgItems"),
        li = document.createElement("li"),
        span = document.createElement("span");

      span.innerHTML = "delete";
      li.innerHTML = text;

      li.onclick = () => {
        ul.removeChild(li);
        Observer.fire("removeCommentMessage", {
          num: -1,
        });
      };

      li.appendChild(span);
      ul.appendChild(li);
    },
    changeMsgNum(e) {
      let num = e.args.num;
      let prevNum = this.msgItemNum * 1;
      this.msgItemNum = prevNum + num;
    },
    onUserSubmit() {
      if (!this.user_input) return;
      Observer.fire("addCommentMessage", {
        text: this.user_input,
        num: 1,
      });

      this.user_input = "";
    },

    
  },
};
</script>

<style lang="less" scoped>

</style>
```

## 优缺点
#### 优点
- 降低了目标与观察者之间的耦合关系，两者之间是抽象耦合关系
- 目标与观察者之间建立了一套触发机制
- 支持广播通信
- 符合“开闭原则”的要求

#### 缺点
- 目标与观察者之间的依赖关系并没有完全解除，而且有可能出现循环引用
- 当观察者对象很多时，通知的发布会花费很多时间，影响程序的效率


