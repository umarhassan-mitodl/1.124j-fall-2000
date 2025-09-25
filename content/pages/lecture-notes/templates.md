---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Templates
uid: 75669def-94dc-da57-0156-40ac5f7060a4
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Introduction](#1)
2.  [Function Templates](#2)
3.  [Class Templates](#3)

{{< anchor "1" >}}{{< /anchor >}}1\. Introduction
-------------------------------------------------

Templates allow us to write functions and classes that are based on parameterized types. For example, we may wish to write a function or class to run quicksort on (1) an array of _int_s and (2) an array of _float_s. Rather than writing two separate versions, one for _int_s and one for _float_s, we may write a single generic template from which the compiler can generate the _int_ and _float_ versions of quicksort.

{{< anchor "2" >}}{{< /anchor >}}2\. Function Templates
-------------------------------------------------------

The following example illustrates how to use function templates.

_**FunctionTemplates.cpp**_

_#include \<iostream.h>_

_// A function template for creating functions that reverse the order of the elements in an array._  
_template\<typename ItemType>_  
_void reverse(ItemType a\[\], int N) {_  
 _for (int i = 0; i \< N/2; i++) {_  
 _ItemType tmp = a\[i\];_  
 _a\[i\] = a\[N-1-i\];_  
 _a\[N-1-i\] = tmp;_  
 _}_  
_}_

_// A function template, where the type cannot be inferred from the function arguments._  
_template\<typename ItemType>_  
_void print(void \*p, int N) {_  
 _ItemType \*a = (ItemType \*)p;_

 _for (int i = 0; i \< N; i++)_  
 _cout \<\< "Element " \<\< i \<\< " is " \<\< a\[i\] \<\< endl;_  
_}_  
 

_// Optional: you are allowed to explicitly instantiate the function templates, if you wish. If you don't_  
_// do this, the instantiation will occur implicitly as a result of the functions calls below._  
_template void print\<int>(void \*, int);_  
_template void print\<float>(void \*, int);_

_const int aLength = 5;_  
_const int bLength = 10;_

_int main() {_  
 _int i;_  
 _int a\[aLength\];_  
 _float b\[bLength\];_

 _for (i = 0; i \< aLength; i++)_  
 _a\[i\] = i;_

 _for (i = 0; i \< bLength; i++)_  
 _b\[i\] = (float)i;_

 _// The compiler will create two versions of reverse(), one to handle ints and one to handle floats._  
 _// In this case, ItemType can be inferred from the first argument._  
 _reverse(a, aLength);_  
 _reverse(b, bLength);_

 _// The compiler will create two versions of print(), one to handle ints and one to handle floats._  
 _// In this case, ItemType cannot be inferred from the function arguments. Hence, explicit_  
 _// specification of the parameter is required. (VC++ users note: VC++ 6.0 has a bug which_  
 _// causes it to use the float version in both cases.)_  
 _print\<int>((void \*)a, aLength);_  
 _print\<float>((void \*)b, bLength);_

 _return 0;_  
_}_

{{< anchor "3" >}}{{< /anchor >}}3\. Class Templates
----------------------------------------------------

The following example illustrates how to use class templates.

**ArrayClass.h**

_#include \<iostream.h>_

_// This class template allows us to create array objects of any type and size._  
_template\<typename ItemType, int size>_  
_class ArrayClass {_  
 _private:_  
 _ItemType array\[size\];_

 _public:_  
 _ArrayClass();_  
 _~ArrayClass() {}_  
 _void print();_  
_};_  
 

_// In a class template, all member function definitions should be placed in the header file._

_template\<typename ItemType, int size>_  
_ArrayClass\<ItemType, size>::ArrayClass() {_  
 _for (int i = 0; i \< size; i++) {_  
 _array\[i\] = (ItemType)(i/2.0);   // The chosen default behavior._  
 _}_  
_}_

_template\<typename ItemType, int size>_  
_void ArrayClass\<ItemType, size>::print() {_  
_for (int i = 0; i \< size; i++) {_  
 _cout \<\< array\[i\] \<\< endl;_  
 _}_  
_}_  
 

**Main.cpp**

_#include "ArrayClass.h"_

_int main() {_  
 _ArrayClass\<int, 5> a;_  
 _ArrayClass\<float, 10> b;_

 _a.print();_  
 _cout \<\< endl;_  
 _b.print();_

 _return 0;_  
_}_