---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Inheritance
uid: a4708bad-8d4b-e4aa-eb25-0446faa7d391
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Inheritance, Polymorphism and Virtual Functions
-----------------------------------------------

_(Ref. Lippman 2.4, 17.1-17.6)_

Inheritance allows us to specialize the behavior of a class. For example, we might write a _Shape_ class, which provides basic functionality for managing 2D shapes. Our _Shape_ class has member variables for the centroid and area. We may then specialize the _Shape_ class to provide functionality for a particular shape, such as a circle. To do this, we write a class called _Circle_, which inherits the properties and methods of _Shape._

 _class Circle : public Shape {_  
 _..._  
 _};_

The _Circle_ class adds a new member variable for the radius. Now, when we create a _Circle_ object, it will have centroid and area variables (the _Shape_ part) in addition to the radius variable (the _Circle_ part). The _Circle_ object can also call methods associated with class _Shape_, such as _get\_Centroid()_. We refer to the _Shape_ class as the base class and we refer to the _Circle_ class as the derived class.

Members of class _Shape_ that are _private_ (e.g. _mCentroid_) cannot be directly accessed from within the _Circle_ class definition. However, they can be accessed indirectly through the _Shape_ class's _public_ interface (e.g. _get\_Centroid()_). If we wish to allow class _Circle_ to directly access members of class _Shape_, those members should be made _protected_ (e.g. _mfArea_). To the outside world, i.e. in _main()_, _protected_ members behave in exactly the same way as _private_ members.

It is possible to use a base class pointer to address a derived class object, e.g.

 _Circle \*pc_  
 _Shape \*ps;_

 _pc = new Circle();_  
 _ps = pc;_

This feature is known as _polymorphism_. We can use the _Shape_ pointer to access those methods of the _Circle_ object that are inherited from _Shape.  e.g._

    _ps->get\_Centroid()_

The _Circle_ class can also override functions that it inherits from the _Shape_ class, as in the case of _print()_. To make this work, we must declare _print()_ as a _virtual_ function in class Shape. Then, when we use the _Shape_ pointer to access the _print()_ function, as in

    _ps->print();_

we will invoke the _print()_ function in the underlying _Circle_ object. In the example below, we have used an array of _Shape_ pointers, _sa,_ to store a heterogeneous collection of _Circle_ and _Rectangle_ objects. In the code fragment

 _for (i = 0; i \< num\_shapes; i++) {_  
 _sa\[i\]->print();    // This will call either Circle::print() or Rectangle::print(), as appropriate._  
 _}_

the decision to call the _print()_ function in class _Circle_ or the one in class _Rectangle_ must be made at run-time. The mechanism by which virtual function calls are resolved is known as _dynamic binding_.

The implementation of the _print()_ function in class _Shape_ serves as a default implementation, which will be used if the derived class chooses not to provide an overiding implementation. It is possible, however, for the _Shape_ class to require all derived classes to provide an overriding implementation, as in the case of _draw()_. The _draw()_ function is known as a _pure virtual function_, because it does not have an implementation in class _Shape_. Pure virtual functions have a declaration of the form

 _virtual void draw() = 0;_

Since we have not implemented _draw()_ in class _Shape_, the class is incomplete and we cannot actually create _Shape_ objects. The _Shape_ class is therefore said to be an _abstract_ base class.

We must take care when deleting the objects stored in the array of _Shape_ pointers. In the code fragment

 _for (i = 0; i \< num\_shapes; i++)_  
 _delete sa\[i\];  // This will call either Circle::~Circle() or Rectangle::~Rectangle(), as appropriate,_  
 _// before calling Shape::~Shape()._

we have called _delete_ on _sa\[i\]_, which is a _Shape_ pointer, even though the object that it points to is really a _Circle_ or a _Rectangle_. To ensure that the appropriate _Circle_ or _Rectangle_ destructor is called, we must make the _Shape_ destructor a _virtual destructor_.  
 

_**shape.h**_

_#ifndef \_SHAPE\_H\__  
_#define \_SHAPE\_H\__

_#include \<iostream.h>_  
_#include "point.h"_

_#ifndef DEBUG\_PRINT_  
_#ifdef \_DEBUG_  
_#define DEBUG\_PRINT(str) cout \<\< str \<\< endl;_  
_#else_  
_#define DEBUG\_PRINT(str)_  
_#endif_  
_#endif_

_class Shape {_  
 _// The private members of the Shape class are only accessible within_  
 _// the definition of class Shape. They are not accessible within_  
 _// the definitions of classes derived from the Shape class, e.g. Circle,_  
 _// or within main()._  
 _private:_  
 _Point mCentroid;_

 _// The protected members of the Shape class are accessible within the_  
 _// definition of class Shape. They are also accessible within the_  
 _// definitions of classes derived immediately from the Shape class, e.g._  
 _// Circle. However, they are not accessible within main()._  
 _protected:_  
 _float mfArea;_

 _// The public members of the Shape class are accessible everywhere i.e. in_  
 _// the Shape class definition, in derived class definitions and in main()._  
 _public:_  
 _Shape(float fX, float fY);_  
 _virtual ~Shape();               // A virtual destructor._  
 _virtual void print();           // A virtual function._  
 _virtual void draw() = 0;    // A pure virtual function._  
 _const Point& get\_centroid() {_  
 _return mCentroid;_  
 _}_  
_};_

_#endif_  
 

_**shape.C**_

_#include "shape.h"_

_Shape::Shape(float fX, float fY) : mCentroid(fX, fY) {_  
 _// We must use an initialization list to initialize mCentroid._  
 _// Here in the body of the constructor would be too late._  
 _DEBUG\_PRINT("In constructor Shape::Shape(float, float)")_  
_}_

_Shape::~Shape() {_  
 _DEBUG\_PRINT("In destructor Shape::~Shape()")_  
_}_

_void Shape::print() {_  
 _DEBUG\_PRINT("In Shape::print()")_  
 _cout \<\< "Centroid: ";_  
 _mCentroid.print();_  
 _cout \<\< "Area = " \<\< mfArea \<\< endl;_  
_}_  
 

_**circle.h**_

_#ifndef \_CIRCLE\_H\__  
_#define \_CIRCLE\_H\__

_#include "shape.h"_

_class Circle : public Shape {_  
 _private:_  
 _float mfRadius;_

 _public:_  
 _Circle(float fX=0, float fY=0, float fRadius=0);_  
 _~Circle();_  
 _void print();_  
 _void draw();_  
_};_

_#endif_  
 

_**circle.C**_

_#include "circle.h"_  
_#define PI 3.1415926536_

_Circle::Circle(float fX, float fY, float fRadius) : Shape(fX, fY) {_  
 _// We must use an initialization list to initialize the Shape part of the Circle object._  
 _DEBUG\_PRINT("In constructor Circle::Circle(float, float, float)")_  
 _mfRadius = fRadius;_  
 _mfArea = PI \* fRadius \* fRadius;  // mfArea is a protected member of class Shape._  
_}_

_Circle::~Circle() {_  
 _DEBUG\_PRINT("In destructor Circle::~Circle()")_  
_}_

_void Circle::print() {_  
 _DEBUG\_PRINT("In Circle::print()")_  
 _cout \<\< "Circle Radius: " \<\< mfRadius \<\< endl;_

 _// If we want to print out the Shape part of the Circle object as well,_  
 _// we could call the base class print function like this:_  
 _Shape::print();_  
_}_

_void Circle::draw() {_  
 _// Assume that this draws the circle._  
 _DEBUG\_PRINT("In Circle::draw()")_  
_}_  
 

_**rectangle.h**_

_#ifndef \_RECTANGLE\_H\__  
_#define \_RECTANGLE\_H\__

_#include "shape.h"_

_class Rectangle : public Shape {_  
 _private:_  
 _float mfWidth, mfHeight;_

 _public:_  
 _Rectangle(float fX=0, float fY=0, float fWidth=1, float fHeight=1);_  
 _~Rectangle();_  
 _void print();_  
 _void draw();_  
_};_

_#endif_  
 

_**rectangle.C**_

_#include "rectangle.h"_

_Rectangle::Rectangle(float fX, float fY, float fWidth, float fHeight)  : Shape(fX, fY) {_  
 _// We must use an initialization list to initialize the Shape part of the Rectangle object._  
 _DEBUG\_PRINT("In constructor Rectangle::Rectangle(float, float, float, float)")_  
 _mfWidth = fWidth;_  
 _mfHeight = fHeight;_  
 _mfArea = fWidth \* fHeight;  // mfArea is a protected member of class Shape._  
_}_

_Rectangle::~Rectangle() {_  
 _DEBUG\_PRINT("In destructor Rectangle::~Rectangle()")_  
_}_

_void Rectangle::print() {_  
 _DEBUG\_PRINT("In Rectangle::print()")_  
 _cout \<\< "Rectangle Width: " \<\< mfWidth \<\< " Height: " \<\< mfHeight \<\< endl;_

 _// If we want to print out the Shape part of the Rectangle object as well,_  
 _// we could call the base class print function like this:_  
 _Shape::print();_  
_}_

_void Rectangle::draw() {_  
 _// Assume that this draws the rectangle._  
 _DEBUG\_PRINT("In Rectangle::draw()")_  
_}_  
 

_**myprog.C**_

_#include "shape.h"_  
_#include "circle.h"_  
_#include "rectangle.h"_

_int main() {_  
 _const int num\_shapes = 5;_  
 _int i;_

 _// Create an automatic Circle object._  
 _Circle c;_

 _// We cannot instantiate a Shape object because the Shape class has a pure virtual function_  
 _// i.e. a virtual function without a definition within class Shape. Class Shape is therefore said_  
 _// to be an abstract base class._  
 _// Shape s;  // This is not allowed._

 _// We are allowed to have Shape pointers, however._  
 _Shape \*sa\[num\_shapes\];      // Create an array of Shape pointers._

 _// C++ allows us to use a base class pointer to point to a derived class object. This is known_  
 _// as polymorphism. We can thus store a heterogeneous collection of Circles and Rectangles_  
 _// using the array of Shape pointers._  
 _sa\[0\] = new Circle(2,3,1);_  
 _sa\[1\] = new Rectangle(0,2,2,3);_  
 _sa\[2\] = new Circle(7,6,3);_  
 _sa\[3\] = new Circle(0,2,2);_  
 _sa\[4\] = new Rectangle(4,3,1,1);_  
 

 _// Print out all of the objects. We have made the print function virtual_  
 _// in class shape. This means that it can be overridden by print functions_  
 _// with a similar signature that are specific to the derived classes. If_  
 _// a derived class does not provide an implementation of print, then the_  
 _// Shape::print function will be called by default._  
 _for (i = 0; i \< num\_shapes; i++) {_  
 _sa\[i\]->print();    // This will call either Circle::print() or Rectangle::print(), as appropriate._  
 _}_

 _// Delete the objects. Note that we have called delete on Shape pointers,_  
 _// even though the objects that we created using new were derived class_  
 _// objects. To ensure that the appropriate destructor for the derived_  
 _// object is called, we must make the Shape destructor virtual._  
 _for (i = 0; i \< num\_shapes; i++)_  
 _delete sa\[i\];  // This will call either Circle::~Circle() or Rectangle::~Rectangle(), as appropriate,_  
 _// before calling Shape::~Shape()._

 _return 0;_  
_}_