---
layout: post
title: "C Language"
category: jekyll update
---

### Function
- Variadic function: Function with infinite arity (arguments).

### Pointer
Pointer is a special type of variable that stores the address of another variable

- Pointer Declaration:
{% highlight c %}
#type *var_name
int *p
{% endhighlight %}

- Pointer Assignment: & operator gives the address of a variable
{% highlight c %}
int a
int *p = &a
{% endhighlight %}

- Access value of the variable whose address stored in pointer: * gives that
{% highlight c %}
int a = 10
int *p = &a
printf("%d", *p)    # prints 10
{% endhighlight %}

- NULL Pointer:
{% highlight c %}
int *p = NULL
printf("%d", p)     # prints 0
{% endhighlight %}

- Pointer Arithmetic: +, -, ++, – these 4 operators can operate on pointer. Note that for binary operator + and - the other operands must be an integer.
- Pointer Comparison: <, >, ==, <=, >= these relational operator can be used to compare 2 pointer/addresses.
- Pointer Array: we can define an array of pointer. See one interesting implementation of such array
{% highlight c %}
char *c[] = {
  "Syed Nakib Hossain",
  "Shawkat Ali",
  "Liakat Khan"
} 

print("%s", c[0])     # prints "Syed Nakib Hossain"
{% endhighlight %}

- Pointer to a pointer: 
{% highlight c %}
int a = 10;
int *p = &a;
int **pp = &p

print("%d", **p)    # prints 10 
{% endhighlight %}

- Passing and returning pointer in function: this is called “call by value"