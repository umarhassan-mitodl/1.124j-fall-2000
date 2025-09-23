---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 6
uid: 43cea051-41df-eac9-11ce-e5258adb4160
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).
------------------------------------------------------------------------------

Topics
------

1.  [Introduction to Java®](#1)
2.  [Compiling and running a Java® application and a Java® applet](#2)
3.  [Data types](#3) 
4.  [Variables, declarations, initializations, assignments](#4)
5.  [Operators, precedence, associativity, type conversions, and mixed expressions](#5)
6.  [Control structures](#6)
7.  [Comments](#7) 
8.  [Arrays](#8) 
9.  [Classes and Objects](#9)
10.  [Constructors](#10) 
11.  [Initializers](#11) 
12.  [Member data and functions](#12) 
13.  [Function overloading](#13)

{{< anchor "1" >}}{{< /anchor >}}1\. Introduction to [Java®](http://java.sun.com/)
----------------------------------------------------------------------------------

Java® is an Object-Oriented Programming (OOP) language, which is similar to C++ but with certain characteristics that allow the simple development of portable programs with graphics and graphical user interfaces. The provided classes allow very simple and efficient development of complicated programs that can be executed in any machine irrespectively of the operating system, as long as it supports Java®. You can read more about ["what is Java®"](http://java.sun.com/docs/books/tutorial/getStarted/intro/definition.html) in the relevant paragraph of the [Java® Tutorial,](http://java.sun.com/docs/books/tutorial/) provided by Sun.

The _portability_ of Java® programs is based on the Java® Virtual Machine (Java® VM) and the intermediate compilation into bytecode. The bytecode can, then, be interpreted by the Java® VM, which translates the bytecode instructions into machine instructions that your computer can understand and execute.

The Java® platform consists essentially by the Java® VM, which takes care of the compilation and interpretation issues (e.g. portability), and by the Java® API, which provides a large collection of software components that can be directly used by a Java® programmer. You can read more about it in the on-line paper ["The Java® Platform",](http://java.sun.com/docs/white/platform/javaplatformTOC.doc.html) by Douglas Kramer.

The [Application Programming Interface (API)](http://java.sun.com/j2se/1.3/docs/api/index.html)provides several classes that can be used to efficiently write programs with graphics content and graphical user interfaces. The latter can be achieved with C++ only by combining it with graphic libraries such as Open Inventor or OpenGL, and with toolkit libraries such as TCL and TK.

In addition, Java® facilitates the development of programs that deal with networking, security issues, databases, 3D graphics, and many other issues that a typical high level language, such as C++,  does not provide.

The following are good references to learn Java®:

*   [The Java® Tutorial](http://java.sun.com/docs/books/tutorial/). Mary Campione and Kathy Walrath. 2nd edition.
*   _Core Java®._ Gary Cornell and Cay Horstmann. 2nd edition.
*   _The Java® programming language._ Ken Arnold and James Gosling. 2nd edition.
*   _Java®: How to program._ Deitel & Deitel. 2nd edition.
*   [Java_®_ 2 Platform API, v 1.3](http://java.sun.com/j2se/1.3/docs/api/index.html)

If you are interested to read more about Java® you can find more information in the following on-line paper by James Gosling and Henry McGilton:

*   "[The Java® Language Environment - A White Paper](http://java.sun.com/docs/white/langenv/)." May 1996.

You can find more information about Java® in the [Sun's Java® page](http://java.sun.com/).

{{< anchor "2" >}}{{< /anchor >}}2\. Compiling/Running a Java® Application/Applet
---------------------------------------------------------------------------------

Java® is a pure Object Oriented Programming (OOP) language. Any Java® program is built from classes. C++ can be used as an OOP language but not necessarily since someone can use it to develop non-object oriented programs.

The simplest, probably, Java® program is a Java® application which prints a message. A Java® application is a Java® program that can be executed independently without the need of any browser.

The following java program is written in a file named _welcome.java":_

_welcome.java_

> _class Welcome_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _System.out.println("Welcome to 1.124");_  
>  _}_  
> _}_

  
Because global functions are not allowable in Java® we need to provide the _main()_ function in a class. In addition, we need to make it _public_ so as to be accessible, and _static_ so as to be a class function rather than being a function associated with a certain instance of the class. The _main_ function must have a single parameter of type [String](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.String.html#_top_)\[\] and must return nothing (i.e. being _void_). Any class can have its own _main_ function.

To compile a java program the java compiler [javac](http://java.sun.com/j2se/1.5.0/docs/tooldocs/solaris/javac.html) is used as follows:

_javac welcome.java_

This command generates the bytecode for the classes that are defined in the Java® program. In this case, it generates the file _Welcome.class_ which contains the bytecode for the class _Welcome_. The name of the file with the bytecode is constructed from the name of the class plus the extension _class_. The bytecode is instructions for the _Java_® _Virtual Machine_. These instructions are the same for any type of machine or operating system. To run the program, the Java® interpreter needs to be used to interpret the Java® bytecode into instructions of the specific machine on which the program is running.  
  
The command to run a Java® program is as follows, using the [java](http://java.sun.com/developer/onlineTraining/new2java/overview.html) interpreter:

_java Welcome_

Then, the class _Welcome_ is loaded and interpreted printing out the following:

Welcome to 1.124

Some programming languages, such as Basic, also use an interpreter, which makes the development and the debugging of the programs faster and more efficient. However, most high level languages use a compiler and not an interpreter, while Java® uses both. The bytecode files can, in general, run in  any machine with any operating system, as long as the proper interpreter is available. However, the execution of such interpreted programs is relatively slow.

Many other programming languages, such as C/C++, are using a compiler, which translates the source code files into machine instructions. Although the execution of compiled programs is much faster, the executable cannot run on a machine with a different architecture, since it recognizes a different set of instructions.

Java® combines both a compiler and an interpreter. The compiler (_javac_) compiles the Java® source code files into bytecode, and the interpreter (_java_) is used every time the program is executed to translate the bytecode (i.e. the Virtual Machine instructions) to the specific machine instructions and execute them. This way Java® programs can run on any type of computer and under any operating system assuming that the Java® interpreter is available and can be used on that machine. However, Java® programs are, in general, slower than compiled programs (e.g. C++ executable programs) since interpretation takes place before execution.

[Java® Development Kit (JDK)](http://java.sun.com/docs/books/tutorial/overview/index.html)also provides an [appletviewer](http://java.sun.com/products/jdk/1.1/docs/tooldocs/solaris/appletviewer.html) to check and run applets, a debugger named [jdb](http://java.sun.com/products/jdk/1.2/docs/tooldocs/solaris/jdb.html) to debug Java® programs, and several other tools that help in the development and documentation of Java® programs.

_Java_® _applications_ are stand alone Java® programs that can be executed without the need of a browser, while the _Java_® _applets_ run within a Java® compatible browser. The execution of any Java® application begins with the main method of the corresponding class, i.e.. the class with which the Java® interpreter was invoked. The above example is a Java® application, while the following is a simple Java® applet.

A _Java_® _applet_ is based on a set of conventions and functionalities that are inherited that allows it to be executed in an appletviewer or any Java® enabled browser. The source code for the applet is provided below, followed by the _html_ file that needs to be used so as to load the class from a Java® enabled browser, or using the appletviewer provided with the Java® Development Kit (JDK).

An [applet](http://java.sun.com/applets/index.html) inherits (extending) the [Applet](http://java.sun.com/products/jdk/1.1/docs/api/java.applet.Applet.html#_top_) class provided by the [java.applet](http://java.sun.com/products/jdk/1.1/docs/api/java.applet.Applet.html#_top_) package of the Java® Core API. Here, the AWT Applet is used, mostly for historical reasons. Today, the Swing JApplet is preffered in most cases. In the following example the function _paint()_, which is inherited, is overridden by the new definition. This function is used to draw the applet in the browser, or the appletviewer.

myApplet.java:

> _import java.applet.Applet;_  
> _import java.awt.Graphics;_
> 
> _public class myApplet  extends Applet_  
> _{_  
>  _public void paint(Graphics g)_  
>  _{_  
>  _g.drawString("Welcome to 1.124", 50, 35);_  
>  _}_  
> _}_  
>  

The above program is compiled using the [javac](http://java.sun.com/docs/books/tutorial/getStarted/application/) compiler, i.e. executing the command:

>         _javac myapplet.java_

The resulting file with the bytecode is the _myApplet.class_ which takes its name from the name of the class. This file can be loaded and interpreted in any Java® enabled browser, or the appletviewer, using an _html_ file.

The _html_ code is used to specify at least the location and the dimensions of the applet to be loaded.

myApplet.html:

> \<HTML>
> 
>  \<HEAD>  
>  \<TITLE> A simple program to run a Java Applet\</TITLE>  
>  \</HEAD>
> 
>  \<BODY>  
>     Here is the class myApplet is loaded:  
>    \<APPLET CODE="myApplet.class" WIDTH=150 HEIGHT=100 align=center>  
>    \</APPLET>  
>  \</BODY>
> 
> \</HTML>

  
It is possible to write a Java® program that can work both as an applet and as an application.

You can, also, find detailed instructions on how to write your first Java® program at the [Lesson: "Your First Cup of Java®"](http://java.sun.com/docs/books/tutorial/getStarted/cupojava/index.html) of the on line [Java® Tutorial](http://java.sun.com/docs/books/tutorial/), which is provided by SUN.

{{< anchor "3" >}}{{< /anchor >}}3\. Data Types
-----------------------------------------------

Java® has two kinds of data types, primitive and reference data types. _Primitive data type_ variables contain a corresponding of the data type value, while _reference data type_ variables, such as arrays and classes, contain a reference to the actual set of values.

The following are the primitive (or built-in) data types:

*   _boolean_  (boolean value, true or false)
*   _char_  (2-byte, character - Unicode)
*   _byte_ (1-byte, signed integer)
*   _short_ (2-byte, signed short integer)
*   _int_ (4-byte, signed integer)
*   _long_ (8-byte, signed long integer)
*   _float_ (4-byte, floating point)
*   _double_ (8-byte, double precision floating point)

It is allowable to assign the value of a primitive data type variable from one type to another without an explicit cast if the variable that the value is assigned is on the right of the following order list.

>                                  _byte_ \< _short_ \< _int_ \< _long_ \< _float_ \< _double_

A _char_ can be promoted to an _int, long, float_ or _double._ However_,_ a _boolean_ cannot be converted to any other primitive data type, since boolean values are not considered to be numbers. The following table presents all the allowable promotions:  
 

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
DATA TYPE
{{< thclose >}}
{{< thopen >}}
ALLOWABLE PROMOTIONS
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
double
{{< tdclose >}}
{{< tdopen >}}
none
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
float
{{< tdclose >}}
{{< tdopen >}}
double
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
long
{{< tdclose >}}
{{< tdopen >}}
float, double
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
int
{{< tdclose >}}
{{< tdopen >}}
long, float, double
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
char
{{< tdclose >}}
{{< tdopen >}}
int, long, float, double
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
short
{{< tdclose >}}
{{< tdopen >}}
int, long, float, double
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
byte
{{< tdclose >}}
{{< tdopen >}}
short, int, long, float, double
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

An assignment from a "higher" order to a "lower" is allowed only when an explicit casting is used, because information may be lost from the conversion, e.g.: _int x = (int) 4.75;_

Each of  the primitive data types has a corresponding class, called _wrapper_ class, defined in the [java.lang](http://java.sun.com/products/jdk/1.1/docs/api/Package-java.lang.html) package. e.g. a _double_ primitive data type has the corresponding class [Double](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.Double.html#_top_).

4\. {{< anchor "4" >}}{{< /anchor >}}Variables, Declarations, Definitions, Initializations, and Assignments
-----------------------------------------------------------------------------------------------------------

The data type of every variable has to be specified in a definition, by preceding the name of the variable that is defined with a data type. A data type can be one of the built-in (primitive) data types, one of the data types defined in the provided Java® packages, or the user defined data type. The name of a variable must be a legal identifier and it should not be the same with any other variable that is defined in the same scope.

The scope of a variable is where the variable is accessible. It is specified by the location where the variable is defined. There are 4 different scope categories:

1.  _local variables_: variables defined anywhere in a function
2.  _member variables_: data members of a class (static or non static)
3.  _function parameters_: parameters of functions in which values are passed when invoking the function
4.  _exception-handler parameters_: parameters of exception-handlers in which values are passed when the exception handler is called.

Local variables are undefined prior to initialization. Therefore, a local variable must be either initialized or assigned a value before being used. The scope of a local variable is from the point where it has been defined up to the end of the code block in which it has been defined. The memory allocated for a local variable is automatically be reclaimed when control goes out of its scope, upon exiting the function in which it is defined.

The scope of a function or an exception-handler parameter is the entire corresponding function.

A named constant can be defined using the keywords _static_ and _final._ Static indicates that it is a class variable, while final indicates that its value cannot be changed after it has been initialized.

>                 e.g.: static final double PI = 3.1414926

5\. {{< anchor "5" >}}{{< /anchor >}}Operators, Precedence, Associativity, Type Conversions, and Mixed Expressions
------------------------------------------------------------------------------------------------------------------

Java® has the following categories of operators. Some of them can be used as either unary or binary. Also in Java® the corresponding from the C++ conditional operator is a tertiary operator, i.e. having 3 operands.

*   arithmetic: + , - , \*, / , %
*   shorthand arithmetic: ++ , --
*   relational:  > , \< , >= , \<= , == , !=, instanceof
*   conditional: && , || , ! ,  &, |
*   assignment:  =
*   shorthand assignment: += , -= , \*=  , /= , %=, etc.
*   bitwise and logical operators: >> ,\<\< , etc.
*   conditional operator: (logical Test) ? trueStatement : falseStatement

The order in which the operations in expressions are performed is decided according to the _precedence_ and _associativity_ rules, which are the same as in C++. According to any precedence table, the operators of higher precedence are evaluated first, before operators with lower precedence.

The following _precedence_ table (copied from the Java® Tutorial) lists the operators according to their precedence order. Higher precedence operators are evaluated before lower precedence operators.

{{< tableopen >}}
{{< tropen >}}
{{< tdopen >}}
postfix operators
{{< tdclose >}}
{{< tdopen >}}
\[\] . (params) expr++ expr--
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
unary operators
{{< tdclose >}}
{{< tdopen >}}
++expr --expr +expr -expr ~ !
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
creation or cast
{{< tdclose >}}
{{< tdopen >}}
new (type)expr
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
multiplicative
{{< tdclose >}}
{{< tdopen >}}
\* / %
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
additive
{{< tdclose >}}
{{< tdopen >}}
\+ -
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
shift
{{< tdclose >}}
{{< tdopen >}}
\<\< >> >>>
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
relational
{{< tdclose >}}
{{< tdopen >}}
\< > \<= >= instanceof
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
equality
{{< tdclose >}}
{{< tdopen >}}
\== !=
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
bitwise AND
{{< tdclose >}}
{{< tdopen >}}
&
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
bitwise exclusive OR
{{< tdclose >}}
{{< tdopen >}}
^
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
bitwise inclusive OR
{{< tdclose >}}
{{< tdopen >}}
|
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
logical AND
{{< tdclose >}}
{{< tdopen >}}
&&
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
logical OR
{{< tdclose >}}
{{< tdopen >}}
||
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
conditional
{{< tdclose >}}
{{< tdopen >}}
? :
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
assignment
{{< tdclose >}}
{{< tdopen >}}
\= += -= \*= /= %= &= ^= |= \<\<= >>= >>>=
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

For operators on the same line, that have equal precedence, _associativity_ decides which operator to be executed first. In Java® all operators, except the assignment operators, have left associativity.

6\. {{< anchor "6" >}}{{< /anchor >}}Control Structures
-------------------------------------------------------

Control structures, similar to those of C++, are used to specify the flow of control in Java® programs.

A block of statements, i.e. statements within curly braces, may appear instead of a single statement.

The following are the control structures of Java®:

*   Selection control structures

            _if_(logical test)  
              statement;  
 

            _if_(logical test)  
                statement;  
           _else if_(logical test)  
                statement;  
           _else_  
               statement;  
 

            _switch_(variable)  
                {  
                    case value1:  
                         statements  
                         break;  
                    case value3:  
                         statements  
                         break;  
                    case value4: case value5:  
                         statements  
                         break;  
                    default:  
                         statements  
                 }

*   Repetition control structures (looping)

          _for_(intialization ; logical test; modification)  
                  statement;  
 

          _while_(logical test)  
               statement;  
 

         _do_  
             {  
               statements;  
              } _while(logical test);_

Java® provides the _break_ and _continue_ as branching statements. The former cause the exit from the block of statements in which it resides, while the latter causes the flow of control to be transfer to the next iteration. There are also labeled versions of break and continue in which labels are used  where the control is transferred to the block with the specified label. The _labeled break_ and the _labeled continue_ are useful in nested loops. A _return_ statement also is used to return form a function, passing control to the invoking function.

{{< anchor "7" >}}{{< /anchor >}}7\. Comments
---------------------------------------------

Java® supports 3 kinds of comments. The familiar C++ kinds of comments, the pair /\* \*/ which encloses a comment and the // which indicates that the remaining of the line is a comment are supported.

In addition, Java® supports the documentation comment which is enclosed between /\*\* and \*/. Comments of this kind are used for automatically generated documentation using the _[javadoc](http://java.sun.com/products/jdk/javadoc/index.html)_ tool of the Java® Development Kid (JDK).

Having wrote a java file, such as the file Welcome1.java below, using javadoc someone can automatically create an html file corresponding to that java source code.  
  
Welcome1.java:

> _/\*\*_  
>  _\* This class can take a variable number of parameters on the command_  
>  _\* line. Program execution begins with the main() method._  
>  _\*/_  
> _public class Welcome1_  
> _{_  
>  _/\*\*_  
>  _\* The main entry point for the application._  
>  _\*_  
>  _\* @param args Array of parameters passed to the_  
>  _\* application via the command line._  
>  _\*/_  
>  _public static void main (String\[\] args)_  
>  _{_  
>  _System.out.println("Welcome to 1.124!!!!");_  
>  _}_  
> _}_

Then, the javadoc can be used to create the corresponding html file:

> _\>javadoc Welcome1.ja_  
> _Loading source file Welcome1.java..._  
> _Constructing Javadoc information..._  
> _Building tree for all the packages and classes..._  
> _Building index for all the packages and classes..._  
> _Generating overview-tree.html..._  
> _Generating index-all.html..._  
> _Generating deprecated-list.html..._  
> _Building index for all classes..._  
> _Generating allclasses-frame.html..._  
> _Generating index.html..._  
> _Generating packages.html..._  
> _Generating Welcome1.html..._  
> _Generating serialized-form.html..._  
> _Generating package-list..._  
> _Generating help-doc.html..._  
> _Generating stylesheet.css..._

{{< anchor "8" >}}{{< /anchor >}}

8\. Arrays
----------

An array is a set of values of the same data type stored together as an entity, in a contiguous part of memory, and can be accessed using an integer index.

The declaration of an array in Java does not make any memory allocation, but simply defines a reference to an array. A _new_ statement is required to make the proper allocation of memory. Then, an element of the array is accessed using an index within square brackets. An array in Java® has a _length_ field which stores the number of its elements.

The class [System](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.System.html#_top_) has a function called [arraycopy()](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.System.html#arraycopy_java_lang_Object__int__java_lang_Object__int__int_) that can be used to copy part or the whole array to another array.

A function in which an array is passed as an argument can change it, since the reference to that array is what is passed by value. An array can be returned from a function, i.e. the return data type of a function can be an array.

The length of an array is fixed upon its definition and cannot be modified. A class named [Vector](http://java.sun.com/products/jdk/1.1/docs/api/java.util.Vector.html#_top_) can be used to represent an array whose size can be modified.

An array can contain references to other arrays or objects, in which case memory for the individual members of the array must also be explicitly allocated using a new statement.

A multidimensional array can be defined using an array whose elements are arrays. If the array has the same number of columns then such an array is defined using a statement similar to the following: _double x\[\]\[\] =  new double \[n\]\[m\]_. Otherwise for each row a _new_ expression is used to dynamically allocate memory for it.

_Example of Arrays_

> _class introArrays_  
> _{_  
>  _public static final int SIZE=5;_
> 
>  _public static void main(String args\[\])_  
>  _{_  
>  _double d\[\] = new double\[SIZE\];_  
>  _int \[\] i ;_  
>  _i = new int\[SIZE\];_
> 
>  _for(int j=0 ; j\<d.length ; j++)_  
>  _d\[j\] = j/2;_  
>  _for(int j=0 ; j\<i.length ; j++)_  
>  _i\[j\] = j\*j;_
> 
>  _for(int j=0 ; j\<SIZE ; j++)_  
>  _System.out.println( "  d\[" + j + "\] = " + d\[j\]);_  
>  _for(int j=0 ; j\<i.length ; j++)_  
>  _System.out.println( "  i\[" + j + "\] = " + i\[j\]);_
> 
>  _int m=5, n=3;_  
>  _int im, in;_  
>  _double x\[\]\[\] = new double\[m\]\[n\];_
> 
>  _for(im=0;im\<m;im++)_  
>  _{_  
>  _System.out.println();_  
>  _for(in=0;in\<n;in++)_  
>  _{_  
>  _System.out.print(" " + x\[im\]\[in\] + " ");_  
>  _}_  
>  _}_
> 
>  _}_  
> _}_

  
_**Output:**_

>   _d\[0\] = 0.0_  
>  _d\[1\] = 0.0_  
>  _d\[2\] = 1.0_  
>  _d\[3\] = 1.0_  
>  _d\[4\] = 2.0_  
>  _i\[0\] = 0_  
>  _i\[1\] = 1_  
>  _i\[2\] = 4_  
>  _i\[3\] = 9_  
>  _i\[4\] = 16_
> 
>  _0.0  0.0  0.0_  
>  _0.0  0.0  0.0_  
>  _0.0  0.0  0.0_  
>  _0.0  0.0  0.0_  
>  _0.0  0.0  0.0_  
>  

In Java® you can easily have a ragged array, such as a 2-D array with rows of different lengths. When an array is created only the length of the primary array must be specified. The length of the sub-arrays can be left unspecified until they are created, as it is shown in the following example.

_Example of a Ragged Array_

> _class TriangularArray_  
>  _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _int i, j;_
> 
>  _double \[\]\[\]x;_
> 
>  _x = new double\[5\]\[\];_
> 
>  _for(i=0;i\<5;i++)_  
>  _{_  
>  _x\[i\] = new double\[i+1\];_
> 
>  _System.out.println();_
> 
>  _for(j=0;j\<i+1;j++)_  
>  _{_  
>  _x\[i\]\[j\] = (i+1)\*10+j+1;_  
>  _System.out.print(" " + x\[i\]\[j\] + " ");_  
>  _}_  
>  _}_  
>  _}_  
>  

_**Output:**_

>  _11.0_  
>  _21.0  22.0_  
>  _31.0  32.0  33.0_  
>  _41.0  42.0  43.0  44.0_  
>  _51.0  52.0  53.0  54.0  55.0_

9\. Classes {{< anchor "9" >}}{{< /anchor >}}and Objects
--------------------------------------------------------

In Java® every member function and data belongs to a _class_ and must be defined into a class declaration, i.e. it is not allowable to have global functions and variables. A class may contain data (fields) and functions (methods), which can be class or non-class members of the class.

An object is an instance of a class. It is created using a _new_ operator which instantiates the class, allocating memory for a new object, and initializes the objects data members, usually through constructors rather than directly. The _new_ operator returns a reference to the new instance of the class that has been created, i.e. to the new object. The new object is referenced typically by the variable at the left side of the _new statement_. The declaration of an object, e.g. _Point p_, does not allocate any memory for an instance of the class Point. It simply declares that _p_ can be used as a reference to an instance of the class _Point_. In Java® memory for objects is allocated from the heap using the keyword _new_. If there is not enough memory to be allocated the garbage collector may run to reclaim some memory and if there is still not enough memory an [_OutOfMemoryError_](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.OutOfMemoryError.html#_top_) exception is thrown. The variable that is associated with an object, in contrast to a variable of primitive data type, is actually a reference to that object.

A _class member data, or stat_ic field, is a field that is shared among all objects of that class, as in C++. Similarly, _static (or class) functions_ are methods, that can operate on class member data (static fields), or perform operations on the entire class and not on a certain instance of the class (i.e. object). A static function can access only static members, variables or functions, of the class, since it is not invoked on a specific object. Static fields and methods are declared using the keyword _static_ at its declaration. Class variables and methods are accessible from the class itself. There is no need to create an object, i.e. to instantiate the class in order to access its class (i.e. static) members. The static variables of a class are initialized before any use of any static variable and before the use of any of the member functions of the class.

When a class is defined it is required to use the keyword _class_ followed by the name of the class in the class declaration. The class body, in curly braces, follows the class declaration. Other possible components of a class declaration are the _public_, _abstract_, _final, extends_ (superclass), and _implements_ (one or more interfaces). If any, or all, of these optional components are not provided the Java® compiler considers the defaults, which are nonpublic, non-abstract, non-final subclass of the class _Object_ that does not implement any interface.

A _public_ class is publicly accessible, i.e. it can be used by classes in any package, not necessarily classes in its package.

An _abstract_ class is a class that cannot be instantiated, i.e. no objects of that class can be defined. An abstract class must necessarily be subclassed to be used, since it may contain methods with no implementation, i.e. abstract methods. an abstract class may provide definitions of all or some of the methods that the subclasses may inherit. Although an abstract class cannot be instantiated, a reference to an abstract class can be defined and used to achieve _polymorphism_. Typically, some of the functions are left to be implemented by the subclasses. If a class contains an abstract function then the class is abstract and cannot be instantiated. In that case the class should be explicitly specified as _abstract_.

A _final_ class is a class that cannot be subclassed. Specifying a class as _final_ automatically implies that all its methods are considered to be final. Specifying a class, or a function, as final may sometimes be useful, considering security and optimization issues.

The _extends \<superclass>_ specifies that the class that is declared is a subclass of the provided \<superclass>.  
Finally, the _implements\<interface1>, \<interface2>,....,_ specifies that the class implements one or more interfaces, whose names are provided after the keyword _implements_ in a comma separated list.

Note that assigning a reference data type variable, i.e. a variable that refers to an instance of a class, to another reference variable then both variables refer to the same object. The function [clone()](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.Object.html#clone__) may be used to actually make an actual complete copy of one object to another, i.e. copy the object state into a new identical object but in a different memory location.

The following is an example of a simple class. The class has two member data, x and y, and a class (or static) data and has no functions.

_Example of a Simple Class_

> _class Point_  
> _{_  
>  _public double x, y=100;                        // data member (or field)_  
>  _public static int num = 0;                       // class or static data member_  
> _}_
> 
> _class introClasses_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Point p1;                                            // declaration of a Point object_  
>  _Point p2 = new Point();_  
>  _Point.num++;_
> 
>  _p1 = new Point();_  
>  _p1.y = 1.1;_  
>  _p1.x = 2.2;_  
>  _p2.num ++;_  
>  _System.out.println("Number = " + Point.num);_  
>  _System.out.print("\\n p1:    x = " + p1.x + "      y = " + p1.y );_  
>  _System.out.println("\\n p2:    x = " + p2.x + "      y = " + p2.y );_  
>  _}_  
> _}_

  
 _Output:_

>  _Number = 2_  
>  _p1:    x = 2.2      y = 1.1_  
>  _p2:    x = 0.0      y = 100.0_

{{< anchor "10" >}}{{< /anchor >}}10\. Constructors
---------------------------------------------------

A class can provide one or more constructors to make the proper initializations of newly created objects. As in C++, a constructor has the same name with the class and has no return type. Java® supports _constructor overloading_. Constructors are differentiated from each other from the number and type of their parameters. The compiler, upon an object creation, invokes the constructor that matches with the provided arguments. A constructor with no argument is known as the _default constructor_ (or _no-argument constructor_). If no constructors are provided, Java® provides by default the no-argument (default) constructor which does nothing.  Upon the creation of an object its data fields are set to the default value of zero (for numeric types), '\\u0000' (for char), false (for boolean), or null (for reference) depending on the variable's data type. Then, the initializers and initialization blocks are called to initialize the fields. Finally, the constructor is called, which first, invokes, explicitly or implicitly, its superclass constructor, and then the statements in the body of the constructor(s) are executed.

Another constructor of a class can be invoked from inside a constructor of that class using _this_ which is a reference to the current object. This is called _explicit constructor invocation_. A constructor of a superclass can be invoked from inside a constructor using the _super_ keyword followed by parentheses in which arguments may be provided. The invocation of a superclass constructor must be the first statement in the subclass constructor so as to perform first the super class initialization. Otherwise, the superclass default constructor will be invoked implicitly.

A constructor of a class can be specified as _private_, _protected_, _package_, and _public_ which specifies which classes are eligible to create instances of that class. When a constructor is _private_ no other class can instantiate the class and only if the class provides public classes to instantiate the class, an object can be created. When a constructor is specified as _protected,_ only subclasses can use it to create objects of the class. If a constructor is specified as _public_ any class can create an object of the class using the constructor. Finally, a _package_ constructor can be used only by classes within the same package to create objects of the class.

_Example on Constructors_

> _class Point_  
> _{_  
>  _private double x, y;_
> 
>  _Point()                           // default constructor_  
>  _{_  
>  _x = y = 0.0;_  
>  _}_  
>  _Point(double x, double y)         // constructor overloading_  
>  _{_  
>  _this.x = x;_  
>  _this.y = y;_  
>  _}_
> 
>  _public String toString()            // toString method_  
>  _{_  
>  _return ("x = " + x + "    y = " + y);_  
>  _}_  
> _}_
> 
> _class constructorsClasses_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Point p1= new Point(), p2;_  
>  _p2 = new Point(2.22,4.8);_
> 
>  _System.out.println("\\n p1:    "  +  p1);_  
>  _System.out.println("\\n p2:    "  +  p2);_  
>  _System.out.println();_  
>  _}_  
> _}_

  
**_Output:_**

>  _p1:    x = 0.0    y = 0.0_  
>  _p2:    x = 2.22    y = 4.8_

11\. {{< anchor "11" >}}{{< /anchor >}}Initializers
---------------------------------------------------

In Java® someone can use _static initializers_ and _instance initializers_ to provide initial values for static (i.e. class) and instance (i.e. object) data members. Static initializers cannot call functions that are declared to throw checked exceptions.

If no values are provided to the variables of a class using either initializers or constructors a zero, '\\u0000', false, or null value is assigned depending on the variable's data type.

The following example demonstrates the use of static and instance initializers.

_Initializers Example_

> _class Initialization1_  
>  _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Point p = new Point();_  
>  _System.out.println("Number of points = " + Point.pointsNumber);_  
>  _System.out.println("(x,y) = (" + p.x + ","  + p.y + ")") ;_  
>  _}_  
>  _}_
> 
> _class Point_  
>  _{_  
>  _double x=200, y=100;                     // instance initializer_  
>  _static int pointsNumber=1;               // static initializer_  
>  _}_

_Output:_
---------

> _Number of points = 1_  
> _(x,y) = (200.0,100.0)_

  
However, these initializations can be done only when using assignment statements, i.e. without the ability to call any other method, or throw an exception. For such cases a _static initialization block_ can be used to initialize static members, while a constructor is, in general, used for the initialization of instance members. Constructors are called after the initializers have assigned the default values to the member data.

A _static initialization block_ is a block enclosed with curly braces with the keyword static before it. The static initialization blocks and the static initializers are called in order from left to right and from top to bottom.

_Static Initialization Block Example_

> _class Point_  
>  _{_  
>  _double x=200, y=100;           // instance initializer_  
>  _static int pointsNumber;_
> 
>  _static                                     // static initialization block_  
>  _{_  
>  _pointsNumber = 1;_  
>  _System.out.println("Inside static initialization block");_  
>  _}_  
>  _}_  
>  
> 
>  _class Initialization2_  
>  _{_
> 
>  _public static void main(String args\[\])_  
>  _{_  
>  _System.out.println("Inside main");_  
>  _Point p = new Point();_  
>  _System.out.println("Number of points = " + Point.pointsNumber);_  
>  _System.out.println("(x,y) = " + p.x + ","  + p.y + ")") ;_  
>  _}_  
>  _}_  
>  

_Output:_

> _Inside main_  
> _Inside static initialization block_  
> _Number of points = 1_  
> _(x,y) = 200.0,100.0)_

  
Java® supports also _instance initialization blocks_ (or non-static initialization blocks) which are sometimes useful, such as in anonymous classes where having constructors is not possible. An instance initialization block is placed at the location where a new object of the class is created. The non-static initializers are executed upon the creation of an object before the invocation of the corresponding constructor. The order of execution of instance initializers and initialization blocks is again  from left to right and from top to bottom.

An _anonymous class_ is a class without a name that is defined within another class. At the same time that it is defined an instance of it is created using the _new_ keyword. Since an anonymous class has no name it cannot have any constructors.

12\. {{< anchor "12" >}}{{< /anchor >}}Member Data and Functions
----------------------------------------------------------------

Both member data and member functions are accessed and invoked, respectively, using an object reference followed by a dot and at the right of the dot the name of the data or function of the class. The object reference can be any expression that returns a reference to an object of the class, e.g. a _new_ operator. In the invocation of an object's function, parentheses, which may contain provided arguments, follow the name of the function. Invoking a function of an object is known as "sending a message" to that object.

Member data (or member variables) are declared using the data type followed by the name of the variable. The _data type_ can be any primitive or reference data type, while the _name_ should be any legal Java® identifier. In addition, the following _attributes_ can also be specified:

> *   _access level_: specifies the access level for this variable, which can be public, package, protected, and private.
> *   _static_: specifies that the variable is static (i.e. class) variable
> *   _final_: specifies that the value of the variable after it is assigned cannot be modified
> *   _transient_: indicates that the variable is transient, which is not yet fully specified
> *   _volatile_: indicates that the Java compiler should not perform certain optimizations on the variable

  
Member functions are typically provided, as in C++, to operate on member data allowing data encapsulation, hiding data behind functions (methods). However, in Java® global functions are not allowable. Every function must be provided within a class definition. Also externally defined member functions are not possible in Java®, since everything must be defined within a class. Java® supports recursion, allowing a function to call itself either directly (direct recursion), or indirectly (indirect recursion) through another function.

A function has two parts, the _function declaration_ and the _function body_. The function declaration must provide the return data type and the name of the function followed by parentheses that enclose the parameters of the function.  
  
A function may return a value or no value in which case it is declared as _void_. A function that returns an object of a class can return an object of any subclass of that class as well. In addition, a function may have an interface as a return type, in which case an object of any class that implements that interface may be returned.

The _function name_ should be any legal Java® identifier. The name of a function can be the same as the name of a data member of the class. Java® supports, as C++, function overloading allowing functions to have the same name as long as the individual functions with the same name differs in the number or/and type of the parameters. The signature of a function is its name together with the number and type of its parameters. Functions with different signatures, although with the same name, are allowable.

A function may have no or any number of arguments. A function with no arguments is defined using empty parentheses. An argument with the same name as a member variable of the class hides the member variable. In that case the reference _this_ can be used. The latter, i.e. _this,_ is a reference that refers to the object with which the member function has been invoked. The reference _this_ may be used to pass a reference to the object that has invoked the member function, as an argument to the member functions. Similarly the reference _super_ refers to the superclass of a class and can be used when a member variable or function of a superclass is hidden. In Java, it is not possible to pass a function (or a pointer to a function) as an argument to a function.

All arguments to functions in Java® are passed by value, which means that primitive data type arguments and the actual references cannot be modified. The values of the parameters are copies of the values of the arguments passed to the function. Declaring a function parameter using the _final_ modifier prohibits the modification of that parameter within the function.

A function declaration may also provide more information about it using any of the following _attributes_:

> *   _access level_: specifies the access level for this variable, which can be public, package, protected, and private.
> *   _static_: specifies that the function is static (i.e. class) function, i.e. that it is not associated with a certain object of the class
> *   _abstract:_ indicates that the method is not implemented. Therefore, the class is abstract and cannot be instantiated.
> *   _final_: specifies that the function cannot be overridden by a subclass
> *   native: indicates that the function is implemented in another language (e.g. C++)
> *   _synchronized_: indicates that certain precautions should be taken to ensure that functions that operate on same data, do it in a threat-safe way.
> *   _throw_s _\<exceptions>_: specifies the checked exceptions that the function may throw

An implicit reference to the object with which a function is invoked, called _this_, is available in every non-class (i.e. non-static) function. It is used to explicitly refer to members of the object that have invoked the function, or when an object reference is required.

A function of a class with the name [toString](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.Object.html#toString__)() that takes no arguments and returns a [String](http://java.sun.com/products/jdk/1.1/docs/api/java.lang.String.html#_top_) is a special function. It allows the object to be used in a string concatenation using the + operator, e.g. in a _println_ statement. Note that all the primitive data type variables are implicitly converted to _String_ objects whenever they are used in _String_ expressions.

In Java® there is no need to worry about explicitly destroying objects that are not needed anymore. Java® provides a garbage collector that periodically frees memory of objects that are no more being referenced. When a variable that is used to reference to an object goes out of scope or it is set to null, that object, if not referenced by any other variable becomes eligible for _garbage collection_.  
 

_Example on Member Data and Methods_

> _class Point_  
> _{_  
>  _private static int num = 0;        // static field_  
>  _private double x, y;                      // non-static data members (fields)_
> 
>  _/\* set methods \*/_  
>  _public void setX(double x)_  
>  _{_  
>  _this.x = x;_  
>  _}_  
>  _public void setY(double yy)_  
>  _{_  
>  _y = yy;_  
>  _}_  
>  _public static void incrNum()    // static method_  
>  _{_  
>  _num++;_  
>  _}_
> 
>  _/\* get methods \*/_  
>  _public double getX()_  
>  _{_  
>  _return x;_  
>  _}_  
>  _public double getY()_  
>  _{_  
>  _return y;_  
>  _}_  
>  _public static int getNum()     // static function_  
>  _{_  
>  _return num;_  
>  _}_
> 
>  _public String toString()            // toString method_  
>  _{_  
>  _return ("x = " + x + "    y = " + y);_  
>  _}_  
> _}_  
>  
> 
> _class methodsClasses_  
> _{_  
>  _public static void main(String args\[\])_  
>  _{_  
>  _Point p1, p2 = new Point();_  
>  _Point.incrNum();_
> 
>  _p1 = new Point();_  
>  _p1.incrNum();_
> 
>  _p1.setX(1.1);_  
>  _p2.setX(2.2);_
> 
>  _System.out.print("\\nNumber = " + Point.getNum());_
> 
>  _p1.setY(0.11111);_
> 
>  _System.out.print("\\n p1:   x = " + p1.getX() + "     y = " + p1.getY() );_  
>  _System.out.print("\\n p2:   " + p2 );_  
>  _System.out.println();_  
>  _}_  
> _}_

  
 **_Output:_**

> _Number = 2_  
>  _p1:   x = 1.1     y = 0.11111_  
>  _p2:   x = 2.2     y = 0.0_

{{< anchor "13" >}}{{< /anchor >}}13\. Function Overloading
-----------------------------------------------------------

Java® allows function overloading with which the selection of the function is based on its signature. The signature of a function is its name and the number and type of its parameters, i.e. the return type of a function is not part of its signature.

_Example on Function Overloading_

> _class methodsOverloading  
> {  
>   public static void main(String args\[\])  
>   {  
>     myPrint();  
>     myPrint(3);  
>     myPrint(1.7);  
>   }_
> 
>  _public static void myPrint()  
>   {  
>     System.out.println(" Inside myPrint()");  
>   }  
>   public static void myPrint(int i)  
>   {  
>     System.out.println(" Inside myPrint():    i =" + i);  
>   }  
>   public static void myPrint(double x)  
>   {  
>     System.out.println(" Inside myPrint():   x = " + x );  
>   }  
> }_

 **_Output:_**

>  Inside myPrint()  
>  Inside myPrint():    i =3  
>  Inside myPrint():   x = 1.7