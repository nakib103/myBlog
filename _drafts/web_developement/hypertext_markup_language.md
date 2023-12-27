---
layout: post
title: "HTML: Hypertext Markup Language"
category: jekyll update
---

## What is HTML
HTML is a markup language for websites. It is not case-sensitive.

### Execution Process

HTML page is parsed sequentially from beginning to end. As resources are encountered like image and stylesheets browser executes parallel request for them. But if script tag is found they are loaded and executed first before proceeding. Exception is script tag with attribute `defer` or `sync`. Browser may however sometimes look-ahead and request another script tag execution in parallel with current script tag running.

## Page Structure
{% highlight HTML %}
<html>

<head> Meta data about the HTML document</head>

<body> Document content </body>

</html>
{% endhighlight %}

## Elements and Attributes

An element is defined by a <start tag>, then some content, then </end tag>. An empty element is that does not have any content.

All HTML elements can have attributes and provide additional information about the element. Attributes are always specified in the start tag. Attributes usually come in name-value pairs like: name="value".

| Element | Description | Attributes |
|---------|-------------|------------|
|<!DOCTYPE>|Defines document type.||
|<html>|Defines the root of an HTML document.||
|<head>|Defines metadata about the document and is not shown.||
|<meta>|Defines metadata about the document.|charset&#10;name&#10;contenthtml-equiv|
|<title>|Defines title of the page and shown in page’s tab.||
|<link>|Defines relationship with external resource (stylesheet) with current document|rel&#10href&#10;href&#10;lang&#10;crossorigin|
|<script>|||
|<body>|Defines the document body.||
|<div> <span>|Defines container for elements. <div> is section; <span> is inline||
|<section>|Defines a section in a document||
|<aside>|Define contents aside from the content it is placed in||
|<nav>|||
|<h1> to <h6>|Defines different heading type.|||
|<p>|Defines a paragraph.||
|<i> <em> <strong> <mark> <cite> <dfn>|||
|<br>|Defines a line break.||
|<a>|Defines a hyperlink; stands for anchor|rel&#10;href|
|<ul> <ol> <li> <dl> <dt> <dd> |Unordered list, Ordered list with list item. Description list with term and description||
|\<input> \<button>|Defines an input control.||
|\<style>|Define style information for the document.||
|\<img>||src&#10;alt|

### Web App Manifests

Part of collection of technologies called Progressive Web Apps (PWA). They are websites that can be installed in devices home screen without an appstore. The web app manifest provides information about a web application in a json text file, necessary for the web app to be downloaded and be presented to the user similarly to a native app (e.g., be installed on the home screen of a device, providing users with quicker access and a richer experience).

{% highlight HTML %}
<link rel="manifest" href=/temp.webmanifest>
{% endhighlight %}

{% highlight JSON %}
// temp.webmanifest file (json format)
{
  "icons": [
    {
      "src": 
      "sizes": 
      "type":
    },
    ...
  ]
}
{% endhighlight %}

### Web Feeds

Web site visitor can subscribe to the feeds provided in the website. The updated contents are send to 'feed readers'. In this way they can stay updated about the content of the page even if they do not visit the website.

{% highlight HTML %}
<link rel="feed" href="/temp.xml" type="application/rss+xml">
{% endhighlight %}

### Twitter Cards
If you use twitter cards in your website if someone shares content of your site on twitter it will show a card with a preview.

## Source
- https://www.w3schools.com/html/default.asp
- https://developer.mozilla.org/en-US/docs/Web 
- https://schema.org/