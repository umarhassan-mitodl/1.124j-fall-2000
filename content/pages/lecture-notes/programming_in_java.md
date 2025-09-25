---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Programming in Java
uid: 9a014f7b-64b4-0939-8660-891239c1a00a
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Introduction](#1)
2.  [Online Java® Resources](#2)
3.  [Applications and Applets](#3)
4.  [Java® Basics](#4)

{{< anchor "1" >}}{{< /anchor >}}1\. Introduction
-------------------------------------------------

Java® is an object-oriented programming language that resembles C++ in many respects. One of the major differences is that Java® programs are intended to be architecture-neutral i.e. a Java® program should, in theory, be able to run on a Unix® workstation, a PC or a Macintosh® _without recompilation._ In C++, we compiled our programs into machine-dependent _object code_ that was linked to produce an executable. By contrast, Java® programs are compiled into machine-independent _byte code_. The compiled program is then run within a Java® interpreter, which is responsible for executing the byte code instructions. The Java® interpreter is typically referred to as the _Java® Virtual Machine_, and it must be present on each computer that runs the program.  
 

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}



{{< tdclose >}}
{{< tdopen >}}


Java® compiler


{{< tdclose >}}
{{< tdopen >}}



{{< tdclose >}}
{{< tdopen >}}


Java® interpreter


{{< tdclose >}}
{{< tdopen >}}



{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}


_myprog.java_


{{< tdclose >}}
{{< tdopen >}}


\-------------->


{{< tdclose >}}
{{< tdopen >}}


_myprog.class_


{{< tdclose >}}
{{< tdopen >}}


\---------------->


{{< tdclose >}}
{{< tdopen >}}


Program output


{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}



{{< tdclose >}}
{{< tdopen >}}


_javac_


{{< tdclose >}}
{{< tdopen >}}



{{< tdclose >}}
{{< tdopen >}}


_java_  
_appletviewer_  
_netscape_


{{< tdclose >}}
{{< tdopen >}}



{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

Follow this link to see Sun Microsystems' overview: [About the Java® Technology](http://java.sun.com/docs/books/tutorial/getStarted/intro/definition.html)

It takes time to learn everything about Java® and it is important to set your expectations accordingly. There are two main challenges:

*   Learning the basic syntax of the language.
*   Gaining familiarity with the libraries of reusable software components that are available to Java® programmers, especially the commonly used parts of the Java® Core API (Application Programming Interface).

In the lectures that follow, we will attempt to familiarize you with the basic syntax, and point out the syntactic and semantic differences between Java® and C++. We will also introduce you to some of the more important class libraries. The Java® API is well documented and you should quickly learn how to navigate the online documentation to find the classes that you need.

The Java® language is still evolving. We will be using the Java® 2 platform, which is also known as the Java® Development Kit (JDK). The latest release is Java® 2 version 1.3. Be prepared to encounter bugs in the implementation of the language from time to time. This includes inconsistencies across hardware platforms. Also note that the latest version of Java® is not supported by the Netscape® browser.

{{< anchor "2" >}}{{< /anchor >}}2\. Online Java® Resources
-----------------------------------------------------------

Here is an online Java® tutorial.

*   [Java® tutorial](http://java.sun.com/docs/books/tutorial/)  
    

{{< anchor "3" >}}{{< /anchor >}}3\. Applications and Applets
-------------------------------------------------------------

An _application_ is a stand-alone program that executes independently of a browser. It is usually launched from the command line, using the command line interpreter, _java_.

An _applet_ is a program that can be embedded in an HTML page. The program can be run by loading the page into a Java®-enabled browser. The JDK includes a tool, called _appletviewer_, that can also be used to view applets.

A Java® program can be designed to function

*   as an application
*   as an applet
*   both as an application and as an applet

The Hello World Application
---------------------------

Here is an example of a simple Java® application. We make our program an application by writing a class, _HelloWorldApp_, that contains a function named _main()_. We can compile our program by typing

 _javac HelloWorld.java_

This will produce a file named _HelloWorldApp.class_.

We can run the program as application by typing

 _java HelloWorldApp_

The command line interpreter looks for a function named _main()_ in the _HelloWorldApp_ class and then executes it.

_Points to Note_

The _.class_ file gets its name from the name of the class and not the name of the source file. In this example we deliberately gave the source file a different name, but in practice, we will place each class in a separate file with the same name. This convention becomes important when we want to write a class that is publicly accessible.  
 

Global functions are not allowed in Java®. This is why we placed our _main()_ function inside our class. We must make our _main()_ function _static_, since it should not be associated with a particular object, and we must also make it _public_, since it is the entry point to our program.

**HelloWorld.java**

_class HelloWorldApp {_  
 _public static void main(String\[\] args) {_  
 _System.out.println("Hello World!");_  
 _}_  
_}_

The Hello World Applet

Here is an example of a simple Java® applet. We make our program an applet by writing a class, _HelloWorld_, that inherits the _JApplet_ class provided in the Java® Swing API. The _extends_ keyword declares that class _HelloWorld_ inherits class _JApplet_. Before we can refer to the _JApplet_ class, we must declare its existence using the _import_ keyword. Here we have imported the _JApplet_ class, which belongs to the _javax.swing_ package, and we have also imported the _Graphics_ class, which belongs to the _java.awt_ package.

The _JApplet_ class possesses a method named _paint()_, which it inherits from one of its superclasses. Our _HelloWorld_ class inherits this _paint()_ method when it inherits the _JApplet_ class. The purpose of _paint()_ is to draw the contents of the applet. Unfortunately, the default _paint()_ method that we inherit cannot do anything useful since it has no way of knowing what we want to draw. We must therefore _override_ the default _paint()_ in our _HelloWorld_ class. (Note that while C++ requires the use of the _virtual_ keyword to indicate function overriding, Java® does not require us to inform the compiler that overriding will take place.)

The _paint()_ method receives as an argument a _Graphics_ object, which contains information about where and how we can draw. In this example, we choose to draw the text "Hello World!" at coordinates (50,25) by calling the _drawString_ method.

We can compile our program by typing

    _javac HelloWorld.java_

This produces a file named _HelloWorld.class_. We now embed our applet in an HTML file, _Hello.html_, and we can run it by typing

    _appletviewer Hello.html_

We can also view Hello.html in a Java®-enabled browser.  
 

**HelloWorld.java**

_import javax.swing.JApplet;_  
_import java.awt.Graphics;_

_public class HelloWorld extends JApplet {_  
 _public void paint(Graphics g) {_  
 _g.drawString("Hello world!", 50, 25);_  
 _}_  
_}_  
 

**Hello.html**

_\<HTML>_  
_\<HEAD>_  
_\<TITLE> A Simple Program \</TITLE>_  
_\</HEAD>_

_\<BODY>_  
_Here is the output of my program:_  
_\<APPLET CODE="HelloWorld.class" WIDTH=150 HEIGHT=25>_  
_\</APPLET>_  
_\</BODY>_  
_\</HTML>_ 


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

{{< anchor "4" >}}{{< /anchor >}}4\. Java Basics
------------------------------------------------

_Java Data Types_

Java® has two main categories of data types: _primitive_ data types and _reference_ data types. Java® does not support the notion of pointers.

Here is a list of primitive data types.

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
PRIMITIVE DATA TYPE
{{< thclose >}}
{{< thopen >}}
SIZE IN BYTES / FORMAT
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
byte
{{< tdclose >}}
{{< tdopen >}}
1
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
char, short
{{< tdclose >}}
{{< tdopen >}}
2
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
int, float 
{{< tdclose >}}
{{< tdopen >}}
4
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
long, double
{{< tdclose >}}
{{< tdopen >}}
8
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
boolean
{{< tdclose >}}
{{< tdopen >}}
true or false
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

  

Reference data types include arrays and classes. Here is an example of a Line class.

**Line.java**

_class Line {_

 _private int miX1, miX2, miY1, miY2;_

 _public Line() {_  
 _miX1 = miX2 = miY1 = miY2 = 0;_  
 _}_

 _public Line(int iX1, int iX2, int iY1, int iY2) {_  
 _miX1 = iX1;_  
 _miX2 = iX2;_  
 _miY1 = iY1;_  
 _miY2 = iY2;_  
 _}_  
_}_

Creating Objects - Constructors
-------------------------------

In Java®, objects of user defined data types must be dynamically created. In the following example, the first statement declares a _Line_ object, but does not actually create it. The second statement uses the _new_ operator to actually create the object. Note the subtle differences between Java® and C++.

_Line line;                        // Declaration of object (does not create object.)_  
_line = new Line();            // Instantiation of object._

Garbage Collection and Finalization
-----------------------------------

The Java® runtime system provides a _garbage collector_, which periodically destroys any unused objects in dynamic memory. The Java® garbage collector uses a _mark-sweep_ algorithm. The dynamic memory is first scanned for referenced objects and then all remaining objects are treated as garbage. Prior to deleting an object, the garbage collector will call the object's _finalizer,_ which allows the object to perform an orderly cleanup of any associated system resources, such as open files.

Finalization and garbarge collection happen asynchronously in the background. It is also possible to force these tasks to occur using the _System.runFinalization()_ and _System.gc()_ commands.

A finalizer has the form

 _protected void finalize() throws Throwable {_  
 _..._  
 _// Clean up code for this class here._  
 _..._  
 _super.finalize();  // Call the superclass's finalizer (if provided.)_  
 _}_

Inheritance
-----------

As indicated above, the _extends_ keyword allows us to write classes that inherit the properties and methods of another class.

 _class SubClassName extends SuperClassName {_  
 _..._  
 _}_

If a superclass name is not specified, the superclass is assumed to be _java.lang.Object_. Also, note that each class can have only one immediate superclass i.e. Java® does not support multiple inheritance.

Packages
--------

A package is a group of related classes or interfaces. Each package defines its own namespace. Thus, two different packages may contain classes with the same name.

We can create a package by placing a _package_ statement at the top of every source file that defines a class belonging to the package. We may later use the classes in the package by placing an _import_ statement at the top of the source file that needs to access the classes in the package.  
 

**graphics/Line.java** (Path of the file is relative to the CLASSPATH environment variable.)

 _package graphics;       // Class Line belongs to package graphics._

 _public class Line {      // The public class modifier makes this class accessible outside the package._  
 _..._  
_}_

**MyTest.java**

_import graphics.\*;     // Provides access to all public classes in package graphics._

_class MyTest {_  
 _public static void main(String\[\] args) {_  
 _Line line;_  
 _graphics.Line line2;   // Can be used for conflict resolution if two packages have a Line class._  
 _line = new Line(0,0,3,4);_  
 _line2 = new Line();_  
 _}_  
_}_  
 

If a package name is not specified for a class, then the class belongs to the default package. The default package has no name and it is always imported.

Here are a few of the core Java® packages:

*   java.lang            - core Java® language.
*   java.io               - input/output streams.
*   java.util             - utility classes, e.g. Stack, Vector, Hashtable, Oberserver/Observable.
*   java.net             - networking classes.
*   java.security      - security classes.
*   javax.swing       - Swing Graphical User Interface (GUI) components (the new preferred way).
*   java.awt            - Abstract Window Toolkit GUI components (the old way).
*   java.awt.image  - image processing.

Member Access Specifiers
------------------------

There are four types of member access levels: _private_, _protected_, _public_ and _package_. Note that, unlike C++, we must specify access levels on a per-member basis.

_class Access {_  
 _private privateMethod();                      // Access level is "private"._  
 _protected protectedMethod();               // Access level is "protected"._  
 _public publicMethod();                        // Access level is "public"._  
 _packageMethod();                               // Access level is "package"._  
_}_

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
ACCESS SPECIFIER
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY CLASS DEFINITION
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY SUBCLASS DEFINITION
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY REST OF PACKAGE
{{< thclose >}}
{{< thopen >}}
ACCESSIBLE BY REST OF WORLD
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
none i.e. package  

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

  

Instance and Class members
--------------------------

As in C++, we can have instance members or class members. A class member is declared using the _static_ keyword.

_class MyPoint {_  
 _int x;_  
 _int y;_  
 _static int x\_origin;_  
 _static int y\_origin;_  
_}_

In this example, every object has its own _x_ member, however, all objects share a single _x\_origin_ member. 

Constant Members
----------------

A _final_ variable is one whose value cannot be changed e.g.

_class Avo {_  
 _final double AVOGADRO = 6.023e23;_  
_}_

Class Modifiers
---------------

We have already seen some examples of member modifiers, such as _public_ and _private_. Java® also allows us to specify class modifiers.

*   A _public_ class is one which can be used by objects outside the current package e.g. _package graphics;       // Class Line belongs to package graphics._
    
    _public class Line {      // The public class modifier makes this class accessible outside the package._  
     _..._  
    _}_  
     
    
*   An _abstract_ class is one which cannot be instantiated, and must be subclassed instead. An abstract class may contain abstract methods i.e. methods with no implementation, however, it may also provide default implementations for other methods.  e.g.
    
      
    _abstract class GraphicObject {_  
     _int x, y;_  
     _..._  
     _void moveTo(int newX, int newY) {_  
     _..._  
     _}_  
     _abstract void draw();  //  This means that the class must be made abstract._  
    _}_
    
    _class Circle extends GraphicObject {_  
     _void draw() {_  
     _..._  
     _}_  
    _}_  
     
    
*   A _final_ class is one which cannot be subclassed. This may be required for security or design reasons. e.g.
    
      
    _final class String {_  
     _..._  
    _}_
    
    It is also possible to make individual methods final.