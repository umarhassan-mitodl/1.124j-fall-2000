---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Operator Overloading
uid: 856b251e-e05f-8ffe-ac12-de49977a2a23
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Operator Overloading
--------------------

_(Ref. Lippman 15.1-15.7, 15.9)_

We have already seen how functions can be overloaded in C++. We can also overload operators, such as the + operator, for classes that we write. Note that operators for built-in types may not be created or modified. A complete list of overloadable operators can be found in Lippman, Table 15.1.

A Complex Number Class
----------------------

In this example, we have overloaded the following operators: +, \*, >, =, (), \[\] and the cast operator.

**operator+() and operator\*()**

Let _a_ and _b_ be of type _Complex_. The _+_ operator in the expression _a+b_, can be interpreted as

 _a.operator+(b)_

where _operator+()_ is a member function of class _Complex_. We then have to write this function so that it adds the real and imaginary parts of _a_ and _b_ and returns the result as a new _Complex_ object. Note that the function returns by value, since it has to create a temporary object for the result of the addition.

Our implementation will also work for an expression like _a+b+c_. In this case, the operator will be invoked in the following order

    (_a.operator+(b)).operator+(c)_

The member _operator+()_ will also work for an expression like

    _a + 7.0_

because we have a constructor that can create a _Complex_ from a single _double_. However, the expression

    _7.0 + a_

will not work, because _operator+()_ is a member of class _Complex_, and not the built-in _double_ type.

To solve this problem, we can make the operator a _global function_, as we have done with _operator\*()_. The expression _7.0 \* a_ will be interpreted as

    _operator\*(7.0, a)_

Since a global function does not automatically have access to the private data of class _Complex_, we can grant special access to _operator\*()_ by making it a _friend_ function of class _Complex_. In general, _friend_ functions and classes should be used sparingly, since they are a violation of the rule of encapsulation.

**operator>()**

We have overloaded this operator to allow comparison of two _Complex_ numbers, based on their magnitudes.

**operator=()**

The _\=_ operator is designed to work with statements like

    _a = b;_  
 _a = b = c;_

These statements respectively interpreted as

    _a.operator=(b);_  
    _a.operator=(b.operator=(c));_

In this case, the operator changes the object that invokes it, and it returns a reference to this object so that the second statement will work. The keyword _this_ gives us a pointer to the current object within the class definition.

**operator Point()**

This operator allows us to convert a _Complex_ object to a _Point_ object. It can be used in an explicit cast, like

    _Complex a;_  
    _Point p;_  
    _p = (Point)a;_

but it could also be invoked implicitly, as in

    _p = a;_

Hence, a great deal of caution should be used when providing user-defined type conversions in this way. An alternative way to convert from a _Complex_ to a _Point_ is to give the _Point_ class a constructor that takes a _Complex_ as an argument. However, we might not have access to the source code for the _Point_ class, if it were written by someone else.

Note that overloaded cast operators do not have a return type.

**operator()()**

This is the function call operator. It is invoked by a _Complex_ object _a_ as

    a()

Here we have overloaded _operator()()_ to return _true_ if the object has an imaginary part and _false_ otherwise.

**operator\[\]()**

The overloaded subscript operator is useful if we wish to access fields of the object like array elements. In our example, we have made _a\[0\]_ refer to the real part and _a\[1\]_ refer to the imaginary part of the object.

**operator\<\<()**

The output operator cannot be overloaded as a member function because we do not have access to the _ostream_ class to which the predefined object _cout_ belongs. Instead, _operator\<\<()_ is overloaded as a global function. We must return a reference to the _ostream_ class so that the output operator can be concatenated. For example,

    _cout \<\< a \<\< b;_

will be invoked as

    _operator\<\<((operator\<\<(cout, a),b)_  
 

_**complex.h**_

_// Interface for class Complex._  
_#ifndef \_COMPLEX\_H\__  
_#define \_COMPLEX\_H\__

_#include \<iostream.h>_  
_#include "point.h"_

_#ifndef DEBUG\_PRINT_  
_#ifdef \_DEBUG_  
_#define DEBUG\_PRINT(str)  cout \<\< str \<\< endl;_  
_#else_  
_#define DEBUG\_PRINT(str)_  
_#endif_  
_#endif_

_class Complex {_  
 _private:_  
 _double mdReal;_  
 _double mdImag;_

 _public:_  
 _// This combines three constructors in one. Here we have used an initialization list to initialize_  
 _// the private data, instead of using assignment statements in the body of the constructor._  
 _Complex(double dReal=0.0, double dImag=0.0) : mdReal(dReal), mdImag(dImag) {_  
 _DEBUG\_PRINT("In Complex::Complex(double dReal, double dImag)")_  
 _}_

 _// The copy constructor._  
 _Complex(const Complex& c);_  
 _~Complex() {_  
 _DEBUG\_PRINT("In Complex::~Complex()")_  
 _}_  
 _void print();_

 _// Overloaded member operators._  
 _Complex operator+(const Complex& c) const;      // Overloaded + operator._  
 _int operator>(const Complex& c) const;                // Overloaded > operator._  
 _Complex& operator=(const Complex& c);           // Overloaded = operator._  
 _operator Point() const;                  // Overloaded cast-to-Point operator._  
 _bool operator()(void) const;          // Overloaded function call operator._  
 _double& operator\[\](int i);              // Overloaded subscript operator._

 _// Overloaded global operators. We make these operators friends of class_  
 _// Complex, so that they will have direct access to the private data._  
 _friend ostream& operator\<\<(ostream& os, const Complex& c);       // Overloaded output operator._  
 _friend Complex operator\*(const Complex& c, const Complex& d);   // Overloaded \* operator._  
_};_  
_#endif    // \_COMPLEX\_H\__  
 

_**complex.C**_

_// Implementation for class Complex._  
_#include "complex.h"_  
_#include \<stdlib.h>_

_// Definition of copy constructor._  
_Complex::Complex(const Complex& c) {_  
 _DEBUG\_PRINT("In Complex::Complex(const Complex& c)")_  
 _mdReal = c.mdReal;_  
 _mdImag = c.mdImag;_  
_}_

_// Definition of overloaded + operator._  
_Complex Complex::operator+(const Complex& c) const {_  
 _DEBUG\_PRINT("In Complex Complex::operator+(const Complex& c) const")_  
 _return Complex(mdReal + c.mdReal, mdImag + c.mdImag);_  
_}_  
 

_// Definition of overloaded > operator._  
_int Complex::operator>(const Complex& c) const {_  
 _double sqr1 = mdReal \* mdReal + mdImag \* mdImag;_  
 _double sqr2 = c.mdReal \* c.mdReal + c.mdImag \* c.mdImag;_

 _DEBUG\_PRINT("In int Complex::operator>(const Complex& c) const")_  
 _return (sqr1 > sqr2);_  
_}_  
 

_// Definition of overloaded assignment operator._  
_Complex& Complex::operator=(const Complex& c) {_  
 _DEBUG\_PRINT("In Complex& Complex::operator=(const Complex& c)")_  
 _mdReal = c.mdReal;_  
 _mdImag = c.mdImag;_  
 _return \*this;_  
_}_  
 

_// Definition of overloaded cast-to-Point operator. This converts a Complex object to a Point object._  
_Complex::operator Point() const {_  
 _float fX, fY;_

 _DEBUG\_PRINT("In Complex::operator Point() const")_  
 _// Our Point class uses floats instead of doubles. In this case, we make a conscious decision_  
 _// to accept a loss in precision by converting the doubles to floats. Be careful when doing this!_  
 _fX = (float)mdReal;_  
 _fY = (float)mdImag;_

 _return Point(fX, fY);_  
_}_

_// Definition of overloaded function call operator. We have defined this operator to allow us to test_  
_// whether a number is complex or real._  
_bool Complex::operator()(void) const {_  
 _DEBUG\_PRINT("In bool Complex::operator()(void) const")_  
 _if (mdImag == 0.0)_  
 _return false;     // Number is real._  
 _else_  
 _return true;      // Number is complex._  
_}_

_// Definition of overloaded subscript operator. We have defined this operator to allow access to_  
_// the real and imaginary parts of the object._  
_double& Complex::operator\[\](int i) {_  
 _DEBUG\_PRINT("In double& Complex::operator\[\](int)")_  
 _switch(i) {_  
 _case 0:_  
 _return mdReal;_

 _case 1:_  
 _return mdImag;_

 _default:_  
 _cerr \<\< "Index out of bounds" \<\< endl;_  
 _exit(0);                           // A function in the C standard library._  
 _}_  
_}_

_// Definition of a print function._  
_void Complex::print() {_  
 _cout \<\< mdReal \<\< " + j" \<\< mdImag \<\< endl;_  
_}_

_// Definition of overloaded output operator. Note that this is a global function. We can_  
_// access the private data of the Complex object c because the operator is a friend function._  
_ostream& operator\<\<(ostream& os, const Complex& c) {_  
 _DEBUG\_PRINT("In ostream& operator\<\<(ostream&, const Complex&)")_  
 _cout \<\< c.mdReal \<\< " + j" \<\< c.mdImag;_  
 _return os;_  
_}_

_// Definition of overloaded \* operator. By making this operator a global function, we can_  
_// handle statements such as a = 7 \* b, where a and b are Complex objects._  
_Complex operator\*(const Complex& c, const Complex& d) {_  
 _DEBUG\_PRINT("In Complex operator\*(const Complex& c, const Complex& d)")_  
 _double dReal = c.mdReal\*d.mdReal - c.mdImag\*d.mdImag;_  
 _double dImag = c.mdReal\*d.mdImag + c.mdImag\*d.mdReal;_  
 _return Complex(dReal, dImag);_  
_}_  
 

_**complex\_test.C**_

_#include "complex.h"_

_void main() {_  
 _Complex a;_  
 _Complex b;_  
 _Complex \*c;_  
 _Complex d;_

 _// Use of constructors and the overloaded operator=()._  
 _a = (Complex)2.0;                 // Same as a = Complex(2.0);_  
 _b = Complex(3.0, 4.0);_  
 _c = new Complex(5.0, 6.0);_

 _// Use of the overloaded operator+()._  
 _d = a + b;                              // Same as d = a.operator+(b);_  
 _d.print();_

 _d = a + b + \*c;                      // Same as d = (a.operator+(b)).operator+(\*c);_  
 _d.print();_

 _// Use of the overloaded operator>()._  
 _if (b > a)_  
 _cout \<\< "b > a" \<\< endl;_  
 _else_  
 _cout \<\< "b \<= a" \<\< endl;_

 _// Use of cast-to-Point operator. This will convert a Complex object to a Point object._  
 _// An alternative way to handle the type conversion is to give the Point class a constructor_  
 _// that takes a Complex object as an argument._  
 _Point p;_  
 _p = (Point)b;_  
 _p.print();_

 _// Use of the overloaded operator()()._  
 _if (a() == true)_  
 _cout \<\< "a is a complex number" \<\< endl;_  
 _else_  
 _cout \<\< "a is a real number" \<\< endl;_

 _// Use of the overloaded operator\[\](). This will change the imaginary part of a._  
 _a\[1\] = 8.0;_  
 _a.print();_

 _// Use of the overloaded global operator\<\<()._  
 _cout \<\< "a = " \<\< a \<\< endl;_

 _// User of the overloaded global operator\*(). The double literal constant will be passed as the_  
 _// first argument to operator\*() and it will be converted to a Complex object using the Complex_  
 _// constructor.  This statement would not be legal if the operator were a member function._  
 _d = 7.0 \* b;_

 _cout \<\< "d = " \<\< d \<\< endl;_  
_}_