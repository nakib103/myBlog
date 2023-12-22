---
layout: post
title: "Perl Language"
category: jekyll update
---

- Case Sensitive
- File extension - .PL or .pl
- No whitespace in file name 
- Free-form language - indent or format however you like
- Interpreted language but creates a intermediate form

### Comment
{% highlight perl %}
# single line comment

=begin
Multi line comment
Embedded Documnentation or pod
=cut
{% endhighlight %}

### Data Types
Loosely typed language. So no need to specify data type when declaring variable. Perl interpreter chose data type based on the context.

3 types of data types -
- Scalar → variable name preceded by $. Can be number, string, or reference (address of a variable)
- Arrays of scalar → variable name preceded  by@ . Ordered list of scalar and indexed with number.
- Hashes of scalar → variable name preceded by %. Unordered list with key-value pair.

### Variables
Perl maintains separate namespace for different variable like scalar, array or hash. So, $foo and @foo is different variable.

#### Declaration
It is mandatory to declare variable before using it in statement if we are using use strict in our script.

{% highlight perl %}
$a = 1234
$b = 12.34
$c = 0xFFE
$d = "hello, hooman!" 
{% endhighlight %}

#### Context
- scalar
- list
- boolean
- void
- interpolative

{% highlight perl %}
@a = ("Here", "I", "am", "!");

@b = @a   # @b = ("Here", "I", "am", "!")
$c = @a   # $c = 3
{% endhighlight %}

#### Numbers
#### Strings
- Single and Double quote
> Double quote interpolate variable and special character and single quote does not

{% highlight perl %}
$a = 1;
print("value of a: $a\n"); # prints - value of a: 1
print('value of a: $a\n'); # prints - value of a: $a\n
{% endhighlight %}

- Multi line string
{% highlight perl %}
$a = "This is a
multi-line string";

$b = 'This is also a
multi-line string';
{% endhighlight %}

- V-strings
- Special literals
{% highlight perl %}
print(__FILE__);    # gives file name
print(__LINE__);    # gives line number
print(__PACKAGE__); # gives package name
{% endhighlight %}

This literals are not interpolated in string.

#### Array
List is the data and array is the variable

{% highlight perl %}
@a = (1, 3, 4);
print("at index 0: $a[0]);  # note that we used $

# Array can contain different data types
@b = (1, "hello", 3);
print("at index 1: $b[1]");

# qw// can also be used - it uses whitespace, new-line as delimiter
@c = qw/hello, there hooman!/;
@d = qw/hello again,
you
there
hooman!/;

# assignment to single index is also possible
@a[3] = 5;

# multi-dimentional array

{% endhighlight %}

- Indexing
{% highlight perl %}
# use $ for accessing single element
@a = (1, 4, 3);
$a[0] = 9;

# negative number can be used as index
print($a[-2])
{% endhighlight %}
- Sequential arrays and range operator
{% highlight perl %}
@a = (1..100);
@b = ("s".."z");
@c = ("ab".."cd");
{% endhighlight %}

.. is a range operator. 
  - For, ("a".."Z") it would start with a and end with z. 
  - We can have preceding 0, like ("01".."10")

- Slicing array
{% highlight perl %}
@a = (1..10);

# using comma
print(@a[1,3, -1]);

# using range operator
print(@a[3..5]);
{% endhighlight %}
- Size of array
{% highlight perl %}
@a = (1..10)

# from implicit scalar context
$size = @a;

# from explicit scalar context
$size = scalar @a;
{% endhighlight %}

  - note that, `size of array = maximum index of array + 1`
  - maximum index of array can be obtained by `$#`, like `$#a`

- Array functions
  - push - 
  - pop -
  - shift - 
  - unshift - 
  - splice -
  - split -
  - sort -

- Merging array
{% highlight perl %}
@a = (1, 2, (3, 4, 5), 6);
{% endhighlight %}

- Special variable
  - `$[` - first index of array, by default 0.

#### Hash
##### Declaration
{% highlight perl %}
# using a list
%a = ("a", 1, "b", 2, 1, 45);
print("a{1} - $a{1}\n");  # note we used $

# for clarity we can use =>
%b = ("a" => 1, "b" => 2, 1 => 45);

# quote can be ommited(?) if we use - with keys
%b = (-a => 1, -b => 2, 1 => 45);

# using single index
%c{"hello"} = "world!";
{% endhighlight %}

##### Indexing 
{% highlight perl %}
%a = ("a" => 1, "b" => 2);
\$a{"a"} = 3;
{% endhighlight %}
##### Slicing hash
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);
@b = %a{"a", 1};     # we used @ here because the returned value is a list
{% endhighlight %}
##### Extracting keys & values
- The keys of hash can be extracted using keys function.
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);

@k = keys(%a);
# or,
@k = keys %a;
{% endhighlight %}

- The values of hash can be extracted using values function.
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);

@k = keys(%a);
# or,
@k = keys %a;
{% endhighlight %}

The order the keys or values returned are random

##### Check exists
We can check if a key exists in hash using exists  function
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);
if(exists($a{"a"})){
  print("Key a exists\n");
}
{% endhighlight %}

##### Size of hash
We can get size of hash from its keys or values array
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);

# from implicit scalar context
@keys = keys(%a);
$size = scalar @keys;

# from explicit scalar context
@values = values(\%a);
$size = scalar @values;
{% endhighlight %}

##### Deleting element
{% highlight perl %}
%a = ("a" => 1, "b" => 2, 1 => 45);

delete $a{"a"};
{% endhighlight %}

#### Special variable
Generally the are punctuation marks after variable indicator ($, @, %). They also have English full name but we need to add use English to be able to use that

- `$_` 
- `$!` or `$OS_ERROR`

### Operators
#### Arithmetic
+, -, *, /, %, **

#### Equality
==, !=, <, >,<=, >=, <=> , lt, gt, le, ge, ne, eq, cmp

#### Assignment
=, +=, -=, *=, /=, %=, **= 

#### Bitwise
&, |, ^, ~, <<, >> 

#### Logical
&&, ||, and, or, not 

#### Quote
q{}, qq{}, qx{} 

#### Others
., x, .., ++, --, -> 

#### Operator precedence

### Conditionals
#### True/False
- Number 0, string '0' and ““, empty list (), and undef is considered False
- The ! or not of a True value returns a special False.

#### If..elsif..else
{% highlight perl %}
if(condition){
  statements
}
elsif(condition){
  statements
}
else{
  statements
}
{% endhighlight %}

#### unless..elsif..else
{% highlight perl %}
if(condition1){
  statements  # executes when condition1 is false
}
elsif(condition2){
  statements
}
else{
  statements
}
{% endhighlight %}

#### switch
#### ? operator
{% highlight perl %}
$a = ($b > 0) ? "positive" : "negative";
{% endhighlight %}

### Loops
#### For loop

for(init; condition; increment){
  statements;
}

for($a = 0; $a < 10; $a = $a + 1){
  print("value of a: ", $a, "\n");
}

#### Foreach loop
The same thing can be done using for too.
{% highlight perl %}
foreach var (list){
  statements;
}

@list = (1, 2, 3, 4);
foreach $a (@list){
  print("value of a: ", $a, "\n");
}
{% endhighlight %}

#### While loop
{% highlight perl %}
while(condition){
  statements;
}

$a = 0;
while($a < 10){
  print("value of a: ", $a, "\n");
  $a = $a + 1;
}
{% endhighlight %}

#### Until loop
{% highlight perl %}
until(condition){   # go inside the loop if condition is false
  statements;
}

$a = 0;
while($a > 10){
  print("value of a: ", $a, "\n");
  $a = $a + 1;
}
{% endhighlight %}

#### Do..while loop
{% highlight perl %}
do{
  statements;
} while(condition);

$a = 0;
do{
  print("value of a: ", $a, "\n");
  $a = $a + 1;
}while($a < 10);
{% endhighlight %}

#### Control statements
- last 
- continue 
- next 
- redo
- goto 

### Functions or subroutine
#### Definition
{% highlight perl %}
sub subroutine_name {
  statements;
}

sub sayHello{
  print("Hello!");
}
{% endhighlight %}

#### Calling subroutine
{% highlight perl %}
subroutine_name(list of argument);

sayHello();
{% endhighlight %}

#### Passing arguments
Arguments passed inside a subroutine can be accessed via @_ variable.
{% highlight perl %}
sub average{
  $n = scalar(@_);
  $sum  = 0;
  foreach $val (@_){
    $sum += $val;
  }
  
  $average = $sum / $n;
  print("average of given numbers: ", $average, "\n");
}

average(1, 3, 5);

# list and scalars gets combined
$a = 9;
$b = 2;
@c = (4, 6, 7);
average($a, $b, @c);
{% endhighlight %}

##### Passing hash to subroutine
The hash is converted to a list in @_ which can be converted by assigning to hash
{% highlight perl %}
sub mySub{
  my (%hash) = @_;
  
  for my $key (keys(%hash)){
    $val = %hash{key};
    print("value for key ", $key, " is ", $val);
  } 
}

%hash = ("a" => 1, "b" => 2, 1 => 45);
mySub(%hash);
{% endhighlight %}

####  Returning values
- scalar or array can be returned using return keyword
- if nothing is returned whatever calculation was done last is the return value.

{% highlight perl %}
sub average{
  $n = scalar(@_);
  $sum  = 0;
  foreach $val (@_){
    $sum += $val;
  }
  
  $average = $sum / $n;

  return $average;  
}
{% endhighlight %}

####  Private variable
By default all variables in perl are global

- We can create private or lexical using my keyword.
- We can also use local keyword. But it is generally used to modify a already existing variable compared to my which creates a new variable.
- Another lexical variable is state which retains the value of the variable.

{% highlight perl %}
sub incremental{
  state $a = 0;
  print("value of a: ", $a, "\n");
  $a += 1;
}

for (1..5){
  incremental();
}
{% endhighlight %}

#### Context of subroutine
Context of a subroutine is defined by the return value expected from it.

{% highlight perl %}
# for scalar context localtime returns a string
$date = localtime(time);

# for a list context localtime returns a list
($sec, $min, $hour, $mday, $mon, $year, $wday, $yday, $isdst) = localtime(time);
{% endhighlight %}

#### Reference
Reference is like pointer and can store the location of other variable.

##### Referencing
Reference is created using \

{% highlight perl %}
$ref_scalar = \$scal;
$ref_array = \@arr;
$ref_hash = \%hash;
$ref_code = \&code;    # function handle or name
$ref_glob = \*glob     # what's this?

# anonymous array can be referenced using []
$ref_arr = [1, 2, [4, 5], 6];

# anonymous hash can reference using {}
$ref_hash = {"a" => 1, "b" => 2, 1 => 45};

# subroutine can be referenced without the subroutine name
\$ref_sub = sub {
  print("hello!");
}
{% endhighlight %}

reference to a I/O handle (filehandle or dirhandle) cannot be created

##### Dereferencing
Dereference means getting the value stored in the location of the reference. It can be done using $ , @ , % depending on what data type the reference is referencing

{% highlight perl %}
$var = 10;
$ref_var = \$var
print("value inside var: ", $$var, "\n");
{% endhighlight %}

##### Extracting type
We can use ref function to know the type of data a reference is referencing to.

{% highlight perl %}
$var = 10;
$ref_var = \$var
print("ref_var is referencing to a: ", ref($ref_var));
{% endhighlight %}

#### I/O
##### Print
can have comma separated values - 

print("Hello", ", ", "World!");

##### File I/O
###### open
open(FILEHANDLE, expression)

Modes -
- < or r - read-only 
- > or w - create, write, and truncates
- >> or a - create, write, and append
- +< or r+ - read and write
- +> or w+ - read, create, write, and truncate
- +>> or a+ - read, create, write, and append 

###### sysopen
sysopen(FILEHANDLE, filename, mode, permission)

Modes - 
- f
Permissions is by default 0x666 and can be overwritten.

###### close
close(FILEHANDLE)

##### Reading from file
- <FILEHANDLE> operator
With <FILEHANDLE> operator we can read the content from the file.
{% highlight perl %}
# scalar context gives single line
print("what is your name");
$name = <STDIN>
print("Name is ", $name, "\n");

# list context gives all the lines as a list
open(DATA, "<file.txt");
@data = <DATA>;
{% endhighlight %}

- getc gives a single char. default is STDIN

getc(FILEHANDLE)

- read gives specific bytes from file, default is STDIN
{% highlight perl %}
read(FILEHANDLE, scalar, length, offset)
{% endhighlight %}

###### Writing to file
print we use print function. By default it prints in STDOUT

{% highlight perl %}
print(FILEHANDLE, list)
{% endhighlight %}

###### Other file related functions
- rename
- unlink
- tell
- seek

### Directories
### Error Handling
#### Warn and die
- warn
- die 

#### Carp module
- carp
- cluck
- clock
- confess

### OOP
- class - Class in Perl is essentially a package that contains corresponding variable and methods.
- method - a method in Perl is a subroutine defined inside a package and the first argument is the package reference or class name.

#### Defining a class
- To create a class we first create package
- The scope of the package definition extends to the end of file or until another package keyword is encountered.

{% highlight perl %}
package Person;
{% endhighlight %}

#### Creating an class variable
We can create this by using bless function which takes an object reference and a class name and make the object a member of the class.

{% highlight perl %}
package Person;
sub new {
  $class = shift;
  $self = {
    _first_name = shift;
    _last_name = shift;
    _n_id = shift;
  }
  
  bless($self, $class);
  return $self;
}
{% endhighlight %}

- the shift function returns the first argument of array and shift the array by removing the first element (look in Array)
- By convention the constructor method is named new in Perl.

We can create an object as follows - 
{% highlight perl %}
\$me = Person("Syed Nakib", "Hossain", 143223432); 
{% endhighlight %}

#### Defining method
{% highlight perl %}
sub getFirstName{
  my ($self) = @_;      # the right side is an array but left side is a scalar
  return $self->{_first_name};
}

sub setFirstName{
  my ($self, $first_name) = @_;
  $self->{_first_name} = $first_name if defined($first_name);
  return $self->{_first_name}
}
{% endhighlight %}

#### Inheritance
Perl has inheritance through a special variable called @ISA 
{% highlight perl %}
package Employee;

use Person;
use strict;

our @ISA = qw(Person);
{% endhighlight %}

- our is a similar keyword like my but it creates a global variable in the scope of the package it is defined in. That is we can access it without any package identifier within the package. It can be accessed outside the package with package identifier, package_name::variable_name 
- qw breaks a string into array (see in Array)

Perl searches for variable or method in the following way - 
- Perl first searches in the class of specified object.
- Then it searches in the @ISA array.
- Then Perl uses AUTOLOAD subroutine.
- Then Perl searches in UNIVERSAL class that comes as Perl standard library.
- Finally Perl raises a runtime exception.

##### Method overriding
We can re-define a method in a child class.

{% highlight perl %}
package Employee;

use Person;
use strict;

our @ISA = qw(Employee);

sub new{
  my $class = @_;
  
  my $self = $class->SUPER::new($_[1], $[2], $[3]);
  
  $self->{employee_id} = undef;
  $self->{salary} = undef;
  
  bless($self, $class);
  return $self;
}
{% endhighlight %}

#### AUTOLOAD
Perl enables to define an AUTOLOAD subroutine which is called if any undefined subroutine is called.

#### Destructor
We can define a destructor by DESTRUCTOR method. It is called when - 

- object’s reference variable goes out of scope
- object’s reference variable is undef-ed
- script terminates
- Perl interpreter terminates

### Package and modules
- A package is collection of code that lives within it’s own namespace
- namespace is a named collection of unique variable names or symbol table
- :: operator is used for referring a variable or subroutine inside a specific package

#### Creating a package
As described earlier a package can be created using package keyword and the whole file is under the scope of the package if another package keyword is not reached.

#### BEGIN and END blocks
BEIGIN{} and END{} blocks work as constructor and destructor.

- every BEGIN block is executed after Perl code is loaded and compiled but before any statement is executed
- every END block is executed after Perl interpreter exits.

#### Creating a module
A module is essentially a package defined in a library file. The file name must be same as the package name and the extension is .pm .

{% highlight perl %}
# the file name is Person.pm
package Person

sub printName{
  print("name of the person: ", $_[0], "\n");
}
{% endhighlight %}

#### Exporting a module

{% highlight perl %}
h2xs -AX -n Person

# -A  omits AUTOLOADER code
# -X  omits eXternal subroutine
# -n  specifies the name of the module
{% endhighlight %}

It creates a directory structure which can be shipped for example using tar 

#### Installing a module
We can download a Perl module for example in a tar format and use the following commands to install - 

{% highlight bash %}
tar -xvzf Person.tar.gz
cd Person 
perl Makefile.PL
make 
make install
{% endhighlight %}

#### Using a module
##### require

{% highlight perl %}
require Person

Person::printName("Nakib");
{% endhighlight %}

##### use
We can also use use and omit the package qualifier with few extra steps in Person.pm

{% highlight perl %}
# in Person.pm file
require Exporter;
@ISA = qw(Exporter);
@EXPORT = qw(printName);

...


# in our main Perl file
use Person
printName("Nakib");
{% endhighlight %}

### Miscellaneous 
#### Pragma
A pragma is a module that effect some compile time or run time behavior of Perl

#### Here Document
#### Date and time
#### Format
#### Regular Expression
#### Email
#### Coding standard

### Source
- https://www.tutorialspoint.com/perl/index.htm
- https://docstore.mik.ua/orelly/perl2/index.htm
- https://docstore.mik.ua/orelly/perl2/perlnut/index.htm
- https://docstore.mik.ua/orelly/perl2/prog/index.htm
- https://docstore.mik.ua/orelly/perl2/advprog/index.htm
- https://docstore.mik.ua/orelly/perl2/cookbook/index.htm
- https://docstore.mik.ua/orelly/perl2/sysadmin/index.htm