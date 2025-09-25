---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Static Class Members
uid: 0f2e5fd5-ac35-ade3-feed-1ed2cd37e418
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Static Member Data and Static Member Functions
----------------------------------------------

_(Ref. Lippman 13.5)_

The _Point_ class that we have developed has both member data (properties) and member functions (methods). Each object that we create will have its own variables _mfX_, and _mfY_, whose values can vary from one _Point_ to another. In order to access a member function, we must have created an object first e.g. if we want to write

_a.print();_

then the object _a_ must already exist.

Suppose now that we wish to have a counter that will keep track of the number of _Point_ objects that we create. It does not make sense for each _Point_ object to have its own copy of the counter, since the counter will have the same value regardless of which object we are referring to. We would rather have a single integer variable that is shared by all objects of the class. We can do this by creating a _static_ member variable as the counter. What if we wish to provide a member function to query the counter? We would not be able to access the member function unless we have created at least one object. We would rather have a function that is associated with the class itself and not with any object. We can do this by creating a _static_ member function. The following example illustrates this.

**point.h**

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
 _static int miCount;_

 _// The behavior of a Point object._  
 _public:_  
 _Point(float fX=0, float fY=0);        // A constructor that takes two floats._  
 _~Point();                                         // The destructor._  
 _static int get\_count();_  
 _// ..._  
_};_

_#endif // \_POINT\_H\__

**point.C**

_// Definition of class Point._

_#include "point.h"_

_// Initialize the counter._  
_int Point::miCount = 0;_

_// A constructor which creates a Point object from two floats._  
_Point::Point(float fX, float fY) {_  
 _cout \<\< "In constructor Point::Point(float,float)" \<\< endl;_  
 _mfX = fX;_  
 _mfY = fY;_  
 _miCount++;_  
_}_

_// The destructor._  
_Point::~Point() {_  
 _cout \<\< "In destructor Point::~Point()" \<\< endl;_  
 _miCount--;_  
_}_

_// Accessor for the counter variable._  
_int Point::get\_count() {_  
 _return miCount;_  
_}_

**point\_test.C**

_#include "point.h"_

_int main() {_  
 _cout \<\< Point::get\_count() \<\< endl;  // We don't have any Point objects yet!_

 _Point a;_  
 _Point \*b = new Point(1.0, 2.0);_

    _cout \<\< b->get\_count() \<\< endl;      // This is allowed, since \*b exists._

 _delete b;_

 _cout \<\< a.get\_count() \<\< endl;           // This is allowed, since a exists._

 _return 0;_  
 _}_