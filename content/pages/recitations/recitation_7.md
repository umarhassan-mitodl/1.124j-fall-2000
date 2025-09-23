---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 7
uid: a0fed608-bcf6-b4cc-ed12-a80b51d8f0b1
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).  
  
Topics
------------------------------------------------------------------------------------------

1.  [Sun Java® Studio Standard 5](#1) 
2.  [Inheritance](#2) 
3.  [Controlling access to class members](#3)
4.  [Strings](#4)
5.  [Packages](#5) 
6.  [Interfaces](#6) 
7.  [Nested classes and interfaces](#7) 
8.  [Garbage Collection](#8) 
9.  [Applets](#9) 

{{< anchor "1" >}}{{< /anchor >}}1\. Sun Java Studio Standard 5
---------------------------------------------------------------

Sun Java® Studio Standard 5 is an integrated Java® development environment (IDE) that provides visual design, editing, compilation, debugging, and deployment of Java® software. It is itself written entirely in Java® and is from the Sun's Java® web site: [Sun Java® Studio Standard 5 update 1](https://docs.oracle.com/cd/E19786-01/index.html). If you prefer to use a free IDE and only require J2SE and web application development capabilities then use the open source IDE [NetBeans](http://www.netbeans.org).

{{< anchor "2" >}}{{< /anchor >}}2\. Inheritance
------------------------------------------------

A class (called _subclass_) can inherit the behavior of another class (called _superclass_). This is called _inheritance_ and it is essential for Object Oriented Programming (OOP)_,_ allowing the extension of existing classes. A class is extended using the keyword _extends_ following the name of the new class (i.e. the subclass) and before the name of the superclass.

>           e.g.: _class Pixel extends Point_

A subclass object can be used in any function that an object of its superclass is expected. Note, that the converse i.e. using a superclass where a subclass is expected is, in general, false. This feature enables _polymorphism_, another important characteristic of OOP, which allows a different function to be called depending on the actual object that is associated with the function call. _Polymorphism_ is a Greek word which means that it allows many (poly) forms or shapes (morphes). An object in Java® can be polymorphic, i.e. have various different forms and this is possible due to the fact that a subclass can be used wherever a superclass is legal and the _late binding_ feature of Java®. With late binding the compiler does not associate the function call with a certain function during compilation, but delays that decision until execution (i.e. running)  time. In contrast, with _static binding_ the decision of which function to be invoked is decided at compile time.

Although when calling a function the decision of which function of a class to call depends on the actual class of the object, when accessing a data field of an object the decision is according to the type of the reference to the object.

Although a subclass object can be assigned to a superclass object, i.e. to a variable that may refer to a superclass, the converse is not allowable unless an explicit _casting_ is used. The syntax for casting between two objects is the similar to the casting from one primitive data type to another. In order to avoid illegal castings the _instanceof_ operator may be used to verify the data type of the object prior to any casting. Casting of objects is allowable only between objects within an inheritance hierarchy. If an object has been assigned to a reference to its superclass, then to be able to use the objects (i.e. the subclass' functions) it is required to cast it back to the subclass.

An implicit reference, named _super_, is available and references to members of the superclass of the class of the object that invoked a function. It is similar to the _this_ reference.

Subclasses can add other member and class data, or member or class functions. Data fields of a subclass can hide data fields of a superclass if they are given the same name. Then, although the data fields of the superclass exist they can be accessed only indirectly. Similarly, a subclass can inherit and use, or override, the methods provided in its superclasses. Member functions of the superclass can be overridden by new implementations provided in the subclass. However, a subclass cannot override superclass functions that have been declared as _final_ or _static_ (i.e. class functions). It can only override accessible non-static functions. A subclass must override functions that are declared as _abstract_ in the superclass or the subclass must be abstract itself.

A subclass function with a name the same as a superclass function may have different parameters, according to function overloading. However, a subclass function with the same signature with a superclass function must also have the same return type, in order to hide the superclass' function. The overriding function must have the same signature (name and parameters) and the same return type with the function it overrides. Which function is called depends on the actual object and its class that is referenced by the object reference and not by the class of the reference to the object itself.

The overriding function can have a different access specifier but only if it allows more access than the one of the superclass function that overrides. It can have also different throws specified but not a throw clause that has not been declared by the superclass function or an exception type that is not a subtype of the exceptions specified in the superclass. The hidden variables and overridden functions of a superclass can be accessed using the _super_ keyword.

Inheritance Example

> _class Point_  
> _{_  
>  _private double x, y;_
> 
>  _Point()_  
>  _{_  
>  _System.out.println(" In default constructor of Point class");_  
>  _x = y = 100.0;_  
>  _}_  
>  _Point(double x, double y)_  
>  _{_  
>  _System.out.println(" In constructor Point(double x, double y)");_  
>  _this.x = x;_  
>  _this.y = y;_  
>  _}_
> 
>  _public void set(double x, double y)_  
>  _{_  
>  _System.out.println(" In set method of Point");_  
>  _this.x = x;_  
>  _this.y = y;_  
>  _}_
> 
>  _public String toString()_  
>  _{_  
>  _System.out.print(" In toString method of Point class");_  
>  _return ("x = " + x + "    y = " + y);_  
>  _}_  
> _}_  
>  
> 
> _class Pixel extends Point_  
> _{_  
>  _private int color;_
> 
>  _Pixel()_  
>  _{_  
>  _System.out.println(" In default constructor of Pixel class");_  
>  _color = 111111111;_  
>  _}_  
>  _Pixel(double x, double y, int color)_  
>  _{_  
>  _super(x,y);_  
>  _System.out.println(" In  Pixel(double x, double y, int color) ");_  
>  _this.color = color;_  
>  _}_
> 
>  _public void set(double x, double y, int color)_  
>  _{_  
>  _System.out.println(" In set of Pixel class calling Point's set");_  
>  _super.set(x,y);_  
>  _this.color = color;_  
>  _}_
> 
>  _public String toString()_  
>  _{_  
>  _System.out.print(" In toString method of Pixel class");_  
>  _return ("color = " + color );_  
>  _}_  
> _}_
> 
> _class introInheritance_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Pixel p1;_  
>  _p1 = new Pixel();_  
>  _p1.set(1.11, 0.22, 100111010);_  
>  _System.out.println();_
> 
>  _Point p2 = new Point(200,25.7);_  
>  _Pixel p3 = new Pixel(3.33,9.6,111000111);_  
>  _Point p4 = new Pixel();_  
>  _System.out.println();_
> 
>  _System.out.println("\\n p1: " + p1);_  
>  _System.out.println("\\n p2: " + p2);_  
>  _System.out.println("\\n p3: " + p3);_  
>  _System.out.println("\\n p4: " + p4);_  
>  _System.out.println();_  
>  _}_  
> _}_

  
 _**Output:**_

>  _In default constructor of Point class_  
>  _In default constructor of Pixel class_  
>  _In set of Pixel class calling Point's set_  
>  _In set method of Point_
> 
>  _In constructor Point(double x, double y)_  
>  _In constructor Point(double x, double y)_  
>  _In  Pixel(double x, double y, int color)_  
>  _In default constructor of Point class_  
>  _In default constructor of Pixel class_
> 
>  _In toString method of Pixel class_  
>  _p1: color = 100111010_  
>  _In toString method of Point class_  
>  _p2: x = 200.0    y = 25.7_  
>  _In toString method of Pixel class_  
>  _p3: color = 111000111_  
>  _In toString method of Pixel class_  
>  _p4: color = 111111111_  
>  

Java® does not allow multiple inheritance. All classes in Java® are subclasses of the class Object, which is defined in the package java.lang. Even if no inheritance is used, i.e. no extension, the class is considered to be a subclass of the Object class. Variables of  class Object can be used to refer to any reference data type, object or array. The functions toString(), equals(), clone(), and finalize() are functions of the class _Object_ that are often overridden by the subclasses. The toString() method returns a string representation  of the object. The clone() method is used to make a field-by-field copy of one object to a new one which is returned by the method. The equals() method is used to compare two objects for equality according to a selected equality test. Finally, the finalize() method can be used to clean up resources that may have been allocated from the object before it is garbage collected. Another useful function is the getClass(), which, however, cannot be overridden since it is a final function. This function returns the runtime class of the object, an instance of Class, which can be then query for various information. The class Class provides various useful functions.

_Object Wrappers_

Java® provides _object wrappers_ which are subclasses of the Object class that are counterparts of the primitive data types and allow the conversion of a primitive data type variable to an object.

The wrapper classes which are the Boolean, Character, Byte, Double, Float, Integer, Long, Short and Void, are final classes that are useful when doing _generic programming_. The wrapper classes provide several useful functions.

3\. {{< anchor "3" >}}{{< /anchor >}}Controlling Access to Class Members
------------------------------------------------------------------------

Java® provides, as C++ does, an access control mechanism which restricts the access to member data and functions of a class. In Java® the _access level_ is specified for each individual member of the class. There are 3 different access specifiers which may be used to specify one of the 4 access levels. The _access specifiers_ (or _access control modifiers_) are the _private_, _protected_, _public_ and _package_ which are specified as follows:

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
ACCESS SPECIFIER
{{< thclose >}}
{{< thopen >}}
ACCESS LEVEL
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE IN CLASS
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE IN SUBCLASS
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE IN PACKAGE
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE IN WORLD
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
private
{{< tdclose >}}
{{< tdopen >}}
private
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
no
{{< tdclose >}}
{{< tdopen >}}
no
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
protected
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
yes
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
public
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
none
{{< tdclose >}}
{{< tdopen >}}
package
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
no
{{< tdclose >}}
{{< tdopen >}}
yes
{{< tdclose >}}
{{< tdopen >}}
no
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

A _private_ member of a class is accessible only within the class itself. Instances of the same class have access to each other's private members. The keyword _private_ is used to specify a private member.

A _protected_ member of a class allows access for and can be inherited by only the class itself, its subclasses, and classes defined in the same package. A protected member (data or function) can be accessed using a reference variable that can be either a reference to the class itself or to one of its subclasses. Protected static data and functions of a class can be accessed in any of its subclasses as well as by any class in the same package. The keyword _protected_ is used to specify a protected member.

A _package_ member is accessible from and is inheritable by all classes in the same package as the class. This is the default access level used when no access specifier is used.

Finally, a _public_ member is accessible from all classes and is inherited by any subclass. It is specified using the keyword _public_.

Therefore, a subclass inherits the members of its superclass that are protected and public, as well as the members without access specifier, i.e. the package members, as long as  the subclass is in the same package with the superclass. However, subclass member variables hide the superclass members variables with the same name, and subclass member functions override the corresponding ones in the superclass. The keyword _super_ can be used to refer to hidden variables and overridden functions of the superclass.

4\. {{< anchor "4" >}}{{< /anchor >}}Strings
--------------------------------------------

The String class can be used to deal with strings, i.e. a sequence of characters. This class provides several functionalities that can be used on strings. It provides a concatenation operator "+", and a shorthand operator "+=". In addition, it provides a _length()_ method to obtain the number of the characters in the string. A method, named _equals()_ is also available to compare two strings whether they have the same contents.

When concatenating any primitive data type value with a string it is always converted to a string. For objects a special function named toString() which is inherited from the Object class can be overridden to provide this facility.

String objects are only readable. Their contents cannot be modified, i.e. they are immutable. When a concatenation, or assignment is done, what actually happened is that a new String object is created and referenced. Java® provides another class, named _StringBuffer_ which can be used to store and modify a set of characters.

Example with Strings
--------------------

>  _class introStrings_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _String course = new String();_  
>  _double number = 1.124;_  
>  _String title\[\] = new String\[3\];_
> 
>  _title\[0\] = "Computer" + "-";_  
>  _title\[1\] = "Aided";_  
>  _title\[2\] = " Engineering";_
> 
>  _course = number + ": ";_  
>  _for(int i=0 ; i\<title.length ; i++)_  
>  _course += title\[i\];_  
>  _System.out.println(course);_  
>  _}_  
> _}_  
>  

 _**Output:**_

> _1.124: Computer-Aided Engineering_

{{< anchor "5" >}}{{< /anchor >}}5\. Packages
---------------------------------------------

A _package_ essentially defines a certain namespace, allowing functions in different packages to use same names. A package is used to group together a collection of related classes and interfaces.

Every class in Java® belongs to a package, either the one specified at the top in a package statement or the default package. Everything in the java.lang package is by default imported in any Java® program, and therefore, it does not need to be imported.

A package is created by using a package statement in the java® source code file. The statement is the keyword package followed by the name of the package. Then, everything defined after that point is considered to belong to that package. When a Java® source code file is compiled the resulting class file(s) is (are) created in the directory specified by the package statement. An extra option to the javac compiler (javac -d \<directory> \<myProgram.java>) can be used to specify where to create all subdirectories according to the package statement. To enable the use of any new packages it may be necessary to properly setup the CLASSPATH environment variable. The latter variable indicates where to search for user-developed packages.

The classes defined in a package can be used in a program using an import statement. This statement consists of the keyword import followed by the name of the package to be inserted. The import statement specifies to the Java® compiler the location of the classes enabling the use of shorter names for each imported class. No import statements are required if the class files that are used in a Java® program are in the same directory that the class that uses them is located.

A class for which a package name has not been specified belongs to the default package. The default package is without a name and it is always imported by default.

The Core Java® API provides a collection of packages that can be used.

6{{< anchor "6" >}}{{< /anchor >}}. Interfaces
----------------------------------------------

_Interfaces_ are similar to classes, but they contain only declarations of methods. An interface declares sets of constants and functions, without providing implementations for any of them. They are used to declare methods that should be supported by a class without, however, to actually implement these functions. In particular, interfaces may contain public abstract methods and public final static data.

Any class that implements an interface must provide the actual implementation for any functions that have been declared in the interface. Such a class is said to implement the interface. If even one function is left unimplemented the class is considered to be abstract.

A class is specified to implement an interface using the keyword _implements_. A class can implement more than one interfaces, although it cannot extent more than one class. However, a class that implements an interface must provide implementations for all of the functions of the interface.

In addition interfaces can be extended using the keyword _extends_.

 Example with Interfaces

>  _interface Geometry_  
> _{_  
>  _public void print();_  
> _}_
> 
> _class Point implements Geometry_  
> _{_  
>  _private double x, y;_
> 
>  _Point()_  
>  _{_  
>  _x = y = 100.0;_  
>  _}_  
>  _Point(double x, double y)_  
>  _{_  
>  _this.x = x;_  
>  _this.y = y;_  
>  _}_
> 
>  _public void print()_  
>  _{_  
>  _System.out.print(" x = " + x + "   y = " + y );_  
>  _}_  
> _}_  
>  
> 
> _class introInterfaces_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Point p1;_  
>  _p1 = new Point();_  
>  _Point p2 = new Point(2.2, 0.44);_
> 
>  _System.out.print("\\n p1: ");_  
>  _p1.print();_  
>  _System.out.print("\\n p2: ");_  
>  _p2.print();_  
>  _System.out.println();_  
>  _}_  
> _}_

  
**_Output:_**

>  _p1:  x = 100.0   y = 100.0_  
>  _p2:  x = 2.2   y = 0.44_

{{< anchor "7" >}}{{< /anchor >}}7\. Nested Classes and Nested Interfaces
-------------------------------------------------------------------------

A nested class is a class defined within another class. Similarly Java® allows nested interfaces, i.e. interfaces which are members of another interface.

The simplest nested class is a static nested class which is a class with a name provided inside another class with the specifier static used at its declaration. Since it is a member of the class the access level can be set using the access specifiers. Outside the class someone refers to the nested class by the name of the class in which it is nesting followed by a dot and the name of the nested class.

A non-static nested class is called an inner class and it is associated with a particular instance of the class rather than the entire class. When an object of an inner class is created an enclosing object, of the "outer" class is, in general, associated with that object. Inner classes cannot have static members. A local inner class is an inner class that is not a member of a class but it is defined in a function of a class and, therefore, it is local to the function.

A nested class, non-static nested or inner class, can use any member of its enclosing class without the need for qualification and with access to all members, including the private ones. However, a static nested class can access only the static members of the enclosing class, since it is not associated with any particular object.

In some cases, e.g. handling AWT events, there is no reason for naming an inner class. In those cases, an anonymous class is preferable to be used if the class is only for a single use. An anonymous class is an inner class without a name that is defined at the point where it is needed rather somewhere within the class with a name.

Nested interfaces can only be static since an interface cannot have an implementation.

8\. {{< anchor "8" >}}{{< /anchor >}}Garbage Collection
-------------------------------------------------------

Java® provides a _garbage collector_ which takes care of dynamic memory deallocation. As soon as Java® objects become unreferrenced the corresponding memory may automatically reclaim it. The garbage collector periodically destroys any unused object in dynamic memory, typically only when running out of memory. In Java® there is no need of explicit dynamic memory release and, therefore, the danger of memory leak is reduced.

A mark-sweep algorithm is used by the garbage collector. First, the dynamic memory is scanned for referenced objects and then all remaining objects are treated as garbage. Any object that is not referenced in any way is eligible for garbage collection. An object that is only referenced by objects that are also unreferrenced is considered unreferrenced and is eligible for garbage collection. An object is considered unreferrenced when any references that used to refer to it have changed, referring to another object or to null, or if there has been a return from a function in which the local references used to refer to the object. However, a memory leak is still possible when references are kept to objects that are no longer needed.

Prior to the actual memory deallocation of memory for an object, the object's **finalizer**, i.e. a function named _finalize_, is invoked. This process know as finalization, allows the object to perform a cleanup of any associated system resources. It is typically used to reclaim external resources that have been allocated, e.g. to make sure that files that have been opened are properly closed. The finalize() function is inherited from the Object class and can be overridden. It is allowable to use _try-catch_ in a finalize function to handle exceptions that may result from function calls within its body. In general, the last thing that a _finalize()_ method should do is to call _super.finalize()_ to give the superclass the chance to finalize itself, since the superclass finalize is overridden.

The garbage collection may be performed at any time and in any order according to efficiency considerations of the garbage collector. However, it is possible to explicitly request finalization and garbage collection using the System.runFinalization() and System.gc() commands, respectively.

{{< anchor "9" >}}{{< /anchor >}}9\. Applets
--------------------------------------------

An applet inherits functionalities that allow it to run in a Java®-enabled browser. Although applets do not need to implement a main method, every applet has to implement at least one of the _init_, _start_, or _paint_ methods that inherits from its superclass. For AWT, the class Applet that is provided in the package java.applet of the Application Programming Interface (API) is inherited by any applet. For Swing applets the class JApplet is inherited by any applet. Class JApplet extends the AWT Applet class and implements the Accessible and RootPaneContainer interfaces.

A **Java® applet** is based on a set of conventions and functionalities that are inherited allowing it to be executed in an appletviewer or any Java® enabled browser. An _html_ file needs to be used so as to load the class from a Java® enabled browser, or using the appletviewer provided with the Java® Development Kit (JDK). The class file of an applet can be loaded and interpreted in any Java® enabled browser, or the appletviewer, using an _html_ file. The _html_ code is used to specify at least the location and the dimensions of the applet to be loaded. When a Java®-enabled browser, or the appletviewer, encounters an \<APPLET> tag, it reserves a display area according to the specified width and height for the applet, loads the bytecodes for the specified subclass of **Applet**, then, creates an instance of that subclass. Finally, it calls the applets _init()_ and _start()_ methods. The execution of the applet can be customized using the options that the \<APPLET> tag provides. When the applet needs to use a class, the browser, first,  tries to find the class on the host that's running the browser, and if it cannot find, it searches for it in the same place from where the Applet subclass bytecode came from in order to create that applet's instance.

An AWT applet inherits, since it _extends_ it, the **Applet** class provided by the java.applet package of the Java® Core API. The **Applet** class extends the AWT (Abstarct Window Toolkit) Panel class, which itself extends the Container class (which provides the ability to include other components and using a layout manager to control the size and position of those components). The latter extends the Component class (which provides the drawing and handling events capabilities). _Swing applets_ extend the JApplet class, which is a subclass of the AWT Applet class and implements the Accessible and RootPaneContainer interfaces.

As soon as an applet (i.e. an instance of an Applet subclass) is loaded, that instance of the _Applet_ subclass is created, the applet initializes itself (i.e. method _init()_ is called), and starts running (i.e. method _start()_ is invoked). If the user leaves from the page with an applet, or icognify the window that contains an applet, the applet has the chance to stop itself. In case of returning to that page, or opening the icognified window, the applet can start itself again. Upon quitting a browser that shows an applet, or in general unloading an applet, the applet has the chance to stop itself (i.e. call the method _stop())_ and do final cleanup (i.e. call the method _destroy()_).  
  
It is preferable to put the code for initialization of an object of an _Applet_ subclass in the _init()_ method instead of using a constructor, which, in general, should be avoided. The code to be executed by an applet after its initialization should be put in the _start()_ method. The code to stop that execution should be provided in the _stop()_ method.

The main display method of an applet is the_paint()_  method which is inherited by the _Panel_ class and can be overridden. This method is invoked when the applet needs to draw itself to the screen. Method _update()_ can also be overridden to improve the quality and performance of the drawing.

Any Applet subclass must provide at least one of the _init()_, _start()_, and _paint()_ methods.

In general, due to **_security_** considerations, an applet cannot read and write files, or start any program on the host that's executing it. It, also, cannot make network connections except to the host from where it was loaded and it cannot read certain system properties. On the other hand, applets have some additional capabilities that are not available to applications. The _Applet_ API enables an applet to load data files specified relative to the URL of the applet or the page in which the applet is running, force the browser to display a document, find and communicate with other applets running in the same page, play sounds, etc.

Since the _Applet_ class is a subclass of the _Panel_ class, which provides drawing and event-handling capabilities, it is easy to create a GUI (graphical interface), or, in general, to use graphical compontents. An applet does not have to create a window to display itself in, since it can display itself within the browser window.

An applet can have its own threads allowing it to create and use its own threads to perform time-consuming tasks. In most cases, a browser, in which an applet is loaded, allocates a thread, or a thread group, for the applet. The drawing methods of an applet (i.e. _paint()_ and _update()_) are called from the AWT drawing thread.

When implementing **_Swing_** applets, the _JApplet_ class should be used instead of the _Applet_ class in order to avoid problems due to mixing of _AWT_ and **_Swing_** components. Similarly, when implementing Swing applications the _JFrame_ should be used instead of the _Frame_ class.