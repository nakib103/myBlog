---
layout: post
title: "JQuery"
category: jekyll update
---

## Basic Syntax

{% highlight JQuery %}
\$(selector).action()
{% endhighlight %}

`$` is synonymous with jQuery<br>
`$(“document“).ready(function(){})` <br>
The advantage of this syntax over `window.onload()` is that the later triggers when all html, css and external resource have loaded but the earlier one will trigger when the html has been parsed - even if the external resource still has not finished loading.