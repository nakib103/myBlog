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

### Class

## JavaScript HTML DOM

### Document

### Element
an javascript Element object refers to HTML element like <p>, <body>, <div>. Can be created by `createElement()` and added by a function such as `appendChild()`.

## JavaScript Browser BOM

![need_replacing bom]({{ site.baseurl }}/_images/js_bom.png)

## JavaScript Web API

## JavaScript Async

### Callbacks
A callback is a function passed as a argument of another function.

{% highlight JavaScript %}
// calling callbackFunction as argument of myFunction
function callbackFunction(){
  // do something
}
function myFunction(arg1, arg2, callbackFunction){
  // do something
}

// we can define callback inside parameter list
function myFunction(arg1, arg2, function(){//do something}){
  // do something
}
{% endhighlight %}

### Promises
Promise object contains a producing code (either success or failure) that runs asynchronously.

{% highlight JavaScript %}
let promise = Promise(function(resolve, reject){
  // do somthing
  // if successfull call resolve callback
  resolve(value);
  // if fail call reject callback
  reject(error);
});
promise.then(
  function(value){// do something with value};
  function(error){// do something with error};
);
{% endhighlight %}

Promise object has 2 Properties - state and result and there value is changed as follows -

![need_replcing js_promise]({{ site.baseurl }}/_images/js_promise.png)

We can use the resolve and reject callbacks to set the state and result properties, but only the first one is counted.

### Async and Await
async before a function returns a Promise object. We can use await in async function to wait for a Promise object.

## JavaScript AJAX
AJAX → Asynchronous JavaScript and XML

### XMLHTTPRequest Object

XMLHTTP Request object can be used to exchange data with the server behind the scene. But it can only communicate with the server the web page is hosted not across domains - we can use fetch for that.
The following code xhttp opens a text.txt in asynchronously and send the data in it. We update an element content with the data.

{% highlight JavaScript %}
var xhttp = new XMLHTTPRequest();
xhttp.open("GET", "http:<domain>/text.txt", false);
xhttp.send();
document.getElementById("someID").innerHTML = xhttp.responseText

// send method
{% endhighlight %}

- open method: `open(method, url, async, user, psw)`
- send method: `send()` `send(data)`

But this is considered dangerous as JavaScript will stop executing until the response is ready and if server is slow it can hang the application. Synchronous method -

{% highlight JavaScript %}
var xhttp = new XMLHTTPRequest();
xhttp.onreadystatechange = function(){
  if(this.readyState == 4 && this.status == 200){
    document.getElementById("some_id").innerHTML = this.response.Text;
  }
};
xhttp.open("GET", "http:<domain>/text.txt", false);
xhttp.send();
{% endhighlight %}

XMLHTTPRequest properties:

- readyState: value → 0: uninitialized, 1: connection established, 2: request received, 3: request processing, 4: response ready
- status
- onreadystatechange: called 4 times for 4 state change
- responseText
- responseXML

### fetch()
fetch can use cross domain request and returns a Response Promise object.

{% highlight JavaScript %}
vat respose = fetch(<url>)

// response is promise object. say we want to read a text file from our server at 8000
async readText(){
  response = await fetch("http://localhost:8000/temp.txt");
  // text() also returns a Promise object; thenable
  response.text().then((text) => alert(text));
}
{% endhighlight %}

## Source
https://www.w3schools.com/js/