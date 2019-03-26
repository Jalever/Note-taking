---
layout: post
title: Uncontrolled Components
subtitle: React学习笔记系列
date: 2019-03-26
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

In most cases, we recommend using `controlled components` to implement forms. In a `controlled component`, form data is handled by a `React` component. The alternative is `uncontrolled components`, where form data is handled by the `DOM` itself.<br>
To write an `uncontrolled component`, instead of writing an event handler for every state update, you can use a `ref` to get form values from the `DOM`.
For example, this code accepts a single name in an `uncontrolled component`:

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert("A name was submitted: " + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

Since an `uncontrolled component` keeps the source of truth in the DOM, it is sometimes easier to integrate `React` and `non-React` code when using `uncontrolled components`. It can also be slightly less code if you want to be quick and dirty. Otherwise, you should usually use `controlled components`.

## Default Values
In the `React` rendering lifecycle, the `value` attribute on form elements will override the value in the `DOM`. <br>
With an `uncontrolled component`, you often want `React` to specify the initial value, but leave subsequent updates uncontrolled. <br>
To handle this case, you can specify a `defaultValue` attribute instead of value.
```javascript
render() {
  return (
    <form onSubmit={this.handleSubmit}>
      <label>
        Name:
        <input
          defaultValue="Bob"
          type="text"
          ref={this.input} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```
Likewise, `<input type="checkbox">` and `<input type="radio">` support `defaultChecked`, and `<select>` and `<textarea>` supports `defaultValue`.


## The file input Tag
In HTML, an `<input type="file">` lets the user choose one or more files from their device storage to be uploaded to a server or manipulated by `JavaScript` via the `File API`.
```javascript
<input type="file" />
```
In `React`, an `<input type="file" />` is always an `uncontrolled component` because its value can only be set by a user, and not programmatically.