---
layout: post
title: Web Components API in a Nutshell
subtitle: Web Development
date: 2019-12-23
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Web Development
---

## Requirements
We all know that re-using code as much as possible is generally a good idea. Sharing code between components saves us money, energy, and, most importantly, time.

Re-using code hasn’t been so easy for the complex HTML. You’ve sometimes had to write to render custom UI controls, and using them multiple times can turn your page into a mess if you are not careful.

Here’s where Web Components come in.<b>Web Components is a suite of different technologies which allow you to create reusable custom elements — with their functionality encapsulated away from the rest of your code — and to utilize them in your web apps.</b>

For example, web components let us define custom elements in `HTML` files.
```js
<body>
    <app-button>Hello</app-button>

</body>
```

## Getting Started
All we need is the `index.html` and the `app.js` file.

![lSNPud.png](https://s2.ax1x.com/2019/12/23/lSNPud.png)
![lSNEUP.png](https://s2.ax1x.com/2019/12/23/lSNEUP.png)

Notice how the browser global window object has a property called `customElements` — we call the define method on the property to create our custom HTML element. It takes three arguments, the last one is optional.
![lSNoIP.png](https://s2.ax1x.com/2019/12/23/lSNoIP.png)

The first argument is the name of the custom element, app-button in the example above. The second argument is the constructor for the element. We use the constructor to build up our custom element, like attaching event listeners and logic.

Notice how our `WebComponentButton` class extends the `HTMLElement`class. To put it simply, we inherit from and extend the built-in HTML elements.

![lSUmIx.png](https://s2.ax1x.com/2019/12/23/lSUmIx.png)

As expected, if we click on the button, nothing happens. We need to tell the button what to do after clicking on it. In order to accomplish this, let’s add an event listener for our button.

<b>app.js</b>
```js
class WebComponentButton extends HTMLElement {

  constructor() {

    super()

    this.addEventListener('click', () => {

      console.log('click')

    })

  }
 
}
```

`WebComponentButton` class has lifecycles out of the box. If you come from the <strong>React</strong>, <strong>Vue</strong>, <strong>Angular</strong>, etc., this might be familiar to you already. Lifecycle methods let us control what happens when certain actions happen. For example, when the browser renders the button, we want to attach styles to it.

```js
class WebComponentButton extends HTMLElement {

  // The connectedCallback() runs each time the element is added to the DOM

  connectedCallback() {}

  // Called every time the element is removed from the DOM. Useful for running clean up code.

  disconnectedCallback() {}

  //When the element is either removed from the DOM, or moved to a different page:

  adoptedCallback() {}
  
}
```

We can style our button via the standard `CSSStyleDeclaration` API. For example, `<div style=”…”>` uses the `CSSStyleDecleration` API.
```js
// The connectedCallback() runs each time the element is added to the DOM

  connectedCallback() {

    this.style.border = 'solid 1px #333'

    this.style.padding = '10px 20px'

  }
```

`This` references our class, `WebComponentButton` in this case. The above code will give our button a dark border with padding.


