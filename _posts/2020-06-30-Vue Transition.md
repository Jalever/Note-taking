---
layout: post
title: Vue Transition
subtitle: Vue Tutorial Takeaway
date: 2020-06-30
author: Jalever
header-img: img/vue_bg.jpeg
catalog: true
tags:
  - Vue
---

## 动画不同周期

- enter
- enter-active
- enter-to
- leave
- leave-active
- leave-to

usage:

```js
<transition name="fade" mode="out-in">
  <div class="animation-block" v-show="isShowAnimationBlock"></div>
</transition>
<button @click="handleShowAnimationBlock">click</button>

...

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
  background-color: #00ffff;
  transition: all 2s;
}
.fade-enter-to {
  background-color: #000fff;
}
.fade-leave {
  background-color: #fafafa;
  transition: all 2s;
}
```

## 动画组不同周期
- enter-class
- enter-active-class
- enter-to-class
- leave-class
- leave-active-class
- leave-to-class


