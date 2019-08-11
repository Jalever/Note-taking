---
layout: post
title: Compoarison between React and Vue
subtitle: React Advanced Guides
date: 2019-08-11
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [Overview](#overview)
- [Runtime Performance](#runtime-performance)
    - [Optimization Efforts](#optimization-efforts)
- [HTML & CSS](#html-css)
    - [JSX vs Templates](#jsx-vs-templates)
    - [Component-Scoped CSS](#component-scoped-css)
- [Scale](#scale)
    - [Scaling up](#scaling-up)
    - [Scaling Down](#scaling-down)
- [Native Rendering](#native-rendering)
- [With MobX](#with-mobx)
- [Preact and Other React-Like Libraries](#preact-and-other-react-like-libraries)

## Overview
React and Vue share many similarities. They both:
- utilize a virtual DOM
- provide reactive and composable view components
- maintain focus in the core library, with concerns such as routing and global state management handled by companion libraries

## Runtime Performance
Both React and Vue are exceptionally and similarly fast, so speed is unlikely to be a deciding factor in choosing between them. For specific metrics though, check out this 3rd party benchmark, which focuses on raw render/update performance with very simple component trees.

#### Optimization Efforts
In React, when a component’s state changes, it triggers the re-render of the entire component sub-tree, starting at that component as root. To avoid unnecessary re-renders of child components, you need to either use <strong>PureComponent</strong> or implement <strong>shouldComponentUpdate</strong> whenever you can. You may also need to use immutable data structures to make your state changes more optimization-friendly. However, in certain cases you may not be able to rely on such optimizations because <strong>PureComponent</strong>&sol;<strong>shouldComponentUpdate</strong> assumes the entire sub tree’s render output is determined by the props of the current component. If that is not the case, then such optimizations may lead to inconsistent DOM state.

In Vue, a component’s dependencies are automatically tracked during its render, so the system knows precisely which components actually need to re-render when state changes. Each component can be considered to have shouldComponentUpdate automatically implemented for you, without the nested component caveats.

Overall this removes the need for a whole class of performance optimizations from the developer’s plate, and allows them to focus more on building the app itself as it scales.

## HTML & CSS
In React, everything is just JavaScript. Not only are HTML structures expressed via JSX, the recent trends also tend to put CSS management inside JavaScript as well. This approach has its own benefits, but also comes with various trade-offs that may not seem worthwhile for every developer.

Vue embraces classic web technologies and builds on top of them. To show you what that means, we’ll dive into some examples.

#### JSX vs Templates
In React, all components express their UI within render functions using JSX, a declarative XML-like syntax that works within JavaScript.

Render functions with JSX have a few advantages:

- You can leverage the power of a full programming language (JavaScript) to build your view. This includes temporary variables, flow controls, and directly referencing JavaScript values in scope.
- The tooling support (e.g. linting, type checking, editor autocompletion) for JSX is in some ways more advanced than what’s currently available for Vue templates.

In Vue, we also have render functions and even support JSX, because sometimes you do need that power. However, as the default experience we offer templates as a simpler alternative. Any valid HTML is also a valid Vue template, and this leads to a few advantages of its own:

- For many developers who have been working with HTML, templates feel more natural to read and write. The preference itself can be somewhat subjective, but if it makes the developer more productive then the benefit is objective.
- HTML-based templates make it much easier to progressively migrate existing applications to take advantage of Vue’s reactivity features.
- It also makes it much easier for designers and less experienced developers to parse and contribute to the codebase.
-  You can even use pre-processors such as Pug (formerly known as Jade) to author your Vue templates.

Some argue that you’d need to learn an extra DSL (Domain-Specific Language) to be able to write templates - we believe this difference is superficial at best. First, JSX doesn’t mean the user doesn’t need to learn anything - it’s additional syntax on top of plain JavaScript, so it can be easy for someone familiar with JavaScript to learn, but saying it’s essentially free is misleading. Similarly, a template is just additional syntax on top of plain HTML and thus has very low learning cost for those who are already familiar with HTML. With the DSL we are also able to help the user get more done with less code (e.g. <strong>v-on</strong> modifiers). The same task can involve a lot more code when using plain JSX or render functions.

On a higher level, we can divide components into two categories: presentational ones and logical ones. We recommend using templates for presentational components and render function / JSX for logical ones. The percentage of these components depends on the type of app you are building, but in general we find presentational ones to be much more common.

#### Component-Scoped CSS
Unless you spread components out over multiple files (for example with <strong>CSS Modules</strong>), scoping CSS in React is often done via CSS-in-JS solutions (e.g. <strong>styled-components</strong>, <strong>glamorous</strong>, and <strong>emotion</strong>). This introduces a new component-oriented styling paradigm that is different from the normal CSS authoring process. Additionally, although there is support for extracting CSS into a single stylesheet at build time, it is still common that a runtime will need to be included in the bundle for styling to work properly. While you gain access to the dynamism of JavaScript while constructing your styles, the tradeoff is often increased bundle size and runtime cost.

If you are a fan of CSS-in-JS, many of the popular CSS-in-JS libraries support Vue (e.g. <strong>styled-components-vue</strong> and <strong>vue-emotion</strong>). The main difference between React and Vue here is that the default method of styling in Vue is through more familiar style tags in <strong>single-file components</strong>.

<strong>Single-file components</strong> give you full access to CSS in the same file as the rest of your component code.
![ejqAot.png](https://s2.ax1x.com/2019/08/11/ejqAot.png)
The optional <strong>scoped</strong> attribute automatically scopes this CSS to your component by adding a unique attribute (such as <strong>data-v-21e5b78</strong>) to elements and compiling <strong>.list-container:hover</strong> to something like <strong>.list-container[data-v-21e5b78]:hover</strong>.

Lastly, the styling in Vue’s single-file components is very flexible. Through <strong>vue-loader</strong>, you can use any preprocessor, post-processor, and even deep integration with <strong>CSS Modules</strong> – all within the <strong>&lt;style&gt;</strong> element.

## Scale

#### Scaling up
For large applications, both Vue and React offer robust routing solutions. The React community has also been very innovative in terms of state management solutions (e.g. Flux/Redux). These state management patterns and even Redux itself can be easily integrated into Vue applications. In fact, Vue has even taken this model a step further with <strong>Vuex</strong>, an Elm-inspired state management solution that integrates deeply into Vue that we think offers a superior development experience.

Another important difference between these offerings is that Vue’s companion libraries for state management and routing (among other concerns) are all officially supported and kept up-to-date with the core library. React instead chooses to leave these concerns to the community, creating a more fragmented ecosystem. Being more popular though, React’s ecosystem is considerably richer than Vue’s.

Finally, Vue offers a <strong>CLI project generator</strong> that makes it trivially easy to start a new project by featuring an interactive project scaffolding wizard. You can even use it to instant prototyping a component. React is also making strides in this area with <strong>create-react-app</strong>, but it currently has a few limitations:
- It does not allow any configuration during project generation, while Vue CLI runs on top of an upgradeable runtime dependency that can be extended via <strong>plugins</strong>.
- It only offers a single template that assumes you’re building a single-page application, while Vue offers a wide variety of default options for various purposes and build systems.
- It cannot generate projects from user-built presets, which can be especially useful for enterprise environments with pre-established conventions.
It’s important to note that many of these limitations are intentional design decisions made by the create-react-app team and they do have their advantages. For example, as long as your project’s needs are very simple and you never need to “eject” to customize your build process, you’ll be able to update it as a dependency. You can read more about the differing philosophy here.

#### Scaling Down
React is renowned for its steep learning curve. Before you can really get started, you need to know about JSX and probably ES2015+, since many examples use React’s class syntax. You also have to learn about build systems, because although you could technically use Babel Standalone to live-compile your code in the browser, it’s absolutely not suitable for production.

While Vue scales up just as well as React, it also scales down just as well as jQuery. That’s right - to get started, all you have to do is drop a single script tag into the page:
![ejLtAI.png](https://s2.ax1x.com/2019/08/11/ejLtAI.png)
Then you can start writing Vue code and even ship the minified version to production without feeling guilty or having to worry about performance problems.

Since you don’t need to know about JSX, ES2015, or build systems to get started with Vue, it also typically takes developers less than a day reading the guide to learn enough to build non-trivial applications.

## Native Rendering
React Native enables you to write native-rendered apps for iOS and Android using the same React component model. This is great in that as a developer, you can apply your knowledge of a framework across multiple platforms. On this front, Vue has an official collaboration with <strong>Weex</strong>, a cross-platform UI framework created by Alibaba Group and being incubated by the Apache Software Foundation (ASF). Weex allows you to use the same Vue component syntax to author components that can not only be rendered in the browser, but also natively on iOS and Android!

At this moment, Weex is still in active development and is not as mature and battle-tested as React Native, but its development is driven by the production needs of the largest e-commerce business in the world, and the Vue team will also actively collaborate with the Weex team to ensure a smooth experience for Vue developers.

Another option is <strong>NativeScript-Vue</strong>, a <strong>NativeScript</strong> plugin for building truly native applications using Vue.js.

## With MobX
MobX has become quite popular in the React community and it actually uses a nearly identical reactivity system to Vue. To a limited extent, the React + MobX workflow can be thought of as a more verbose Vue, so if you’re using that combination and are enjoying it, jumping into Vue is probably the next logical step.

## Preact and Other React-Like Libraries
React-like libraries usually try to share as much of their API and ecosystem with React as is feasible. For that reason, the vast majority of comparisons above will also apply to them. The main difference will typically be a reduced ecosystem, often significantly, compared to React. Since these libraries cannot be 100% compatible with everything in the React ecosystem, some tooling and companion libraries may not be usable. Or, even if they appear to work, they could break at any time unless your specific React-like library is officially supported on par with React.
