---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Overview of C++ and Object-Oriented Design
uid: e312aafc-945e-a3e5-3f05-35d1a78c3705
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Contents
--------

1.  [Object-Oriented Design vs Procedural Design](#1)
2.  [The HelloWorld Procedure and the HelloWorld Object](#2)
3.  [C++ Data Types](#3)
4.  [Expressions](#4)
5.  [Coding Style](#5)

{{< anchor "1" >}}{{< /anchor >}}1\. Object-Oriented Design vs Procedural Design
--------------------------------------------------------------------------------

Many of you will already be familiar with one or more procedural languages. Examples of such languages are FORTRAN 77, Pascal and C. In the procedural programming paradigm, one focuses on the decomposition of software into various _functional components_. In other words, the program is organized into a collection of functions, (also known as procedures or subroutines), which will be executed in a defined order to produce the desired result.

By contrast, object-based programming focuses on the organization of software into a collection of components, called _objects_, that group together

1.  Related items of data, known as _properties_.
2.  Operations that are to be performed on the data, which are known as _methods_.

In other words, an object is a model of a real world concept, which posesses both state and behavior.  
Programming languages that allow us to create objects are said to support _abstract data types_. Examples of such languages are CLU, Ada, Modula-2.

The object-oriented programming paradigm goes a step beyond abstract data types by adding two new features: inheritance and polymorphism. We will talk about these ideas in depth later, but for now it will be sufficient to say that their purpose is to facilitate the management of objects that have similar characteristics. For example, squares, triangles and circles are all instances of shapes. Their common properties are that they all have a centroid and an area. Their common method might be that they all need to be displayed on the screen of a computer. Examples of languages that support the object-oriented paradigm are C++, Java® and Smalltalk.

{{< anchor "2" >}}{{< /anchor >}}2\. The _HelloWorld_ Procedure and the _HelloWorld_ Object
-------------------------------------------------------------------------------------------

Let's take a look two simple programs that print out the string, _Hello World!_

**The _HelloWorld_ Procedure**

Here is the procedural version of the program, written in C. The first statement is a preprocessor directive that tells the compiler to include the contents of the header file _stdio.h_. We include this file because it declares the existence of the built-in function, _printf()_. Every C program must have a top-level function named _main()_, which provides the entry point to the program. 

_#include \<stdio.h>_

_/\* The HelloWorld procedure definition. \*/  
void HelloWorld() {  
    printf("Hello World!\\n");  
}_ 

_/\* The main program. \*/  
int main() {  
    HelloWorld();               /\* Execute the HelloWorld procedure. \*/  
    return 0;                      /\* Indicates successful completion of the program. \*/  
}_

**The _HelloWorld_ Object**

Here is the object-based version of the program, written in C++. We have created a new data type, _HelloWorld_, that is capable of printing out the words we want. In C++, the keyword _class_ is used to declare a new data type. Our class has three publicly accessible methods, _HelloWorld()_, _~HelloWorld()_ and _print()_. The first two methods have special significance and they are respectively known as a constructor and the destructor. The constructor has the same name as the class. It is an initialization method that will be automatically invoked whenever we create a _HelloWorld_ object. The destructor also has the same name as the class, but with a ~ prefix. It is a finalization method that will be automatically invoked whenever a _HelloWorld_ object is destroyed. In our class, the _print()_ method is the only one that actually does anything useful.

It is important to understand the distinction between a class and an object. A class is merely a template for creating one or more objects. Our main program creates a single object named _a_ based on the class definition that we have provided. We then send the object a "print" message by selecting and invoking the _print()_ method using the **.** operator. We are able to access the _print()_ method in _main()_ because we have made it a _public_ member function of the class.  
 

_#include \<stdio.h>_

_// The HelloWorld class definition.  
class HelloWorld {  
        public:  
    HelloWorld() {}            // Constructor.  
    ~HelloWorld() {}          // Destructor.  
    void print() {  
        printf("Hello World!\\n");  
    }  
};                                      // Note that a semicolon is required here._ 

_// The main progam.  
int main() {  
    HelloWorld a;           // Create a HelloWorld object.  
    a.print();                  // Send a "print" message to the object.  
    return 0;  
}_

**C++ as a Superset of C**

Although C++ is generally thought of as an object-oriented language, it does support the procedural progamming paradigm as well. In fact, C++ supports all the features of C in addition to providing new features of its own. For example, a C++ program may include C-style comments that use the _/\* \*/_ delimiters as well C++-style comments that use the _//_ syntax.

_/\* C-style comments are also allowed in C++. \*/_

_// Alternative comment syntax that is only allowed in C++._

{{< anchor "3" >}}{{< /anchor >}}3\. C++ Data Types
---------------------------------------------------

**Built-in Data Types**

(_Ref. Lippman 3.1, 3.2_)

C++ built-in data types are similar to those found in C. The basic built-in types include

*   A boolean type: _bool_ (only available in Standard C++).
*   Character types: _char_, _unsigned char_ and _wchar\_t_ (_wchar\_t_ supports wide characters and is only available in Standard C++).
*   Integer types: _short_ (or _short int_), _int_ (or _long int_), _unsigned short_ and _unsigned int_.
*   Floating point types: _float_, _double_ and _long double_.

Not all computing platforms agree on the actual size of the built-in data types, but the following table indicates the typical sizes on a 32-bit platform:  
 

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
BUILT-IN DATA TYPE
{{< thclose >}}
{{< thopen >}}
SIZE IN BYTES
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
char, unsigned char
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
short, unsigned short
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
wchar\_t, bool,  
int, unsigned int, float 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
double
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
long double
{{< tdclose >}}
{{< tdopen >}}
8 or 16
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  

A literal constant is a constant value of some type. Examples of literal constants are  
 

{{< tableopen >}}
{{< theadopen >}}


{{< tropen >}}
{{< thopen >}}
DATA TYPE
{{< thclose >}}
{{< thopen >}}
LITERAL CONSTANT
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
char
{{< tdclose >}}
{{< tdopen >}}
'a', '7'
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
wchar\_t
{{< tdclose >}}
{{< tdopen >}}
L'a', L'7'
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
bool
{{< tdclose >}}
{{< tdopen >}}
true, false
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
long int
{{< tdclose >}}
{{< tdopen >}}
8L, 8l
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
unsigned long int
{{< tdclose >}}
{{< tdopen >}}
8UL, 8ul
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
float
{{< tdclose >}}
{{< tdopen >}}
2.718F, 2.718f
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
double
{{< tdclose >}}
{{< tdopen >}}
2.718, 1e-3
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
long double
{{< tdclose >}}
{{< tdopen >}}
2.718L, 2.718l
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  

Note that there is no built-in data type for strings. Strings can be represented as character arrays or by using the _string_ type provided in the Standard C++ library. A string literal constant is of the form

_"Hello World!"_

**User-defined Data Types**

We have already seen how we can define new data types by writing a _class_, and for the most part we will use classes. However, C++ also provides extended support for C-style structures. For example, C++ allows member functions to be packaged in a _struct_ in addition to member data. The most significant difference between a _class_ and a _struct_ is that by default, the members of a class are _private_, whereas the members of a struct are _public_.

_struct date {  
    int day;  
    int month;  
    int year;  
    void set\_date(int d, int m, int y);    // Member functions only allowed in C++.  
};_

_int main() {  
    struct date a;   /\* C-style definition. \*/  
    date a;            // Allowable C++ definition.  
}_ 

**Pointer Types**

(_Ref. Lippman 3.3_)

Pointer variables (or pointers) are a powerful concept that allow us to manipulate objects by their memory address rather than by their name. It is important to understand pointers clearly since they are used extensively in this course and in real world software.

A pointer must convey two pieces of information, both of which are necessary to access the object that it points to:

1.  the memory address of the object
2.  the type of the object

The following example illustrates the use of a pointer to an object of type _double_. The pointer is defined by the statement

_double \*p;_

_p_ can now hold the memory address of a double object, such as _d_. We obtain the address of _d_ by applying the _address of_ operator, _&d_, and we then store it in _p_. Now that _p_ contains a valid address, we can refer to the object _d_ by applying the _dereference_ operator, _\*p_. Notice that we have used _\*_ in two different contexts, with different meanings in each case. The meaning of _&_ also depends on the context in which it is used.

_#include \<stdio.h>_

_int main() {  
    double d;         // An double object.  
    double \*p;       // A variable that is a pointer to an double._

 _p = &d;          // Take the memory address of d and store it in p._

 _d = 7.0;          // Store a double precision number in d.  
    printf("The value of the object d is %lf\\n", d);  
    printf("The value of the object that p points to is %lf\\n", \*p);  
    printf("The address of the object that p points to is %u\\n", p);  
}_   
Here is the output from a trial run:

The value of the object d is 7.000000  
The value of the object that p points to is 7.000000  
The address of the object that p points to is 4026528296

**Reference Types**

(_Ref. Lippman 3.6_)

As an added convenience, C++ provides reference types, which are an alternative way to use the functionality that pointers provide. A reference is just a nickname for existing storage.

The following example defines an integer object, _i_, and then it defines a reference variable, _r_, by the statement

_int& r = i;_

Be careful not to confuse this use of _&_ with the _address of_ operator. Also note that, unlike a pointer, a reference must be initialized at the time it is defined.

_#include \<stdio.h>_

_int main() {  
    int i = 0;  
    int& r = i;    // Create a reference to i._

 _i++;  
    printf("r = %d\\n", r);  
}_

**Explicit Type Conversion**

(_Ref. Lippman 4.14_)

Explicit type conversion can be performed using a _cast_ operator. The following code shows three alternative ways to explicitly convert an _int_ to a _float_.

_int main() {  
    int a;  
    float b;_

 _a = 3;  
    b = (float)a;                           /\* C-style cast operator. \*/  
    b = float(a);                          // Alternative type conversion notation allowed in C++.  
    b = static\_cast\<float>(a);    // A second alternative, allowed only in Standard C++.  
}_

**_const_ Keyword**

(_Ref. Lippman 3.5_)

The _const_ keyword is used to designate storage whose contents cannot be changed. A _const_ object must be initialized at the time it is defined.

const int i = 10;    /\* Allowed both in C and C++. \*/  
const int j;            /\* This is illegal. \*/

**Variable Definitions**

In C++, variable definitions may occur practically anywhere within a code block. A code block refers to any chunk of code that lies within a pair of scope delimiters, _{}_. For example, the following C program requires _i_ and _j_ to be defined at the top of the _main()_ function.

_#include \<stdio.h>_

_int main() {  
    int i, j;    /\* C requires variable definitions to be at the top of a code block. \*/_

 _for (i = 0; i \< 5; i++) {  
         printf("Done with C\\n");  
    }  
    j = 10;  
}_

In the C++ version of the program, we can define the variables _i_ and _j_ when they are first used.

_#include \<stdio.h>_

_int main() {  
    for (int i = 0; i \< 5; i++) {         // In Standard C++, i is available anywhere within the for loop.  
        printf("Still learning C++\\n");  
     }  
    int j = 10;  
}_

{{< anchor "4" >}}{{< /anchor >}}4\. Expressions
------------------------------------------------

(_Ref. Lippman 4.1-4.5, 4.7, 4.8, 4.13, 4.14_)

**Operator Precedence**

An expression consists of one or more operands and a set of operations to be applied to them. The order in which operators are applied to operands is determined by operator precedence. For example, the expression

_1 + 4 \* 3 / 2 == 7 && !0_

is evaluated as

_((1 + ((4 \* 3) / 2)) == 7) && (!0)_

Note that the right hand side of the logical _AND_ operator is only evaluated if the left hand side evaluates to _true_. (For a table of operator precedence, see _Lippman, Table 4.4_.)

**Arithmetic Conversions**

The evaluation of arithmetic expressions follows two general guidelines:

1.  Wherever necessary, types are promoted to a wider type in order to prevent the loss of precision.
2.  Integral types (these are the various boolean, character and integer types) are promoted to the _int_ data type prior to evaluation of the expression.

{{< anchor "5" >}}{{< /anchor >}}5\. Coding Style
-------------------------------------------------

Coding styles tend to vary from one individual to another. While you are free to develop your own style, it is important to make your code consistent and readable. Software organizations frequently try to enforce consistency by developing a set of coding guidelines for programmers.

Here is an example of an inconsistent coding style. The curly braces in the two _for_ loops are aligned differently. The second style is usually preferred because it is more compact and it avoids excessive indentation.  
 

_#include \<stdio.h>_

_int main() {  
    int i;_

 _for (i = 0; i \< 5; i++)  
       {  
            printf("This convention aligns the curly braces.\\n");  
       }_

 _for (i =0; i \< 5; i++) {  
        printf("This is a more compact convention which aligns ");  
        printf("the closing brace with the for statement.\\n");  
    }  
}_