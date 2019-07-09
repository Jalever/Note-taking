---
layout: post
title: Refs and the DOM
subtitle: React Advanced Guides
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg.png
catalog: true
tags:
  - React
---

&ensp;&ensp;**_Refs_** provide a way to `access DOM nodes` or `React elements` created in the render method.

&ensp;&ensp;In the typical React dataflow, props are the only way that parent components interact with their children. To modify a child, you re-render it with new props.

&ensp;&ensp;There are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child to be modified could be an instance of a React component, or it could be a DOM element.

- [When to Use Refs](#when-to-use-refs)
- [Creating Refs](#creating-refs)
- [Accessing Refs](#accessing-refs)
    - [Adding a Ref to a DOM Element](#adding-a-ref-to-a-dom-element)
    - [Adding a Ref to a Class Component](#adding-a-ref-to-a-class-component)
    - [Refs and Function Components](#refs-and-function-components)
- [Exposing DOM Refs to Parent Components](#exposing-dom-refs-to-parent-components)
- [Callback Refs](#callback-refs)
- [Legacy API: String Refs](#legacy-api-string-refs)
- [Caveats with callback refs](#caveats-with-callback-refs)

## When to Use Refs

- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.

## Creating Refs

&ensp;&ensp;`Refs` are created using `React.createRef()` and attached to `React` elements via the `ref` attribute.
&ensp;&ensp;`Refs` are commonly assigned to an instance property when a component is constructed so they can be referenced throughout the component.

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```

## Accessing Refs

When a `ref` is passed to an element in <ins>**_render_**</ins>, a reference to the node becomes accessible at the <ins>**_current_**</ins> attribute of the ref.

```javascript
const node = this.myRef.current;
```

The value of the ref differs depending on the type of the node:

- When the <ins>**_ref_**</ins> attribute is used on an HTML element, the <ins>**_ref_**</ins> created in the constructor with <ins>**_React.createRef()_**</ins> receives the underlying DOM element as its <ins>**_current_**</ins> property.
- When the <ins>**_ref_**</ins> attribute is used on a custom class component, the <ins>**_ref_**</ins> object receives the mounted instance of the component as its <ins>**_current_**</ins>.
- You may not use the ref attribute on function components because they don’t have instances.

#### Adding a Ref to a DOM Element

This code uses a <ins>**_ref_**</ins> to store a reference to a DOM node:

```javascript
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // create a ref to store the textInput DOM element
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // Explicitly focus the text input using the raw DOM API
    // Note: we're accessing "current" to get the DOM node
    this.textInput.current.focus();
  }

  render() {
    // tell React that we want to associate the <input> ref
    // with the `textInput` that we created in the constructor
    return (
      <div>
        <input
          type="text"
          ref={this.textInput} />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

&ensp;&ensp;React will assign the <ins>**_current_**</ins> property with the DOM element when the component mounts, and assign it back to <ins>**_null_**</ins> when it unmounts. <ins>**_ref_**</ins> updates happen before <ins>**_componentDidMount_**</ins> or <ins>**_componentDidUpdate_**</ins> lifecycle methods.

#### Adding a Ref to a Class Component

If we wanted to wrap the <ins>**_CustomTextInput_**</ins> above to simulate it being clicked immediately after mounting, we could use a ref to get access to the custom input and call its <ins>**_focusTextInput_**</ins> method manually:

```javascript
class AutoFocusTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }

  componentDidMount() {
    this.textInput.current.focusTextInput();
  }

  render() {
    return (
      <CustomTextInput ref={this.textInput} />
    );
  }
}
```

#### Refs and Function Components

&ensp;&ensp;You may not use the ref attribute on function components because they don’t have instances:

```javascript
function MyFunctionComponent() {
  return <input />;
}

class Parent extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }
  render() {
    // This will *not* work!
    return (
      <MyFunctionComponent ref={this.textInput} />
    );
  }
}
```

&ensp;&ensp;You can use the ref attribute inside a function component as long as you refer to a DOM element or a class component:

```javascript
function CustomTextInput(props) {
  // textInput must be declared here so the ref can refer to it
  let textInput = React.createRef();

  function handleClick() {
    textInput.current.focus();
  }

  return (
    <div>
      <input
        type="text"
        ref={textInput} />
      <input
        type="button"
        value="Focus the text input"
        onClick={handleClick}
      />
    </div>
  );
}
```

## Exposing DOM Refs to Parent Components

&ensp;&ensp;In rare cases, you might want to have access to a child’s DOM node from a parent component.

## Callback Refs

&ensp;&ensp;Instead of passing a <ins>**_ref_**</ins> attribute created by <ins>**_createRef()_**</ins>, you pass a function. The function receives the React component instance or HTML DOM element as its argument, which can be stored and accessed elsewhere.

```javascript
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);

    this.textInput = null;

    this.setTextInputRef = element => {
      this.textInput = element;
    };

    this.focusTextInput = () => {
      // Focus the text input using the raw DOM API
      if (this.textInput) this.textInput.focus();
    };
  }

  componentDidMount() {
    // autofocus the input on mount
    this.focusTextInput();
  }

  render() {
    // Use the `ref` callback to store a reference to the text input DOM
    // element in an instance field (for example, this.textInput).
    return (
      <div>
        <input
          type="text"
          ref={this.setTextInputRef}
        />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

&ensp;&ensp;React will call the ref callback with the DOM element when the component mounts, and call it with null when it unmounts.

You can pass callback refs between components like you can with object refs that were created with <ins>**_React.createRef()_**</ins>.

```javascript
function CustomTextInput(props) {
  return (
    <div>
      <input ref={props.inputRef} />
    </div>
  );
}

class Parent extends React.Component {
  render() {
    return (
      <CustomTextInput
        inputRef={el => this.inputElement = el}
      />
    );
  }
}
```

&ensp;&ensp;In the example above, Parent passes its ref callback as an inputRef prop to the CustomTextInput, and the CustomTextInput passes the same function as a special ref attribute to the <input>. As a result, this.inputElement in Parent will be set to the DOM node corresponding to the <input> element in the CustomTextInput.

## Legacy API: String Refs

&ensp;&ensp;If you worked with React before, you might be familiar with an older API where the ref attribute is a string, like "textInput", and the DOM node is accessed as this.refs.textInput. We advise against it because string refs have some issues, are considered legacy, and are likely to be removed in one of the future releases.

## Caveats with callback refs

&ensp;&ensp;If the <ins>**_ref_**</ins> callback is defined as an `inline function`, it will get called `twice` during updates, first with <ins>**_null_**</ins> and then again with the DOM element. This is because a new instance of the function is created with each render, so React needs to clear the old ref and set up the new one. You can avoid this by defining the <ins>**_ref_**</ins> callback as a bound method on the class, but note that it shouldn’t matter in most cases.
