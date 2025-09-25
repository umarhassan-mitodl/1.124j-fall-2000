---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 4
uid: 1576744a-2518-3f40-7d8f-37045356d09c
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).
------------------------------------------------------------------------------

Topics
------

1.  [Inheritance: public, protected and private derivation](#1)
2.  [Multiple inheritance](#2)
3.  [Inheritance: constructors and destructors](#3) 
4.  [Inheritance: redefining member functions](#4) 
5.  [Virtual functions and polymorphism](#5)
6.  [Abstract classes](#6)
7.  [File streams](#7)

Appendix: Extra Material
------------------------

1.  [Namespaces](#A1_Namespaces) 
2.  [Assertions](#A2_Assertions) 
3.  [C++ standard library string class](#A3_C_Standard_Library_string_class)
4.  [Other topics](#A4)

{{< anchor "1" >}}{{< /anchor >}}1\. Inheritance: Public, Protected and Private Derivation
------------------------------------------------------------------------------------------

**_Inheritance_** is the ability to create a new class, called _derived class_, from an existing one, called _base class_. The derived class is also called _subclass_ of the base class, which in turn is called _superclass_ of the derived class. A derived class inherits all the data members and member functions of its superclasses, and, in general, it implements an **_is-a_** relationship. In contrast, a **_has-a_** relationship is implemented using a class object as a member of another class. New members can be defined in the derived class refining the definitions of its superclasses. Inheritance can be used to extend the capabilities of a base class. Classes can be derived by classes that are themselves derived and this process can be extended to an arbitrary number of levels of inheritance.

An object inherits data members and member functions from the superclass  of its class, and from all superclasses of that class. Member functions  of a derived class can only access members of its base class that are declared  in the _public_ or _protected_ part, i.e. _private_ members cannot be accessed. The derived class methods invoked by a derived class object can access only the protected members that have been inherited from the base class of the particular object that invoked the member function (i.e. \*_this_), or any other object of the derived class. The derived class member functions have also access to all _private_ and _protected_, as well as _public_ of course, members of its own class.

The derived member functions and data of a derived class object, can be accessed directly as if they were members of the derived class and not of the base class, as long as access is permitted. However, if the same name is used for both a member of the base class and a member of the derived class, the member of the derived class hides the corresponding member of the base class. By using the class scope resolution operator, the base class member, instead of the derived one, can be explicitly accessed. If the base class has a _static member data_ then there will be only one instance of that regardless of how many subclasses have been derived from the base class and how many objects have been created.

To specify the base class of a derived class a colon is used after the name of the class, at its definition, followed by a specifier that defines the type of inheritance and the name of the superclass. The expression after the colon, which is used to specify the inheritance, is called class **_derivation list_**. To define a subclass using _public_ derivation the keyword _public_ should be used. In addition to public derivations, we can use _protected_ and _private_ class derivations. The following example shows a public derivation of a class.

> _class derivedClassName :  public  baseClassName_ _{_ _    ..........._ _};_

The colon (:) specifies that the _derivedClassName_ class is derived from the _baseClassName_ class. The derived class inherits the member variables and functions of the class from which it is derived, as well as the member variables and functions of all superclasses of that class. 

The access to specific member variables and functions of the superclasses of a class are specified according to the location where they have been defined (i.e. in which section of the class definition) in those superclasses, and the way that the subclasses are derived, i.e. which of the keywords _public_, _protected_, and _private_ has been used during the derivations. The access to members of a superclass and the "cost" of that access do not depend on the depth of the inheritance tree.

With a **_public derivation_** of a subclass all member variables and functions of the superclass retain their status in the derived subclass, i.e. a public member remains public allowing (unlimited) access to everyone.

Using a **_private derivation_**, all public and protected members of the superclass become private in the derived class, i.e. a public member of the superclass within the derived class can only be accessed by the members of the derived class.

Finally, with **_protected derivation_** all the public parts of the superclass become protected in the derived class. A protected member data, or function, can be accessed only by member functions of the class and certain subclasses of the class, or by friend functions.

Therefore, when deriving a subclass we can reduce the access privileges using private or protected derivation. The access specifier (_public_, _protected_, and _private_) defines the type of access of the members inherited by the derived class from its base class. The access is specified based on which part (_public_, _protected_, and _private_) the declaration of a member data and function is declared. The _protected_ part is used to allow access to the members declared in there only to members of that class and any subclasses.

The derived class has no access to the _private_ members of the base class unless it is declared to be a friend of the base class. Note that friendship is not inherited, i.e. a subclass of a derived class that has been declared a friend of its own base class, is not considered a friend of its base class superclass. Friendship must be explicitly granted from each class to all classes that should have access privileges to that class.

The access level to a member that is inherited from a superclass can be adjusted to the access it has in the superclass, instead of following the rules based on the keyword used in the subclass derivation, by declaring the member in the _public_, or _protected_, access section accordingly using the name of the superclass followed by the class scope resolution operator and the name of the member. However, any attempt to change the access status of a base class member is invalid.

**_/\* Example on public, protected and private derivation \*/_**

> _class Point_ _{_ _private:_ _  double x;_ _protected:_ _  double y;_ _public:_ _  double z;_ _  Point(double,double,double);_ _ };_
> 
> > _Point::Point(double xx=0, double yy=0, double zz=0)_ _{_ _   x = xx ;    y = yy ;    z=zz;_ _}_
> > 
> >   // Alternative derivations _  class Voxel : public Point                         _   // all members retain their status                                                                    // in the derived class _//class Voxel : protected Point                _ // public members become protected                                                               // in the derived class _//class Voxel : private Point        _ // all members become private in the derived class _{_ _private:_ _  int color;_
> > 
> > _public:_ _  Point::z; _                    // e.g. declared in the public section to                                    // adjust the access of z to public _  Voxel(double x, double y, double z, int col);_ _  void print();_ _};_
> > 
> > _Voxel::Voxel()_ _{_ _   color=0;_ _}_
> > 
> > _Voxel::Voxel(double x=0, double y=0, double z=0, int col) : Point(x,y,z)_ _{_ _   color = col;_ _}_
> > 
> > _void Voxel::print()_ _{                                 _ //  x is always not accessible since x is private _   cout \<\< y ;            _ // Accessible but if the derivation is private it                                    // becomes private in the derived class _   cout \<\<  z ;               _ //  Accessible but it becomes whatever is                                      // the derivation in the derived class _}_
> > 
> > _void main()_ _{_ _                Voxel v(4,7,2,101110101);_ _                v.print();_ _}_

{{< anchor "2" >}}{{< /anchor >}}2\. Multiple Inheritance
---------------------------------------------------------

A class may inherit the member variables and functions from more than one superclasses, i.e. a derived class may have multiple base classes. Then, all superclasses are defined after the colon separated by commas and with the indication of the type of derivation the should be used, i.e. one of the access specifiers: _public_, _protected_, or _private_. There is no limit on the number of the base classes that a derived class inherits from. The base class constructors are invoked in the order that appear in the class derivation list, while the destructors are invoked in the reverse order.

**_/\* Example: on multiple inheritance \*/_**

> _class People_ _{_ _ public:_ _   char first\_name\[20\];_ _   char last\_name\[20\];_ _   int age;_ _};_
> 
> > > _class Student : **public** People_ _{_ _  public:_ _   int student\_id;_ _};_
> > > 
> > > _class Staff_ _{_ _  private:_ _   int social\_sec\_num;_ _};_
> > > 
> > > _class Faculty : **public** People, **protected** Staff_ _{_ _ private:_ _   int num\_papers;_ _....._ _};_

If  a member function is hidden by another member function we  can explicitly specify which one we want to be used by putting the name  of the class and two colons in front of the name of the member function.

> _className::functionName(...)_

{{< anchor "3" >}}{{< /anchor >}}3\. Inheritance: Constructors and Destructors
------------------------------------------------------------------------------

Although a derived class inherits the member data and functions of its base class, the constructors of the base class are not inherited. Therefore, the derived class needs to provide its own constructors which are called after the base class and member object constructors are called. When a derived class object is created, first a _base class constructor_ is automatically invoked, typically to initialize the member data that correspond to the base class, and then the _derived class constructor_ is called to initialize the additional data members of the derived class. The constructors of the superclasses/subclasses chain are executed in a _top-down order_, i.e. a base class constructor, if executed, is executed prior to the derived class construction.

A new set of constructors is typically provided for a derived class to make the proper initialization and, if necessary, call the proper superclass constructor with certain arguments. The derived class constructor is used to initialize the members that have been added by the derived class, while the superclass constructor(s) should take care of the corresponding classes data members.

A specific constructor of a superclass can be invoked by providing after the header of the constructor definition a colon followed by the name of the superclass (i.e. the constructor name) and the desired arguments with which it is to be called. This is called**_member initialization list_** and it can be used to pass arguments to the constructor of the base class. The order of the comma separated member initialization list does not affect the order of construction invocation. The order in which the constructors are invoked is: first, the base class constructor is called and in case of multiple inheritance the order is according to the order that has been used in the class derivation list. Next the constructors of member objects are called in the order in which the members have been defined in the derived class definition. Finally, the derived class constructor is called. A derived class constructor can invoke a constructor only of its direct superclass.

If the derived class has constructors but the base class has not, then the proper derived class constructor is called every time a derived class object is defined.

In the opposite case, i.e. the derived class having no constructors while the base class has, the base class must have a default constructor which is automatically invoked whenever a derived class object is defined.

A derived class constructor needs to explicitly invoke one of the base class constructors, if the base class has constructors but not a default constructor, i.e. a derived class constructor must explicitly invoke one of the base class’ constructors in its header. Alternatively, a default constructor can be provided for the base class. Then, if no base class constructor is explicitly invoked, the default constructor is automatically invoked whenever an object of the derived class is defined.

If a class is used as a base class only to be able to define the subclasses and there is no intention to have objects of that class, the constructors of the base class can be defined as protected, which restricts their access to the derived class (constructors). A class that has no actual objects, instances of itself, is called an **_abstract base class_**.

The following example demonstrates how the constructors of the class and its superclass are invoked and how a specific constructor of a superclass can be explicitly called with certain arguments.

**_/\* Example on constructors calling other constructors \*/_**

> _class Point_ _{_ _private:_ _    double x, y;_ _public:_ _  Point();_ _  Point(double,double);_ _ };_
> 
> _Point::Point()_ _{_ _   x = 0 ;   y = 0 ;_ _}_
> 
> _Point::Point(double xx, double yy)_ _{_ _   x = xx ;   y = yy ;_ _}_
> 
> _class Pixel : public Point_ _{_ _private:_ _  int color;_ _public:_ _  Pixel();_ _  Pixel(double x, double y, int col);_ _};_
> 
> _Pixel::Pixel()_ _{_ _  color=0;_ _}_
> 
> _Pixel::Pixel(double x, double y, int col) : Point(x,y)_ _{_ _  color = col;_ _}_
> 
> _void main ( )_ _{_ _  Point p(1.7,7.2);             _ //  The Point::Point(double xx=0, double yy=0)                                             // is called with (1.7,7.2)
> 
>  _Pixel px1;_ //  The default constructors, Point::Point()                                          // and then  Pixel::Pixel(), are called
> 
>  _Pixel px2(2.75, 8.23, 111000101);_                        // The Point::Point(double xx, double yy) constructor and then                        // the Pixel::Pixel(double x, double y, int col) are called }

In the above example the expression: _Point(x,y)_ after the parameters in the header of the Pixel constructor causes the invocation of a specific constructor of the class _Point_.

Similarly, the derived class, member object class and base class **_destructors_** are invoked as soon as the lifetime of an object (of the derived class) reaches its end. In contrast to the constructors that are invoked in a top-down order starting from the base class first, the destructors are called in the _reverse order_, invoking first the derived class destructor, and then, its member objects constructors, and, finally, the superclass constructor, etc. In addition, although constructors may not be virtual, destructors may be virtual allowing the invocation of the destructor of the class derived for the object pointed to by a pointer (of base class data type). The reverse order is used so as to ensure that the most recently allocated memory is the first to be released.

{{< anchor "4" >}}{{< /anchor >}}4\. Inheritance: Redefining Member Functions
-----------------------------------------------------------------------------

A member function of a superclass can be redefined (with the same name) in a subclass and, depending on which object invokes it, the corresponding one is invoked. When an object of the derived class is used to invoke a function, the search to find the member function starts from the derived class definition, which results in invocation of the derived class member function if it is available, unless a class scope resolution operator is used to explicitly specify whose class the member function should be called. A specific member function of a superclass can be called by using the name of the superclass followed by the class scope resolution operator before the name of the class to be invoked, since the member of the derived class hides the inherited member. The invocation, i.e. the explicit call of a member function of a superclass, can also be achieved from inside the body of the member function of the subclass. i.e. if the member function of a superclass is hidden by a member function of the subclass, the class scope resolution operator can be used to explicitly specify whose class the member function should be invoked.

The member functions of any superclass and subclass can be _overloaded_ as any other set of functions in a certain scope. Note that the member functions of a base class and the member functions of its derived class do not all together make up a set of overloaded member functions, because the former are considered to be in the base class scope, while the latter in the derived class scope.

The previous example has been extended, as shown below, to show how to explicitly call a superclass member function.

**_/\* Example on redefining and invoking member functions \*/_**

> _class Point_ _{_ _private:_ _    double x, y;_ _public:_ _  Point();_ _  Point(double,double);_ _  void **print**();_ _};_
> 
> _Point::Point()_ _{_ _  x = 0 ;   y = 0 ;_ _}_
> 
> _Point::Point(double xx, double yy)_ _{_ _  x = xx ;   y = yy ;_ _}_
> 
> _void Point::print()_ _{_ _  cout \<\< " (x,y) = (" \<\< x \<\< "," \<\< y \<\< ")  "  ;_ _}_
> 
> _class Pixel : public Point_ _{_ _private:_ _  int color;_ _public:_ _  Pixel();_ _  Pixel(double x, double y, int col);_ _  void print();_ _};_
> 
> _Pixel::Pixel()_ _{_ _  color=0;_ _}_
> 
> _Pixel::Pixel(double x, double y, int col) : Point(x,y)_ _{_ _  color = col;_ _}_
> 
> _void Pixel::print()_ _{_ _  this -> Point::print();         _           // the member function print()                                                       // of class Point is called _  cout \<\< " color = " \<\< color;_ _}_
> 
> _int main ( )_ _{_ _  Pixel px1;_ _  cout \<\< "\\n Pixel px1:" ;_ _  px1**.print();  **                                _   // the member function print()                                                        // of class Pixel is called _  cout \<\< endl;_
> 
>  _Pixel px2(2.75, 8.23, 111000101);_ _  cout \<\< " Pixel px2:" ;_ _  px2.**Point::print();    **                   _     // the member function print()                                                         // of class Point is called
> 
>  _cout \<\< endl;_ _  return EXIT\_SUCCESS;_ _}_
> 
> Output
> ------
> 
>  _Pixel px1: (x,y) = (0,0)   color = 0_ _ Pixel px2: (x,y) = (2.75,8.23)_

{{< anchor "5" >}}{{< /anchor >}}5\. Virtual Functions and Polymorphism
-----------------------------------------------------------------------

**Virtual functions** allow dynamic (or late) binding, which means that the selection of which function to call is done during execution, rather than during compilation. This provides the flexibility to perform the same kind of action on different types of objects as long as they are all instances of classes of or derived from, a superclass whoce function  is defined as **virtual**. The selection of which of the virtual functions to invoke is done at run-time. In contrast the resolution of a non-virtual function is done by the compiler during compilation and the process is called static binding. A non-virtual member function is invoked using implicitly the pointer this which is of a certain data type. If a pointer to a base class object is used to invoke the function, even if the pointer stores the address of a derived object, the base class member function will be called.

**Polymorphism** is the ability of having a member function, or an operator overloading function, that behave differently on different types of data. It is the ability of dynamic (i.e. run-time) binding of a pointer of a base class to a method, based on what is stored in the memory pointed to by the pointer and not the data type of the pointer. This is possible by the ability of a pointer to a base class to point not only to base class objects, but also to any object of any of its subclasses. In contrast, a pointer to a derived class object cannot point to a base class object unless explicit casting is used. The decision of which function is invoked is delayed until the run-time, instead of being made during compilation as in non-virtual functions. However, polymorphism which is a major characteristic of object-oriented programming can be used only when pointers (or references) are used and not actual objects.

A function is defined as **virtual** by preceding the return data type at the member function declaration of the base class with the keyword virtual, e.g. virtual void print(void); Declaring a member function of a class as virtual, the corresponding member functions in all that class’s subclasses are automatically considered to be virtual. However, the keyword virtual, although optional, is typically used also in the derived classes at the corresponding virtual function declarations to clarify the nature of the function. The keyword virtual should be used only in the function declarations and not at external definitions of the defined functions. The keyword virtual indicates that the selection of which function to invoke should be delayed until run time and be based on the data type of the object that is pointed to by the pointer that invoked the member function.

A derived class does not need to redefine a member function that has been indicated as virtual in its base class. In that case it inherits the member function from the base class. A virtual function that is redefined in a derived class must have the same signature as the base class function. Otherwise it will simply hide the base class function and compile-, rather than run-, time binding will be used. It is wrong to provide in a derived class a member function with the same signature as the virtual function declared in the base class but with different return data type. The only exception is to have as return data type the address or reference of a derived class object instead of a base class object.

_**/\* Simple example on virtual functions \*/**_

> _#include \<iostream.h> #include \<stdlib.h>_
> 
> _class MyBase { public:_
> 
>  _void print()   {     cout \<\< "\\n Printing through the base class: MyBase" \<\< endl;   }_
> 
>  _**virtual** void print(int i)   {     cout \<\< "\\n Printing through the base class: MyBase:"   \<\< " i = " \<\< i \<\< endl;   } };_ 
> 
> _class MyDerived : public MyBase { public:_
> 
>  _void print()   {     cout \<\< "\\n Printing through the derived class: MyDerived" \<\< endl;   }_
> 
>  _**virtual** void print(int i)   {     cout \<\< "\\n Printing through the derived class: MyDerived:"   \<\< " i = " \<\< i \<\< endl;   } };_ 
> 
> _int main(void) {   MyBase b;   MyDerived d;_
> 
>  _b.print();   d.print();_
> 
>  _MyBase \*pb=&d;   MyDerived \*pd=&d;_
> 
>  _pb -> print();   pd -> print();_
> 
>  _pb -> print(1);   pd -> print(2);_
> 
>  _return EXIT\_SUCCESS; }_
> 
> Output
> ------
> 
>  _Printing through the base class: MyBase  Printing through the derived class: MyDerived_
> 
>  _Printing through the base class: MyBase  Printing through the derived class: MyDerived_
> 
>  _Printing through the derived class: MyDerived: i = 1  Printing through the derived class: MyDerived: i = 2_ 

A pointer to an object of a certain class can point not only to any object of that class but also to any object of that class’ subclasses. Therefore, we may have an array of pointers to a base class which are used to point to objects of any of the base class’ subclasses. Having defined a virtual function, a pointer to the base class can be used to point to an object of the base or any of its subclasses object, and the decision which member function to invoke depends on the current contents of the pointer, i.e. to which class object it points to, rather than its (the pointer’s) data type. In contrast a pointer to a derived class cannot point to an object of the base class unless it is an explicit cast is used. If a pointer to a base class stores the address of a derived class object and both base and derived class have a non-virtual function, or data, with the same name, the base class member function, or data, is selected during static binding.

If the virtual member function is never expected to be used with an object of the base class, it can be specified as **pure virtual function** by providing instead of the body of the function an assignment to 0, e.g. virtual void print(void) = 0; Then, if the function is called run-time error will occur, since it is not intended to be invoked, but it is only provided to allow derived functions to define the actual functions, which will be called based on the contents of the memory pointed by the pointer that invokes the virtual function.

The class scope resolution operator may be used to disable the virtual mechanism and explicitly invoke the member function of a certain class. Such explicit invocation is resolved at compile, rather than at run, time. Declaring a pure virtual function results in no consideration of it during the virtual mechanism resolution, i.e. it cannot be invoked through the virtual mechanism, and specifies the class to be an **abstract base class**. However, a definition for a pure virtual function may be provided (i.e. the pure virtual function may be defined) and the function may be statically invoked (i.e during compile time).

If a pointer to a class is used to point to objects of subclasses of that class, the destructor of the class must be declared as virtual, to ensure that proper deallocations of memory occur when an object is deleted.

Although a constructor may not be declared as virtual, a destructor can be a virtual function. The reason for having a destructor declared as virtual is that if the dynamically allocated memory for a derived class is assigned to a pointer to a base class object, then the base class destructor will be called instead of the derived class destructor resulting in a memory leak. Therefore, it is good to declare as virtual the destructor of the base class if any virtual functions are used and especially when dynamic memory allocation is used. When the destructor is virtual then the order of destructor invocations starts with the derived class and continues with the destructors of its superclasses. Also a virtual function may not be static, since a virtual member function needs to be associated with a particular object of a class rather than the class as a whole.

Another use of the keyword virtual is to declare a base class as virtual. This is useful when a derived class inherits from multiple (direct) superclasses that happen to have already inherited from a common superclass higher in the class hierarchy. Then, the derived class inherits multiple times from the same (the common class to its superclasses) base class. To avoid this we can use the keyword **virtual** at the derivation of its superclasses, as shown below:

> _class MyBase { .......}; class MySuper1: public **virtual** MyBase { .......}; class MySuper2: public **virtual** MyBase { .......}; class MyDerived: public MySuper1, public MySuper2 { .......};_

The use of **virtual base class** (as above), which is called **virtual inheritance,** allows the inheritance and sharing of a single base class sub-object instead of having unecessary multible copies of the base class whenever the base class occurs in the derivation hierarchy. Virtual inheritance avoids duplications of the base class sub-objects and ambiguities that rise with such duplicates. However, there is a performance and complexity impact when using virtual inheritance.

{{< anchor "6" >}}{{< /anchor >}}6\. Abstract Classes
-----------------------------------------------------

A class that is used as a general base class to derive other classes, without any instances of that class ever being created, is called an **_abstract class_**. A class can be made abstract by declaring one or more of its member functions of the class as a _pure virtual function(s)_. This is achieved by setting to zero the declaration of the function. then, the member function will not be considered when a function of the same signature is called, rather one of the derived class functions will be called.

> e.g.:  _virtual void print(void) = 0;_

An _abstract class_ needs to have a derived class, i.e. it is invalid to define an object of an abstract class. A set of functions are typically defined as**_pure virtual functions_** in the base class to provide a common public interface for any current or future derived classes. A member function of an abstract base class is not ever intended to be called, as no instance of the abstract base class is ever anticipated. An attempt to define an object of an abstract base class results in a compile-time error.  

{{< anchor "7" >}}{{< /anchor >}}7\. File Streams
-------------------------------------------------

Although the easiest way to read from a file or to write to a file is using redirection, the direct way to open a file and read from or write to it is using the file-handling library of C++. The declarations of the library are in the header file _fstream.h_, which must be included in a program so as to be able to use input and output streams to a file.

To create an input stream, i.e. open an input file for reading, the following definition should be used, which instantiates an ifstream object:

> _**ifstream** inputStreamName ("fileName");_

Then, the _inputStreamName_ can be used instead of the input operator _cin_ to read from a file named _fileName,_ instead from the standard input.

Similarly to write to a file, i.e open an output file for writing to it, the following definition should be used, which instantiates an _ofstream_ object:

> _**ofstream** outputStreamName ("fileName");_

Then, the _outputStreamName_ can be used instead of the output operator _cout_ to write to a file named _fileName_ instead to the standard output.

After using the _ifstream_, or _ofstream_, object to read from, or write to, a file, the file should be closed when access to it is no longer needed. A file can be closed using the member function _close()_, i.e.     _inputStreamName.close();_ or  _outputStreamName.close();_

 **_EOF_** (end-of-file), which is a constant defined in the iostream.h header file can be used to read data until the end of file (EOF) is reached, by checking whether what was read is equal to EOF (machine dependent). EOF is entered in Unix workstations using \<Control-d>.

You may optionally take a look to the following topics, which were not covered in the course.

### {{< anchor "A1_Namespaces" >}}{{< /anchor >}}_A1. Namespaces_

When several different libraries are used in a program there may be conflicts among identical global names of variables and functions. **_Namespace_** definitions can be used to reduce this problem by enclosing the source code (declarations and definitions) in certain namespaces. Each namespace has an associated namespace scope and contains the namespace members, which can be variables, class definitions, functions, etc., i.e. anything that could have been declared in the global scope. A namespace is defined using the keyword namespace followed by the name of the namespace and the declarations and definitions enclosed in curly braces. The definition of a namespace does not need to be contiguous, but it can be provided in several different points, even in different files.

To refer to a namespace member the qualified name notation indicating the namespace is required. The name of the namespace should be provided followed by the name of the member (variable or function) that is to be accessed. In addition, to be able to refer to a member of a namespace it is required to have earlier declared the namespace. Typically, the namespace declaration is provided in a header file which is included everywhere the namespace needs to be used. Since a member variable should be defined only once, the keyword extern should be used in the declaration of the member variables of a namespace. A member of the global namespace can be referred to by using the scope resolution operator (::) without a namespace preceding it. Therefore, it can be used to access global member that are hidden by local ones. Nested namespaces, i.e. defining a namespace within another namespace, are allowed. In that case more than one namespace names and scope resolution operators need to be used to specify the namespace scope.

Namespaces is a recent feature of C++ and not all compilers conform to the corresponding to namespaces C++ standard.

To avoid the need for typing of long names to specify the namespace scope there are two mechanisms that can be used the **_namespace aliases_** and the**_using directives_**. However, not all compilers support these mechanisms according to the C++ standard.

Using a **_namespace alias_** we can associate a simpler name to an existing (and often long) namespace that we need to use. In particular, we can declare an alias (e.g. MYLIB) for a namespace with a long name (e.g. GraphicsDrawingFunctions) using the following declaration:

> _namespace MYLIB = GraphicsDrawingFunctions;_

Then, to invoke the member function draw of the namespace we can use _MYLIB::draw()_, instead of _GraphicsDrawingFunctions::draw()_.

The _using_ directive can be used to access members of a namespace without the need to explicitly refer to the specific namespace, i.e. it provides unqualified access to the namespace. A namespace can become visible with a declaration in which the keyword _using_ is used followed by the name of the namespace and the name of a member of the namespace we want to access. If no specific member is given then all members of the namespace become visible, i.e. are considered in the scope in the scope in which the using declaration is used. The next example demonstrates the use of a namespace named _NameSpaceTest2_ and its declaration (in the file _test2.h_) and definition (in the file _test2.C_).

**_test2.h_**

> _**namespace** NameSpaceTest2_ _{_ _  extern int x;_ _  extern void print(double d);_ _}_

**_test2.C_**

> _#include \<iostream.h>_
> 
> _**namespace** NameSpaceTest2_ _{_ _  int x = 22;_ _}_
> 
> _**namespace** NameSpaceTest2_ _{_ _  void print(double d)_ _    {_ _      cout \<\<"\\n printing through NStest2::print(double d) "_ _    \<\< " d = " \<\< d \<\< endl;_ _    }_ _}_  

**_test1.C_**

> _#include \<iostream.h>_ _#include \<stdlib.h>_ _#include "test2.h"_
> 
> _int x = 11;_
> 
> _void print(int i)_ _{_ _  cout \<\<"\\n printing through ::print(int i):   i = " \<\< i \<\< endl;_ _}_
> 
> **_using NameSpaceTest2::print;_**
> 
> _main()_ _{_ _  int x = 77;_
> 
>  _cout \<\< "\\n x = " \<\< x \<\< endl;_ _  cout \<\< " ::x = " \<\< ::x \<\< endl;_ _  cout \<\< " NameSpaceTest2::x = " \<\< **NameSpaceTest2::**x \<\< endl;_
> 
>  _print(3);_ _  **NameSpaceTest2::**print(4);_
> 
>  _print(4.11);_ _  **NameSpaceTest2::**print(4.22);_
> 
>  _return EXIT\_SUCCESS;_ _}_  
> 
> Output
> ------
> 
>  _x = 77_ _ ::x = 11_ _ NameSpaceTest2::x = 11_
> 
>  _printing through ::print(int i):   i = 3_ _ printing through NStest2::print(double d)  d = 4_
> 
>  _printing through NStest2::print(double d)  d = 4.11_ _ printing through NStest2::print(double d)  d = 4.22_

A namespace without defining its name, called **_unnamed namespace_**, can be used to define members (functions, classes, and variables) only in a portion of a program without access from other files. An unnamed namespace is defined using the keyword _namespace_ followed by curly braces where all definitions are located. Its members are visible only in that file (scope limited in that file) but have extent until the termination of the program. An unnamed namespace is equivalent to a static global member that is defined and used in one file but cannot be accessed from any other file although its extent lasts until the end of the program.

A special namespace named **_std_** has been used to declare and define all components of the C++ standard library. However, many compilers do not support this feature. All members of this namespace can become visible with the following statement:    _using namespace std;_

### {{< anchor "A2_Assertions" >}}{{< /anchor >}}_A.2. Assertion_

**Assertions** are used in a program as conditions that must be true in order to ensure correctness of the program. They can be used as preconditions, postconditions, and invariants, to verify that a condition is true, e.g. in the entrance, exit, or anywhere within a function.

To use assertions the header file assert.h must be included and the preprocessor macro assert() can be used to check whether a condition is true. If the assertion fails the program terminates providing information about the error that occurred.

The following example demonstrates how assertions can be used to check whether a file has properly opened for reading. In this case, it was attempted to open a nonexistent file and the assert which checks whether the pointer to a file is not equal to null fails resulting in a program termination.

_**/\* Example on the use of assertions \*/**_ 

> _#include \<iostream.h> #include \<fstream.h> #include \<stdlib.h> #include \<assert.h>_ 
> 
> _int main() {   char str1\[\]="existing";   system("ls>existing");   // Using system() an OS command can be executed   ifstream ifp1 (str1);   assert(ifp1);           // line 14   cout \<\< "\\n File " \<\< str1 \<\< " has been opened properly" \<\< endl;_
> 
>  _char str2\[\]="nonexisting";   ifstream ifp2 (str2);   assert(ifp2);           // line 19   cout \<\< "\\n File " \<\< str2 \<\< " has been opened properly" \<\< endl;_
> 
>  _return EXIT\_SUCCESS; }_ 
> 
> Output
> ------
> 
> assertions.C:19: failed assertion ‘ifp2’ Abort

### {{< anchor "A3_C_Standard_Library_string_class" >}}{{< /anchor >}}A.3. C++ Standard Library String Class

A **string** class, that has several convenient and object-oriented capabilities, is provided by the C++ Standard library. In order to use it, the string header file needs to be included, the following example shows how an object of this class can be defined and used, and how it can be combined with the more traditional C Standard library string which is represented as an array of characters.

_**/\* Example on the C++ standard library string class \*/**_

> _#include \<iostream.h> #include \<iomanip.h> #include \<cstring> #include \<string>_
> 
> _int main(void) {   string str1("Testing"), str2;   string str3(str1);   char str4\[\] = "MIT";   const char \*str5 = "";_
> 
>  _cout \<\< "\\n str1: " \<\< setw(20) \<\< str1 \<\< "\\t size = " \<\< str1.size();   str1.empty() ?  cout \<\< "\\t (empty)" \<\< endl : cout \<\< endl ;_
> 
>  _cout \<\< " str2: " \<\< setw(30) \<\< str2 \<\< "\\t size = " \<\< str2.size();   str2.empty() ?  cout \<\< "\\t (empty)" \<\< endl : cout \<\< endl ;_
> 
>  _cout \<\< " str3: " \<\< setw(20) \<\< str3 \<\< "\\t size = " \<\< str3.size();   str3.empty() ?  cout \<\< "\\t (empty)" \<\< endl : cout \<\< endl ;_
> 
>  _cout \<\< " str4: " \<\< setw(20) \<\< str4 \<\< "\\t size = " \<\< strlen(str4);   strlen(str4) ?  cout \<\< endl : cout \<\< "\\t (empty)" \<\< endl ;_
> 
>  _cout \<\< " str5: " \<\< setw(20) \<\< str5 \<\< "\\t size = " \<\< strlen(str5);   strlen(str5) ?  cout \<\< endl : cout \<\< "\\t (empty)" \<\< endl ;_
> 
>  _if(str1==str3)     str2 = str1 + str4 ;   str2 += str3 ;   str2\[10\] = 't' ;_
> 
>  _cout \<\< " str2: " \<\< setw(15) \<\< str2 \<\< "\\t size = " \<\< str2.size();   str2.empty() ?  cout \<\< "\\t (empty)" \<\< endl : cout \<\< endl ;_
> 
>  _return 1; }_
> 
> **Output**
> 
>  _str1: Testing                   size = 7  str2:                           size = 0        (empty)  str3: Testing                   size = 7  str4:                  MIT      size = 3  str5:                           size = 0        (empty)  str2: TestingMITtesting         size = 17\< /EM >_

### {{< anchor "A4" >}}{{< /anchor >}}A.4. Linkage Specifications: extern "C"

An existing compiled C function may be incorporated in a C++ program and used if a declaration of the function with extern "C" preceding its return data type is provided. e.g.: _extern "C" double fun(int, double);_ 

**Command line arguments**

To be able to use command-line arguments, i.e. provide arguments while executing a program main must be declared as: _main(int argc, char \*argv\[ \]){........}_, where _argc_ is the number of command-line arguments and _argv_ is an array of strings each of them corresponding to a command-line argument.