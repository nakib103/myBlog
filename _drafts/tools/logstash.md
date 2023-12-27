---
layout: post
title: "Logstash"
category: jekyll update
---

Open source data collection engine with real-time pipelining capabilities. 
{% highlight bash %}
bin/logstash -e 'input {stdin{}} output {stdout{}}'
{% endhighlight %}

### Source
https://www.elastic.co/guide/en/logstash/current/index.html