---
layout: post
title: "C++ Language"
category: jekyll update
---

### Enumeration
{% highlight cpp %}
enum <enum type name> {
  <value1>,
  <value2>, ..
} <variable name>;
{% endhighlight %}

### Class 
{% highlight cpp %}
class <class name> {
  <private members>
  public:
    <public members>
};
{% endhighlight %}

|Access|public|protected|private|
|------|------|---------|-------|
|Same class|Y|Y|Y|
|Derived classes|Y|Y|N|
|Outside classes|Y|N|N|

#### Constructor
##### Copy Constructor
#### List Initialization
#### Derived class
{% highlight cpp %}
class <derived class name> : <access specifier> <base class name>
{% endhighlight %}

Based on the access specifier the inheritance can be of 3 types - 
- Public: when access specifier is public the public members of base class become public member of derived class and protected member of base class become protected member of derived class.
- Protected: when access specifier is protected the public and protected member of base class become protected member of derived class.
- Private: when access specifier is private the public and protected member of base class become private member of derived class.

##### Derived Class Constructor
For inherited class base object is initiated first. Therefore derived class constructor calls base class constructor (unparameterized by default). If unparameterized constructor is not defined for base class it will through error. We can otherwise define parameterized base class constructor and call it from derived class constructor.
{% highlight cpp %}
class Base{
  ..
  public:
    Base(int val){..}
}

class Derived{
  ..
  public:
    derived(int val): Base(val) {..}
}
{% endhighlight %}

#### Abstract class

### Virtual function
virtual function tells C++ compiler to do late binding. It is defined in the base class and re-defined in the derived class. Late binding makes the call to this function executes from the object the pointer currently holds not the type of the pointer.

{% highlight cpp %}
class derived : public base {
public:
    void print()
    {
        cout << "print derived class" << endl;
    }
 
    void show()
    {
        cout << "show derived class" << endl;
    }
};
 
int main()
{
    base* bptr;
    derived d;
    bptr = &d;
 
    // virtual function, binded at runtime
    bptr->print();
 
    // Non-virtual function, binded at compile time
    bptr->show();
}
{% endhighlight %}

{% highlight cpp %}
print derived class
show base class
{% endhighlight %}

An abstract and virtual function is not possible but a virtual function inside an abstract class is possible!

#### vtable and vptr
- vtable: A table of function pointers, maintained per class
- vptr: A pointer to vtable, maintained per object instance

### Overloading
#### Operator Overloading
We can define custom behavior for operators for object we define.

{% highlight cpp %}
// as member-function of class
<return type> operator<operator character>(const &<second argument type>){
..
}
// as non member-function of class
<return type> operator<operator character>(const &<first argument type>, const &<second argument type>){
..
}
{% endhighlight %}

### Generics
Template is used to implement generic type as parameter and return types to function, method, interfaces.

{% highlight cpp %}
template <typename T>
T myFunc(T x, T y){
  return (x > y)? x : y;
}
int main(){
  cout << myFunc(3, 5) << endl; // output is 5
  cout << myFunc(5.6, 2.5) << endl; // output is 5.6
}
{% endhighlight %}

#### Explicit Instantiation
Sometime it is not deducible of typename of template from function definition and we have to explicitly state type when calling the function.

{% highlight cpp %}
template <typename T>
T myFunc(int a){
  return (T)a;
}
int main(){
  cout << myFunc<float>(3) << endl; 
}
{% endhighlight %}

### STL 
- array
- vector
- list
- forward list
- stack
- queue
- dequeue
- set
- unordered set
- map
- unordered map
- multimap
- unordered multimap

#### map
- The elements are sorted according to keys
- no 2 element can have the same key
- internally binary search trees is used to implement map

{% highlight cpp %}
#initialization
map<int, int> m = \{\{1, 100}, {2, 200}};

# insert using insert()
m.insert(pair<int, int>(3, 300));
# insert using insert() - hint position
map<int, int>::iterator it = m.begin();
m.insert(it, pair<int, int>(4, 400));
# insert using insert() - range insertion
map<int, int> anotherMap;
anotherMap.insert(m.begin(), m.find(2));

# insert using []
m[3] = 300;

# erase using key
m.erase(2);
# erase using iterator
map<int, int>::iterator it;
it = m.find(3);
if(it != m.end()) m.erase(it);
# erase using range
m.erase(it, m.end());
{% endhighlight %}

#### unordered_map
- The elements are not sorted
- no 2 elements can have the same key
- direct access is possible

#### multimap
- The elements are sorted according to keys
- 2 or more elements can have same key (use equal_range to find them)
- internally binary search trees is used to implement multimap

#### unordered_multimap
- The elements are not sorted
- 2 or more elements can have same key (use equal_range to find them)
- direct access is possible
- this is an implementation of hashmap.