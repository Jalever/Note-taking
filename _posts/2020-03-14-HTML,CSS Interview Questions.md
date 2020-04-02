---
layout: post
title: HTML & CSS面试题
subtitle: 面试题
date: 2020-03-15
author: Jalever
header-img: img/post_bg_fancyCrave.jpg
catalog: true
tags:
  - Interview Questions
---

- [HTML中的href与src的区别](#html%e4%b8%ad%e7%9a%84href%e4%b8%8esrc%e7%9a%84%e5%8c%ba%e5%88%ab)
- [link和@import的区别](#link%e5%92%8cimport%e7%9a%84%e5%8c%ba%e5%88%ab)
- [CSS中单位px和em,rem的区别](#css%e4%b8%ad%e5%8d%95%e4%bd%8dpx%e5%92%8cemrem%e7%9a%84%e5%8c%ba%e5%88%ab)
- [CSS position属性](#css-position%e5%b1%9e%e6%80%a7)



## HTML中的href与src的区别
`href`表示超文本引用，用在`link`和`a`等元素上，`href`是引用和页面关联，是在当前元素和引用资源之间建立联系

`src`表示引用资源，表示替换当前元素，用在`img`，`script`，`iframe`上，`src`是页面内容不可缺少的一部分

`<link href="common.css" rel="stylesheet"/>`当浏览器解析到这一句的时候会识别该文档为`CSS`文件，会下载并且不会停止对当前文档的处理

`<script src="js.js"></script>`当浏览器解析到这一句的时候会暂停其他资源的下载和处理，直至将该资源加载，编译，执行完毕，图片和框架等元素也是如此，类似于该元素所指向的资源嵌套如当前标签内

## link和@import的区别

两者都是外部引用CSS的方式，但是存在一定的区别：

区别1：link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS。

区别2：link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。

区别3：link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持。

区别4：link支持使用Javascript控制DOM去改变样式；而@import不支持


## CSS中单位px和em,rem的区别
`px`像素(Pixel):像素px是相对于显示器屏幕分辨率而言的

`em`是相对长度单位。相对于当前对象内文本的字体尺寸

任意浏览器的默认字体高都是`16px`。所有未经调整的浏览器都符合: `1em=16px`。那么`1px=0.0625em`,10px=0.625em。为了简化`font-size`的换算，需要在`CSS`中的body选择器中声明`Font-size=62.5%`，这就使em值变为 `16px*62.5%=10px`, 这样`10px=1em`, 也就是说只需要将你的原来的`px`数值除以10，然后换上`em`作为单位就行了

`EM`特点 
1. `em`的值并不是固定的；
2. `em`会继承父级元素的字体大小

在写`CSS`的时候，需要注意两点：

1. `body`选择器中声明`Font-size=62.5%`
2. 将你的原来的px数值除以10，然后换上em作为单位
3. 重新计算那些被放大的字体的em数值。避免字体大小的重复声明


`rem`是`CSS3`新增的一个相对单位(`root em`, 根`em`)，这个单位引起了广泛关注。这个单位与`em`有什么区别呢？区别在于使用`rem`为元素设定字体大小时，仍然是相对大小，但相对的只是`HTML`根元素。这个单位可谓集相对大小和绝对大小的优点于一身，通过它既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应。目前，除了IE8及更早版本外，所有浏览器均已支持`rem`。对于不支持它的浏览器，应对方法也很简单，就是多写一个绝对单位的声明。这些浏览器会忽略用`rem`设定的字体大小

## CSS position属性
position定位属性，检索或设置对象的定位方式,一共有四种属性：
- Static(默认定位) 
- Absolute(绝对定位)
- Relative(相对定位)
- Fixed(相对浏览器的绝对定位) 
- Sticky(粘性定位)

<strong>static</strong><br/>
(默认定位)默认值.位置设置为 `static` 的元素会正常显示,它始终会处于文档流给予的位置(`static`元素会忽略任何 `top`, `bottom`, `left`或 `right` 声明)

<strong>absolute</strong><br/>
(绝对定位)相对于父级元素的绝对定位, 浮出, 脱离布局流, 它不占据空间, 就是我们所说的层, 其位置相对于最近的已定位父元素而言的位置, 可直接指定`left`, `top`, `right` 以及 `bottom`属性. 若父级都没有定位，则以`HTML`(根元素)

(层叠的顺序`z-index: value`)默认情况是按照网页可视窗口（最大的包含块）绝对定位

<strong>relative</strong><br/>
(相对定位)是相对于默认位置的相对定位, 通过设置`left`, `top`, `right`, `bottom`值可将其移至相对于其正常位置的地方(相对于自己的开始的位置发生的位置上的移动[ 不会破坏正常的布局流，占据空间 ])

通常是定义`包含块`的

通常使用`Absolute`属性时需要有相对的包含块

`包含块`: 绝对定位的参照物，告诉元素在什么范围进行偏移。只要元素属性中具有`position:relative\absolute\fixed`，都可以称为`包含块`

<strong>fixed</strong><br/>
(相对于浏览器的绝对定位)相对浏览器的绝对定位, 始终都是相对于浏览器窗口的指定坐标进行定位. 此元素的位置可通过 `left`, `top`, `right`以及`bottom` 属性来规定. 不论窗口滚动与否，元素都会留在那个位置

<strong>sticky</strong><br/>
(粘性定位)可以看出是`position:relative`和`position:fixed`的结合体——当元素在屏幕内, 表现为`relative`, 就要滚出显示器屏幕的时候, 表现为fixed


