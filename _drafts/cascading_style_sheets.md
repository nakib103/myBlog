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

- Content (height/width):<br>
properties: height, width, max-width.<br>
value: length, percentage of the containing block, auto, inherit, initial.

- Padding:<br>
properties: padding-top, padding-right, padding-bottom, padding-left, padding (shorthand), box-sizing<br>
value: length, percentage of the containing block, inherit.

- Border:<br>
properties: border-style, border-width, border-color, border-top, border-right, border-bottom, border-left, border (shorthand), border-radius.

- Margin:
properties: margin-top, margin-right, margin-bottom, margin-left, margin.<br>
value: length, percentage of containing containing element, auto, inherit.

Outline:
Color:
Background:

### CSS Position
### CSS Text/Font
properties: animation-name, animation-duration, animation-timing-function, animation-delay, animation-iteration-count, animation-direction, animation-fill-mode, animation (shorthand).

@key-frame 

### CSS Transforms
properties: transform, transform-origin
value: transition, rotate, scale, scaleX, scaleY, skew, skewX, skewY, matrix

### CSS Display
properties: display, visibility.<br>
value: none, block, inline

## Bootstrap
Bootstrap is a front-end framework. It include HTML and CSS based design template and gives ability to create responsive design easily.

### Adding Bootstrap
{% highlight HTML %}
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
{% endhighlight %}

### Components
- [navbar][bootstrap-navbar]:
- [card][bootstrap-card]:

### Layouts
[containers][bootstrap-containers]: give a responsive … .container (fixed-width) .container-fluid (full-width)

### Content
[typography][bootstrap-typography]: bootstrap typography like heading, display

### Utility
- [flex][bootstrap-flex]:
- [grid][bootstrap-grid]:
- [spacing][bootstrap-spacing]: shorthand classes for margin and padding. Format → {property}{sides}-{size} or {property}{sides}-{breakpoint}-{size}<br>
property: m - margin; p - padding
sides: t - *-top; b - *-bottom; l - *-left; r - *-right; x - *-left, *-right; y - *-top, *-bottom;<br>
size: 0 → 0, 1 → .25, 2 → .50, 3 → 1, 4 → 1.5, 5 → 3, auto
- [float][bootstrap-float]: toggle float. Format → float-{breakpoint}-{direction}
- [color][bootstrap-color]: specific color types for content or background. link-* have :hover and :focus states. Format → text-{type} or bg-{type} or bg-gradient-{type}  link-{type}<br>
type: primary, secondary, success, danger, warning, info, light, dark, muted, white
--bs-blue: #0d6efd;
--bs-indigo: #6610f2;
--bs-purple: #6f42c1;
--bs-pink: #d63384;
--bs-red: #dc3545;
--bs-orange: #fd7e14;
--bs-yellow: #ffc107;
--bs-green: #198754;
--bs-teal: #20c997;
--bs-cyan: #0dcaf0;
--bs-white: #fff;
--bs-gray: #6c757d;
--bs-gray-dark: #343a40;
--bs-primary: #0d6efd;
--bs-secondary: #6c757d;
--bs-success: #198754;
--bs-info: #0dcaf0;
--bs-warning: #ffc107;
--bs-danger: #dc3545;
--bs-light: #f8f9fa;
--bs-dark: #212529; 

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