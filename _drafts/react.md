---
layout: post
title: "React"
category: jekyll update
---

React is JavaScript Library to build UI and used to build single page application. It helps to build reusable UI components.

## Why React
- virtual DOM - faster!
- reusable components - cleaner!

## Creating React Application
### From Scratch

Pre-requisite for creating React app for scratch
- index.html
- root component
- webpack
- support for ES6
- react-hot-loader

## Concepts

### JSX
JSX is a variation of javascript that React team created. It is a lot like html.

- We need react library to compile JSX. Use import React form 'react'
- JSX does not support sibling root element. `<h1>hello</h1><h2>World</h2` will create error. To do this include them inside a parent element such as <div>.

### ES6 syntax
Some ES6 syntax of JavaScript is important in React - 

- import export: we need `import` and `export` to create React Components and import them.
- let unlike var: `let` lets you declare variable within block statement or expression scope where it is defined.

### Components
We can write JavaScript function that returns a JSX component and rendered in ReactDOM. The function name convention is camelCase with capitalization and called a React Component.

parent/child component

#### JSX to JavaScript and back
We use `{}` to write JavaScript inside JSX.

#### Styling JSX component
- external CSS: use className instead of class to add a class to JSX element. Because React actually use javascript className DOM api to do this.
- inline CSS: we need to provide a JavaScript object instead of a string which we used to do in HTML. This calls for some changes from CSS syntax - 
  - as JavaScript object is wrapped around `{}` which is also used to escape from JSX to JavaScript. Therefore we will be needing `{{}}` to pass CSS style object for styling JSX elements. 
  - we cannot use `-` inside JavaScript, therefore for JSX styling we can omit the `-` and make the word camelCase.
- Styled Components - 

#### Class based components
We can also create a class based components instead of function based components. 

{% highlight React %}
class MyComponent extends React.Componenet 
{% endhighlight %}

We should include `render` method in our class based components.
Props - to access props in class-based components use `this.props`.

### Props - Attributes to React Component
We can define attributes to React Component much like HTML element attribute using props.

{% highlight React %}
const App = (props) => (
  <div>
    <img src={props.imgUrl}/>
    <p>{props.name}</p>
    <p>{props.salary}</p>
  </div>
)
{% endhighlight %}

Note that props is a javascript object and that’s why we need to wrap it around using `{}`. For Props with large number of elements like 20-30 we would be better to pass it from a json file.

### Stats - Mutable Property
Props are immutable. In class-based React Components we can use Stats that is mutable that is we can change the value of the Stats later in Components that is receiving the Stats.

Stats are actually similar to property of class object in javascript and defined in `constructor` method.

{% highlight React %}
class MyContainer extends React.Component {
  constructor(){
    super()
    this.state= 'value'
  }
}
{% endhighlight %}

We can pass State as Props to child component in React.
Changing Stats: we can just access Stats and change their value by this.state= 'newValue' but React has some setter mechanism for this.

{% highlight React %}
class MyContainer extends React.Component {
  constructor(){
    super()
    this.state = {
      key1: 'value1',
      key2: 'value2',
    }
    this.stateChangeFunc = this.stateChangeFunc.bind(this)
  }
  
  stateChangeFunc(){
    this.setState({key1: 'newValue1'})
    this.setState((prevState) => {
      key2: 'new' + prevState.key2
    })
  }
}
{% endhighlight %}

The cool thing is if we change the State of a Component this change is passed down to all the child Components which are receiving this state.

### Event Handling
- the event handler in JSX are same as javascript instead of HTML syntax. That’s why we should use onClick instead of onclick in buttons.
- we will also pass function as object instead of strings. So, we will write `<button onClick={MyFunction}>Click me!<button/>`

### Lifecycle
- componentDidMount
- getDerivedStateFromProps
- componentWillReceiveProps
- shouldComponentUpdate
- getSnaphotBeforeUpdate
- componentWillUnmount

### Conditional Rendering

### Forms
- Controlled Forms
- Formik library

### Synthetic Events
### Smart and Dump Components