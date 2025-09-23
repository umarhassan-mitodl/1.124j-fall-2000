---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Object Construction and Destruction
uid: 8c606902-9761-4d7e-7e5a-c945f6cf00af
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Contents
--------

1.  [Local and Global Variables](#1)
2.  [Reference Types](#2)
3.  [Functions in C++](#3) 
4.  [Basic Input and Output](#4)
5.  [Creating and Destroying Objects - Constructors and Destructors](#5)

{{< anchor "1" >}}{{< /anchor >}}1\. Local and Global Variables
---------------------------------------------------------------

(_Ref. Lippman 8.1-8.3_)

Local variables are objects that are only accessible within a single function (or a sub-block within a function.) Global variables, on the other hand, are objects that are generally accessible to every function in a program. It is possible, though potentially confusing, for a local object and a global object to share the same name. In following example, the local object _x_ shadows the object _x_ in the global namespace. We must therefore use the _global scope operator_, _::_, to access the global object.

_**main\_file.C**_

_float x;            // A global object._

_int main () {_  
 _float x;        // A local object with the same name._

 _x = 5.0;       // This refers to the local object._  
 _::x = 7.0;     // This refers to the global object._  
}  
 

What happens if we need to access the global object in another file? The object has already been defined in _main\_file.C_, so we should not set aside new memory for it. We can inform the compiler of the existence of the global object using the _extern_ keyword.

_**another\_file.C**_

_extern float x;   // Declares the existence of a global object external to this file._

_void do\_something() {_  
 _x = 3;          // Refers to the global object defined in main\_file.C._  
_}_  
 

{{< anchor "2" >}}{{< /anchor >}}2\. Reference Types
----------------------------------------------------

_(Ref. Lippman 3.6)_

Reference types are a convenient alternative way to use the functionality that pointers provide. A reference is just a nickname for existing storage. The following example defines an integer object, _i_, and then it defines a reference variable, _r_, by the statement

_int& r = i;_

Be careful not to confuse this use of _&_ with the _address of_ operator. Also note that, unlike a pointer, a reference must be initialized at the time it is defined.

_#include \<stdio.h>_

_int main() {_  
 _int i = 0;_  
 _int& r = i;    // Create a reference to i._

 _i++;_  
 _printf("r = %d\\n", r);_  
_}_  
 

{{< anchor "3" >}}{{< /anchor >}}3\. Functions in C++
-----------------------------------------------------

**Argument Passing**

_(Ref. Lippman 7.3)_

Arguments can be passed to functions in two ways. These techniques are known as

Pass by value.

Pass by reference.

When an argument is passed by value, the function gets its own local copy of the object that was passed in. On the other hand, when an argument is passed by reference, the function simply refers to the object in the calling program.

_// Pass by value._  
_void increment (int i) {_  
 _i++;                               // Modifies a local variable._  
_}_

_// Pass by reference._  
_void decrement (int& i) {_  
 _i--;                               // Modifies storage in the calling function._  
_}_

_#include \<stdio.h>_

_int main () {_  
 _int k = 0;_

 _increment(k);                   // This has no effect on k._  
 _decrement(k);                   // This will modify k._  
 _printf("%d\\n", k);_  
_}_  
 

Passing a large object by reference can improve efficiency since it avoids the overhead of creating an extra copy. However, it is important to understand the potentially undesirable side effects that can occur. If we want to protect against modifying objects in the calling program, we can pass the argument as a constant reference:

_// Pass by reference._  
_void decrement (const int& i) {_  
 _i--;                               // This statement is now illegal._  
_}_  
 

Return by Reference
-------------------

_(Ref. Lippman 7.4)_

A function may return a reference to an object, as long as the object is not local to the function. We may decide to return an object by reference for efficiency reasons (to avoid creating an extra copy). Returning by reference also allows us to have function calls that appear on the left hand side of an assignment statement. In the following contrived example, _select\_month()_ is used to pick out the _month_ member of the object _today_ and set its value to _9_.

s_truct date {_  
 _int day;_  
 _int month;_  
 _int year;_  
_};_

_int& select\_month(struct date &d) {_  
 _return d.month;_  
_}_

_#include \<stdio.h>_

_int main() {_  
 _struct date today;_

 _select\_month(today) = 9;                       // This is equivalent to: today.month = 9;_  
 _printf("%d\\n", today.month);_  
_}_  
 

Default Arguments
-----------------

_(Ref. Lippman 7.3.5)_

C++ allows us to specify default values for function arguments. Arguments with default values must all appear at the end of the argument list. In the following example, the third argument of _move()_ has a default value of zero.

_void move(int dx, int dy, int dz = 0) {_  
 _// Move some object in 3D space.  If dz = 0, then move the object in 2D space._  
_}_

_int main() {_  
 _move(2, 3, 5);_  
 _move(2, 3);       // dz assumes the default value, 0._  
_}_  
 

Function Overloading
--------------------

_(Ref. Lippman 9.1)_

In C++, two functions can share the same name as long as their _signatures_ are different. The signature of a function is another name for its parameter list. Function overloading is useful when two or more functionally similar tasks need to be implemented in different ways. For example:

_void draw(double center, double radius) {_  
 _// Draw a circle._  
_}_

_void draw(int left, int top, int right, int bottom) {_  
 _// Draw a rectangle._  
_}_

_int main() {_  
 _draw(0, 5);                  // This will draw a circle._  
 _draw(0, 4, 6, 8);           // This will draw a rectangle._  
_}_  
 

Inline Functions

_(Ref. Lippman 3.15, 7.6)_

Every function call involves some overhead. If a small function has to be called a large number of times, the relative overhead can be high. In such instances, it makes sense to ask the compiler to expand the function inline. In the following example, we have used the _inline_ keyword to make _swap()_ an inline function.  
 

_inline void swap(int& a, int& b) {_  
 _int tmp = a;_  
 _a = b;_  
 _b = tmp;_  
_}_

_#include \<stdio.h>_

_main() {_  
 _int i = 2, j = 3;_

 _swap(i, j);_  
 _printf("i = %d j = %d\\n", i, j);_  
_}_  
 

This code will be expanded as

_main() {_  
 _int i = 2, j = 3;_

 _int tmp = i;_  
 _i = j;_  
 _j = tmp;_  
 _printf("i = %d j = %d\\n", i, j);_  
_}_

Whenever the compiler needs to expand a call to an _inline_ function, it needs to know the function definition. For this reason, _inline_ functions are usually placed in a header file that can be included where necessary. Note that the _inline_ specification is only a recommendation to the compiler, which the compiler may choose to ignore. For example, a recursive function cannot be completely expanded inline.  
 


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

{{< anchor "4" >}}{{< /anchor >}}4\. Basic Input and Output
-----------------------------------------------------------

_(Ref. Lippman 1.5)_

C++ provides three _predefined_ objects for basic input and output operations: _cin_, _cout_ and _cerr_. All three objects can be accessed by including the header file _iostream.h_.  
 

Reading from Standard Input: cin
--------------------------------

_cin_ is an object of type _istream_ that allows us to read in a stream of data from _standard input_. It is functionally equivalent to the _scanf()_ function in C. The following example shows how _cin_ is used in conjunction with the _\>>_ operator. Note that the _\>>_ points _towards_ the object into which we are reading data.  
 

_#include \<iostream.h>                // Provides access to cin and cout._  
_#include \<stdio.h>                     /\* Provides access to printf and scanf. \*/_

_int main() {_  
 _int i;_

 _cin >> i;                                  // Uses the stream input object, cin, to read data into i._  
 _scanf("%d", &i);                      /\* Equivalent C-style statement. \*/_

 _float a;_  
 _cin >> i >> a;                          // Reads multiple values from standard input._  
 _scanf("%d%f", &i, &a);           /\* Equivalent C-style statement. \*/_  
_}_  
 

Writing to Standard Output: _cout_
----------------------------------

_cout_ is an object of type _ostream_ that allows us to write out a stream of data to _standard output_. It is functionally equivalent to the _printf()_ function in C. The following example shows how _cout_ is used in conjunction with the _\<\<_ operator. Note that the _\<\<_ points _away_ from the object from which we are writing out data.  
 

_#include \<iostream.h>                // Provides access to cin and cout._  
_#include \<stdio.h>                     /\* Provides access to printf and scanf. \*/_

_int main() {_  
 _cout \<\< "Hello World!\\n";       // Uses the stream output object, cout, to print out a string._  
 _printf("Hello World!\\n");          /\* Equivalent C-style statement. \*/_

 _int i = 7;_  
 _cout \<\< "i = " \<\< i \<\< endl;     // Sends multiple objects to standard output._  
 _printf("i = %d\\n", i);                 /\* Equivalent C-style statement. \*/_  
_}_  
 

Writing to Standard Error: _cerr_
---------------------------------

_cerr_ is also an object of type _ostream_. It is provided for the purpose of writing out warning and error messages to _standard error_. The usage of _cerr_ is identical to that of _cout_. Why then should we bother with _cerr_? The reason is that it makes it easier to filter out warning and error messages from real data. For example, suppose that we compile the following program into an executable named _foo_:

_#include \<iostream.h>_

_int main() {_  
 _int i = 7;_  
 _cout \<\< i \<\< endl;                                   // This is real data._  
 _cerr \<\< "A warning message" \<\< endl;    // This is a warning._  
_}_

We could separate the data from the warning by redirecting the standard output to a file, while allowing the standard error to be printed on our console.

_athena% foo > temp_  
_A warning message_

_athena% cat temp_  
_7_  
 

{{< anchor "5" >}}{{< /anchor >}}5\. Creating and Destroying Objects - Constructors  and Destructors
----------------------------------------------------------------------------------------------------

_(Ref. Lippman 14.1-14.3)_

Let's take a closer look at how constructors and destructors work.

**A Point Class**

Here is a complete example of a _Point_ class. We have organized the code into three separate files:

_point.h_ contains the _declaration_ of the class, which describes the structure of a _Point_ object.

_point.C_ contains the _definition_ of the class i.e. the actual implementation of the methods.

_point\_test.C_ is a program that uses the _Point_ class.

Our _Point_ class has three constructors and one destructor.

 _Point();                               // The default constructor._  
 _Point(float fX, float fY);       // A constructor that takes two floats._  
 _Point(const Point& p);         // The copy constructor._  
 _~Point();                             // The destructor._

These constructors can be respectively invoked by object definitions such as

 _Point a;_  
 _Point b(1.0, 2.0);_  
 _Point c(b);_

The default constructor, _Point()_, is so named because it can be invoked without any arguments. In our example, the default constructor initializes the _Point_ to (0,0). The second constructor creates a _Point_ from a pair of coordinates of type _float_. Note that we could combine these two constructors into a single constructor which has default arguments:

 _Point(float fX=0.0, float fY=0.0);_

The third constructor is known as a copy constructor since it creates one _Point_ from another. The object that we want to clone is passed in as a constant reference. Note that we cannot pass by value in this instance because doing so would lead to an unterminated recursive call to the copy constructor. In this example, the destructor does not have to perform any clean-up operations. Later on, we will see examples where the destructor has to release dynamically allocated memory.

Constructors and destructors can be triggered more often than you may imagine. For example, each time a _Point_ is passed to a function by value, a local copy of the object is created. Likewise, each time a _Point_ is returned by value, a temporary copy of the object is created in the calling program. In both cases, we will see an extra call to the copy constructor, and an extra call to the destructor. You are encouraged to put print statements in every constructor and in the destructor, and then carefully observe what happens.  
 

_**point.h**_

_// Declaration of class Point._

_#ifndef \_POINT\_H\__  
_#define \_POINT\_H\__

_#include \<iostream.h>_

_class Point {_  
 _// The state of a Point object. Property variables are typically_  
 _// set up as private data members, which are read from and_  
 _// written to via public access methods._  
 _private:_  
 _float mfX;_  
 _float mfY;_

 _// The behavior of a Point object._  
 _public:_  
 _Point();                               // The default constructor._  
 _Point(float fX, float fY);       // A constructor that takes two floats._  
 _Point(const Point& p);         // The copy constructor._  
 _~Point();                             // The destructor._  
 _void print() {                       // This function will be made inline by default._  
 _cout \<\< "(" \<\< mfX \<\< "," \<\< mfY \<\< ")" \<\< endl;_  
 _}_  
 _void set\_x(float fX);_  
 _float get\_x();_  
 _void set\_y(float fX);_  
 _float get\_y();_  
_};_

_#endif // \_POINT\_H\__  
 

_**point.C**_

_// Definition class Point._

_#include "point.h"_

_// A constructor which creates a Point object at (0,0)._  
_Point::Point() {_  
 _cout \<\< "In constructor Point::Point()" \<\< endl;_  
 _mfX = 0.0;_  
 _mfY = 0.0;_  
_}_

_// A constructor which creates a Point object from two_  
_// floats._  
_Point::Point(float fX, float fY) {_  
 _cout \<\< "In constructor Point::Point(float fX, float fY)" \<\< endl;_  
 _mfX = fX;_  
 _mfY = fY;_  
_}_

_// A constructor which creates a Point object from_  
_// another Point object._  
_Point::Point(const Point& p) {_  
 _cout \<\< "In constructor Point::Point(const Point& p)" \<\< endl;_  
 _mfX = p.mfX;_  
 _mfY = p.mfY;_  
_}_

_// The destructor._  
_Point::~Point() {_  
 _cout \<\< "In destructor Point::~Point()" \<\< endl;_  
_}_

_// Modifier for x coordinate._  
_void Point::set\_x(float fX) {_  
 _mfX = fX;_  
_}_

_// Accessor for x coordinate._  
_float Point::get\_x() {_  
 _return mfX;_  
_}_

_// Modifier for y coordinate._  
_void Point::set\_y(float fY) {_  
 _mfY = fY;_  
_}_

_// Accessor for y coordinate._  
_float Point::get\_y() {_  
 _return mfY;_  
_}_  
 

_**point\_test.C**_

_// Test program for the Point class._

_#include "point.h"_

_void main() {_  
 _Point a;_  
 _Point b(1.0, 2.0);_  
 _Point c(b);_

 _// Print out the current state of all objects._  
 _a.print();_  
 _b.print();_  
 _c.print();_

 _b.set\_x(3.0);_  
 _b.set\_y(4.0);_

 _// Print out the current state of b._  
 _cout \<\< endl;_  
 _b.print();_  
 _}_