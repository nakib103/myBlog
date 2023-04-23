---
layout: post
title: "CSS: Cascading Style Sheets"
category: jekyll update
---

## What is CSS
CSS or cascading style sheets define how HTML elements are shown in webpage, paper, media etc.

## CSS syntax

![css syntax]({{ site.baseurl }}/_images/css_syntax.png)

{% highlight css %}
h1 {
    color: blue;
    font-size: 12px;
}
{% endhighlight %}

## Adding CSS

### External CSS
{% highlight HTML %}
<html>
    <head>
        <link rel="stylesheet" type="text/css" href="mystyle.css">
    </head>
    <body>
    </body>
</html>
{% endhighlight %}

### Internal CSS

{% highlight HTML %}
<html>
    <head>
        <style>
            * {
                font-family: "Malgun Gothic", sans-serif;
            }
        </style>
    </head>
    <body>
    </body>
</hmlt>
{% endhighlight %}

### Inline CSS

{% highlight HTML %}
<html>
    <head>
    </head>
    <body>
        <h1 style="font-family: 'Malgun Gothic'"> Title Page </h1>
    </body>
</html>
{% endhighlight %}


Cascading order is Inline > Internal/External > Browser default

If multiple properties for same selector is defined in muliple stylesheet the last read stylesheet will take effect.

## CSS Selector

### Simple Selectors
- element selector: with element name, e.g. - h1 {colo: blue}
- id selector: #id: {color: blue}
- class selector: .class {color: blue}
- grouping selector: ele, ele {color: blue}
- universal selector: * {clor: blue}

### Combinators
A CSS selector can have multiple simple selector. Between the selector we can include a combinator that explains the relationship between selector. 
- descendaent: ele ele {color: blue}
- child: ele > ele {color: blue}
- adjacent sibling: ele + ele {color: blue}
- general sibling: ele ~ ele {color: blue} 

### Attribute Selectors
Select an element having attribute=value
- [attribute]
- [attribute="value"]
- [attribute~="value"]
- [attribute\|="value"]
- [attribute^="value"]
- [attribute$="value"]
- [attribute*="value"]

h1[target="_blank"] {color:blue}

### Pseudo class and element selector

### Not selector

## CSS Box Model

![box model]({{ site.baseurl }}/_images/css_box_model.png)

## Source
https://www.w3schools.com/css/default.asp