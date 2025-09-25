---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 3
uid: 8376d036-9b1e-e759-42ae-6cfd94600d2a
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).  
  
Topics
------------------------------------------------------------------------------------------

1.  [Classes and Objects](#1)
2.  [Classes: member variables & member functions](#2) 
3.  [Classes: constructors & destructor](#3)
4.  [Constructor header initialization](#4)
5.  [Copy constructors](#5)
6.  [Member variables & functions protection: private, protected & public](#6) 
7.  [Static class data and class functions](#7)
8.  [Class scope](#8)
9.  [Pointers to class members](#9)
10.  [Operator overloading](#10)
11.  [Friend functions](#11)
12.  [Type conversions](#12)

1{{< anchor "1" >}}{{< /anchor >}}. Classes and Objects
-------------------------------------------------------

A **_class_** is a user-defined data type with which we can define not only _data members_ (or data members), but also _member functions_ to manipulate these data. It is essentially an aggregate of data elements and a set of operations to manipulate them.

The **_definition_** of a class consists of the _class head_ (the keyword _class_ and the class tag name, i.e. the class name) and the _class body_ enclosed by braces { }; and terminated by a semicolon. The class body contains the member variables, and the definitions or/and declarations of the member functions. The access levels of the class members can be  specified in the class body by placing declarations in certain parts of the class body.

The definition of a class should be provided in every source code files that uses the class. A class definition is allowable to appear many times in a program as long as it is identical in each case. Since the definition should be exactly the same, its preferable to have a class definition in a header files that is included whenever necessary, in order to avoid inconsistencies due to different definitions of the same class.

A class **_declaration_** is the class header followed by a semicolon. It can be  used to inform the compiler that a certain class is defined somewhere in the program.

> _class MyComplex;           _ //                 Class declaration
> 
> _class MyComplex   _ // class head             Class definition  
> _{                       _ // class body  
> _public:_  
>  _double real;_ //  member variables  
>  _double imaginary;_
> 
>  _MyComplex()_   // default constructor definition  
>  _{_  
>  _real = 0.0 ;_  
>  _imaginary = 0.0;_  
>  _}_
> 
>  _MyComplex(double r, double i)_   // **inline,** since its definition is provided  
>  _{_  
>  _real=r;_  
>  _imaginary=i;_  
>  _}_
> 
>  _~MyComplex()_ //  Destructor definition  
>  _{_  
>  _......._  
>  _}_
> 
>  _double get\_real(void);_ //  Member function prototype  
>  _void print(void);_   //  Member function prototype  
>  _void set\_real(double)_ //  Member function definition  
>  _{_  
>  _..............._  
>  _}_  
> _};_
> 
> _double MyComplex:: get\_real(void)   _ // Externally defined member function  
>  _{_  
>  _.........._  
>  _}_
> 
> _void MyComplex::print(void)_  
>  _{_  
>  _.........._  
>  _}_

Definition of an Object
-----------------------

An object is defined using the class’ name, in the same way a built-in data type is used to define a variable of that data type. The keyword **_class_** can optionally be used before the name of the class. Memory, sufficient to store the data members of an object, is allocated as soon as an object is defined.

 e.g.:

>  _MyComplex x;_  
>  _double d;_  
>  _MyComplex y(3,2.5);_  
>  _class MyComplex t,r;_

Access of an Object
-------------------

A publicly declared data member, or a member function, of an object can be accessed using the _dot operator_ (.)

>    _x.real = 12;_  
>  _y.imaginary = 2.5;_

To access a member data or function of an object using a pointer to that object, the _arrow operator_ (->) can be used instead. Alternatively, the pointer can be dereferenced and then the _dot operator_ can be applied on the dereferenced pointer.

> _MyComplex \*px ;_  
> _px = &x ;_  
> _px ->real =24.5;_  
> _(\*px).real =24.5;_

{{< anchor "2" >}}{{< /anchor >}}2\. Classes: Data Members and Member Functions
-------------------------------------------------------------------------------

The class body typically contains the class data members and the member functions. It may also contain constructors, a destructor, friend function declarations, operator overloadings, etc. Data members are the variables in which the state of each instance (i.e. object) of a class is stored, while member functions are used to specify the behavior of any instance of the class.

**Data members (or member variables)** of a class are usually defined in the private part of the class definition in order to restrict access to them. Data members can be of any build-in, or user-defined, data type. A class cannot have data members of its own type, although it may have pointers or references to such data type objects.

A **member function** is a class specific function which is declared, or defined, in the body of the class definition, and it is always associated with a certain object, i.e. a specific instance of the class, the one that has been used to call the function. A member function can be invoked using one of the class-member selector, the dot operator (.) for objects (i.e. instances of that class), or the arrow operator (->) for pointers to objects.

> classObject.memberFunctionName(arguments) ;  
> pointerToClassObject  ->   memberFunctionName(arguments) ;

 _e.g., from the previous example:_

> _MyComplex x, \*px ;_  
> _double y ;_  
> _y = x.get\_real() ;_  
> _px = &x;_  
> _px -> get\_real() ;_  
> _(\*px).get\_imaginary();_

Whenever a member function is called, a special parameter, named **this**, is implicitly used. Actually, whenever a (non-static) member function is invoked a pointer to that class type that points to the object that is used to invoke the function, is implicitly passed as an argument (behind the scenes) to the member function. The member function has an additional parameter, a pointer to that class data type, named **this**. The parameter **“this”** is a pointer to the object which was used to invoke the function. Therefore, this special parameter can be used as any other pointer to access explicitly a member variable, or function, of the object, e.g.:

> _this -> member\_variable    _       or      _this -> member\_function(....)_

Thus, the actual object with which the member function is invoked can be obtained by dereferencing this special pointer, i.e. by using \*this. This special pointer can be used to resolve name conflicts, e.g. when an argument has the same name as the data members of the class. Pointer this can also be used to return the object with which the member function has been invoked. Finally, this can be used to check whether the object that was used to invoke a member function is the same with an argument passed to the member function by comparing this with the address of the object passed as parameter, e.g. when copying one object to another.

Data members and member functions of a class can be accessed from inside a member function that has been invoked with a certain object of that class without the need to use the dot or the arrow operator. The object pointed by this is the one with which the member function is invoked.

A member function can be **overloaded**, as any other regular function. The compiler uses the signature of the alternative member functions and the data type of the passed arguments to select the proper function to invoke. The constructors of a class are typically overloaded considering all possible arguments that can be used during the definition of an object of the class.

An **externally defined member functions** can be defined outside the class, as long as its declaration has been provided in the class body. The function definition consists of the header and the body of the definition. The header is similar to the function declaration (prototype) with the only difference the specification that defines to which class the member function belongs. This is indicated by providing the class name followed by the class scope resolution operator after the return data type, i.e. before the name, of the member function.

> _returnDataType    className :: memberFunctionName(arguments)_  
> _{_  
>  _........._  
> _}_

A member function that is defined within the body of the class definition (i.e. not externally), is automatically considered to be an inline function. Functions defined outside the class body, that are small and frequently called, can be declared as **inline** to save the overhead due to the function call. The declaration of a function to be inline can be done either in the function declaration inside the class body, in the header of the class definition, or both. However, the definitions of externally defined functions declared as inline should be placed into a header file that can be included in every source code file that invokes that function.

Typically the member data of a class are defined in its **private** part which provides restrictions on the accessibility of them, by allowing only to the members of this class to access it, supporting information hiding. Most member functions are defined in the **public** part of the class, providing a public interface to the private part.

A class may also have another class as one of its member, and the latter class is called a **nested** **class**. In general, a nested class and its enclosing class follow the usual access privileges, i.e. they do not have access to the private members of each other.

Finally, a class can be defined within a function body, i.e. having a local scope. However, the members of a local class cannot be defined outside the class definition, and static members are not allowable since they require a definition outside the body of the class definition which is impossible.

{{< anchor "3" >}}{{< /anchor >}}3\. Classes: Constructors & Destructor
-----------------------------------------------------------------------

**Constructors** and **destructors** are special member functions that are automatically, i.e. implicitly, invoked when an object is created, i.e. when defined, or destroyed, i.e. going out of scope. It is allowable to define within curly braces values to which the member data of an object should be initialized as long as the members are public, e.g.: Point p = { 3 ,1.5}. However, with the exception of specific applications that need to initialize huge number of data members with constant values, it is preferable to use constructors to explicitly define the desired initializations while retaining the data hiding and encapsulation of C++.

A **constructor** is automatically called whenever a new class object is created allowing the explicit initialization of the member data upon the creation of the object. The name of a constructor is the same as the name of the class. A constructor should not have a return type specified, not even void, although it does not return anything. A constructor is used for initialization, assignment of certain values, that may be implicitly passed to it as arguments, type conversion, and dynamic memory management. You may have many constructors as long as they have different signatures, i.e. with different arguments so that the compiler can distinguish among them which one to call. It is preferable to provide a default constructor, rather than let the compiler to implicitly define and use one. This is necessary when having pointers as data members, since the constructor that is implicitly employed by the compiler probably cannot do the correct dynamic memory allocation and copying.

The **default constructor** is a constructor that does not necessarily requires arguments when it is invoked. It is called automatically whenever a new object is created without providing arguments at the definition. You can also use a constructor with parameters as the default constructor by assigning default values to its parameters, which allows its invocation without using any arguments. However, if constructors, but not a default one, are defined, it is not allowable to define an object without specifying the required arguments so as to invoke the one of the existing (and non-default) constructors. Therefore, it is preferable to always define a default constructor if any other constructor is defined.

> _**/\* Example on constructors \*/**_
> 
> _class MyComplex_  
> _{_  
> _public:_  
>  _double real;_  
>  _double imaginary;_
> 
>  _MyComplex()_    // default constructor  
>  _{_  
>  _real = 0.0 ;_  
>  _imaginary = 0.0;_  
>  _}_
> 
>  _MyComplex(double real, double imaginary)_  
>  _{_  
>  _this->real = real;_  
>  _MyComplex::imaginary = imaginary;_  
>  _}_
> 
>  _MyComplex(const MyComplex &c)_ // copy constructor  
>  _{_  
>  _real = c.real ;_  
>  _imaginary = c.imaginary ;_  
>  _}_  
> _};_
> 
> _int main()_  
> _{_  
>  _MyComplex x;_  
>  _cout \<\< "\\n x = " \<\< x.real \<\< " + "_  
>  _\<\< x.imaginary \<\< " i " \<\< endl ;_
> 
>  _x.real = 15.5;_  
>  _x.imaginary = 2.5;_  
>  _cout \<\< " x = " \<\< x.real \<\< " + "_  
>  _\<\< x.imaginary \<\< " i " \<\< endl ;_
> 
>  _double r=3.3;_  
>  _double i=7.5;_  
>  _MyComplex y(r,i);_  
>  _cout \<\< " y = " \<\< y.real \<\< " + "_  
>  _\<\< y.imaginary \<\< " i " \<\< endl ;_
> 
>  _MyComplex z(x);_  
>  _cout \<\< " z = " \<\< z.real \<\< " + "_  
>  _\<\< z.imaginary \<\< " i " \<\< endl ;_  
>  _}_
> 
> _**Output**  
> _ _x = 0 + 0 i_  
>  _x = 15.5 + 2.5 i_  
>  _y = 3.3 + 7.5 i_  
>  _z = 15.5 + 2.5 i_  
>  

A constructor can be invoked using any of the following two forms to define an object:

> _MyComplex c(7.3, 0.65);_  
> _MyComplex c = MyComplex(7.3, 0.65);_

Any constructor, as well as the destructor, can also be defined as inline to avoid the overhead of the function call, when it is defined outside the class. A constructor cannot be defined using the const keyword to consider the object pointed by the pointer this as constant, because the const property of an object is set after the constructor returns and the object is completely initialized.

Typically, the constructors are defined in the public section of a class definition. However, in some cases a constructor may be declared as a private member to prevent the definition of an object of that class using specific data type parameters as arguments (or no arguments for the default), or to forbid, in general, the use of objects of that class.

A constructor with a single parameter can serve as a conversion function, and the compiler can implicitly invoke such a constructor to convert a data type variable to the constructor’s class. To avoid the implicit use of a constructor as conversion function, we can declare an explicit conversion rule.

An array of objects can be defined and initialized using the following form. With this statement an array of 3 objects is defined. Each of them is initialized using the provided values and the corresponding constructor, i.e. the MyComplex(double real, double imaginary) constructor.

> MyComplex mat\[\]= { MyComplex(3,5), MyComplex(7,1), MyComplex(2,4) };

Another special member function in C++ is the **destructor**, which has the name of the class preceded by a tilde (~). The destructor is used for cleanup that may be required whenever an object goes out of scope and before, the memory allocated for it, is released, or, when the delete operator is used to free memory dynamically allocated for an object. The destructor is used to free resources allocated by the constructor, such as release dynamically allocated memory, close files, etc. However, many classes do not need a destructor, because no resources need to be deallocated, and no special actions need to be performed when an object is "destroyed".

The destructor is automatically called whenever an object is destroyed, either because of going out of scope, or because its dynamically allocated memory is released using the delete operator. Memory dynamically allocated for an object of a class can be reallocated (i.e. release) using the **delete** operator which invokes the corresponding destructor. Release of dynamically allocated memory, typically allocated earlier by a constructor, is done in the destructor using the operator delete (or delete\[\]) in order to avoid **memory leaks**. To release memory dynamically allocated for an array of objects (built-in or user defined) the brackets are required to ensure that the entire memory is released and all necessary calls to the class destructor have been made. The destructor of an object can be explicitly invoked without necessarily releasing dynamically allocated memory by calling the destructor using the pointer to the object, the arrow operator and the destructor name, i.e. the class name following a tilde.

It is illegal to specify a return type, including void, for the destructor of a class, as well as to specify any parameters. Therefore, there can be only one destructor per class.

When a function is called passing an object by value, a temporary object with a copy of the object is created using the copy constructor and allocating temporarily memory to store the object parameter. Similarly, when an object of a class is returned by value from a function, the copy constructor is implicitly invoked to allocate the necessary memory and initialize the object's data, member according to the object returned by the function.

{{< anchor "4" >}}{{< /anchor >}}4\. Constructor Header Initialization
----------------------------------------------------------------------

An alternative way to initialize the data members of an object is using **header initialization**, which is a comma separated list of data members with the desired initial values in the constructor's definition. It is also known as **member initialization list**. The header initialization is achieved by using a colon after the header of a constructor followed by a comma separated list of the data members to be initialized and the value to which each of them is to be initialized inside parentheses. Typically, the parameters that are passed as arguments to the constructor are used to provide values for the data members. Using a member initialization list is considered to be an initialization, while initializing the members inside the constructor’s body is considered to be an assignment.

The header initialization is preferred, in cases of user defined data members considering performance, relative to assignment, since the latter involves extra calls to constructors. The use of header initialization is necessary when a constant member data must be initialized, since a const data type is not allowable to appear on the LHS of an assignment, i.e. it is illegal to initialize a const in a constructor’s body. In addition, a reference data member can also be initialized only using a member initialization list, since it cannot appear of the LHS of an assignment.

The following example demonstrates the use of a constructor header initialization.

> _class MyComplex_  
> _{_  
> _private:_  
>  _double real;_  
>  _double imaginary;_
> 
> _public:_  
>  _MyComplex(double re=0, double im=0) **: real(re), imaginary(im) {  }**_  
>  _void print(void);_  
> _};_  
> _void MyComplex::print(void)_  
> _{_  
>  _cout \<\< real \<\< " + " \<\< imaginary \<\< " i " ;_  
> _}_
> 
> _int main()_  
> _{_  
>  _MyComplex x, y(7, 2.1);_  
>  _cout \<\< "\\n x = " ;     x.print() ;_  
>  _cout \<\< "\\n y = " ;     y.print() ;_  
> _}_
> 
> _**Output  
> **  
> _ _x = 0 + 0 i_  
>  _y = 7 + 2.1 i_

{{< anchor "5" >}}{{< /anchor >}}5\. Copy Constructors
------------------------------------------------------

A **copy constructor** is a constructor with one parameter, an object of the same class of which the constructor belongs passed by reference. It is used whenever an object is explicitly initialized with another object of the same class as argument. It is also used whenever an object is passed as an argument to a function, or, when an object of the class is returned from a function by value. Finally, the copy constructor can also be used when an object is assigned using the assignment operator another object, when the assignment operator is not explicitly overloaded, or when the assignment operator is used to initialize an object at its definition.

If a copy constructor is not provided a default member wise initialization takes place, which in some cases may not be the proper action, e.g. when having pointers as data members, to take.

> _MyComplex(const MyComplex &c)              _ // copy constructor  
>  _{_  
>  _real = c.real ;_  
>  _imaginary = c.imaginary ;_  
>  _}_

{{< anchor "6" >}}{{< /anchor >}}6\. Member Variables and Functions Protection: Private, Protected, and Public
--------------------------------------------------------------------------------------------------------------

You can specify different access privileges to specific member data and functions by selectively defining them in the private, protected, or public parts of the class definition. These sections, i.e.the private, protected, and public parts, are specified using the corresponding **access specifiers ** keywords private, protected and public.

The member variables and functions declared, or defined, in the **public part** of a class are accessible by everywhere within the program without any limitation. Usually the member data of a class are defined in the private (or protected) part and member functions to access them are defined in the public part of the class.

The member variables and functions declared, or defined, in the**private part** of the class definition can be accessed only by member functions defined in the same class and by friend functions of the class. Member functions declared, or defined, in the private part of the class definition, i.e. private member functions, can be invoked only by member functions of the class, or by friend functions to the class, similarly as the data members.

Finally, the member variables and functions in the **protected part** are accessible only by member functions defined in the member class, or in subclasses of that class, and any friend functions of the class.

Member functions of a class have access to variables and functions defined in any part, private, protected or public, of the class. Typically all data of a class, i.e. its member variables, are defined in its private or protected parts to restrict access to them which provides **information hiding**. The member functions, which represent the behavior of the class that should be accessible to the user of the class, are typically defined in its public section providing a **public interface** of the class.

There can be any number of labeled with the access specifiers, i.e. public, protected and private, sections. The access level that is specified remains the same until a new access specifier is encountered. The default access level is private, in case no access specifier is specified.

An object that is passed by reference to a member function of a class, using another object to invoke the function, can be protected against modification by declaring the corresponding parameter as const, e.g.:  
  
                    MyComplex(const MyComplex &c);

The object that is used to invoke the member function, i.e. the object pointed by this, can be protected by declaring is as const. This is specified after the parameter list and before the body of the member function in the definition of a function, e.g.:  
                   double get\_real(void) const { ............  }  
If the function is externally defined, it must also be specified as const after the parameter list and before the semicolon in the function declaration, e.g.:  
                   double get\_real(void) const;  
An object declared as const is considered constant after its initialization, i.e. by a constructor, is finished and ends up when its deletion, i.e. using a destructor, starts. Therefore, constructors and destructors, which are never defined as const member functions, can be invoked by a constant object. In contrast, a non-const member function cannot be invoked by a const object.

Modifying the last example by putting the member variables in the private part, we no longer have access to them from outside of the class. Therefore, we must provide functions that can read their values and functions and modify their values. With these member functions which are defined in the public part of the class definition we have indirect access to the private member data.

> _/\* Example on member variables & functions protection  \*/_  
> _class MyComplex_  
> _{_  
> _private:                                                  // private part_  
>  _double real;_  
>  _double imaginary;_
> 
> _public:                                                    // public part_  
>  _MyComplex()        // default constructor_  
>  _{_  
>  _real = 0.0 ;_  
>  _imaginary = 0.0;_  
>  _}_
> 
>  _MyComplex(double r, double i) : real(r), imaginary(i)       // header intialization_  
>  _{_  
>  _}_
> 
>  _MyComplex(const MyComplex &c)            // copy constructor_  
>  _{_  
>  _real = c.real ;_  
>  _imaginary = c.imaginary ;_  
>  _}_
> 
>  _~MyComplex()_  
>  _{_  
>  _//    cout \<\<  "\\nAn object has been detroyed" \<\< endl;_  
>  _}_
> 
>  _double **get\_real**(void) const ;_  
>  _double **get\_imaginary**(void) const;_  
>  _void **set\_real(**double);_  
>  _void **set\_imaginary**(double);_  
> _};_  
>  
> 
> _// Member functions defined outside the body of the class definition_  
> _double **MyComplex::get\_real**(void) const_  
> _{_  
>  _return real;_  
> _}_
> 
> _double **MyComplex::get\_imaginary**(void) const_  
> _{_  
>  _return imaginary;_  
> _}_
> 
> _void **MyComplex::set\_real**(double real)_  
> _{_  
>  _this -> real = real ;_  
> _}_
> 
> _void **MyComplex::set\_imaginary**(double im)_  
> _{_  
>  _imaginary = im;_  
> _}_
> 
> _int main()_  
> _{_  
>  _MyComplex x;_  
>  _cout \<\< "\\n x = " \<\< **x.get\_real**()_  
>  _\<\< " + " \<\< **x.get\_imaginary**()_  
>  _\<\< " i " \<\< endl ;_
> 
>  _double r=3.3;_  
>  _double i=7.5;_
> 
>  _MyComplex y(r,i);_  
>  _cout \<\< " x = " \<\< **y.get\_real**()_  
>  _\<\< " + " \<\< **y.get\_imaginary**()_  
>  _\<\< " i " \<\< endl ;_  
>  _return EXIT\_SUCCESS;_  
> _}_
> 
> _**Output  
> **  
> _ _x = 0 + 0 i_  
>  _x = 3.3 + 7.5 i_

{{< anchor "7" >}}{{< /anchor >}}7\. Static Class Data and Class Functions
--------------------------------------------------------------------------

If a data member of a class is defined using the keyword **static** before its data type, then memory is allocated for only one such element for the entire class, irrespectively of the number of instances (i.e. objects) of that class. The lifetime (i.e. the extent) of this static data is the entire program and there is only one such a variable shared by all objects of the class. A **static class data** is typically used to store information common to all objects of a class and to avoid unnecessary duplication of information.

Memory space is allocated for each static class variable only once even if there are no objects of that class. Not only member data i.e. variables, but also member functions can be defined as **static**. The latter are used to manipulate the former. A function is declared as static in the class body, i.e. at its declaration, and not at its definition.

A static class member, data or function, can be accessed using an object and the dot, operator, or a pointer to an object and the arrow operator. In addition, it can be accessed using the class name followed by the class scope resolution operator (::).

Because the pointer this is not associated with function calls to a static member function, it is a compile time error to attempt to access directly non-static members of the class from a static function.

The access levels and constraints of a static class member, data or function, are the same as those of non-static members. The only exception is when a static variable is initialized. Then, the access level is relaxed to allow the initialization, as shown in the following example.

A static class member is defined and initialized outside the class definition, as any other non-member global variable, i.e. outside of any function. The definition of a static member should appear only once in a program and, therefore, it should not be placed in a header file.

Someone could alternatively use a regular global variable to store information that refers to the entire class and not to individual objects. However, the use of static class members should be preferred since it provides all advantages of object-oriented programming, namely information hiding, data encapsulation, physical and direct correspondence and association of the specific information with the class, etc.

Because there is only one instance (one copy) of a static member data of a class, a static member data can be of the same type as the class itself.

The following example shows how a static class variable and function are defined and used.

> _**/\*  Example on static class data and functions \*/**  
> __class Employee_  
> _{_  
> _private:_  
>  _char \*first\_name ;_  
>  _char \*last\_name ;_  
>  _double salary ;_  
>  _int social\_security ;_  
>  _**static** int employeesNumber;_ **// static class data declaration**
> 
> _public:_  
>  _Employee(char \*first="None",char \*last="None", double sal=0.0, int soc=0)_  
>  _{_  
>  _first\_name = new char\[strlen(first)+1\] ;_  
>  _last\_name = new char\[strlen(last)+1\] ;_  
>  _strcpy(first\_name,first) ;_  
>  _strcpy(last\_name,last) ;_  
>  _salary = sal ;_  
>  _social\_security = soc ;_  
>  _employeesNumber++;_  
>  _}_  
>  _......_  
>  _**static** void printEmployeesNumber(void);_  
>  **// static class function declaration**  
> _}_
> 
> _**void Employee::printEmployeesNumber(void)   ** // static class function definition_  
> _{_  
>  _cout \<\< "\\n Number of employees: " \<\<  employeesNumber;_  
> _}_  
>  
> 
> _int  Employee::employeesNumber=0;_  
>  **// static class data definition and intialization**
> 
> _int main ( )_  
> _{_  
>  _**Employee::printEmployeesNumber();**_
> 
>  _Employee a;_  
>  _**a.printEmployeesNumber();**_
> 
>  _char first\_name\[20\]="Bugs";_  
>  _char last\_name\[30\]="Bunny";_  
>  _double salary=100000 ;_  
>  _int social\_security=103038 ;_  
>  _Employee b(first\_name,last\_name,salary,social\_security);_  
>  _**b.****printEmployeesNumber();**_  
> _}_

{{< anchor "8" >}}{{< /anchor >}}8\. Class Scope
------------------------------------------------

The member data and functions of a class are considered to belong in the corresponding class scope. Inside the **class scope**, in general, there is no need to specify the class that a member belongs so as to access it. The body of a class definition, the code that follows the name of an externally defined member function up to the end of the body of its definition, and the code following the name of a static member at its definition up to the semicolon are all considered to be in class scope. However, outside class scope the access operators, i.e. the dot and arrow operators, and the class scope resolution operator must be used to specify the class scope in which the member belongs.

When an identifier, i.e. a variable or function name, is used in a class definition, first the declarations of the already declared members are considered, and if no member matches the name the declarations in the namespace scope (e.g. the global scope) located before the class definition are considered.  When an identifier is used in a member function of a class the resolution of the name starts with the local scope declarations, e.g. local variables and function parameters, then if nothing is found, it continues with declarations of all members of the class. Finally, if the name is still not resolved the declarations that appear in the namespace scope are also considered.

> _**/\* Example on class scope \*/**  
> __class MyClass_  
> _{_  
> _public:_  
>  _int number;_  
> _};_
> 
> _int number = 33;_
> 
> _void main()_  
> _{_  
>  _MyClass n;_  
>  _n.number=22;_  
>  _int number = 11;_
> 
>  _cout \<\< "\\n number = " \<\< **number** ;_  
>  _cout \<\< "\\n n.number = " \<\< **n.number** ;_  
>  _cout \<\< "\\n ::number = " \<\< **::number**\<\< endl;_  
> _}_
> 
> _**Output  
> **  
> _ _number = 11_  
>  _n.number = 22_  
>  _::number = 33_

{{< anchor "9" >}}{{< /anchor >}}9\. Pointers to Class Members
--------------------------------------------------------------

Member data can also be accessed using **pointers** to specific member data. To define a pointer to a member data of a class the name of the class followed by the class scope resolution operator must be used between the data type of the variable to which the pointers may point and the dereference operator (\*). Then, the pointer can be assigned the address of a specific member data of the class using the address-of operator (&) followed by the class name, the class scope resolution operator and the specific member data name. Having defined a pointer to a specific data member of a class, the pointer can be dereferenced and used with any instance ,i.e. object, of the class, as shown in the following example. Therefore, a specific object should be used when using a pointer to a data member.

Similarly a **pointer to a member function** can be defined. Again it is necessary to provide the class type whose member is the function, in addition to the return type and the number and type of the parameters of the function.

Note that pointers to static member data and functions should be defined as regular pointers to variables and functions, i.e. without specifying the class. No association with a specific object when accessing a member data needs to be resolved, and no this pointer is associated with static member functions calls.

> _**/\* Example on the use of pointers to class objects \*/**  
> __class MyComplex {_  
> _public:_  
>  _double real, imaginary;_  
>  _void print()  {  cout \<\< real \<\< " + " \<\< imaginary \<\< "i ";   }_  
> _};_
> 
> _void main()_  
> _{_  
>  _MyComplex x, y, \*py=&y ;_  
>  _**double MyComplex:: \*pd; **_ // pointer to a double data member  
>  _**void (MyComplex::\*pf)()=0;**_ // pointer to a member function
> 
>  _**pd = &MyComplex::real;**_  
>  **_x.\*pd_** _\= 1.1;_  
>  **_y.\*pd_** _\= -22.4;_  
>  **_pd = &MyComplex::imaginary;_**  
>  _**x.\*pd** = 0.3;_  
>  _**y.\*pd** = 44.5;_  
>  _cout \<\< "\\n x = " \<\< x.real \<\< " + " \<\< x.\*pd \<\< " i " ;_  
>  _cout \<\< "\\n y = " \<\< y.real \<\< " + " \<\< y.\*pd \<\< " i " \<\< endl;_
> 
>  _**pf = &MyComplex::print;**_  
>  _cout \<\< "\\n\\n x = " ;_  
>  _**(x.\*pf)();**_  
>  _cout \<\< "\\n y = " ;_  
>  _**((\*py).\*pf)();**_  
>  _cout \<\< "\\n y = " ;_  
>  _**(py->\*pf)()****;**_  
> _}_
> 
> _**Output:**  
> _ _x = 1.1 + 0.3 i_  
>  _y = -22.4 + 44.5 i_
> 
>  _x = 1.1 + 0.3i_  
>  _y = -22.4 + 44.5i_  
>  _y = -22.4 + 44.5i_

{{< anchor "10" >}}{{< /anchor >}}10\. Operator Overloading
-----------------------------------------------------------

C++ allows us to define new definitions for operators to be used with user-defined data types, i.e. objects. This is feature is called **operator overloading** and allows us to give to normal operators additional meaning when they are applied to user defined data types.

All operators can be overloaded except the following ones in double quotes: ".", ".\*", "::", "?:", and "sizeof". The subscript \[ \], function call ( ) and arrow access ->, operators can be overloaded only as member functions. An operator overloading function needs to be either a member function of a class, or have a class object as parameter, except when the overloaded operator is new, delete, or delete\[\].

To overload an operator we need to define a member function with the keyword **operator** followed by the operator that is overloaded, instead of a name for the member function. This declaration syntax informs the compiler that this member function should be called whenever the particular operator is encountered next to an object of this class as operand. A member function that is overloading an operator can also be overloaded as a function, having the same operator overloading function in several forms, as long as each of them has a unique signature, i.e. differs in its parameters from all others. The compiler distinguishes among overloaded operators by looking at the operator and the data types of its operands. The precedence and associativity of operators is retained when overloaded. It is not possible to define additional operators for the built-in data types. Also it is not possible to change the arity of an operator, e.g. use a unary operator as a binary and vice versa, unless its one of the four operators that have both a unary and a binary form, (+), (-), (\*), and (&).

Member functions that overload operators require one less argument than the number of the operands used on the operator, since the one operand is the object whose member function is invoked, i.e. \*this.

The following example demonstrates the definition and use of an **overloaded operator**. A unary operator (++) and a binary operator (+) are defined and whenever either of these is encountered together with an object in an expression, the corresponding member function is invoked.

> _**/\* Example on operator overloading \*/**_

> _class MyComplex_  
> _{_  
>  _......._  
>  _void **operator ++**(void);                           // member function declarations_  
>  _Complex **operator +**(const MyComplex &c);_  
> _};_
> 
> _void MyComplex::**operator ++**(void)_  
> _{_  
>  _++real;_  
> _}_  
>  _// member function definitions_
> 
> _Complex MyComplex::**operator +**(const MyComplex & c)_  
> _{_  
>  _MyComplex sum;_  
>  _sum.real = real **+** c.real;_  
>  _sum.imaginary = imaginary + c.imaginary;_  
>  _return sum;_  
> _}_
> 
> _main()_  
>  _{_  
>  _MyComplex x,y(5,2.4);_  
>  _MyComplex z = **++**x **+** y;_  
>  _}_

  
Although the **input and output operators** are usually overloaded as **friend functions**, an alternative way is to define it as a non-friend operator overloading function and provide proper get and set member functions that can be called from inside the overloaded operator functions.

> _ostream& operator \<\< (ostream &o, const MyComplex &c)_  
> _{_  
>  _o \<\< c.get\_real() \<\< " + " \<\< c.get\_imaginary() \<\< " i " ;_  
>  _return o;_  
> _}_
> 
> _int main()_  
>  _{_  
>  _MyComplex x;_  
>  _...._  
>  _cout \<\< " x = " \<\< x \<\<  endl;_  
>  _}_

  
An alternative way to access an operator overloading member function is to use its actual name which consists of the keyword operator followed by the specific operator that is overloaded. For example the member function that overloaded the operators ++ and +, in the previous example can also be accessed as follows.

> _int main()_  
>  _{_  
>  _MyComplex x,y(5 , 2.4);_  
>  _MyComplex z ;_  
>  _x.operator++( );_  
>  _z = x.operator+(y);_  
>  _cout \<\< "\\n x = " \<\< x \<\<  " y = " \<\< y \<\<  " z = " \<\< z;_  
>  _}_

If no assignment operator is overloaded, a one-by-one member copy is performed by default using a compiler-provided assignment operator that is implicitly invoked. However, there are some cases in which such a "shallow" copy is not our intention, e.g. when there are pointer data members pointing to dynamically allocated memory. In those cases, an assignment operator can be used to make a "deep" copy, i.e. instead of copying pointer values, resulting in pointer data members of two objects to point to the same memory location, memory is dynamically allocated and the contents in the memory pointed by the source-object pointer is copied at the memory location pointed by the corresponding pointer of the other object (the target one).

When an initialization of an object is done at its definition using an object of the same class, even if there is an assignment operator overloading available, the **copy constructor** is used, instead, to initialize the object.

Postfix and prefix versions of **increment (++) and decrement (--) operators** can be overloaded. The methods that overload the postfix operators have an additional integer parameter that is used to distinguish them from the prefix versions, i.e. the postfix form is defined as binary operator with an auxiliary extra operand of type int. The prefix version can be invoked using ++x, or x.operator++(), in the operator or method form respectively. The postfix version, operator++(int), can be invoked using x++, or x.operator++(0), (any number can be used as parameter).

The memory management operators **new, new\[\], delete,** or**delete\[\],** can also be overloaded to achieve specific memory management requirements. The overloaded **new** operator should return a type pointer to void and have its first parameter of type size\_t, (size\_t is a typedef defined in the header file cstddef).

> _e.g:._ _void \* operator new (size\_t s) { ......... }_

The **delete** operator should return void and have a parameter of type void\* which points to the memory that is to be released.

> _e.g.:_  _void operator delete (void \* p) { ......... }_

In both cases other parameters of any type are optional. If the new and delete operators are overloaded, they are automatically invoked every time the operators are used, instead of the provided standard ones. The global new and delete operators can still be selectively called by using the global scope resolution operator,

> _e.g_ _MyComplex \*pc = ::new MyComplex and ::delete pc._

Similarly the array versions **new\[\]** and **delete \[\]** can be overloaded and used.

{{< anchor "11" >}}{{< /anchor >}}11\. Friend Functions
-------------------------------------------------------

A **friend function** is not a member function of a class, but a function that is granted special access privileges to all member data and functions of a class. This is achieved by declaring the function in the class body using the keyword **friend** which gives unlimited access to that function, even to the private part of the class. A friend declaration may appear in any section of the class definition without any effect in which, private, protected, or public, part it appears.

A **friend function** can be a member function of another class, or even all the member functions of another class. One case where friend functions are useful is when a function needs to have access to two or more unrelated classes. In addition, friend functions allow more flexible operator overloadings, since the object of the class is passed as an argument and the function its not an object's member function.

For example if we overload the + operator as a member function of MyComplex class then we can add two objects of this class c1+c2, and an object of this class and a number, e.g. c1+4.5, assuming for the latter case that a convert constructor is available to be used to convert the number to a MyComplex object. An overloaded operator of a class is considered and may be invoked only if an instance of the class (i.e. an object) appears to the left of the operator. However, the addition 4.5+c1 is not valid because operator+ is a member function of the class of c1. Using a friend function to overload the operator+ both c1+4.5 and 4.5+c1 are valid because in both cases the convertion constructor of MyComplex is invoked to convert it, if necessary, to a MyComplex object. However, in the latter case we need to provide a way to make the conversion from a double to an object of our class.

**Input and output overloaded operators** are typically defined to be friend functions in order to have access to the data members of the class.

The following example shows a use of two friend functions, of which the one is overloading the input operator:

> _**/\* Example on friend functions \*/**  
> __class MyComplex_  
> _{_  
> _private:_  
>  _double real, imaginary;_  
>  _........_  
>  _**friend** void printMyComplex(const MyComplex &c);_  
>  _**friend** istream& operator >> (istream &i, MyComplex &c);_  
> _};_
> 
> _void printMyComplex(const MyComplex &c)_  
>  _// a friend function has unlimited access_  
> _{_  
>  _cout \<\< c.real \<\< " + " \<\< c.imaginary \<\< " i " ;_  
> _}_
> 
> _istream& operator >> (istream &i, MyComplex &c)_  
> _{_  
>  _cout \<\< "\\n Please give the real part: " ;_  
>  _i >> c.**real** ;                                                // access to private members_  
>  _cout \<\< "\\n   and the imaginary part: " ;_  
>  _i >> c.**imaginary** ;                                               // access to private members_  
>  _return i;_  
> _}_
> 
> _int main()_  
> _{_  
>  _MyComplex x;_  
>  _cin >>x;_  
>  _printMyComplex(x) ;_  
> _}_

A function may be declared as friend for more than one classes. Also a member function of a class may be declared as friend for another class. In addition, a whole class, i.e. all its member functions, may be declared as friend for another class, which grants access to all member functions of the friend class to all member data and functions, even those defined in the private part, of the other class.

> _class Point_  
> _{_  
>  _........_  
>  _friend Design::draw();_ // the member function draw() of  
>                                            // the  Design class is declared friend  
>  _friend Spline;_    // the Spline class, i.e. all its member  
> _};_                                 //  functions,  is declared friend

There are cases in which overloading an operator needs to be done using a friend rather than a member function. For example, if the multiplication operator (\*) is overloaded using a member function, in particular using a set of overloaded member functions with the same name to allow the multiplication with any possible data type, i.e. an int, double, a MyComplex, etc. Then, although the multiplication of a MyComplex number with a different data type value is allowable when the latter is on the right of the operator, the case of having the Mycomplex on the right is not allowable. For that case a friend function can be used as shown in the next example.

> _class MyComplex_  
> _{_  
>  _........._  
>  _**friend** MyComplex operator+(double d, const MyComplex &c);_  
> _};_
> 
> _MyComplex operator+(double d, const MyComplex &c)_  
> _{_  
>  _MyComplex sum;_  
>  _sum.real = d + c.real;_  
>  _sum.imaginary = c.imaginary;_  
>  _return sum;_  
> _}_
> 
> _int main()_  
>  _{_  
>  _MyComplex x(3,1.5), y;_  
>  _y = 17.5 + x;_  
>  _}_

{{< anchor "12" >}}{{< /anchor >}}12\. Type Conversions
-------------------------------------------------------

**Implicit type conversions** are performed when different built-in data types occurred in mixed expressions. The rules that govern these conversions are specified by the language as we have seen in an earlier recitation. C++ allows the definition of **conversion rules** for user-defined data types that can be used when conversions from one data type to another are required.

Member functions can be defined and used to achieve certain conversions when objects are used as operands to operators (either built-in or overloaded), or as arguments to functions. These functions are implicitly invoked by the compiler whenever necessary to handle conversions.

Even when no explicit conversions are provided the compiler tries to use constructors that are related with the conversion that has to be performed, e.g. by assigning to a user-defined data type object of the constructor’s class a different data type. By default a constructor with one parameter may be used by the compiler for a type conversion, as a conversion function. The following example shows how a constructor is employed to make a type conversion from a built-in data type to a user defined, i.e. a class type.

> _**/\* Example on the use of a convert constructor \*/**  
> __class LengthFT_  
> _{_  
> _public:_  
>  _int feet;_  
>  _double inches;_
> 
>  _LengthFT(double d)                 **// convert constructor**_  
>  _{_  
>  _cout \<\< "\\n Using the convert constructor" ;_  
>  _feet = (d\*100/2.54)/12;_  
>  _inches =  d\*100/2.54 - 12\*feet ;_  
>  _}_  
> _};_
> 
> _int main()_  
> _{_  
>  _LengthFT x;_  
>  _double distance = 0.65;_
> 
>  _x = (LengthFT)1.45;_ **//  Type casting (conversion) using the convert constructor**  
>  _cout \<\< "\\n x = " \<\< x.feet \<\< " - " \<\< setprecision(3) \<\< x.inches \<\< "'" \<\< endl;_
> 
>  _x = distance;_ **//  Implicit type conversion using the convert constructor**  
>  _cout \<\< "\\n Distance (m) = " \<\< distance \<\< endl ;_  
>  _cout \<\< " x = " \<\< x.feet \<\< " - " \<\< x.inches \<\< "'\\n" \<\< flush;_
> 
>  _return EXIT\_SUCCESS;_  
> _}_
> 
> _**Output  
> **  
> _ _Using the convert constructor_  
>  _x = 4 - 9.09"_
> 
>  _Using the convert constructor_  
>  _Distance (m) = 0.65_  
>  _x = 2 - 1.59"_

In addition, operator overloading functions may also be used to handle different data types. An **explicit conversion rule** can be defined using a **conversion function**. A conversion function can be used to define how a conversion between a user-defined data type and another data type, user-defined or built-in, should be performed. A type conversion function is defined using the keyword operator followed by the data type name. Although a (converted) value is returned the function declaration and definition should not specify a return data type. Also a parameter list should not be defined. A conversion function can be invoked by an explicit cast, or when a mixed expression is encounter and conversions are necessary to be performed.

The following example shows a very simple case where a conversion function is defined in the class LengthFT to convert a LengthFT object to a double (in this case considering only its real part. The class LengthFT is used to represent a length in feet-inches form and whenever appears in a mixed expression we want to convert it to a double and express the length in meters.

> _**/\* Example on conversion functions using explicit conversion\*/**  
> __class LengthFT_  
> _{_  
> _public:_  
>  _int feet;_  
>  _double inches;_  
>  _LengthFT(int f=0, double i=0)_  
>  _{_  
>  _feet = f;_  
>  _inches = i;_  
>  _}_  
>  _operator double();_  
> _};_
> 
> _LengthFT::operator double()_  
> _{_  
>  _return 0.0254\*(feet\*12+inches);_  
> _}_
> 
> _int main()_  
> _{_  
>  _LengthFT x(6,3);_  
>  _double distance=4.2;_
> 
>  _cout \<\< "\\n x = " \<\< x.feet \<\< " - " \<\< x.inches \<\< "'" \<\< endl;_  
>  _**distance += x**;_ **// the member function LengthFT::operator** _double() is called_  
>  _cout \<\< " Distance \[m\] = " \<\< distance \<\< endl ;_  
>  _cout \<\< " x \[m\] = " \<\< **x** \<\< endl ;_  
>   **     //  LengthFT::operator double() is called**
> 
>  _return EXIT\_SUCCESS;_  
> _}_
> 
> _**Output  
> **  
> _ _x = 6 - 3"_  
>  _Distance \[m\] = 6.105_  
>  _x \[m\] = 1.905_