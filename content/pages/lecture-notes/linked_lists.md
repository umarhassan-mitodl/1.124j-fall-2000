---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Linked Lists
uid: 030b40c6-3c0f-72a6-b3c6-c628e49db05f
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Member Access](#1)
2.  [A Linked List Class](#2)

{{< anchor "1" >}}{{< /anchor >}}1\. Member Access
--------------------------------------------------

_(Ref. Lippman 13.1.3, 17.2, 18.3)_

Types of Access Privilege
-------------------------

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
TYPE OF MEMBER
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE IN CLASS DEFINITION
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY OBJECTS
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
private
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
no
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
protected
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
no
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
public
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  

Member Access Under Inheritance
-------------------------------

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
INHERITANCE ACCESS SPECIFIER
{{< thclose >}}
{{< thopen >}}
TYPE OF MEMBER IN BASE CLASS
{{< thclose >}}
{{< thopen >}}
ACCESS LEVEL IN FIRST DERIVED CLASS
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY FIRST DERIVED CLASS DEFINITION
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY FIRST DERIVED CLASS OBJECTS
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
private
{{< tdclose >}}
{{< tdopen >}}
private  
protected  
public
{{< tdclose >}}
{{< tdopen >}}
\-  
private  
private
{{< tdclose >}}
{{< tdopen >}}
no  
yes  
yes
{{< tdclose >}}
{{< tdopen >}}
no  
no  
no
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
protected
{{< tdclose >}}
{{< tdopen >}}
private  
protected  
public
{{< tdclose >}}
{{< tdopen >}}
\-  
protected  
protected
{{< tdclose >}}
{{< tdopen >}}
no  
yes  
yes
{{< tdclose >}}
{{< tdopen >}}
no  
no  
no
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
public
{{< tdclose >}}
{{< tdopen >}}
private  
protected  
public
{{< tdclose >}}
{{< tdopen >}}
\-  
protected  
public
{{< tdclose >}}
{{< tdopen >}}
no  
yes  
yes
{{< tdclose >}}
{{< tdopen >}}
no  
no  
yes
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  

Key Points
----------

*   Private members are only accessible within the class that they are declared. They are not accessible by derived class definitions.
*   Protected members are not accessible by objects. They are always accessible by a first level derived class.
*   The inheritance access specifier places an upper limit on the access level of inherited members in the derived class.

{{< anchor "2" >}}{{< /anchor >}}2\. A Linked List Class
--------------------------------------------------------

Class Declaration
-----------------

_**list.h**_

_#ifndef \_LIST\_H\__  
_#define \_LIST\_H\__

_#include \<iostream.h>_  
_#ifndef TRUE_  
_#define TRUE 1_  
_#endif                          // TRUE_  
_#ifndef FALSE_  
_#define FALSE 0_  
_#endif                          // FALSE_

_// Generic list element. ListElement is an abstract class which will be_  
_// subclassed by users of the List class in order to create different types_  
_// of list elements._  
_class ListElement {_  
 _private:_  
 _ListElement \*mpNext;        // Pointer to next element in the list._

 _public:_  
 _ListElement() {mpNext = NULL;}_  
 _virtual ~ListElement() {}_

 _// A pure virtual method which returns some measure of the element's_  
 _// importance for purposes of ordering the list. The implementation_  
 _// will be provided by individual subclasses. The list will be ordered_  
 _// from most significant (at the head) to least significant._  
 _virtual float ElementValue() = 0;_

 _// A pure virtual method which prints out the contents of the list element._  
 _// Implementation will be provided by individual subclasses._  
 _virtual void print() = 0;_

 _// Grant special access privilege to class list._  
_friend class List;_

 _// An operator\<\< which prints out a list._  
_friend ostream& operator\<\<(ostream &os, const List& list);_  
_};_  
 

_// A linked list class._  
_class List {_  
 _private:_  
 _ListElement \*mpHead;        // Pointer to the first element in the list._

 _public:_  
 _// Create an empty list._  
 _List();_

 _// Destroy the list, including all of its elements._  
 _~List();_

 _// Add an element to the list. Returns TRUE if successful._  
 _int AddElement(ListElement \*pElement);_

 _// Remove an element from the list. Returns TRUE if successful._  
 _int RemoveElement(ListElement \*pElement);_

 _// Return a pointer to the largest element. Does not remove it from the list._  
 _ListElement \*GetLargest();_

 _// Return a pointer to the smallest element. Does not remove it from the list._  
 _ListElement \*GetSmallest();_

 _// An operator\<\< which prints out the entire list._  
 _friend ostream& operator\<\<(ostream &os, const List& list);_  
_};_

_#endif                          // \_LIST\_H\__

Class Definition
----------------

_**list.C**_

_#include "list.h"_

_// Create an empty list._  
_List::List() {_  
 _mpHead = NULL;_  
_}_

_// Destroy the list, including all of its elements._  
_List::~List() {_  
 _ListElement \*pCurrent, \*pNext;_

 _for (pCurrent = mpHead; pCurrent ! = NULL; pCurrent = pNext) {_  
 _pNext = pCurrent->mpNext;_  
 _delete pCurrent;_  
 _}_  
_}_

_// Add an element to the list. Returns TRUE if successful._  
_int List::AddElement(ListElement \*pElement) {_  
 _ListElement \*pCurrent, \*pPrevious;_  
 _float fValue = pElement->ElementValue();_

 _pPrevious = mpHead;_  
 _for (pCurrent = mpHead; pCurrent != NULL; pCurrent = pCurrent->mpNext) {_  
 _if (fValue > pCurrent->ElementValue()) {_  
 _// Insert the new element before the current element._  
 _pElement->mpNext = pCurrent;_  
 _if (pCurrent == mpHead)_  
 _mpHead = pElement;_  
 _else_  
 _pPrevious->mpNext = pElement;_  
 _return TRUE;_  
 _}_  
 _pPrevious = pCurrent;_  
 _}_

 _// We have reached the end of the list._  
 _if (mpHead == NULL)_  
 _mpHead = pElement;_  
 _else_  
 _pPrevious->mpNext = pElement;_  
 _pElement->mpNext = NULL;_

 _return TRUE;_  
_}_

_// Remove an element from the list. Returns TRUE if successful._  
_int List::RemoveElement(ListElement \*pElement) {_  
 _ListElement \*pCurrent, \*pPrevious;_

 _pPrevious = mpHead;_  
 _for (pCurrent = mpHead; pCurrent != NULL; pCurrent = pCurrent->mpNext) {_  
 _if (pCurrent == pElement) {_  
 _if (pCurrent == mpHead)_  
 _mpHead = pCurrent->mpNext;_  
 _else_  
 _pPrevious->mpNext = pCurrent->mpNext;_  
 _delete pCurrent;_  
 _return TRUE;_  
 _}_  
 _pPrevious = pCurrent;_  
 _}_

 _// The given element was not found in the list._  
 _return FALSE;_  
_}_

_// Return a pointer to the largest element. Does not remove it from the list._  
_ListElement \*List::GetLargest() {_  
 _return mpHead;_  
_}_

_// Return a pointer to the smallest element. Does not remove it from the list._  
_ListElement \*List::GetSmallest() {_  
 _ListElement \*pCurrent, \*pPrevious;_

 _pPrevious = mpHead;_  
 _for (pCurrent = mpHead; pCurrent != NULL; pCurrent = pCurrent->mpNext) {_  
 _pPrevious = pCurrent;_  
 _}_

 _return pPrevious;_  
_}_

_// An operator\<\< which prints out the entire list._  
_ostream& operator\<\<(ostream &os, const List& list) {_  
 _ListElement \*pCurrent;_

 _for (pCurrent = list.mpHead; pCurrent ! = NULL;_  
 _pCurrent = pCurrent->mpNext) {_  
 _// Print out the contents of the current list element. Since the_  
 _// print method is declared to be virtual in the ListElement class,_  
 _// the actual print method to be used will be determined at run time._  
 _pCurrent->print();_  
 _}_  
_}_  
 

Using the Linked List Class
---------------------------

_**shapes.h**_

_// Some shapes that we may wish to store in a linked list._  
_// We will order the shape objects according to their areas._

_#ifndef \_SHAPE\_H\__  
_#define \_SHAPE\_H\__

_#define PI 3.14159_

_#include "list.h"_

_class Triangle : public ListElement {_  
 _private:_  
 _float mfBase, mfHeight;_

 _public:_  
 _// Unless we provide an explicit base class initializer, the base_  
 _// class will be initialized using its default constructor._  
 _Triangle() {mfBase = mfHeight = 0.0;}_  
 _Triangle(float fBase, float fHeight) {mfBase = fBase; mfHeight = fHeight;}_  
 _~Triangle() {}_  
 _float ElementValue() {return (mfBase \* mfHeight / 2);}_  
 _void print() {cout \<\< "Triangle: area = " \<\< ElementValue() \<\< endl;}_  
_};_  
 

_class Rectangle : public ListElement {_  
 _private:_  
 _float mfBase, mfHeight;_

 _public:_  
 _// Unless we provide an explicit base class initializer, the base_  
 _// class will be initialized using its default constructor._  
 _Rectangle() {mfBase = mfHeight = 0.0;}_  
 _Rectangle(float fBase, float fHeight) {mfBase = fBase; mfHeight = fHeight;}_  
 _~Rectangle() {}_  
 _float ElementValue() {return (mfBase \* mfHeight);}_  
 _void print() {cout \<\< "Rectangle: area = " \<\< ElementValue() \<\< endl;}_  
_};_  
   
 

_class Circle : public ListElement {_  
 _private:_  
 _float mfRadius;_

 _public:_  
 _// Unless we provide an explicit base class initializer, the base_  
 _// class will be initialized using its default constructor._  
 _Circle() {mfRadius = 0.0;}_  
 _Circle(float fRadius) {mfRadius = fRadius;}_  
 _~Circle() {}_  
 _float ElementValue() {return (PI \* mfRadius \* mfRadius);}_  
 _void print() {cout \<\< "Circle: area = " \<\< ElementValue() \<\< endl;}_  
_};_  
_#endif                          // \_SHAPE\_H\__  
 

_**list\_test.C**_

_#include "shapes.h"_

_main() {_  
 _List list;_  
 _ListElement \*p;_

 _p = new Triangle(4, 3);_  
 _list.AddElement(p);_  
 _p = new Rectangle(2, 1);_  
 _list.AddElement(p);_  
 _p = new Circle(2);_  
 _list.AddElement(p);_  
 _p = new Triangle(3, 2);_  
 _list.AddElement(p);_  
 _p = new Circle(1);_  
 _list.AddElement(p);_

 _cout \<\< list \<\< endl;_

 _list.RemoveElement(list.GetLargest());_

 _cout \<\< list \<\< endl;_

 _list.RemoveElement(list.GetSmallest());_

 _cout \<\< list \<\< endl;_  
_}_