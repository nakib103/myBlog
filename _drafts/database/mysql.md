---
layout: post
title: "MySQL"
category: jekyll update
---

## Clauses

### SELECT
{% highlight MySQL %}
SELECT <column name>
FROM <table name>
WHERE <condition>
ORDER BY <column name>
LIMIT <offset, no of records>
{% endhighlight %}

1. column name : 
- multiple column name can be separated by , . To select all columns we can use * 
- we can use expression using column names, such as SELECT (points * 20) + 10 FROM users;  
- AS can be used to create an alias for column name.
- DISTINCT can be used to get unique records for the columns.

2. condition : 
a conditional expression using column values.
- conditional operator: <, >, <=, >=, ==, !=, <>
- multiple conditions using: AND, OR, NOT
- IN\NOT IN : return if a column value matches from a range of values -

{% highlight MySQL %}
SELECT * FROM users WHERE points IN (100, 200, 300);
{% endhighlight %}

- BETWEEN\NOT BETWEEN : return if column value is within a range - 

{% highlight MySQL %}
SELECT * FROM users WHERE points BETWEEN (100, 300);
{% endhighlight %}

- LIKE\NOT LIKE : return if a column value is like a string. % matches any number of character and _ matches a single character -

{% highlight MySQL %}
# matches users with first name with a at second character
SELECT * FROM users WHERE first_name LIKE _a%; 
{% endhighlight %}

- REGEXP\NOT REGEXP : return if a column value matches with a regular expression. ^ matches beginning of string, $ matches end of string, | for alteration or multiple pattern, [] match any single character, [-] matches a single character from range of character.
 
- IS NULL\IS NOT NULL : return if a column value is NULL -

{% highlight MySQL %}
SELECT * FROM users WHERE points IS NOT NULL;
{% endhighlight %}

3. ORDER BY : 
Returns the records in ascending order. 
- ASC for ascending order and DESC for descending order
- we can use multiple columns using , . In that case first column value is used for sorting and if values from two or more records matches the second column values then used for sorting and so on.

{% highlight MySQL %}
SELECT * FROM users ORDER BY points, name DESC;
{% endhighlight %}

4. LIMIT : 
Returns only number of rows mentioned by limit clause.
- offset : number of rows to skip. This is optional
- no of records : no of records to return from start or after the offset value if mentioned.

{% highlight MySQL %}
SELECT * FROM users LIMIT 3, 4;
{% endhighlight %}

### INSERT
### UPSATE
### DELETE