---
layout: post
title: "Python Language"
category: jekyll update
---

- Case sensitive
- File extension is .py
- Blocks of code is identified by indentation.
- Number of whitespace in indentation can be variable but all lines in block of code must have same number of whitespaces

### Comment
{% highlight python %}
# this is a single line comment

'''
This is a multi-line 
comment
'''
{% endhighlight %}

### Multi-line statements
{% highlight python %}
# use \
item = item_one + \
  item_two + \
  iteM_three
  
# no need for \ when using [], {}, ()
{% endhighlight %}

### Multiple command in single line
{% highlight python %}
import sys; x = "foo"; sys.stdout.write(x + "\n");
{% endhighlight %}

### Variables
#### Data Types
- Numbers
- String
- List
- Tuple
- Dictionary
- Set

#### Declaration
There is no need to declare variable like C. We can directly assign variable value and Python interprets the type.
{% highlight python %}
a = 10
b = "string"
{% endhighlight %}

#### Multiple assignment
{% highlight python %}
a = b = c = 1
{% endhighlight %}

#### Deletion
The reference to a variable can be deleted by using del
{% highlight python %}
del var_a, var_b, ..
{% endhighlight %}

#### Numbers
Python support four different numeral types - 

- integer
- long a = 100L  → Deprecated in Python 3
- float
- complex a = 3 + 4j

#### Strings
##### Quotation
Single, double, and triple quotation can be used. Triple quotation is used for multi-line string.

#### List
#### Tuple
#### Dictionary
#### Set
#### Data type conversion

### Modules
`__init__.py` : this file indicates the containing folder is a package

### Class
Magic methods
`__str__()` : this method represents a class object as string

### Source
- https://www.tutorialspoint.com/python/index.htm
- https://docs.python.org/3/reference/index.html
- https://peps.python.org/pep-0008/