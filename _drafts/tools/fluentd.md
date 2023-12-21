---
layout: post
title: "fluentd"
category: jekyll update
---

### Concepts
#### Input
Input plugin is responsible for generating fluentd events from data sources

#### Event 
- tag: specifies where the event originated from and used for message routing
- time: timestamp of the event (with nanoseconds resolution)
- record” actual data in JSON format

#### Output
#### Filter
{% highlight xml %}
<filter <tag_name>>
  @type <type>
  rule..
</filter>
{% endhighlight %}

#### Router Engine
#### Label
#### Buffer

### Plugins
Fluentd has eight (8) types of plugins:
- Input
- Parser
- Filter
- Output
- Formatter
- Storage
- Service Discovery
- Buffer

### Source
https://docs.fluentd.org/quickstart