---
layout: post
title: "ElasticSearch"
category: jekyll update
---

- Elasticsearch is the distributed search and analytics engine of the elastic stack
- It stores documents as JSON
- It gives result in near real-time - (~1s) with the use of data structure inverted index
- An inverted index lists every unique words appeared in any documents and can identify the documents that a words appeared.

### Concepts
#### Data In
We store data in Elasticsearch using JSON as document. Elasticsearch stores this document in searchable indices.

#### Index
#### Documents
#### Fields
Each field has dedicated optimized data structure - e.g. inverted index for text; BKD tree for number, geo data etc.

#### Dynamic Mapping
#### Data Stream
Time series data is typically added to a data stream. A data stream create multiple and auto-generated backing indices to store the documents. The data must contain @timestamp field to be stored in data stream.

{% highlight bash %}
curl -X GET -H "Content-Type: application/json" -d"{ "@timestamp": "2021-07-09T13:45:45.009Z", "event": { "original": "blah ba blah ba"} }" http://localhost:9200/<data stream name>/_doc?pretty
{% endhighlight %}

### Data Out
#### REST API
- Structured query
- Full text query
- Complex query
phrase searches, similarity searches, and prefix searches. geo and numerical queries.

#### Query DSL
#### SQL like query
#### Elasticsearch client

### Infra
#### Cluster
#### Node
#### Shard
A shard is a self-contained index. The documents inside a index can be distributed across multiple shards and those shards are distributed over multiple nodes. There are primary shards and replicas. Replica shards gives redundancy that increases resilience.

Balancing the size of shards and number of shards is crucial.

#### CCR (Cross Cluster Replication)

### Source
https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html