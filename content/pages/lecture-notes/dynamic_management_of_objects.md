---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Dynamic Management of Objects
uid: 10cbc2f6-01a3-e189-7699-ef4c2482f9f9
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Contents
--------

1.  [Creating and Destroying Objects - Constructors and Destructors](#1)
2.  [The new and delete Operators](#2)
3.  [Scope and the Lifetime of Objects](#3)
4.  [Data Structures for Managing Objects](#4)

{{< anchor "1" >}}{{< /anchor >}}1\. Creating and Destroying Objects - Constructors and Destructors

_(Ref. Lippman 14.1-14.3)_

Let's take a closer look at how constructors and destructors work.


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

A Point Class
-------------

Here is a complete example of a _Point_ class. We have organized the code into three separate files:

> _point.h_ contains the _declaration_ of the class, which describes the structure of a _Point_ object.
> 
> _point.C_ contains the _definition_ of the class i.e. the actual implementation of the methods.
> 
> _point\_test.C_ is a program that uses the _Point_ class.

Our _Point_ class has three constructors and one destructor.

 _Point();                               // The default constructor._  
 _Point(float fX, float fY);       // A constructor that takes two floats._  
 _Point(const Point& p);         // The copy constructor._  
 _~Point();                             // The destructor._

These constructors can be respectively invoked by object definitions such as

 _Point a;_  
 _Point b(1.0, 2.0);_  
 _Point c(b);_

The default constructor, _Point()_, is so named because it can be invoked without any arguments. In our example, the default constructor initializes the _Point_ to (0,0). The second constructor creates a _Point_ from a pair of coordinates of type _float_. Note that we could combine these two constructors into a single constructor which has default arguments:

 _Point(float fX=0.0, float fY=0.0);_

The third constructor is known as a copy constructor since it creates one _Point_ from another. The object that we want to clone is passed in as a constant reference. Note that we cannot pass by value in this instance because doing so would lead to an unterminated recursive call to the copy constructor. In this example, the destructor does not have to perform any clean-up operations. Later on, we will see examples where the destructor has to release dynamically allocated memory.

Constructors and destructors can be triggered more often than you may imagine. For example, each time a _Point_ is passed to a function by value, a local copy of the object is created. Likewise, each time a _Point_ is returned by value, a temporary copy of the object is created in the calling program. In both cases, we will see an extra call to the copy constructor, and an extra call to the destructor. You are encouraged to put print statements in every constructor and in the destructor, and then carefully observe what happens.  
 

 _**point.h**_

_// Declaration of class Point._

_#ifndef \_POINT\_H\__  
_#define \_POINT\_H\__

_#include \<iostream.h>_

_class Point {_  
 _// The state of a Point object. Property variables are typically_  
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

_int main() {_  
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

 _return 0;_  
 _}_

{{< anchor "2" >}}{{< /anchor >}}2\. The _new_ and _delete_ Operators
---------------------------------------------------------------------

_(Ref. Lippman 4.9, 8.4)_

Until now, we have only considered situations in which the exact number of objects to be created is known at compile time. This is rarely the case in real world software. A web-browser cannot predict in advance how many image objects it will find on a web page. What is needed, therefore, is a way to dynamically create and destroy objects at run time. C++ provides two operators for this purpose:

The _new_ operator allows us to allocate memory for one or more objects. It is similar to the _malloc()_ function in the C standard library.

The _delete_ operator allows us to release memory that has previously been allocated using _new_. It is similar to the _free()_ function in the C standard library. Note that it is an error to apply the _delete_ operator to memory allocated by any means other than _new_.

We can allocate single objects using statements such as

 _a = new Point();_  
 _b = new Point(2.0, 3.0);_

Object arrays can be allocated using statements such as

 _c = new Point\[num\_points\];_

In either case, _new_ returns the starting address of the memory it has allocated, so _a_, _b_, and _c_ must be defined as pointer types, _Point \*_. A single object can be released using a statement such as

  _delete a;_

When releasing memory associated with an array, it is important to remember to use the following notation:

 _delete\[\] c;_

If the square brackets are omitted, only the first object in the array will be released, and the memory associated with the rest of the objects will be leaked.  
 

_**nd\_test.C**_

_// Test program for the new and delete operators._

_#include "point.h"_

_int main() {_  
 _int num\_points;_  
 _Point \*a, \*b, \*c;_  
 _float d;_  
   
 _// Allocate a single Point object in heap memory. This invokes the default constructor._  
 _a = new Point();_

 _// This invokes a constructor that has two arguments._  
 _b = new Point(2.0, 3.0);_

 _// Print out the two point objects._  
 _cout \<\< "Here are the two Point objects I have created:" \<\< endl;_  
 _a->print();_  
 _b->print();_

 _// Destroy the two Point objects._  
 _delete a;_  
 _delete b;_

 _// Now allocate an array of Point objects in heap memory._  
 _cout \<\< "I will now create an array of Points. How big shall I make it? ";_  
 _cin >> num\_points;_  
 _c = new Point\[num\_points\];_

 _for (int i = 0; i \< num\_points; i++) {_  
 _d = (float)i;_  
 _c\[i\].set\_x(d);_  
 _c\[i\].set\_y(d + 1.0);_  
 _}_  
   
 _// Print out the array of point objects._  
 _cout \<\< "Here is the array I have created:" \<\< endl;_  
 _for (int i = 0; i \< num\_points; i++) {_  
 _c\[i\].print();_  
 _}_

 _// Destroy the array of Point objects._  
 _delete\[\] c;                 // What happens if \[\] is omitted?_

 _return 0;_

{{< anchor "3" >}}{{< /anchor >}}3\. Scope and the Lifetime of Objects
----------------------------------------------------------------------

_(Ref. Lippman 8.1-8.4)_

There are three fundamental ways of using memory in C and C++.

*   **Static memory.** This is memory allocated by the linker for the duration of the program. Global variables and objects explicitly defined as _static_ fall into this category.
*   **Automatic memory.** Objects that are allocated in automatic memory are destroyed automatically when they go out of scope. Examples are local variables and function arguments. Objects that reside in automatic memory are said to be _allocated on the stack_.
*   **Dynamic memory.** Memory allocated using the _new_ operator (or _malloc()_) falls into this category. Dynamic memory must be explicitly released using the _delete_ operator (or _free(),_ as appropriate.) Objects that reside in dynamic memory are said to be _allocated on the heap_.

A _garbage collector_ is a memory manager that automatically identifies unreferenced objects in dynamic memory and then reclaims that memory. The C and C++ standards do not require the implementation of automatic garbage collection, however, garbage collectors are sometimes implemented in large scale projects where it can be difficult to keep track of memory explicitly.

The following program illustrates various uses of memory. Note that the _static_ object in the function _foo()_ is only allocated once, even though _foo()_ is invoked multiple times.  
 

_**sl\_test.C**_

_// Test program for scope and the lifetime of objects._

_#include "point.h"_

_Point a(1.0, 2.0);                            // Resides in static memory._

_void foo() {_  
 _static Point a;                             // Resides in static memory._

 _a.set\_x(a.get\_x() + 1.0);_  
 _a.print();_  
_}_

_int main() {_  
 _Point a(4.0, 3.0);                        // Resides in automatic memory._

 _a.print();_  
 _::a.print();_

 _for (int i = 0; i \< 3; i++)_  
 _foo();_

 _Point \*b = new Point(5.0, 6.0);    // Resides in heap memory._  
 _b->print();_  
 _delete b;_

 _// Curly braces serve as scope delimiters._  
 _{_  
 _Point a(7.0, 9.0);                     // Resides in automatic memory._

 _a.print();_  
 _::a.print();_  
 _}_

 _return 0;_  
_}_  
 

Here is the output from the program:

In constructor Point::Point(float fX, float fY)                                     \<-- Global object _a_.  
In constructor Point::Point(float fX, float fY)                                     \<-- Local object _a_.  
(4,3)  
(1,2)  
In constructor Point::Point()                                                              \<-- Object _a_ in _foo()_.  
(1,0)  
(2,0)  
(3,0)  
In constructor Point::Point(float fX, float fY)                                     \<-- Object _\*b_.  
(5,6)  
In destructor Point::~Point()                                                             \<-- Object _\*b_.  
In constructor Point::Point(float fX, float fY)                                     \<-- Second local object _a_.  
(7,9)  
(1,2)  
In destructor Point::~Point()                                                             \<-- Second local object _a_.  
In destructor Point::~Point()                                                             \<-- Local object _a_.  
In destructor Point::~Point()                                                             \<-- Object _a_ in _foo()_.  
In destructor Point::~Point()                                                             \<-- Global object _a_.

{{< anchor "4" >}}{{< /anchor >}}4\. Data Structures for Managing Objects
-------------------------------------------------------------------------

We have already seen an example of how to dynamically create an array of objects. This may not be the best approach for managing a collection of objects that is constantly changing, since we may wish to delete a single object while retaining the rest. Instead, we might consider using an array of pointers to hold individually allocated objects, as illustrated in the following example. Even this approach has its limitations since we need to know how big to make the pointer array. In general, a linked list is the data structure of choice, since it makes no assumptions about the maximum number of objects to be stored. We will see an example of a linked list later.  
 

 _**pa\_test.C**_

_// Pointer array test program._

_#include "point.h"_

_int main() {_  
 _int i, max\_points;_  
 _Point \*\*a;_

 _max\_points = 5;_

 _// Create an array of pointers to Point objects. We will use the_  
 _// array elements to hold on to dynamically allocated Point objects._  
 _a = new Point \*\[max\_points\];_

 _// Now create some point objects and store them in the array._  
 _for (i = 0; i \< max\_points; i++)_  
 _a\[i\] = new Point(i, i);_

 _// Let's suppose we want to eliminate the middle Point._  
 _i = (max\_points-1) / 2;_  
 _delete a\[i\];_  
 _a\[i\] = NULL;_

 _// Print out the remaining Points._  
 _for (i = 0; i \< max\_points; i++) {_  
 _if (a\[i\])_  
 _a\[i\]->print();_  
 _}_

 _// Delete the remaining Points. Note that it is acceptable to pass a NULL_  
 _// pointer to the delete operator._  
 _for (i = 0; i \< max\_points; i++)_  
 _delete a\[i\];_

 _// Now delete the array of pointers._  
 _delete\[\] a;_

 _return 0;_  
_}_