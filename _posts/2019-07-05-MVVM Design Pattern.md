---
layout: post
title: MVVM Design Pattern
subtitle: Architectural Pattern
date: 2019-07-05
author: Jalever
header-img: img/design_pattern_bg_simple.png
catalog: true
tags:
  - Design Pattern
---

- [Overview](#overview)
- [Components of MVVM pattern](#components-of-mvvm-pattern)
    - [Model](#model)
    - [View](#view)
    - [View Model](#view-model)
    - [Binder](#binder)
- [Rationale](#rationale)
- [Criticism](#criticism)
- [Implementations](#implementations)
    - [JavaScript frameworks](#javaScript-frameworks)

## Overview
<strong>odel–View–ViewModel</strong>(MVVM) is a <strong>Software Architectural Pattern</strong>.

<strong>MVVM</strong> facilitates a separation of development of the Graphical User Interface – be it via a markup language or GUI code – from development of the business logic or back-end logic (the data model).

The <strong>View Model</strong> of MVVM is a value converter, meaning the <strong>View Model</strong> is responsible for exposing (converting) the data objects from the <strong>Model</strong> in such a way that objects are easily managed and presented. In this respect, the <strong>View Model</strong> is more model than view, and handles most if not all of the <strong>View</strong>'s display logic. The <strong>View Model</strong> may implement a `Mediator Pattern`, organizing access to the back-end logic around the set of use cases supported by the <strong>View</strong>.

<strong>MVVM</strong> is a variation of <strong>Martin Fowler</strong>'s <strong>Presentation Model</strong> design pattern. <strong>MVVM</strong> abstracts a <strong>View</strong>'s state and behavior in the same way, but a <strong>Presentation Model</strong> abstracts a view (creates a view model) in a manner not dependent on a specific User-Interface platform.

<strong>MVVM</strong> was invented by Microsoft architects <strong>Ken Cooper</strong> and <strong>Ted Peters</strong> specifically to simplify event-driven programming of user interfaces. The pattern was incorporated into `Windows Presentation Foundation` (WPF) (Microsoft's .NET graphics system) and Silverlight (WPF's Internet application derivative). John Gossman, one of Microsoft's WPF and Silverlight architects, announced <strong>MVVM</strong> on his blog in 2005.

<strong>odel–View–ViewModel</strong> is also referred to as <strong>Model–View–Binder</strong>, especially in implementations not involving the `.NET` platform. `ZK` (a web application framework written in Java) and `KnockoutJS` (a JavaScript library) use <strong>Model–View–Binder</strong>.

![Zdoces.png](https://s2.ax1x.com/2019/07/05/Zdoces.png)

## Components of MVVM pattern

#### Model
<strong>Model</strong> refers either to a `domain model`, which represents real state content (an object-oriented approach), or to the `Data Access Layer`, which represents content (a data-centric approach)

#### View
As in the <strong>odel-View-Controller</strong>(MVC) and <strong>Model-View-Presenter</strong>(MVP) patterns, the <strong>View</strong> is the structure, layout, and appearance of what a user sees on the screen. It displays a representation of the <strong>Model</strong> and receives the user's interaction with the <strong>View</strong> (clicks, keyboard, gestures, etc.), and it forwards the handling of these to the <strong>View Model</strong> via the data binding (properties, event callbacks, etc.) that is defined to link the <strong>View</strong> and <strong>View Model</strong>.

#### View Model
The <strong>View Model</strong> is an abstraction of the <strong>View</strong> exposing public properties and commands. Instead of the <strong>Controller</strong> of the <strong>MVC</strong> pattern, or the <strong>Presenter</strong> of the <strong>MVP</strong> pattern, <strong>MVVM</strong> has a <strong>Binder</strong>, which automates communication between the <strong>View</strong> and its bound properties in the <strong>View Model</strong>. The <strong>View Model</strong> has been described as a state of the data in the <strong>Model</strong>.

The main difference between the <strong>View Model</strong> and the <strong>Presenter</strong> in the <strong>MVP</strong> pattern, is that the <strong>Presenter</strong> has a reference to a <strong>View</strong> whereas the <strong>View Model</strong> does not. Instead, a <strong>View</strong> directly binds to properties on the <strong>View Model</strong> to send and receive updates. To function efficiently, this requires a binding technology or generating boilerplate code to do the binding.

#### Binder
Declarative data and command-binding are implicit in the <strong>MVVM</strong> pattern. In the Microsoft solution stack, the <strong>Binder</strong> is a markup language called `XAML`. The <strong>Binder</strong> frees the developer from being obliged to write boiler-plate logic to synchronize the <strong>View Model</strong> and <strong>View</strong>. When implemented outside of the Microsoft stack, the presence of a declarative data binding technology is what makes this pattern possible, and without a <strong>Binder</strong>, one would typically use <strong>MVP</strong> or <strong>MVC</strong> instead and have to write more boilerplate (or generate it with some other tool).

## Rationale
<strong>MVVM</strong> was designed to make use of data binding functions in `WPF` (Windows Presentation Foundation) to better facilitate the separation of <strong>View</strong> layer development from the rest of the pattern, by removing virtually all GUI code ("code-behind") from the <strong>View</strong> layer. Instead of requiring `User Experience`(UX) developers to write GUI code, they can use the framework markup language (e.g., `XAML`) and create data bindings to the view model, which is written and maintained by <strong>Application Developers</strong>. <ins>The separation of roles allows interactive designers to focus on UX needs rather than programming of business logic.</ins> The layers of an application can thus be developed in multiple work streams for higher productivity. Even when a single developer works on the entire code base, a proper separation of the <strong>View</strong> from the <strong>Model</strong> is more productive, as user interface typically changes frequently and late in the development cycle based on end-user feedback.

The <strong>MVVM</strong> pattern attempts to gain both advantages of separation of functional development provided by <strong>MVC</strong>, while leveraging the advantages of data bindings and the framework by binding data as close to the pure application model as possible. It uses the <strong>Binder</strong>, <strong>View Model</strong>, and any business layers' data-checking features to validate incoming data. The result is that the model and framework drive as much of the operations as possible, eliminating or minimizing application logic which directly manipulates the <strong>View</strong> (e.g., code-behind).

## Criticism
A criticism of the pattern comes from <strong>MVVM</strong> creator John Gossman himself, who points out that the overhead in implementing <strong>MVVM</strong> is "overkill" for simple UI operations. He says that for larger applications, generalizing the <strong>ViewModel</strong> becomes more difficult. Moreover, he illustrates that data binding in very large applications can result in considerable memory consumption.

## Implementations
#### JavaScript frameworks
- Angular
- React
- Vue
