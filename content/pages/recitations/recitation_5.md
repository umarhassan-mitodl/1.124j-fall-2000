---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 5
uid: 85e3e2b7-be39-f207-1805-efe724b15f5f
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).  
  
Topics
------------------------------------------------------------------------------------------

1.  [Function templates](#1) 
2.  [Class templates](#2) 
3.  [Sorting and searching algorithms](#3) 
4.  [Insertion sort](#4)
5.  [Selection sort](#5) 
6.  [Shellsort](#6) 
7.  [Quicksort](#7)
8.  [Linear search](#8) 
9.  [Binary search](#9) 

{{< anchor "1" >}}{{< /anchor >}}1\. Function Templates
-------------------------------------------------------

The _template mechanism_ of C++ allows the development of general functions and classes without the need to know the data type of the variables used during implementation. _Templates_ allow the development of type-independent source code. Suppose that we want to find the maximum of a set of numbers that may be of _int_, _float_, or _double_ data type, the algorithm is the same regardless of the particular data type. Using templates a single function, a function template, can be written that can selectively be instantiated and work considering a specific data type. Similarly, class templates can provide generic descriptions of classes without the need to specify the data types used.

A _template line_, called template parameter list, precedes a _template function declaration_ or definition specifying the parameters that are to be used as data types in the function. One or more data types are parameterized, allowing the instantiation of the function with varying data types specified to the corresponding parameters. The _template parameter list_ begins with the keyword _template_ followed by comma separated parameters enclosed in \<> brackets. Two types of parameters can be specified as template parameters: _template type parameters_, that consist of the keyword _class_, or _typename_, and an identifier; and template nontype parameters which are essentially ordinary parameter declarations that are used to represent a constant in the template definition.

The template parameter list is followed by a _function template declaration or definition_. The only difference of the function definition of a template function from an ordinary function is the presence and use of the _template type parameters_ as data types. The template type parameters can be used in the same way as any other built-in or user-defined data type, in the template declaration or definition that follows the template line. Similarly, the template nontype parameters can be used as constant values. If there is a name conflict in the function template declaration or definition with a name used in the global scope, the latter is hidden. Although the name of a template parameter can be used in several function template declarations and definitions, it is not allowable to use the name of a template parameter more than once in the same template parameter list. The template parameter names used in template declarations and the actual definition of a function template may be different. To specify a function template as inline or extern, the corresponding keyword must be used after the template parameter list, i.e before the return type of the function.

A _template function_ is a specification for an actual function that is created when the template is instantiated with a certain data type. During _template instantiation_, the parameters of a template are replaced by the actual data types, and the actual code for an individual function (with the data types defined) is created by the compiler. Any data type dependent errors are detected only during instantiation and not at the template definition. Prior to instantiation a function is not defined, since the function template is simply a specification on how function should be created during instantiation. A function template is instantiated either when it is  invoked, or when its address is taken to be assigned to a pointer to a function. Then, according to the arguments that are used for the function call, the data types that correspond to the template type parameters, and the values corresponding to the template nontype parameters are determined. This process is called _template argument deduction_ and it is based on the examination of the function arguments. Note, that the return data type of the function template is not considered in the template argument deduction. In addition, the template arguments can be explicitly specified, instead of relying on the template argument deduction mechanism. _Template arguments_ can be explicitly specified by a comma separated list of template arguments in a \<> brackets between the name of the function template and its, enclosed in parentheses, argument list.

The following simple example shows how a template function can be used to determine the maximum element of a vector of numbers that can be of _int_ or _double_ data type.

_/\*  Simple example of using function templates \*/_

> _template\<typename MyType>_  
> _MyType_ _findMax(MyType vect\[\], int n)_  
> _{_  
>  _MyType maximum = vect\[0\];_
> 
> >  _for(int i=1; i\<n ;i++)_  
> >  _if(vect\[i\]>maximum)_  
> >  _maximum = vect\[i\];_
> > 
> >  _return maximum;_  
> > _}_
> > 
> > _template\<class MyType, int SIZE>       _ // keywords class and typename are equivalent  
> > _inline MyType findMin(MyType (&vect)\[SIZE\])_  
> > _{_  
> >  _MyType minimum = vect\[0\];_
> > 
> >  _for(int i=1; i\<SIZE ;i++)_  
> >  _if(vect\[i\]\<minimum)_  
> >  _minimum = vect\[i\];_
> > 
> >  _return minimum;_  
> > _}_
> > 
> > _int main(void)_  
> > _{_  
> >  _int nx = 10, x\[\] = {3, -78, 12, 52, 17, -53, 2, 49, -9, 43}, ny = 7;_  
> >  _double y\[\] = {39.2, -72.8, 5.2, 14.7, -15.3, 41.9, -92.3};_
> > 
> >  _cout \<\< "\\n Maximum element of x = " \<\< findMax(x,nx) \<\< endl;_  
> >  _cout \<\< " Maximum element of y = " \<\< findMax(y,ny) \<\< endl;_
> > 
> >  _cout \<\< "\\n Minimum element of x = " \<\< findMin(x) \<\< endl;_  
> >  _cout \<\< " Minimum element of y = " \<\< findMin(y) \<\< endl;_
> > 
> >  _return EXIT\_SUCCESS;_  
> > _}_
> > 
> > _Output  
> > _
> > 
> >   
> > 
> >  _Maximum element of x = 52_  
> >  _Maximum element of y = 41.9_
> > 
> >  _Minimum element of x = -78_  
> >  _Minimum element of y = -92.3_

  
The definition must be visible at the point of instantiation, e.g. when a function template is called. In the above simple example the definition of the function template and the code in which it was instantiated appeared in the same file.

For larger programs the function template definitions are typically provided in a header file that is included in every file in which the function template is used, similarly as when using inline functions.

{{< anchor "2" >}}{{< /anchor >}}2\. Class Templates
----------------------------------------------------

_Class templates_ can be used to develop a generic class prototype (specification) that can be instantiated with different data types. This is very useful when the same kind of class is used with different data types for individual members of the class. Parameterized types are used as data types, as in the function templates, and then a class can be instantiated, i.e. constructed and used, by providing arguments for the parameters of the class template. A _class template_ is a specification of how a class should be built (i.e. instantiated) given the data type or values of its parameters.

A _class_ _template_ is defined by a line which defines the parameters, using the keyword _template_ followed by the parameters (template type and nontype parameters) enclosed in \<> brackets known as _template parameter list_. Each template type parameter is preceded by the keyword _class_ or _typename_, and it is replaced by the corresponding argument when the class is instantiated. The name of a template type parameter represents a built-in or user-defined data type that would be defined during the _class instantiation_. A template nontype parameter is like a an ordinary (function-parameter) declaration, and represents a constant in the class template definition, i.e. it should be possible to be determined at compilation time. A parameter can be specified only once in the template parameter list and should not have the same name with a member of the class. The name of a template parameter can be reused in other template declarations or definitions, and also can be different in declarations or definitions of the same class template. If the name of a template parameter is the same as a global variable then the latter is hidden by the parameter.

In addition, the _class template parameters_ (both type and nontype) can have default arguments that are used, during class template instantiation, if arguments are not provided. Because the provided arguments are used starting from the far left parameter, default arguments should be provided for the rightmost parameters.

Then, the _declaration or definition of the class_ follows, using the defined type parameters as data types. The definition of a class template as well as the definitions of externally defined member functions are similar to ordinary class and member function definitions with the only difference being, besides the template parameter list at their beginning, the use of the template parameters. To define externally defined member functions of a class template, the template parameter list must precede the definition to make the parameters available to the function. In addition, the template parameters should also be used in \<> brackets list before the scope resolution operator to indicate the actual name of the specific class which is a certain instantiation of the class template. A member function of a class template is itself a function template which is instantiated only whenever the function is invoked or its address is taken (and not when the class template is instantiated), using the corresponding data types used for the associated class object.

To create a particular class and define an object of that class the name of the template class is used followed by a comma-separated list of either data types that are used as arguments to the type parameters, i.e. specifying the data types to be used for the class creation, or arguments that are passed as values to the non-type parameters of the class template. This is process is called _template substitution_. Each different instantiation of a class template is considered a different class which is identified by the name of the class template followed a comma separated list of parameters enclosed in \<> brackets that are used for the instantiation. In contrast to function templates, where some non-type parameters may be deduced from the way they are used, e.g. the size of an array, the template parameters must be either provided as arguments or have default values that can be used.

Sometimes ambiguity may arise during instantiation of a template class, e.g. due to already existing member functions using certain data types which come in conflict with generated member functions using the specified data type which may happen to be the same.

The following simple example demonstrates the definition and use of a class template.

_myTemplate.h_

> ?
> 
> _template \<class myTypeX, typename myTypeY>_  
> _class Point;_ _template \<typename myTypeX, class myTypeY>_  
> _class Point_  
> _{_  
> _private:_  
>  _myTypeX x;_  
>  _myTypeY y;_  
>  _Point();_
> 
> _public:_
> 
>  _Point(myTypeX x, myTypeY y)_  
>  _{_  
>  _this->x = x;_  
>  _Point::y = y;_  
>  _}_
> 
>  _void print(void);_  
> _};_
> 
> _template \<class myTypeX, class myTypeY>_  
> _void Point\<myTypeX,myTypeY>::print(void)_  
> _{_  
>  _cout \<\< " (x,y) = (" \<\< x \<\< "," \<\< y \<\< ")  "  ;_  
> _}_
> 
>   
>  

_myTemplate.C_

> _#include  \<iostream.h>_  
> _#include  \<stdlib.h>_  
> _#include  "myTemplate.h"_
> 
> _int main ( )_  
> _{_  
>  _Point\<int,double> p1(3,9.25);_  
>  _cout \<\< "\\n p1 = ";_  
>  _p1.print();_
> 
>  _Point\<double,int> p2(3.74,9);_  
>  _cout \<\< "\\n p2 = ";_  
>  _p2.print();_
> 
>  _cout \<\< endl;_  
>  _return EXIT\_SUCCESS;_  
> _}_

{{< anchor "3" >}}{{< /anchor >}}3\. Sorting and Searching Algorithms
---------------------------------------------------------------------

Sorting and searching are fundamental operations in computation and information technology.

Because searching a sorted array is much more efficient than searching an unsorted one, sorting is used to facilitate searching. In many programs the running time is determined by the time required for sorting. Therefore, it is important to implement a fast sorting algorithm.

For all algorithms, presented below, assume that the _N_ data (elements) are stored in an array named _A_.

{{< anchor "4" >}}{{< /anchor >}}4\. Insertion Sort
---------------------------------------------------

This is an elementary algorithm with nested loops which cause an O(N{{< sup "2" >}}) time.

Each element, starting from the element A\[0\], is considered one at a time and it is positioned in the proper ordered among those who have already been considered.

Example:  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
_4_
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
_8_
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
_2_
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
_1_
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
_3_
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

5{{< anchor "5" >}}{{< /anchor >}}. Selection Sort
--------------------------------------------------

This is another elementary sorting algorithm with an O(N{{< sup "2" >}}) time.

The element with the smallest value in the array is identified and placed in the first position. Then, the element with the smallest value among the remaining N-1 elements is selected and placed in the first position of the N-1 subarray. Continuing this procedure the array is sorted as shown by the following example.

Example:  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
 

{{< anchor "6" >}}{{< /anchor >}}6\. Shellsort
----------------------------------------------

Shellsort is an extension of insertion sort which can increase its efficiency. It allows exchanges of non adjacent elements. Although in some rare cases an O(N^2) time is required, the required time is usually O(N{{< sup "3/2" >}}).

First, a gap size is selected by dividing the number of the elements by 2. Then, the corresponding every "gap-size" elements are sorted. Next, the "gap-size" is divided by 2 and repeat the sorting of the elements at every "gap-size". Finally, the "gap-size" becomes equal to 1 and the entire array is sorted.

Example:  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
  
 

{{< anchor "7" >}}{{< /anchor >}}7\. Quicksort
----------------------------------------------

Quicksort is a very fast sorting algorithm which has O(N.lgN) average times. Its worst case performance is O(N{{< sup "2" >}}), but can be avoided with certain techniques. It is a "divide and conquer" algorithm for sorting. It partitions the data into two parts and then sort them independently.  
It uses in place sorting and a simple recursive structure.

An element of the array, called _pivot_, is picked.

Then, one index start from each side of the array moving towards each other. The higher index is decreased until an element with a value smaller than the value of the pivot is found. Similarly the lower index is increased until an element with a value higher than the value of the pivot is found. If the two indices are different, the two corresponding elements are out of order and need to be exchanged with each other.

The above step is repeated from the point where the process was interrupted.  
If the two indices are the same, then if the value of the selected element is less than that of the pivot the selected element and the pivot are exchanged. Otherwise, no exchange should occur.

At this point the algorithm has grouped the elements of the array into two subarrays. One has all elements smaller than or equal to the pivot and the other all the elements larger or equal to the pivot.

Then, the algorithm is applied recursively to each subarray until the number of the elements of a subarray is equal to 0 or 1.  
 

Example:  
   
   
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
   
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 8
{{< tdclose >}}
{{< tdopen >}}
6 
{{< tdclose >}}
{{< tdopen >}}
 5
{{< tdclose >}}
{{< tdopen >}}
 7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 3
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 8
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5 
{{< tdclose >}}
{{< tdopen >}}
 7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 3
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 8
{{< tdclose >}}
{{< tdopen >}}
6 
{{< tdclose >}}
{{< tdopen >}}
5 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 6
{{< tdclose >}}
{{< tdopen >}}
5 
{{< tdclose >}}
{{< tdopen >}}
8 
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
   
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

_Note_

pivot   -   left index  -  right index -both indices

 Black cells are used to separate the elements of the array, i.e. they are not elements of the array.  
The above array is of size N=8.

{{< anchor "8" >}}{{< /anchor >}}8\. Linear Search
--------------------------------------------------

Linear search is the simplest searching algorithm and can be applied to unsorted data. The search proceeds in sequence searching for a certain element. In the worst case, which is the case of an unsuccessful search, it takes N iterations. On average it takes N/2 iterations.

**Example:**

Search for element with key value equal to 33  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
14
{{< tdclose >}}
{{< tdopen >}}
27
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
49
{{< tdclose >}}
{{< tdopen >}}
51
{{< tdclose >}}
{{< tdopen >}}
67
{{< tdclose >}}
{{< tdopen >}}
95
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
14
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
27
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  
 

{{< anchor "9" >}}{{< /anchor >}}9\. Binary Search
--------------------------------------------------

Binary search can be used on sorted data. It splits the data in half, determines in which half the desired element must be located (if it exists in the data set). Then, recursively repeats the cutting in half of the elements and keeps selecting the part in which he desired data element may be.  
This algorithm requires O(lgN) computational time.

**Example:**

Search for element with key value equal to 33  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
14
{{< tdclose >}}
{{< tdopen >}}
27
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
49
{{< tdclose >}}
{{< tdopen >}}
51
{{< tdclose >}}
{{< tdopen >}}
67
{{< tdclose >}}
{{< tdopen >}}
95
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
49
{{< tdclose >}}
{{< tdopen >}}
51
{{< tdclose >}}
{{< tdopen >}}
67
{{< tdclose >}}
{{< tdopen >}}
95
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
49
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
33
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}
{{< tdopen >}}
 
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}