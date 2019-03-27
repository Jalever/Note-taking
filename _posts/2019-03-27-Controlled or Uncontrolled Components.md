---
layout: post
title: Controlled / Uncontrolled Components
subtitle: React学习笔记系列
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.png
catalog: true
tags:
  - React
---

- [Uncontrolled Components](#uncontrolled-components)
- [Controlled Components](#controlled-components)

## Uncontrolled Components
Certain `DOM` elements such as `<input>`, `<textarea>`, and `<select>` that by default maintain state (***user input***) within the `DOM` layer.<br>
A `Uncontrolled Component` is one that stores its own state internally, and you query the `DOM` using a `ref` to find its current value when you need it. <br>
This is a bit more like traditional HTML.
```javascript
class Form extends React.Component{
  
  formHandler(event){
  event.preventDefault();
  const name = this.input.value
  //do something with "name"

  }

  render(){
    return(
      <div >
        <form onSubmit={this.formHandler.bind(this)}>
          <label>Name</label>
            <input type='text' ref={(userInput) => this.input = 
              userInput}/>
            <input type='submit'/>
        </form>
      </div>
    )
  }
}
```

## Controlled Components
`Controlled components` keep that state inside of `React` either in the component rendering the input, a parent component somewhere in the tree, or a flux store.<br>
A `Controlled Component` is one that takes its current value through props and notifies changes through callbacks like `onChange`. <br>
A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component. 

```javascript
class Form extends React.component{
 constructor(){
   super()
    this.state={
     name: ""
    }
 }

 nameChange(event){
  const inputName = event.target.value
   this.setState({
     name: inputName
   })
 }

 render(){
   return(
    <div>
     <form>
       <label>Name:</label>
       <input type="text" value={this.state.name} onChange=
       {this.nameChange.bind(this)}/>
       <input type="submit"/>
     </form>
    </div>
   )
  }
}
```