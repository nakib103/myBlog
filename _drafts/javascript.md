---
layout: post
title: "Javascript"
category: jekyll update
---

## JavaScript Execution
- Inside HTML: JavaScript can be added in <body> or <head> but <body> is better as script interpretation takes longer time. We use \<script> element.

- External JavaScript: Keep JavaScript code in separate folder and tell the location in src attribute of \<script> element.

## JavaScript basics

###  Variables (or Object?)

#### Number
JavaScript only has one number type - it can either contain decimal or not. 
#### String
#### Boolean
{% highlight JavaScript %}
# declaration
var <object_name> = false
var <object_name> = true
{% endhighlight %}

Anything with a value is true and without value is false, such as - 0, -0, ““, `null`, `undefined`.

#### JSON
#### Date

### Array
{% highlight JavaScript %}
# declaration
var <array_name> = [<value>, <value>, <value>, ...]

# accessing element
var <object_name> = <array_name>[index]

# changing an element
<array_name>[index] = <value>
{% endhighlight %}
arrays use numbered indexes and object use named indexes.

Useful array property and methods:

- length
- isArray()
- push()

### Operators/Expressions
### Conditionals
### Loop
### Functions

#### Arrow Functions
{% highlight JavaScript %}
var <object_name> = (par1, par2, ..) => {//do something};

// for function with one statement that returns something {} and return is optional
var hello = () => "Hello JavaScript";
{% endhighlight %}

#### Higher order methods
- map → 
{% highlight JavaScript %}
const arr = {1, 2, 3, 4, 5}
const doubled = arr.map((num) => {
  return num * 2
})
{% endhighlight %}
- filter → 
- sort → 
- reduce → 
- every → 
- some → 
- find → 
- findIndex →

## Source
https://www.w3schools.com/css/default.asp

[bootstrap-navbar]: https://getbootstrap.com/docs/4.0/components/navbar/
[bootstrap-card]: https://getbootstrap.com/docs/4.0/components/card/
[bootstrap-containers]: https://getbootstrap.com/docs/5.0/layout/containers/
[bootstrap-typography]: https://getbootstrap.com/docs/4.0/content/typography/
[bootstrap-flex]: https://getbootstrap.com/docs/4.0/utilities/flex/
[bootstrap-grid]: https://getbootstrap.com/docs/4.0/layout/grid/
[bootstrap-spacing]: https://getbootstrap.com/docs/4.0/utilities/spacing/
[bootstrap-float]: https://getbootstrap.com/docs/4.0/utilities/float/
[bootstrap-color]: https://getbootstrap.com/docs/4.0/utilities/colors/