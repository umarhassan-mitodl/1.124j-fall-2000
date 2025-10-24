---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 2
uid: 6e443d7a-ea50-629d-198f-5b188cc78200
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

{{< anchor "1" >}}{{< /anchor >}}

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).
------------------------------------------------------------------------------

Contents
--------

1.  [Functions: declarations, definitions, and, invocations](#1)
2.  [Inline Functions](#2) 
3.  [Function Overloading](#3)
4.  [Recursion](#4) 
5.  [Scope and Extent of Variables](#5)
6.  [References](#6)
7.  [Pointers](#7) 
8.  [Function call by value, References and Pointers](#8)
9.  [Pointers to functions](#9)
10.  [1-D Arrays](#10)
11.  [Strings as arrays of char](#11)
12.  [Arrays of pointers](#12)
13.  [2-D and higher dimensions arrays](#13)
14.  [Return by reference functions](#14)
15.  [Dynamic memory allocation](#15)
16.  [The sizeof operator](#16)
17.  [Data structures](#17)
18.  [Introduction to classes and objects](#18)

{{< anchor "#1" >}}{{< /anchor >}}

{{< anchor "#1" >}}1\. Functions{{< /anchor >}}
-----------------------------------------------

{{< anchor "#1" >}}{{< /anchor >}}

A **function** is a block of code which performs specific tasks and can be called from another point of our program. After the execution of all statements of a function, control returns to the point from where the function was initially invoked, and the next executable statement is executed. With functions we can organize components of a program into sub-units using procedural abstraction. This allow us to break a complex problem into several small subproblems that can be handled easier by separate blocks of code.

_**main()**_ is a special function that is invoked whenever the program is executed. Upon its return the execution of the program is terminated. It typically returns an _int_, which by convention is equal to zero when there are no problems. In contrast, a nonzero value indicates an error.

_The following three steps are required to use a function:_

**(i) Function declaration or prototype (optional):** It informs the compiler that the specified function exists and that its definition appears somewhere else in one of the source code files. In particular, it specifies its name, and parameters. By providing information about certain characteristics of the function, before invocation statements, the compiler is able to make checks for possible inconsistencies in function calls.

The function declaration specifies the function name, which should follow basic naming restrictions, the number and data types of the arguments to be passed to the function and the data type of the returned value. The keyword _void_ is used when the function does not return a value or/and has no arguments. It is also allowable to use empty parameter list, i.e. empty parentheses, but according to the Standard C++, the return type must be explicitly specified.

The name and the data type of the parameters of a function constitute the function _signature_ which uniquely identifies the function.

The declaration is optional if the definition appears before any function call. However, it is a good practice to always provide function declarations. They should preferably be provided in a header file, which can be included whenever it is necessary. A function can be declared multiple times in a program, and, therefore, a header file with declarations can be included several times as well.

            _returnType functionName(param1Type param1Name, param2Type,.....);_

The return type of a function can be any data type, either built-in or user-defined. It is useful, although optional, to provide the names of the arguments for documentation purposes. A function can return a single value, which can also be a data structure, or an object, when it returns back at the invocation point. If no value is returned then the return type of the function should be defined as _void_.  
  
                                    e.g:   _int fun1(double, int);_  
 _void fun2( double x, double y);_  
 _float fun3(void);_

**(ii) Function definition:** The function definition consists of the **_function definition header_** and the **_body of the function definition_**. Although the definition header looks like the declaration, the names of the local parameters are required. Inside the function body the provided statements are executed. More specifically, a function definition consists of 4 parts:

a return type

a function name

an argument list

 the function body

A function declaration is similar to the header of the function definition, providing the return type, name, and parameter list of the function. The function definition must appear once, except in the case of an inline function, providing the body of the function enclosed in curly braces.

When passed-by-value is used, the parameter names are associated with the values passed during function invocation, and they are actually local variables whose memory is released upon exiting the function. When a return statement is encountered control returns to the point from where the function was invoked.

 _returnType functionName(par1Type par1Name,  par2Type par2Name, .....)_  
 _{_  
 _function body_  
 _}_

e.g:     _void fun2(float x, double yy)_  
 _{_  
 _cout \<\< "\\n x+y = " \<\< x+yy;_  
 _}_  
 

**(iii) Function calling (or, function invocation):** A function is invoked by writing its name followed by the appropriate arguments separated by commas and enclosed in parentheses:  
     
        _function\_name(arg1, arg2);_

If the data types of the arguments are not the same with the corresponding data types of the parameters of the function then, either an implicit conversion is done, if possible, or a compile-time error occurs. In case of an implicit conversion in which accuracy may be lost, e.g. converting a double to an int, a warning should be issued during compilation.

Functions work with copies of the arguments when they are called-by-value (i.e. without using references). Upon entering the function memory is temporarily allocated in order to store the passed values. After the function has been executed, the control returns to the calling function and the values of the local variables and parameters that are called-by-value are lost, since the corresponding memory is no longer reserved. The only exception is when we deal with a static local variable.

**_/\* Example on functions \*/_**  
 _#include \<iostream.h>_  
 _#include \<stdio.h>_  
 _double get\_max(double x , double y);_  
 _void print\_max(double x , double y);_

 _main()_  
 _{_  
 _double x=11, y=22 ;_

 _cout \<\< "\\n Max = " \<\< get\_max(x,y) \<\< endl;_  
 _print\_max(x,y);_  
 _}_

 _double get\_max(double x , double y)_  
 _{_  
 _if(x>y)_  
 _return x;_  
 _else_  
 _return y;_  
 _}_

 _void print\_max(double x , double y)_  
 _{_  
 _if(x>y)_  
 _cout \<\< " Max = " \<\< x \<\< endl;_  
 _else_  
 _cout \<\< " Max = " \<\< y \<\< endl;_  
 _}_

**Output**  
 _Max = 22_  
 _Max = 22_  
   
 

Default Arguments of a Function
-------------------------------

Some, or all, arguments of a function can be specified and used in case only some, or no, arguments, respectively, have been provided at the function call. Whenever less than the total number of expected arguments are provided, the specified defaults values are used for the corresponding right-most arguments, i.e. the provided values by the function call are used for the left-most parameters and the remaining parameters on the right take their specified default values. Therefore, all parameters without default values must appear first in the parameter list.

**_/\* Exaple on default arguments to a function \*/_**  
 _void fun(double a=11.1, int b=22, double c=7.6);_

 _int main(void)_  
 _{_

 _fun();_  
 _fun(34.9);_  
 _fun(5.6, 3);_  
 _fun(12.4, 3, 19.5);_

 _return EXIT\_SUCCESS;_  
 _}_

 _void fun(double a, int b, double c)_  
 _{_  
 _cout \<\< " a = " \<\< a \<\< "   b = " \<\< b \<\<"   c = " \<\< c \<\< endl;_  
 _}_

**Output** _a = 11.1   b = 22   c = 7.6_  
 _a = 34.9   b = 22   c = 7.6_  
 _a = 5.6    b = 3    c = 7.6_  
 _a = 12.4   b = 3    c = 19.5_

{{< anchor "2" >}}{{< /anchor >}}

2\. Inline Functions
--------------------

Using functions saves memory space because all the calls to a particular function execute the same code, which is provided only once. However, there is an overhead due to the extra time required to jump to the point that the instructions of that function are provided and then return back to the invocation point. In some cases, where very small functions are used repeatedly, it may be more efficient to have the code incorporated at the point of the function call instead of actually calling the function, so as to avoid the associated overhead. **_Inline functions_** can be used for this purpose. An inline function is a regular function with a suggestion to the compiler to insert the instructions at the points where the function is called.

A definition of a function as inline suggests to the compiler to expand the body of the function at all points where it is invoked. An inline function is expanded by the compiler during the compilation phase and not by the preprocessor (during macro substitutions). This is useful for very short functions which may result in a computational overhead whenever they are called. Inline functions eliminate the overhead of function calls while allowing the usage of procedural abstraction.

A function is defined as inline using the keyword **_“inline”_** before its header. The _inline_ directive should be specified in the function definition, rather than in its declaration.  
  
e.g.:  
 _inline max(double x, double y)_  
 _{_  
 _........   //  statements_  
 _}_

The compiler may, or may not, expand the function at its invocation points to avoid this overhead. However, it is necessary that the compiler sees the function definition, and not just the declaration, before it encounters the first function call, so as to be able to expand it there.

A disadvantage of inline functions is that if an inline function is modified, then all the source code files that use that function should be recompiled. This is necessary because, if the compiler follows the inline suggestion, the body of an inline function is expanded at any point where the function is called. In contrast, a non-inline function is invoked during run-time. Also, the inline function must be defined in every file that it is used, with identical definitions. an alternative way to avoid having multiple copies of the same function definition is to have the function definition in one file which can be included in all source code files that make use of the inline function.

{{< anchor "3" >}}{{< /anchor >}}

3\. Function Overloading
------------------------

C++ allows **_function overloading_**, i.e. having several functions with the same name, in the same scope, as long as they have different signatures. The compiler can distinguish which one to actually invoke based on the data types of the parameter list of each one, which should be different, and the provided arguments. The only overhead from using overloaded functions is during compilation, i.e. there is no effect during run time.

The signature of a function is considered to be its name and parameters, specifically their number and data types. The return type of a function is **not** considered part of a function signature. When an overloaded function is called, the compiler selects the matching function among those with the same name using the data types of the provided arguments. The process in which a function is selected among a set of overloaded functions is called **_function overload resolution._** The latter process follows certain rules based on the arguments provided at a function call. Briefly, the function overload resolution process first identifies all candidate functions, i.e. all visible functions with the same name. Candidate functions are selected based on the argument data types at the function call and considering possible conversions. Finally, the best matching function, if any, is selected among the remaining candidates based on how good the required conversions are.

**_/\* Example on function overloading \*/_**  
 _int **min**(const int x, const int y) ;_  
 _double **min**(const double x, const double y) ;_  
 _main()_  
 _{_  
 _int x,y,m;_  
 _x=3;_  
 _y=7;_  
 _cout \<\< "\\n min(x,y) = " \<\< min(x,y) \<\< endl;_

 _double z=4.5, w=2.34 ;_  
 _cout \<\< " min(z,w) = " \<\<  min(z,w) \<\< endl;_  
 _}_

 _int **min**(const int x1, const int x2)_  
 _{_  
 _if(x1\<x2)_  
 _return x1;_  
 _else_  
 _return x2;_  
 _}_

 _double **min**(const double x1, const double x2)_  
 _{_  
 _if(x1\<x2)_  
 _return x1;_  
 _else_  
 _return x2;_  
 _}_

**Output**  
 _min(x,y) = 3_         // int min(const int x1, const int x2) has been called  
 _min(z,w) = 2.34_      // double min(const double x1, const double x2) has been called

{{< anchor "4" >}}{{< /anchor >}}

4\. Recursion
-------------

An algorithm can have an iterative formulation, a recursive function, or both formulations combined. A function is said to be **_recursive_** if it calls itself. Each time that a function calls itself a new set of local variables is created. This set is independent of any other local variables created in previous calls, assuming that all calls are by value and no static local variables are used.

Typically a recursive function involves a recursive call to itself with a smaller problem to solve. This is the ‘divide-and-conquer’ approach which decomposes a problem into smaller ones with similar characteristics with the original problem. A recursive function should have, at its beginning, a base case that is tested to determine whether the recursive calls should be terminated.

The following two functions can be used to compute the factorial of a number. First, an iterative version is provided, followed by a recursive one.

  _int factorialIterative(int n)           _     **// iterative version**  
 _{_  
 _int result=1;_  
 _while(n>1)_  
 _result \*= n--;_  
 _return result;_  
 _}_  
 

 _int factorialRecursive(int n)_ **// recursive version**  
 _{_  
 _if(n==0)_  
 _return 1;_  
 _return  n\*factorial\_Recursive(n-1);_  
 _}_

{{< anchor "5" >}}{{< /anchor >}}

5\. Scope and Extent of Variables
---------------------------------

The **_scope_** of a variable is where in the program the variable is accessible and therefore it can be used, i.e. the scope defines where the variable can be used, or assigned. In general, variables are accessible only in the block in which they are declared. In C++ there are 3 different scopes: the _local_ scope, the _namespace_ scope, and the _class_ scope.

A variable defined inside a function is a **_local (or automatic) variable_**. The scope of a variable that is defined in a compound block inside a function is limited inside that block. Local scopes can be nested. However, the parameters of a function have local scope and cannot be redeclared inside the function's local scope, or inside any other nested local scopes in the function.

An entity that is defined outside any function or class definition has a namespace scope. User-defined namespaces can be defined using namespace definition, as we will see in a later recitation. For now we will consider only the global scope, which is a specific case of the namespace scope. In particular, the _global_ _scope_ is the outermost scope of a program. A **_global variable_** (or function) is a variable defined outside of all functions.

The **scope** of a global variable is **_universal,_** since it is accessible by all statements after its declaration or definition. In contrast, the scope of a local variable is **_local_** since it is accessible only inside the function in which it has been declared.

A global entity (i.e. variable, object, function) can be declared several times in the source-code files of program, while only one definition can appear. The only exception is inline functions that can have several definitions, identical however, one at each source code file. A global variable can be declared many times using the keyword _extern_ to indicate that somewhere else (in another source code file) that variable is defined. Only one variable definition must be provided and it is only then that memory is allocated for the variable. If a global variable is not initialized at its definition it is automatically initialized to zero.

In addition, in C++, the user defined data types (classes) allow us to specify certain permissions for the access of data members of the objects we define using the classes we develop.

The **_extent_** or lifetime of a variable is the duration for which memory is reserved for it. The memory allocated for parameters and local variables is in general reclaimed upon returning from the function, and therefore, they have **_dynamic extent_**. In contrast, the global variables have **_static extent_** since the memory allocated for them is never reallocated. Local variables can also have static extent if the keyword static is used when they are defined.

There are 4 **storage classes:**

**Automatic:** Local variables, or objects, are local variables with dynamic extent, unless they have been defined as static. Memory is allocated for automatic variables and objects from the run-time stack upon entering the function and is automatically deallocated, i.e. released, upon exiting the function. If an automatic variable is not initialized then its value is unspecified since the allocated memory contains random information.  
 

**External:** Global variables which, unless they have been defined as static, are accessible from any part of the code, i.e. in any file as long as either the global variable definition (and this can occur only once), or a declaration using the keyword extern (this can occur several times) is provided.  
 

**Static:** Both local and global variables can be defined static using the static keyword. However, static local and static global variables are different.  
  
**_Static local variables_** are initialized once, have extent, i.e. lifetime, throughout the program, but their scope, i.e. visibility, is limited to the function in which they are defined. Defining a local variable as static results in having static extent for that variable, i.e. the allocated memory for that variable is reserved until the termination of the program. Memory for a static local variable is allocated only once at the first time the function is entered and the memory with the currently stored value is retained and can be used during the next entry. An uninitialized static local variable is by default initialized to zero.  
**_  
Static global variables_**, or functions, are global variables, or functions, that are not accessible outside the file they are defined, i.e. their use is restricted only within the file they are defined.  
 

**Register:** This storage class is similar with automatic with the only difference that it is suggested to the compiler to keep these particular variables in some registers in CPU so as to save time when these variables are frequently used, e.g. frequently used variable in a loop. An automatic variable can be declared to have register storage using the register keyword, e.g.: _register int i;_

**Access of variables:** A name resolution process determines, during compile time, to which particular entity, i.e. location in memory, a particular name (of a variable, function, object, etc.) refers, considering the provided name and the scope in which it is used.

  Global Variables: _variableName_ or  _:: variableName_  
  Local Variables:  _variableName_  
  Object Member Variables:  _object.variableName_ or _point\_obj -> variableName_  
  or _this -> variableName_

If inside a function a local variable has the same name with a global variable, then the local variable hides the global. In C++ we can access the global variable using the _scope resolution operator_ _::var,_ access the global _var_ variable.

 **_/\* Example on scope and extent of variables \*/_**  
 _#include \<iostream.h>_  
 _extern double  y;               //  external variable (defined in another file)_  
 _static double x=25.5;      //  static global variable_  
 _void fun(double x);_

 _int main()_  
 _{_  
 _int x=3;                                 // local variable_  
 _fun(x);_  
 _fun(::x);_  
 _fun(x);_  
 _}_

 _static void fun(double x)_  
 _{_  
 _static int s=0;             //  static local variable_  
 _int n=0;                    //  automatic (dynamic local) variable_

 _cout \<\< " n = " \<\< n \<\< "\\t s =" \<\< s_  
 _\<\<  "\\t x = " \<\< x \<\< endl;_  
 _}_

**Output**  
 _n = 0   s =0       x = 3_  
 _n = 0   s =0       x = 25.5_  
 _n = 0   s =0       x = 3_

{{< anchor "6" >}}{{< /anchor >}}

6\. References
--------------

A **_reference_** serves as an alias (i.e. a nickname) for the variable or object with which it has been initialized. A reference is defined using an address-of operator (&) after the data type. References are typically used when a function is called, as an alternative to pointers, in order to be able to work on the actual variables that are used as arguments when calling the function, rather than with their values.

When a parameter of a function is defined to be a reference then that variable is said to be **_passed-by-reference_**, rather than by value. Since all operations on a reference are actually applied to the variable that it refers, the only way to assign a variable to a reference is during its definition, i.e. a reference is assigned a variable to which it refers during its definition. It is also possible to have a reference to a pointer as shown in the following section example.

 e.g:             _double x=15.75, &rx= x;_       //   _rx_ is a reference to a double  
                    _rx += 20;       _                           //   x becomes equal to 35.75

{{< anchor "7" >}}{{< /anchor >}}7\. Pointers
---------------------------------------------

A **_Pointer_** variable is used to hold an memory location address. Every pointer has an associated data type that specifies the data type of the variable, or, in general, object, to which the pointer can point. Since pointers are variables that are used to store addresses of other variables, they must be defined before being used. A pointer is declared as a pointer to a particular type using the _dereference operator_ (\*) between the data type and the name of the pointer. Using the address stored by the pointer, the variable stored in that address can be indirectly manipulated.

e.g.:     _double \*px, \*py, x, z \*pz ;           int  j, \*pj, k ;_

The memory storage allocated for a pointer is the size necessary to hold a memory address (usually an _int_). The address of a variable (i.e. the location in memory where it is stored) can be obtained using the _address-of operator_ (&), e.g. _&x_ gives the address (i.e. the memory location) where the variable (here _x_) is stored. A pointer can be assigned the value 0 or NULL to indicate that it points nowhere. However, it is not allowed to assign to a pointer an address that is used to store a different data type variable.

The address of a variable is stored in a pointer using the address-of operator, by an assignment such as: px =&x;. The value which is stored in an address pointed to by a pointer can be accessed using the _dereference operator_ (\*). The value of a pointer is the address that it points to. Dereferencing a pointer gives the value which is stored at the memory location stored as the value of the pointer.

 e.g.    _double \*px, x;_  
 _px = &x ;_  
 _\*px = 25.5 ;_ // this is equivalent to assigning x=25.5

Pointers can be used in arithmetic, assignment, and comparison expressions. An integral value can be added to, or subtracted from, a pointer. According to the rules of **_pointer arithmetic_**, when adding (or subtracting) a value from a pointer, the new address memory that is assigned to the pointer is equal to the current memory address plus (or minus) the amount of memory required to store that particular data type whose address is stored by the pointer times the value that is added (or subtracted). A pointer can be incremented, decremented, or subtracted from another pointer. However, two pointers cannot be added, and, pointer multiplication and division are not allowed.

A special pointer that can be used to store any type of pointer is called a _pointer-to-void_, and can be defined using the keyword _void_ as the data type. However, no actual manipulation of the contents of the address pointed to by a pointer to void can be performed directly. Since a pointer-to-void does not provide any data type information concerning the data stored in the memory at which it points, an explicit cast is required to specify the data type of the data stored there.

      _double x=10.75, \*px=&x;_  
 _void \*vp = &x;_

 _cout \<\< "\\n x = " \<\< x ;_  
 _cout \<\< "\\n \*px = " \<\< \*px ;_  
 _//  cout \<\< "\\n \*vp = " \<\< \*vp ;_ //    \<-------   Wrong!  
 _cout \<\< "\\n \*vp = " \<\< \*(static\_cast \<double\*>(vp)) ;_ // ok

The following example demonstrates the use of both references and pointers:

 **_/\* Example on references and pointers\*/_**  
 _#include \<iostream.h>_  
 _#include \<stdlib.h>_

 _int main(void)_  
 _{_  
 _int i=5,  &ri = i ;              //  integer and reference to an integer_  
 _double x=24.5, \*px=&x, \*&rpx=px; // double, pointer and a reference to pointer to a double_

 _ri++;_  
 _\*px += 100;_  
 _\*rpx += 1000;_

 _cout \<\< "\\n i = " \<\< i \<\< "\\t ri = " \<\< ri;_  
 _cout \<\< "\\n x = " \<\< x \<\< "\\t \*px = " \<\< \*px_  
 _\<\< "\\t \*rpx = " \<\< \*rpx  \<\< endl;_

 _return EXIT\_SUCCESS;_  
 _}_  
 

**Output**  
 _i = 6   ri = 6_  
 _x = 1124.5      \*px = 1124.5    \*rpx = 1124.5_

{{< anchor "8" >}}{{< /anchor >}}

8\. Function Call by Value, by Reference and Using Pointers
-----------------------------------------------------------

Pointers and references provide ways to overcome the problems associated with the call-by-value. Often we need to change the values of variables within a function call and this is impossible using directly the _call-by-value_ which passes only copies of the values of the provided parameters. These copies are lost upon exiting the function and only one value can be returned by the function. In addition, large user-defined objects are often passed as arguments to a function. In those cases, using _call-by-value_ requires memory allocation and copying of the passing arguments to the corresponding parameters which can be too costly both in computational time and memory space. Finally, in some cases, we may need to return more than one value from a function.

Therefore, in many cases calling a function by-value does not help much. There are two alternative approaches, either using a _call-by-reference_, or sending with _call-by-value_ the address of the objects that we want to pass as arguments and operate on them indirectly using pointers.

We can change variables in the function by passing them by reference in which case the local variables are aliases to the actual variable. To pass an argument by reference we need to declare this by using an _address-of-operator_ (**&**) after the data type of the passing by reference argument. The function is then **_called by reference_**. When an argument is sent by reference, it means that an alias to the argument is used in the function to access the actual variable in the calling function. Then, all changes that take place are actually done on the variable that is used as an argument when the function was invoked. A reference serves as an alias for the object with which the function was called and is initialized once upon entering the function, i.e. a parameter that serves as a reference cannot refer to different variables or objects. In cases where we want to pass a large object, that we do not want to change, by-reference, in order to save the overhead from making a local copy to the function parameter, we can define the reference to be a _const_ so as to prevent any accidental modifications of it.

An alternative way is to use**_pointers_** and pass the _address_ of the variables which allows us to access the variables indirectly and change the values stored at those locations. This is indicated by an **\*** operator after the data type of the argument that is passed as an address, since it is actually a pointer. Using addresses of variables as arguments to functions we can access indirectly and change the values of some variables of the calling function. In addition, memory needs to be allocated only for the pointer and not for the entire object, saving the time and space overhead of copying the arguments to the function parameters. In C++ an array is always passed by a pointer to its first element, i.e. it is never passed by value

The following example demonstrates the use of call by-value, by-reference and using pointers.

 **_/\* Example for call-by-value, call-by-reference and using pointers \*/_**  
 _#include \<iostream.h>_  
 _void fun(double x, double &y, double \*z);_

 _int main()_  
 _{_  
 _double x=11.1, y=22.2, z=33.3;_  
 _fun(x,y,&z);_  
 _cout \<\< "\\n x = " \<\< x \<\< "\\t y = "_  
 _\<\< y \<\< "\\t z = " \<\< z \<\< endl;_  
 _}_

 _void fun(double x, double &y, double \*z)_  
 _{_  
 _x \*= 2;_  
 _y \*= 2;        // using call by reference_  
 _\*z \*= 2;       // using pointer to access the actual variable_  
 _cout \<\< "\\n x = " \<\< x \<\< "\\t y = " \<\< y \<\< "\\t z = " \<\< \*z \<\< endl;_  
 _}_

**Output**  
 _x = 22.2        y = 44.4        z = 66.6_  
 _x = 11.1        y = 44.4        z = 66.6_

{{< anchor "9" >}}{{< /anchor >}}

9\. Pointers to Functions
-------------------------

The name of a function is actually the address of the function in memory. A pointer to a function can be used as an argument to a function to allow us to selectively invoke one out of several different functions, depending on the name of the function we use as argument. To use a pointer to a function we need to declare it in the declaration and definition of the function, i.e. specify that the function accepts as an argument a pointer to another function. A pointer to function is defined using the function’s type, which consists of its return type and parameter list. For example, the following declaration declares that the function _fun()_ has 3 arguments: an _int_, a pointer to a function that itself returns a _double_ and has a _float_ and an _int_ as arguments, and a _float_.

 _double fun(int i, double (\*f) (double, int), float);_

A function name, in general, gives a pointer to that function, although an address-of-operator can also be used to get (explicitly) the same. A pointer to a function can also be initialized, or assigned a value. When calling the function to which the pointer points to, the pointer’s name, either by itself or dereferenced, can be used.

An example of a pointer to a function is presented below. The function _compute()_ has 3 arguments: a pointer to a function, and 2 integers. The name of any function that returns a _double_ and has two doubles as arguments can be provided in the function call of _compute()_. The provided function is then used inside the _compute()_ function whenever _f()_ is used.

 **/_\* Example of Pointers to functions \*/_**  
 _#include \<iostream.h>   // pointers to a functions_  
 _double adding(double x, double y);_  
 _double subtracting(double x, double y);_  
 _double compute(double (\*f)(double,double), int i, int j);_

 _int main()_  
 _{_  
 _int x=7, y=3;_  
 _cout \<\< "\\n compute(adding,x,y) = " \<\< compute(adding,x,y) \<\< endl;_  
 _cout \<\< " compute(subtracting,x,y) = "_  
 _\<\<  compute(subtracting,x,y) \<\< endl;_  
 _}_

 _double  compute(double (\*f)(double,double), int i, int j)_  
 _{_  
 _return f(0.5\*i,j);            // The following is equally valid:  return (\*f)(0.5\*i,j);_  
 _}_

 _double adding(double x, double y)_  
 _{_  
 _return x+y;_  
 _}_

 _double subtracting(double x, double y)_  
 _{_  
 _return x-y;_  
 _}_

**Output**  
 _compute(adding,x,y) = 6.5_  
 _compute(subtracting,x,y) = 0.5_

{{< anchor "10" >}}{{< /anchor >}}

10\. 1-D Arrays
---------------

An array is used to store a set of values, or objects, of the same (either built-in or user- defined) data type, in one entity. An individual element of the array, i.e. a member of this set, can be accessed using the array’s name and an index which should be a value, or an expression, of integral type. The individual objects of an array are accessed by their position in the array using indexing with the index beginning from 0. Therefore, the last element of an n-size array has index equal to n-1. An array is defined using a pair of square brackets as shown below:

 _\<data\_type> \<array\_name> \[size\];_

The dimension of the array, at the array definition, must be a constant expression, i.e. to be known during compilation, except in the case in which all elements of the array are explicitly initialized at the definition. If less elements of an array are initialized, according to the provided size during definition, the remaining elements are initialized to zero, e.g.:

 _double x\[5\];_                 // an array of 5 doubles is defined  
 _int y\[\]={ 3 , 56,  4, 6 };_        // an array of 4 int  
 _float z\[6\] = { 0. };_                // all 6 float members are set to 0.  
 _int h\[7\]={ 13 , 26,  42 };_ // an array of 4 int

When an array is defined, the appropriate amount of consecutive memory is allocated. Memory is also allocated for a constant pointer that is associated with the name of the array and which stores the beginning address of the memory allocated for the array. Therefore, the array name is itself a constant pointer that stores the address of the first element of the array, i.e. the address of memory where the first element is stored, e.g. _x_ is equal to _&x\[0\]_. The name of an array is a constant pointer because it cannot be assigned a different address. Since the name of an array is a pointer, an individual element of an array can be alternatively accessed using pointer arithmetic, instead of using the index notation. In essence, the index notation _mat\[i\]_ is equivalent to _\*(mat+i)_.

You should be particularly careful not to exceed the range of an array since the compiler does not make such checks. However, in most cases memory is wasted when using arrays since we often allocate much more memory that we will probably ever need. Dynamic memory allocation can be used to avoid this waste of memory by allocating dynamically during execution the exact required memory, e.g.:

  _double x\[5\];_  
 _x\[0\]= 5;_  
 _x\[3\] = x\[0\]+23;_

{{< resource "493f266f-14df-0799-423b-0acc9c93027d" >}}

 **_/\* Example on references, pointers and arrays \*/_**

 _#include \<iostream.h>_  
 _#include \<stdio.h>_

 _main()_  
 _{_  
 _double x=11.1 , \*px;_  
 _double &rx = x;_

 _cout \<\< "\\n x = " \<\< x \<\< endl;_  
 _cout \<\< " rx = " \<\< rx \<\< endl;_

 _rx = 33.3;_  
 _cout \<\< "\\n x = " \<\< x \<\< endl;_  
 _cout \<\< " rx = " \<\< rx \<\< endl;_

 _px = &x;_

 _ios::sync\_with\_stdio();_  
 _printf( "\\n px = %p \\n" , px );_  
 _ios::sync\_with\_stdio();_  
 _cout \<\< " \*px = " \<\< \*px \<\< endl;_

 _\*px = 44.4;_  
 _cout \<\< "\\n x = " \<\< x \<\< endl;_  
 _cout \<\< " \*px = " \<\< \*px \<\< endl;_

 _double mat\[\] = { 10 , 20 , 30};_  
 _px = mat ;_  
 _cout \<\< "\\n mat\[0\] = " \<\< mat\[0\] \<\< endl;_  
 _cout \<\< "\\n px = " \<\< \*px++ \<\< endl;_  
 _cout \<\< " px = " \<\< \*px \<\< endl;_  
 _cout \<\< "\\n px\[1\] = \*(px+1) = " \<\< \*(px+1) \<\< endl;_  
 _cout \<\< " mat\[2\] = \*(mat+2) = " \<\< \*(mat+2) \<\< endl;_  
 _}_

**Output**  
 _x = 11.1_  
 _rx = 11.1_

 _x = 33.3_  
 _rx = 33.3_

 _px = 7fffae20_  
 _\*px = 33.3_

 _x = 44.4_  
_\*px = 44.4_

 _mat\[0\] = 10_  
 _px = 10_  
 _px = 20_

 _px\[1\] = \*(px+1) = 30_  
 _mat\[2\] = \*(mat+2) = 30_

{{< anchor "11" >}}{{< /anchor >}}

11\. Strings as Arrays of char
------------------------------

In C++ there are two string representations: the traditional way of an array of characters, and, the newer standard C++ string class. For now, we consider the former string representation.

The string is stored as an array of _char_ with a special character at the end **’\\0’**, which is called the _terminator character_, since it is used to indicate the end of the string. Therefore, memory space for an extra character must be provided to be able to store the terminator character.

Several library functions that can be used to manipulate strings are provided by the Standard C-library. To use them, the cstring header file, which contains their declarations, must first be included. The most commonly used are the following:

_strcpy(char str1\[\] , char str2\[\])_: **strcpy** copies the contents of _str2_ (including the terminator character) into str1

 _strcmp(char str1\[\] , char str2\[\])_: **strcmp** compares the two strings alphabetically, returning zero if they are exactly the same, otherwise a nonzero value

 _strlen(char str1\[\])_: **strlen** counts the number of characters in the string (not including the terminator character)

Although an array of strings can be initialized using the string notation (i.e. a literal enclosed in double quotes), it is not possible to assign a string to an array of char after its definition. A C-standard library need to be used to make this copying, e.g.:

 _char s1\[\] = "MIT" , char s2\[4\] ;_  
 _strcpy (s2,"MIT");_  
 _char str3\[\] = { ‘M‘ , ‘I‘ , ‘T‘ , ‘\\0‘ };_

The following example demonstrates how a string can be defined, initialized or assigned a literal string, how can be modified, etc.

 **_/\* Example for strings as arrays of char \*/_**  
 _#include \<iostream.h>_  
 _#include \<cstring>_

 _int main(void)_  
 _{_  
 _char str1\[\] = "test" ;_  
 _const char \*str2 = "Test" ;_  
 _char str3\[50\] ;_  
 

 _cout \<\< "str1 and str2 are " ;_  
 _strcmp(str1,str2) ? cout \<\< "different" \<\< endl : cout \<\< "the same" \<\< endl;_

 _cout \<\< "\\n str1 = " \<\< str1 \<\< endl ;_  
 _cout \<\< " str2 = " \<\< str2 \<\< endl ;_

 _strcpy(str3,str1);_  
 _strcat(str3,str2);_

 _cout \<\< "\\n str3 = " \<\< str3 \<\< endl ;_  
 _str3\[0\] = 'T';_  
 _cout \<\< " str3 = " \<\< str3 \<\< "\\t length = "_  
 _\<\< strlen(str3) \<\< endl ;_  
 _return 1;_  
 _}_  
 

**_Output_**

_str1 and str2 are different_

 _str1 = test_  
 _str2 = Test_

 _str3 = testTest_  
 _str3 = TestTest         length = 8_

{{< anchor "12" >}}{{< /anchor >}}

12\. Arrays of Pointers
-----------------------

Since pointers are variables we can have arrays of pointers. Such arrays are often used to store the location in memory of a collection of data with the same type. Each element of an array of pointers is a pointer which can be used to point to a memory location.

   e.g.:     _double \*pd\[100\]; _     //   _pd_ is an array of 100 pointers to doubles  
              _char \*pc\[20\]; _           //   _pc_ is an array of 100 pointers to char

{{< anchor "13" >}}{{< /anchor >}}13\. 2-D and Higher Dimensions Arrays
-----------------------------------------------------------------------

Multidimensional arrays (of any dimension) can be defined using additional brackets, one for each dimension. A multidimensional array can be initialized similarly to a 1-D array, with the option to use nested curly braces to group the data along the different dimensions (e.g. rows).

> _double mat2\[6\]\[3\];_  
> _double mat3\[5\]\[3\]\[2\];_  
> _double m\[\]\[\] = { {3 , 6.2 , 0.5} , { 23.7 , 0.75 , 4.8 } };_  
> _double m\[3\]\[10\] = { {4.5} , {13.7} };_

Although it is natural to think a 2-D array having a rectangular 2-D form, the elements of arrays (of any dimension) in C++ are actually stored in a contiguous memory location. The following graph shows how a 2-D array is stored. The top graph shows the virtual representation of a 2-D array, while the bottom one shows how actually it is stored in memory:

{{< resource "aa95256f-9d16-3e59-da6d-6ae0f9e6d010" >}}

Therefore, the following expressions are exactly equivalent to **m\[i\]\[j\]**:

>  **\*(m\[i\]+j)**  
> **(\*(m+i))\[j\]**  
> **\*((\*(m+i))+j)**  
> **\*(&m\[0\]\[0\]+WIDTH\_SIZE\*i+j)**

> **_/\* Example for 2-D arrays \*/_**  
> _#include \<iostream.h>_  
> _#include \<stdlib.h>_  
> _#include \<iomanip.h>_  
> _#define ROW\_SIZE 4_  
> _#define COL\_SIZE 7_
> 
> > _int main()_  
> > _{_  
> >  _double m\[ROW\_SIZE\]\[COL\_SIZE\] = { { 4.5 , 0.45 } ,_  
> >  _{ 13.7 , 67.3 , 17.7 } , { 2.6 } };_  
> >  _int i,j;_
> > 
> >  _for(i=0;i\<ROW\_SIZE;i++)_  
> >  _{_  
> >  _cout \<\< endl;_  
> >  _for(j=0;j\<COL\_SIZE;j++)_  
> >  _cout \<\< "  " \<\< setw(5) \<\< m\[i\]\[j\];_  
> >  _}_  
> >  _return EXIT\_SUCCESS;_  
> > _}_  
> >    
> >    
> >  

**Output  
**  
 _4.5     0.45   0      0      0      0      0_  
 _13.7   67.3   17.7  0      0      0      0_  
 _2.6      0      0      0      0      0      0_  
 _0      0      0      0      0      0      0_

{{< anchor "14" >}}{{< /anchor >}}

14\. Return by Reference Functions
----------------------------------

A function can either return nothing, in which case it is declared as _void_ and a return statement is optional, or return a value. In the latter case the default is to return a value by-value, i.e. a copy of the value that is returned is passed to the function from where the terminating function was called. However, there are some cases that it is preferable to _return a value by-reference,_ or using pointers. For example, it may be useful to return a reference to an object or variable so as to be able to manipulate it, or it may be more efficient to pass by reference, or using a pointer, a large user-defined object to avoid the overhead due to copying it.

When a function _returns by-reference_, i.e. returns a reference to a variable or object, the function call can be placed in the LHS of an assignment statement. However, a variable, or object, with local scope cannot be returned by-reference, since the memory allocated for it is released upon exiting the function.

The following example shows one such a case, in which a reference to a specific element of an array is returned.

> **_/\* Example on return by reference \*/_**  
> _double & fun(int i, double \*x);_  
> _void main(void);_
> 
> _void main(void)_  
> _{_  
>  _double x\[10\]={0};_  
>  _fun(3,x) = 57.6;_  
>  _cout \<\< "\\n x\[5\] = " \<\< x\[5\] \<\< endl;_  
>  _cout \<\< "x\[6\] = " \<\< x\[6\] \<\< endl;_  
> _}_

> _double & fun(int i, double \*x)_  
> _{_  
>  _return x\[2\*i\];_  
> _}_

  
**Output  
**  
 _x\[5\] = 0_  
 _x\[6\] = 57.6_

{{< anchor "15" >}}{{< /anchor >}}

15\. Dynamic Memory Allocation
------------------------------

Memory can be obtained dynamically from the system, in particular from a pool of free memory named the free store (or heap), after the program has been compiled, i.e. during execution, using the **_new_** operator. This operator can be used to allocate sufficient memory for one or more variables of any data type (standard or user-defined), i.e. for a single variable, or object, or an array of variables, or objects.

Memory is allocated dynamically using the operator **_new_** followed by a type specifier and in the case of an array followed by the array size inside brackets. In the case of a single variable an initial value can also be provided within parentheses. The new expression returns the address of the beginning of the allocated memory and can be stored in a pointer in order to access that memory indirectly. If the dynamic memory allocation is not successful a NULL (i.e. a 0 value) is returned by the operator _new_. The following statements allocate memory for one _float_ and an _int_, and the address of that memory location is returned and then assigned to the pointer _pf_ and _pi_, respectively. Dynamically allocated memory, if not explicitly initialized, is uninitialized with random contents.

 _float \*pf = new float;_ // allocate memory for a float  
 _int \*pi = new int(37);_ // allocate memory for an int and assign an initial value to it

Similarly, the following statement allocates contiguous memory for a _size_ number of doubles and then the address of the beginning of that memory is returned and assigned to the pointer pd. The size does not have to be a constant, i.e. known at compilation, but can be specified during execution of the program according to the program demands. However, there is no way to initialize the members of a dynamically allocated array.

 _double \*pd = new double\[size\];_

In contrast, to allocate memory for an array of doubles the size must be known prior to compilation, i.e. the size should be a constant. In the following definition of an array the name of the array is a constant pointer, since it cannot point anywhere else, while in the previous example _pd_ can be used to store any memory address where a double is stored.

 _double mat\[50\];_

Multidimensional arrays can also be dynamically allocated using a _new_ expression. However, only the left-most dimension can be specified at run-time. The other dimensions need to be defined at compilation time, i.e. to have a constant size, e.g.:

    _double (\*pmat)\[100\] = new double \[size\]\[100\];    _ // _size_ does not need to be a constant

The allocation and release of memory for variables for which memory is statically allocated is done automatically by the compiler. Memory of local variables is automatically released upon exiting the function, unless they are defined as static, and that memory can be used for other purposes. However, dynamically allocated memory is not released upon exiting a function and care must be taken to avoid losing the address of that memory, resulting in a **_memory leak_**. **Dynamic allocation and deallocation of memory is a programer's responsibility.** When memory that is allocated dynamically is not needed any more, it should be released using the **_delete_** operator as shown in the following example which is based on the previous one:

> _delete ps;_  
> _delete \[\] pd;_

The brackets are required when the pointer points to consecutive memory of a dynamically allocated array, in order to release all memory that has been allocated earlier. Only memory that has been dynamically allocated (i.e. using the new operator) can be released using the _delete_ operator.

Its a good practice to set the value of a dangling pointer, a pointer that refers to invalid memory, such as a pointer that was used to point to a released memory, to NULL (or 0). Then, we avoid the error of trying to read or write to an already released memory location. However, it is not wrong to apply the _delete_ expression to a pointer that is set to 0, because a test is performed before actually applying the delete operator on the pointer. Therefore, there is no reason to check whether the pointer is set to 0. The delete operator should not be applied twice to the same memory location, e.g. by mistake when having two pointers store the same memory location, because it may lead to corruption of data that have already been stored after the first release of the memory.

If the available memory from the program's free store is exhausted, than an exception is thrown, and as we'll see later there are ways to rationally handle such exceptions.

{{< anchor "16" >}}{{< /anchor >}}16\. The sizeof Operator
----------------------------------------------------------

The **_sizeof_** operator gives the size in bytes of a variable, a built-in data type, or a user-defined data structure, or a class, it can be used to determine the number of bytes that are required to store a certain object.  
  
  e.g:  
 _int i, mat\[10\];   double d;_      //  On an athena SGI or SUN workstation:  
  _sizeof(char);_                         //   returns 1 (byte)  
         _sizeof(int);  sizeof i;   _              //   returns 4 (bytes)  
         _sizeof d ;  _                               //   returns 4  
 _sizeof mat;_                        //   returns 40

{{< anchor "17" >}}{{< /anchor >}}

17\. Data Structures
--------------------

A **_data_** **_structure_** is very similar to a class and it is not often used in C++, since more features are provided by a class. A structure can be used to store as a single entity several different variables not necessarily of the same data type. Structures in C++ have some extra features from the structures in C, such as access restriction capabilities, member functions and operator overloading.

A data structure is defined using the keyword _struct_, followed by the name of the structure and then its body where it is defined. Then, to define an instance of the data structure we can use its name directly (the _struct_ keyword is not required as in C). To access a member of a data structure the dot or the arrow operator are used depending on whether we have the actual data structure instance or a pointer to it.

Structures can be passed to a function as any other variable, i.e. by value, by reference, or, using pointers. Because data structures are large in size, pass by value is typically not preferred, in order to avoid the copy overhead.

> **_/\* Example on data structures \*/_**  
> _struct point_  
> _{_  
>  _double x;_  
>  _double y;_  
> _};_  
> _typedef struct point Point;  // the typedef is not necessary in C++_
> 
> _int main()_  
> _{_  
>  _Point p;          //  p is a data structure point_  
>  _point \*pp;               // pp is pointer to a  point data structure_
> 
>  _p.x = 3.2;                // using the dot operator_  
>  _pp = &p;_  
>  _pp -> y = 7.5;            // using the arrow operator_
> 
>  _cout \<\< "\\n x = " \<\< pp->x \<\< "\\t y = " \<\< (&p) -> y \<\< endl;_  
>  _struct point p2 = {4.7 , 9.2};    //   A data structure instance can be intialized using_  
>  _pp = &p2;                             // comma separated values enclosed in curly braces_  
>  _cout \<\< " x = " \<\< pp->x \<\<  " y = " \<\< p2. y \<\< endl;_  
> _}_

**Output  
**  
 _x = 3.2         y = 7.5_  
 _x = 4.7         y = 9.2_

**Note:** The _typedef_ allow us to assign a name for a specific data type, built-in or user defined, and then, use it as a type specifier. In the above example, _struct point p_ and _Point p_ are exactly equivalent, since the following _typedef_ has been defined: _typedef struct point Point;_ The _typedef_ keyword is followed by a data type and an identifier that we want to specify as alias to that data type.

{{< anchor "18" >}}{{< /anchor >}}

18\. Introduction to Classes and Objects
----------------------------------------

A **_class_** is a user defined specification that encapsulates in a single entity both data and functions that can operate on them. An object is an instance of a class and the class/object relation is similar to the built-in data type/variable relation.

A class is defined using the keyword _class_ followed by the name of the class. A class typically has**_data members_**, which contain the data that is stored using the class; **_member functions_**, which are functions that operate on these data; **_constructors_**, that are member functions with a name the same as the class name and are executed upon a creation of an instance of the class in order to make the proper initialization; **_destructors_**, that are used when an instance of a class goes out of scope; and many other features such as operator**_overloading_**, declarations of **_friend functions_**, etc.

The following simple example demonstrates the use of a _Point_ class with some of the most basic features of a class.

> **_/\* Example on  classes and objects \*/_**  
> _class Point_  
> _{_  
> _private:_  
>  _double x,y;_
> 
> _public:_  
>  _Point();_  
>  _Point(double x, double y);_  
>  _void print();_  
> _};_
> 
> _Point::Point()_  
> _{_  
>  _cout \<\< " In   Point() default constructor " \<\< endl ;_  
>  _x = 0.0 ;_  
>  _y = 0.0 ;_  
> _}_
> 
> _Point::Point(double xx, double yy)_  
> _{_  
>  _cout \<\< " In   Point(double,double)  constructor " \<\< endl ;_  
>  _x = xx ;_  
>  _y = yy ;_  
> _}_
> 
> _void Point::print()_  
> _{_  
>  _cout \<\< " (x,y) = (" \<\< x \<\< "," \<\< y \<\< ")"  ;_  
> _}_  
>  
> 
> _int main ( )_  
> _{_
> 
>  _Point p1;_  
>  _Point p2(17,45.75);_
> 
>  _cout \<\< "\\n Point P1: " ;_  
>  _p1.print();_
> 
>  _cout \<\< "\\n Point P2: " ;_  
>  _p2.print();_
> 
>  _return EXIT\_SUCCESS ;_  
> _}_

  
**Output  
**  
 _In   Point() default constructor_  
 _In   Point(double,double)  constructor_

 _Point P1:  (x,y) = (0,0)_  
 _Point P2:  (x,y) = (17,45.75)_