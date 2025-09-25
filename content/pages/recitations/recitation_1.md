---
content_type: page
description: ''
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 1
uid: 627fc44d-3c41-840b-842b-8cbe6b73ef3d
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).  
  
Topics
------------------------------------------------------------------------------------------

1.  [Course goals & content, references, recitations](#1_course)
2.  [Compilation](#2_compilation) 
3.  [Debugging](#3__Debugging)  
4.  [Makefiles](#4__Use_of_makefiles)
5.  [Concurrent Versions System (CVS)](#5_concurrent)  
6.  [Introduction to C++](#6_Introduction)
7.  [Data Types](#7_Data)
8.  [Variable Declarations and Definitions](#8) 
9.  [Operators](#9_operators)
10.  [Expressions and Statements](#10_Expressions)
11.  [Input/Output Operators](#11_input)
12.  [Preprocessor directives](#12_preprocessors)
13.  [Header files](#13__Header_files)
14.  [Control Structures](#14_control)

{{< anchor "1_course" >}}{{< /anchor >}}1\. Course Goals and Content
--------------------------------------------------------------------

*    **C++:**  
     Procedural and Object Oriented Programming  
     Data structures  
     Software design and implementation  
     
*   **Algorithms:  
    ** sorting (insertion, selection, mergesort, quicksort, shellsort, hashing)  
     searching (linear search, binary search, binary search trees)  
     
*   **Java®:**  
     Object Oriented Programming (OOP) using Java®, Java® application and applets,  
     Graphical User Interfaces, Graphics using Java®  
     
*   **Advanced  Topics:  
    ** Geometric algorithms, Java®3D, Database design using  JDBC, etc.  
     
*   **Term Project**

Textbooks - References
----------------------

*   **C++**
    *   _C++ Primer._ Lippman and Lajoie. 3rd edition (required).
    *   _C++ How to program_. Deitel & Deitel. 3rd edition.
    *   _The C++ programming language._ Bjarne Stroustrup. 3rd edition.
    *   _On to C++_. H. Winston. 2nd edition.
    *   _Object Oriented Programming in C++._ Johnsonbaugh & Kalin.
    *   _C++ FAQ_. Cline/Lomow.  
         
*   **Algorithms**
    *   _Algorithms in C++._ Sedgewick (required).
    *   _Algorithms, Data Structures and Problem Solving with C++_. Weiss.
    *   _Introduction to Algorithms._ Cormen, Leiserson, and Rivest.  
         
*   **Java**®
    *   _The Java® Tutorial_. Mary Campione and Kathy Walrath (required).
    *   _Core Java®._ Gary Cornell and Cay Horstmann. 2nd edition.
    *   _The Java® programming language_. Ken Arnold and James Gosling. 2nd edition.
    *   _Java®: How to program._ Deitel & Deitel. 2nd edition.

Problem Sets
------------

You need to follow the instructions that are provided with each problem set, concerning what you must submit. In all problem sets you must both electronically turnin the source code files, and submit hardcopies of all completed, or modified, source code files. Sometimes you may also need to provide screen dumps of the window with the output results from the execution of your programs.

The problem statement and the provided source code files can be obtained using CVS, which is a version control system (covered later in this recitation). Whenever source code files are provided, the following naming convention is used:  
For each question there is a _ps\<number\_of\_problem\_set>\_\<number\_of\_question>.C_ which you may need to use, e.g. _ps3\_2.C_ for question 2 of problem set 3.  
In some cases a makefile (named _make\<number\_of\_problem\_set>_) is provided, which you may use to compile and link your code.

Please comment your code to make it more readable whenever you think it would be helpful for someone else to understand what and how you do it (i.e. for the graders). Comments may be incorporated in your code by either enclosing them between /\* and \*/, or, by putting them on the right side of two division symbols //.  
It is also very useful for both yourselves, and the graders, to indent your code in order to emphasize loops and different parts of your code. You should indent your code so that different blocks start in different columns making it less obscure and difficult to understand.  
Please, do not make any other changes to the provided code, except those that you are asked to make.

You can print a file in a compact form (saving some paper) using the following command so as to have the name of the file and the time and date printed on the hardcopy.  
        athena% _enscript   -2Gr    -P\<printer name>   \<filename>_  
Whenever necessary, you can dump an X window directly to a printer using the following command and clicking on the window you want to print.  
        athena% _xdpr  -P\<printer name>_

Homework that is turned in late will be penalized as follows:  
 

*   If turned in one day late i.e. by 2:30 p.m. on the day after the due date, the penalty is **10% of the overall score** (i.e. **10 points off**). You can turn in the problem set solution only once. The first hardcopy you will turn in will be the one to be graded, i.e. if you plan to submit it late you should not submit a solution on the due date, as well, but only the late one the day after the due date.
*   If turned in more than one day late, the penalty is 100% i.e. no credit will be awarded. **No exceptions!**

  
Please, always staple your hardcopies together and write clearly on the first page your name and username. Also, type within a comment at the top of each file you submit the following information:

*    your first and last name
*    the problem set number, and
*    the question number

{{< anchor "2_compilation" >}}{{< /anchor >}}2\. Compilation
------------------------------------------------------------

After writing the source code of a program, e.g. using an editor such as emacs, you must compile it, which translates the source code into machine instructions. For the C++ programs you need to use the GNU g++ compiler. To be able to use this compiler, you need to add its locker using the following command (on the Athena prompt):  
    
 _% add -f gnu_

You can customize your account, using a dotfile, so that it will automatically add the gnu locker at start-up. In the file .environment you need to add the following line:  
  
       _add -f gnu_  
  
The add command attaches the specified locker to your workstation and adds it to your path. Dotfiles, such as _.environment_ and _.cshrc.mine_, can be used to set environment variables, shell aliases and attach lockers in order to get the desired working environment. In the .environment dotfile you may also put the following lines to avoid typing them every time you log in:  
  
       _add infoagents_  
       _add  1.124_  
       _setenv CVSROOT /afs/athena.mit.edu/course/1/1.124/src_

You can check if you properly use the GNU compiler by giving the following commands:  
  
    _% which g++  _                  which should give you something like:  
      /mit/gnu/arch/sun4x\_55/bin/g++     or     /mit/gnu/arch/sgi\_53/bin/g++

Then, you can use the GNU compiler to compile a C++ source code file. For example, to compile and link the source code file _ps0\_1.C_, which is provided in _PS0_, you can use the following command:  
  
    _% g++  ps0\_1 .C_

Then, you can run the generated executable file, which is by default named _a.out_, by typing its name at the Athena prompt.  
To give a specific name to the generated executable the -o option must be used:  
  
     _% g++  ps0\_1 .C -o  ps0\_1_  
  
Then, the generated executable file is named _ps0\_1_  
  
Sometimes, you may need to include an external library, e.g. the math library, using the -l option as follows, and the name of the external library (below the math library is included using m after -l) you want to include (in addition to including its header file in your files):  
  
      _%   g++    ps0\_1 .C       -o  ps0\_1     -lm_

In some cases that you only need to compile a file without linking, i.e. to generate only the corresponding object file (machine language versions of the source code) and not the executable, you need to use the -c option. (In the following example a _ps0\_1.o_ will be generated)  
  
     _% g++  -c   ps0\_1 .C_

You also need to use the flags -ansi -pedantic to enforce the rules of ANSI Standard C++. In addition, it is useful to use the -Wall option to get all warnings, e.g.:  
  
     _% g++  -ansi -pedantic -Wall    ps0\_1 .C     -o  ps0\_1    -lm_  
  
It is more convenient to set an alias (e.g. c++), instead of typing all this every time. In particular you can add in your _.cshrc.mine_ dotfile the following:  
 _alias   "c++"  "g++  -ansi   -pedantic   -Wall   -lm"_  
and then simply use the following command to compile and link a program:  
 _% c++   ps0\_1 .C    -o  ps0\_1_

In addition, you can use makefiles to help you automate the compilation and linking of your programs. The following command creates the target\_filename according to the instructions provided in the makefile _make0a_.  
  
    _% gmake -f makePS0a ps0\_1_  
  
Eventually you must learn to use makefiles since they are extremely useful for the development of large programs with several different source code files.

Although you may work at any machine and using any compiler you want, you need to make sure that your code compiles properly using the GNU compiler on an Athena workstations. The graders will be using Athena workstations and the GNU compiler to check your solutions.

{{< anchor "3__Debugging" >}}{{< /anchor >}}

3\. Debugging
-------------

Using a debugger can help you find logical and difficult to detect errors in your code much faster and easier. A debugger can be used to step through the program, line by line and examine the program variables while executing it. Therefore, you need to first correct all syntactical errors, using the messages from the compiler and then execute the program using the debugger to detect potential logical errors. Typically, you compile the program, identify errors using a debugger, correct it in emacs, compile and debug again, and repeat as often as necessary.

The debugger allows you to examine in detail what is happening during a program execution, or when it crashes due to a run-time error. In order to be able to use a debugger, such as gdb and ddd, you must first compile and link your code with the flag -g. e.g.:

     _% g++   -g    ps0\_1 .C    -o  ps0\_1_  
 

*   **gdb debugger:  
    **  
    The  _g++   -g    ps0\_1 .C    -o  ps0\_1_ command generates an executable filename that can be checked with gdb, e.g. using the following command for the program compiled above:

         _% gdb   ps0\_1_

You can find more information about GDB at [Debugging with GDB - The GNU Source-Level Debugger](http://web.mit.edu/afs/athena.mit.edu/project/gnu/doc/html/gdb_toc.html).  
 

*   **ddd debugger:  
      
    **A user friendlier debugger, available on athena, is the Data Display Debugger (ddd), which uses the gdb for its operations. The ddd program is available in the outland locker. Since we also need the g++ compiler from the gnu locker for the compilation you need to type:  
      
    _% add outland_  
    _% add gnu  
      
    _To invoke the ddd debugger with your executable program, e.g. for ps0\_1, please, type:  
      
    _% ddd ps0\_1 &_

You can see that three windows pop up:

1.  The main window, which has three main parts.
    *   the top panel with the menu bar and the tool bar
    *   the middle panel with your source code, which is a read only panel code here.
    *   the bottom panel with the (gdb) prompt, which is the debugging console  
         
2.  Debugger command tool window, titled  ddd
3.  A tip window, which often provides useful debugging tips. You can close this window.

In general, the debugging cycle involves stepping through your program carefully once it compiles and seems to run. In particular, step into each function that you wrote; step over, e.g. using the _’Next’_ button, system functions. At each step, _’Print’_ the variable value(s) computed and  check them for reasonableness. Keep going until you find logical errors. Then, make the proper correction, using the editor, recompile and do this again.

The execution of the program can be controlled from the ddd command tool which has the _Run_, _Interrupt_, _Step_, _Next_ etc. buttons.  
 

*   **To start debugging:**
    *   Find the first executable (non-declaration) line in the program
    *   Place the cursor on that line (mouse click)
    *   Then click on the ’Break’ button in the tool panel at the top of the main window. This will set a breakpoint at that line.  A breakpoint stops program execution. You should see a stop symbol at that   line.
    *   Click on ’Run’ button in the ddd window.
    *   This starts program execution, which will run until the next breakpoint  or the end. The program will run to the first breakpoint and halt.  
         
*     **To step through the program:**

You can step through the program using the buttons on the ddd window. A green arrow will indicate the current program statement being executed in the source code panel.

*   *    clicking on the _’Next’_ button steps over function calls and goes to the next line of the current function
    *   clicking on the _’Step’_ button steps into any function call on the current line
    *   clicking on '_Finish’_ will finish executing the current function. You can use ’Finish’ to come out of any system source code (cout for example) you ’Step’ into  
         
*   Looking at variable values:
    ---------------------------
    
    *   To examine normal variables you can:
    *   move the mouse on top of a variable and a pop up box will show the variable’s value
    *   click on the variable so that it becomes highlighted, and then click on the ’Print’ button in the toolbar. Then, the variable's value will appear in the console  
         
*   **To examine arrays:**
    *   moving the cursor on top of an array, either the memory address of the first element is shown if values have not been set, or if values have been assigned to the array, the array values are shown
    *   highlighting the array name the array name will appear in the text box present in the tool bar. If _’Print’_ is clicked now, the memory address is printed in the console.
    *   adding a \* before the array name and clicking ’Print’ will print the value stored in the first element of the array. If you wish to see all the elements in the array, replace ’\*arrayName’ by ’\*arrayName@arraySize’ in the text box and then click _’Print’._  
         
*   **To display a variable:**

You can continuously see the values stored in a variable, by displaying it instead of printing it. The displayed variable will be shown in a new panel which will pop up above the source code panel. As you step through the program, any changes to the variable’s value will be shown there. You can display a variable by:

*   highlighting a variable and clicking on the _’Display’_ button on the tool bar. Its value is updated every time it changes.
*   To undisplay a variable.

*   Right click on the variable’s box and choose ’undisplay’.

*   **To display values of all local variables in the current function:**
    *   choose _"Display local variables"_ from the _’Data’_ tab in the menu bar of the main window.  
         
*   **To display the arguments passed to the current function:**
    *   choose _"Display function arguments"_  from the _’Data’_ tab in the menu bar of the main window.  
         
*   **To input and output:**
    *   Input and output is done through the debug console.
    *   cout line usually found before cin will display a prompt
    *   stepping to a cin enter your input in the bottom window in the blank line at the bottom  
         
*   Resources:
    ----------
    
      
    You can learn more about ddd from the [DataDisplayDebugger](http://www.gnu.org/software/ddd/ddd.html) web-page.  
      
      
    You can look at the [ddd manual](http://www.gnu.org/software/ddd/manual/html_mono/ddd.html) as well.

{{< anchor "4__Use_of_makefiles" >}}{{< /anchor >}}

4\. Use of makefiles
--------------------

In some cases a makefile (named _make\<number\_of\_problem>_) will be provided, and you may use it to compile and link your code. Makefiles are used to automate the compilation and linking of programs. To compile and link a specific program, assuming that a proper makefile is available, the following command is used:  
 _% gmake -f make\_file\_name   \<program\_name>_  
You do not have to use the provided makefiles, but you can use instead your own makefiles, or any of the makefiles you have seen in the lectures or anywhere else. You need to turnin the makefile that you use to compile your files on athena (either the ones you got using CVS or your own) Learning to use makefiles will help you when you start writing and compiling larger programs with several files, which makes the use of makefiles necessary.

In problem set # 0, a simple makefile is provided for you, called _makePS0a_, which you may use to compile and link your code. There is also a more advanced makefile named _makePS0b_ which you can use.  
  
e.g.           _athena%  gmake   -f makePS0a    ps0\_1_  
  
Executing the above command creates the target filename _ps0\_1_, according to the instructions provided in the makefile _makePS0a_.

5{{< anchor "5_concurrent" >}}{{< /anchor >}}. Concurrent Version Control (CVS)
-------------------------------------------------------------------------------

For the development of large software packages and programs it is useful to use a control system for modifications and revisions. Although it may not seem very useful for the development of small simple programs (like your first homework problems) it would be very useful for your project, and you will benefit from getting used to using it. Therefore, it would be beneficiary for you to get used to using such a revision control system as CVS (Concurrent Versions System). You may obtain more information on CVS from the man command (_% man cvs_) and from the following URLs:

*   [cvs - Concurrent Versions System](http://www.nongnu.org/cvs/)
*   [Concurrent Versions System - Tutorials](http://www.yolinux.com/TUTORIALS/LinuxTutorialCVSintro.html)
*   [CVS Index](http://www.catb.org/~esr/writings/version-control/cederqvist-1.11.22.html#SEC193)
*   [Concurrent Versions System - The Open Standard for Version Control](http://www.cvshome.org/)

The provided source code files are in the directory _/mit/1.124/Problems/\<Problem set number>_ from where you can copy them using CVS to your directory, and, make the necessary additions and/or modifications. To use CVS to check out the problem sets for the 1.124 you should first set the environment variable CVSROOT as below: (you can also put it in your _.environment_ dotfile)  
 _% setenv CVSROOT /afs/athena.mit.edu/course/1/1.124/src_  
then you can use the command:  
 _% cvs co Problems/PS\<Problem set number>_  
or, using the alias defined in 1.124/src/CVSROOT/modules  
 _% cvs co OOP\_PS\<Problem set number>_

{{< anchor "6_Introduction" >}}{{< /anchor >}}6\. Introduction to C++
---------------------------------------------------------------------

C++ is both a procedural oriented programming language and an object oriented programming (OOP) language, since it allows you to organize your program not only around functions (procedures), but also and most commonly used, around data.

A procedural language is based on a list of instructions (statements) organized in procedures (functions) and emphasizing the computations to be performed. Languages such as Fortran and C are procedural languages. C++ which is based on C, has many additional features that enable object oriented programming, where emphasis is given on the data and their behavior. Java® is a pure object oriented language.

The **additional features and advantages of C++** are the following:  
  
Classes allow the programmer to create her/his own data types extending the capabilities of the language according to the physical world problems. Classes are similar with the data structures in C, which are also available in C++. However, within a class both data variables and member functions that are used to work with the data variables can be provided.

 _class Complex_  
 _{_  
 _public:_  
 _double real;_  
 _double imaginary;_  
 _};_

 _main()_  
 _{_  
 _Complex x;_  
 _x.real =15.5;_  
 _x.imaginary = 2.5;_  
 _}_

There are many additional features, like **inheritance** and **virtual functions**, added to C++ which are related with the classes and provide simple ways to handle objects and develop programs in an object oriented programming style.

C++ allows **reusability** since a class which has been written, debugged and checked can be distributed to other programers and with minimal effort be incorporated in several programming packages.

C++ supports **function overloading** which allows the use of functions with the same name, as long as they have different signature. The signature of a function is considered its name and the number and type of its arguments. e.g.:  
 _int min(int x, int y) {      }_  
 _double min(double x,  double y) {      }_

In addition, **virtual functions** and **polymorphism** allows the dynamic binding on functions during run-time instead of static binding during compilation.

C++ allows **operator overloading**, i.e. to use operators with user defined data types according to a specified function associated with the specific operator. For example, we are able to add two complex numbers which are a user defined data type, as long as we provide the necessary functions for operator overloading.  
 _main()_  
 _{_  
 _Complex x,y,z;_  
 _........_  
 _z = x + y ;_  
 _}_

In C++, there are two ways to **comment**, // (which comments everything until the end of line), and /\*  \*/ (which comments everything between /\* and \*/.

Two latest features of C++ are the **templates** and the **exception handling**. The templates allow us to parameterize the types within a function or a class providing a general definition that can be used for many different purposes. The exception handling mechanism provides a mechanism to respond to and handle run time errors (like division by zero, exhaustion of memory, etc.).

{{< anchor "7_Data" >}}{{< /anchor >}}7\. Data Types
----------------------------------------------------

*   Boolean: **bool**
*   Character and very small integers: **char**
*   Integers: **short int, int, long int **    (short, int, long)
*   Floating (single, double and extended precision): **float, double, long double**

The **_bool_** data type can be assigned the values true and false, which correspond to 1 and 0, respectively.  
    
A **_char_** can be used both as a character and as an integer, depending on how it is used. Therefore, _char_, _short_, _int_, and _long_ are all called **integral data types**.  
  
There are also _unsigned_ versions of integer types, which allow the increase of the range of the larger number that can be stored with them, by not using any bit for the sign: _unsigned char, unsigned short int (unsigned short), unsigned int, unsigned long int (unsigned long)_.

The reason of using different data types is mainly for memory efficiency, since we can use the data type which correspond to our needs avoiding useless waste of memory. The proper data type must be selected and used based on the expected requirements during the program’s execution.

To refer to particular variables that correspond to a particular chunk of memory in C++ (and in any other programming language) we have to use **identifiers** (variable names). The variable names in C++ are case sensitive as they are in C, must begin with a letter or an underscore (\_), and should not be a reserved keyword. You should use reasonable variable names that provide some meaning to the reader of your code.

Using the above keywords we can declare the data type of a variable giving to the compiler information about the necessary amount of memory required to store (i.e. the memory that is required to be allocated and reserved for) the variable and which is machine dependent, e.g.:

*   _int i, j ;_
*   _double x,y,z;_
*   _long int k;_
*   _unsigned short int i;_

The _const_ type modifier (or qualifier) defines a variable as a symbolic constant and does not allow any change of its value. Therefore, a _const_ variable must be initialized when defined, since any attempt to change its value results in a compile-time error.  
  
       _const int i=10;_  
  
Note the different meaning of the following declarations:  
  
 _const int \*p: Pointer to a constant integer  
       int \*const p: Constant pointer to an integer  
       const int \*const p: Constant pointer to a constant integer_

{{< anchor "8" >}}{{< /anchor >}}8\. Variable Declarations and Definitions
--------------------------------------------------------------------------

Before using any variable we have to declare it, i.e. inform the C++ compiler what is the data type of the variable. Every variable has a certain data type that determines the storage requirements and the operations that can be performed on it. In C++, as in C, we can combine several separate variable declarations into one declaration, as long as each variable is of the same data type, e.g.:

 _\<data\_type1>  \<variable1\_name>;  
           \<data\_type2>  \<variable2\_name> = \<initial\_value>,  \<variable3\_name>;\< /EM >_

_int a, b, c;  
double x,y ;  
float z ;_

The above declarations are also definitions. A **declaration** simply informs the compiler that the variable exists, its data type and that it is defined somewhere else in the program. C++ allows to have many declarations of the same variable as long as they are consistent. The **definition** of a variable defines the variable’s name, its data type and may also initialize the variable. Defining a variable informs the compiler about the variable's data type so as to reserve the proper amount of memory to store values for that variable. The difference is that the definition reserves memory for the variable. Therefore, there must be only one definition of a variable in a program. A declaration is also a definition if it also sets aside memory at compile time.

For example, the following statement is a declaration because it informs the compiler that an external global variable will be used, but no memory is allocated for that variable. The memory is allocated at the definition of the variable.  
        _extern int x\_limit ;_                         // declaration

We can also initialize a variables in its definition, assigning an initial value and this is called **initialization**. When a value is assigned to an already defined variable this is called **assignment** :  
      _int a, b, c;_                          // definitions  
      _double x = 3.4, y(4.);\< /EM >        // definitions and  initializations  
     _ float  z = 9.9;\< /EM >                    // definition and initialization  
      _c = 10; \< /EM >                            // assignment_

{{< anchor "9_operators" >}}{{< /anchor >}}9\. Operators
--------------------------------------------------------

You will often need to use operators which perform a specified action on their operands. Most operators are binary, i.e. they have two operands, e.g. a+b. The operators in C++ are the same as the ones used in C.  
  
These are:

*    the **arithmetic** operators of C++ are the +, -, \*, / and %
*    the **assignment** operator is the =
*    the **shorthand** (abbreviated) assignment operators: += ,  -= , \*= and /=
*    the (unary) **postfix** and **prefix increment/decrement** operators ++ and --
*    the **relational** operators are: > , \< , >= , and \<=  (used to compare two expressions)
*    the **equality** operators are: == and !=   (used to check two expressions for equality)
*    the **logical** operators are the: && , || , and !

  
An assignment expression has the value that is assigned to the variable on the LHS, and, therefore, several variables can be assigned the same value in one statement,  
  
e.g.:    _x = y = z = 100;_

The RHS of logical operators is executed only if its necessary for the decision that must be taken. e.g. if the LHS of a ‘logical and’ (&&) is false, there is no reason to examine its RHS.

In addition, in C++ it is allowed to create new definitions for operators applied to user defined data types.  
 _main()_  
 _{_  
 _Point x,y,z;_  
 _........_  
 _z = x + y ;_  
 _}_

{{< anchor "10_Expressions" >}}{{< /anchor >}}10\. Expressions and Statements
-----------------------------------------------------------------------------

Each C++ program must contain a function named _**main()**_, as in C. The execution of a C++ program begins from the first statement of main and finishes when the last statement of main is executed (e.g. when the last curly brace of main is reached).

An action in C++ is referred as an expression, while an expression terminated by a semicolon is called a statement. More than one statements enclosed in a pair of curly braces is called a compound statement.

**Precedence and associativity:** The sequence (order) with which individual components of an expression in C++ are executed is based as in C on the order of precedence. When the operators have the same precedence the associativity defines the order of execution. A table with the precedence and associativity of the C++ operators is provided. Similar tables you can find in any C++ textbook.

e.g.         a  =  b   +=    5    +      3      /      2     -     5     +     17    /     2    /     3  
(order):     (8)      (7)        (4)           (1)          (5)         (6)          (2)       (3)

The following table provides the precedence and associativity of the C++ operators with the highest precedence being the operator :: having precedence level equal to 1.

{{< tableopen >}}
{{< theadopen >}}
{{< tropen >}}
{{< thopen >}}
PRECEDENCE
{{< thclose >}}
{{< thopen >}}
ASSOCIATIVITY
{{< thclose >}}
{{< thopen >}}
OPERATOR
{{< thclose >}}
{{< thopen >}}
FUNCTION
{{< thclose >}}

{{< trclose >}}

{{< theadclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
::
{{< tdclose >}}
{{< tdopen >}}
global scope (unary)
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
1
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
::
{{< tdclose >}}
{{< tdopen >}}
class scope (binary)
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\-> , .
{{< tdclose >}}
{{< tdopen >}}
member selectors
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\[\]
{{< tdclose >}}
{{< tdopen >}}
array index
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
()
{{< tdclose >}}
{{< tdopen >}}
function call
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
2
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
()
{{< tdclose >}}
{{< tdopen >}}
type construction
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
sizeof
{{< tdclose >}}
{{< tdopen >}}
size in bytes
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
++ , --
{{< tdclose >}}
{{< tdopen >}}
increment, decrement
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
~
{{< tdclose >}}
{{< tdopen >}}


bitwise NOT


{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
!
{{< tdclose >}}
{{< tdopen >}}
logical NOT
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
\+ , -
{{< tdclose >}}
{{< tdopen >}}


uniary minus, plus


{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
\* , &
{{< tdclose >}}
{{< tdopen >}}
dereference, address-of
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
()
{{< tdclose >}}
{{< tdopen >}}


type conversion (cast)


{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
3
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
new , delete
{{< tdclose >}}
{{< tdopen >}}
free store management
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
4
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\->\* , .\*
{{< tdclose >}}
{{< tdopen >}}


member pointer selectors


{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
5
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\* , / , %
{{< tdclose >}}
{{< tdopen >}}
multiplicative operators
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
6
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\+ , -
{{< tdclose >}}
{{< tdopen >}}
arithmetic operators
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
7
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\<\< , >>
{{< tdclose >}}
{{< tdopen >}}
bitwise shift
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
8
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\< , \<= , > , >=
{{< tdclose >}}
{{< tdopen >}}
relational operators
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
9
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
\== , !=
{{< tdclose >}}
{{< tdopen >}}
equality, inequality
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
10
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
&
{{< tdclose >}}
{{< tdopen >}}
bitwise AND
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
11
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
^
{{< tdclose >}}
{{< tdopen >}}
bitwise XOR
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
12
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
|
{{< tdclose >}}
{{< tdopen >}}
bitwise OR
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
13
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
&&
{{< tdclose >}}
{{< tdopen >}}
logical AND
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
14
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
||
{{< tdclose >}}
{{< tdopen >}}
logical OR
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
15
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
?:
{{< tdclose >}}
{{< tdopen >}}
arithmetic if
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
16
{{< tdclose >}}
{{< tdopen >}}
right
{{< tdclose >}}
{{< tdopen >}}
\= , \*= , /= , %= , += , -=  
\<\<= , >>= , &= , |= , ^=
{{< tdclose >}}
{{< tdopen >}}
assignment operators
{{< tdclose >}}

{{< trclose >}}
{{< tropen >}}
{{< tdopen >}}
17
{{< tdclose >}}
{{< tdopen >}}
left
{{< tdclose >}}
{{< tdopen >}}
,
{{< tdclose >}}
{{< tdopen >}}
comma operator
{{< tdclose >}}

{{< trclose >}}

{{< tableclose >}}

Conversions: C++ defines a set of standard conversions, implicit type conversions, that are used in arithmetic conversions, assignments using different data types, and passing arguments to a function of different data types than the function parameters. In particular, when we have such mixed expressions the compiler makes some standard conversions, e.g. in binary operations the lower data type is promoted to the higher one (which dominates), so as to avoid losing information.

The following order is used:  
  
          **_bool, char, short int \< int \< long int \< float \< double \< long double_**  
_  
bool_, _char_ and _short int_ are always converted to int whenever they appear in any expression, i.e. before performing any operation on them. A bool is promoted to int, getting the value 1 or 0, depending on its value (true or false, respectively). When a number is converted to a type bool all values other than zero are converted to true and a zero value is converted to false. Integer constants (e.g. 17) are considered _int_, and, floating point constants (e.g. 4.53) are considered _double_. We can use L after an integer and a floating point constant to define that should be considered as a long int, and, a long double, respectively.

In C++, we can also define rules of conversions to be used with operators applied on user-defined data types.

We can also explicitly define type conversions using casting to force the explicit conversion from one data type to another.

_(dataType) variableOrExpression ; _ and   _dataType (variableOrExpression) ;_

Another way do an explicit conversion, i.e. to cast a data type constant or variable to another data type, is using the keyword static\_cast followed by a data type name surrounded by angle brackets and the certain variable or constant to cast within parentheses, e.g.  
_  
static\_cast \<dataType> (variableOrExpression)_  
_static\_cast \<float> (5) / 3        _             //  gives  1.66667

**_/\* Example: Mixed Expressions - Precedence - Associativity - Casting \*/_**

_#include \<iostream.h>_  
_main()_  
_{_  
 _int i=4 ;_  
 _float f = 2.5 ;_  
 _double d = 3;_

 _cout \<\< "\\n  i  / 5 \* f = "            // Mixed Expressions_  
 _\<\<  i  / 5 \* f  \<\< endl ;_

 _cout \<\< "\\n 'a'  = "    \<\<  'a' \<\< endl ;_

 _cout \<\< "\\n 'a' - 1 = "                // Mixed Expressions_  
 _\<\<  'a' - 1 \<\< endl ;_  
 _cout \<\< "\\n 'f' - 'd' = "              // Mixed Expressions_  
 _\<\<  'f' - 'd' \<\< endl ;_

 _cout \<\< "\\n  f + 5 \* d = "                 // Precedence_  
 _\<\<  f + 5 \* d  \<\< endl ;_

 _cout \<\< "\\n  f \* 2 \* 2.5 = "               // Associativity_  
 _\<\<  f \* 2 \* 2.5  \<\< endl ;_

 _cout \<\< "\\n (float) i  / 5 \* f = "         // Casting_  
 _\<\<  (float) i  / 5 \* f  \<\< endl ;_  
 _cout \<\< "\\n float i  / 5 \* f = "         // Casting_  
 _\<\<  float (i)  / 5 \* f  \<\< endl ;_  
 _cout \<\< "\\n static\_cast \<float> (5) / 3 = "     // Casting_  
 _\<\< static\_cast \<float> (5) / 3 \<\< endl;_  
_}_

Results
-------

 _i  / 5 \* f = 0               float 0.0_

 _'a'  = a                      character_

 _'a' - 1 = 96                  int 96_

 _'f' - 'd' = 2                  int 2_

 _f + 5 \* d = 17.5        double 17.5_

 _f \* 2 \* 2.5 = 12.5      double  12.5_

 _(float) i  / 5 \* f = 2      float 2_  
 _float(i)  / 5 \* f = 2      float 2_  
 _static\_cast \<float> (5) / 3 = 1.66667_

{{< anchor "11_input" >}}{{< /anchor >}}11\. Input/Output Operators
-------------------------------------------------------------------

In C++ the predefined objects _cin_, _cout_ and _cerr_ are available for input and output operations. The predefined object **_cin_** refers to the standard input (which is by default the keyboard), **_cout_** and **_cerr_** refer to the standard output and the standard error, respectively (which are both by default the display). These defaults can be changed using redirection while executing the program.

The **output operator** (\<\<) (known as insertion operator) directs (display) output information on your standard output (screen), e.g.  
 _cout \<\< "\\n  x = " \<\< x \<\< endl ;_  
"\\n" represents a new line character, while _endl_ inserts a new line and flushes the output buffer. The operating system buffers the output to the display characters and prints them out in a batch to minimize I/O overhead. This may lead to wrong indications of where the error may be if we consider the printed out information without flushing the buffer.  
We may have several output operators in the same output statement

Similarly, you can use the **input operator** (>>) to obtain (read) input values from the standard input (keyboard). e.g.:  
 _cout \<\< "\\n x = "  ;_  
 _cin >> x ;    cin >> y >> z;_

The standard input-output library (_iostream.h_) must be included using a preprocessor directive, in order to be able to use the input and output operators, as well as the manipulators without arguments such as _endl, flush, hex, oct_, etc.

Certain options may be specified when using the output stream operator to select the way that the output should look. The precision can be set using a iostream manipulator, the _setprecision(number\_of\_digits)_, while the _setiosflags(options separated by |)_ can be used e.g. to specify whether the decimal point or tailing zeros should be shown. The _setw()_ specifies the field width in which the next value should be printed out. It is the only manipulator that does not apply to all subsequent input or output, but becomes zero as soon as something is printed. The _setfill(c)_ makes c the fill character. To use these parameterized stream manipulators (i.e. with arguments) we need to include the _iomanip.h_ header file. e.g.:  
 _cout \<\< setprecision(2) \<\< setiosflags(ios::fixed | ios::showpoint)_  
 _\<\< "\\n\\n 3. = " \<\< 3. \<\< "\\t 0.333333 = " \<\< 0.333333 \<\< endl;_  
(will give: 3.=3.00    0.333333 = 0.33)

We can also redirect the input from the keyboard to a file and the output to another file:  
 _athena%  executable\_file\_name  \<  input\_file\_name      >  output\_file\_name_

Finally, there is a standard error stream cerr which is used to display error messages  
  
      _cerr \<\< "\\n Not proper values were provided!"  ;_

The following member functions can be invoked by the input stream, _**cin**: cin.good()_ returns true if everything is ok;, _cin.eof()_ return true if EOF is reached; _cin.fail()_ returns true if a format error has occurred.

The C input/output functions**_scanf()/printf()_** can also be used, since C is a subset of C++. In that case the _stdio.h_ header file (which contains their prototypes) must be included. Then, the buffer can explicitly be flushed using "_fflush(stdout);_".

However, when both C input/output functions and C++ input and output operators are used, you need to provide the following function call before doing any input or output, to avoid problems:  
 _ios::sync\_with\_stdio();_

{{< anchor "12_preprocessors" >}}{{< /anchor >}}12\. Preprocessor Directives
----------------------------------------------------------------------------

The preprocessing takes place prior to the actual compilation. The preprocessor searches all files that are to be compiled and takes action according to the preprocessor directives. The preprocessor directives are the lines which begin with # (usually placed at the top of the source code file).

An **include preprocessor directive** results in the substitution of it, with the contents of the indicated file. i.e. the following include preprocessor directive:  
 _#include \<file.h>_  
  
is equivalent to typing the contents of the included file at that point.

There are two variations of the include preprocessor directive:  
  
       _#include \<file.h> _     or      _#include "file.h"_  
  
The difference is that in the first case the preprocessor searches for the included file in the standard include directory, while in the second case it searches in the current directory. The latter case is usually used for the user written functions.

Another preprocessor directive is the #define which it can be used to associate a token string with an identifier, e.g.  
 _#define PI 3.1415926_

The preprocessor will replace PI wherever it appears in a file with the provided token. After the preprocessing finishes the compilation starts, in which the token is treated as a floating point constant.

Other preprocessor directives are the following: #_ifdef_, #_ifndef_, and, #_endif_  They can be used for conditional compilation.  
e.g. the ...... statements will be skipped if  \_MY\_HEADER\_H has already been defined.  
 _#ifndef \_MY\_HEADER\_H_  
 _#define \_MY\_HEADER\_H_  
 _........_  
 _#endif_

Also, while compiling a program we can define a preprocessor constant on the command line using the -D option followed by the name of the preprocessor constant and therefore certain parts of the code can be selectively excluded.  
  
e.g. compiling the file with -DDEBUG\_MODE option will consider the cout statement:  
 _#ifdef DEBUG\_MODE_  
 _cout \<\< "\\n testing debug mode \\n" \<\< endl;_  
 _#endif_

The define directive can also be used to specify macro substitutions with variable parameters. e.g. having defined the following macro using:               
  
#_define mult(x,y)  (x\*y)_  
  
then, the following statement:                   _product = 267.2 + mult(25.7, 33.6)_  
will be replaced during preprocessing by:     _product = 267.2 + (25.7 \* 33.6)_

{{< anchor "13__Header_files" >}}{{< /anchor >}}

13\. Header Files
-----------------

To be able to use the input and output operators you must first include the standard input-output library (**_iostream.h_**) using a preprocessor directive:  
 _#include \<iostream.h>_

When the C input/output functions _scanf()/printf()_ are used the **_stdio.h_** header file (which contains their prototypes) must be included instead.

Similarly to be able to use any other standard library function you need to include its header file which contains all necessary declarations.  
e.g. to be able to use the math function, such as _sqrt()_ you need to include the **_math.h_** header file using the following command:  
 _#include \<math.h>_

When the header file that you include is in the current directory, e.g. a header file that you wrote, then you should use double quotes, instead of  
brackets, e.g.:  
 _#include "myheader.h"_

According to the new ANSI/ISO standard, which however is not followed by all available compilers yet, the iostream header file can be included using:  
  
  _#include \<iostream>_  
 _using namespace std;_  
 _int main()_  
 _{_  
 _std::cout \<\< "\\n testing:_  
 _pi = " \<\< 3.1415 \<\< endl;_  
 _}_

Header files are very useful to provide **declarations** (e.g. for global variables and functions) in order to avoid incompatible declarations which may happen when multiple declarations are provided in several source-code files. In addition, any changes to a declaration would require only a single local modification instead of having to update all appearances of the declarations. A header file should never contain definitions, (unless its a definition of an inline function).

{{< anchor "14_control" >}}{{< /anchor >}}14\. Control Structures
-----------------------------------------------------------------

Control statements are used to control the flow of our programs which is normally sequential. i.e. statements are executed one after the other in order. Changing this sequential execution in a controlled way is called transfer of control and is achieved using control structures.

The C++ control structures are identical with those of C. The **relational** operators ( > , \< , >= ,  \<= ), **equality** operators ( ==  ,  != ), and the **logical** operators (&& , || ,  !) are used in logical tests which produce either true or false (0).

Typically, the following operators are used to form a logical test for the control structures which determines what action should be taken:

*   the **relational** operators: > , \< , >= , and \<=  (which are used to compare two expressions)
*   the **equality** operators: == and !=   (which are used to check two expressions for equality)
*   the **logical** operators: && , || , and !

The result of the above operators is of type bool, either true (i.e. 1), or false (i.e. 0). You should never compare floating-point values for equality or inequality, since the floating-point numbers can, in general, only be approximated since only a small number of digits are used for computer representation of values.

In all control structures, a simple (i.e. single), or a compound, i.e. a sequence of statements enclosed in curly braces, statement is either conditionally or repeatedly executed, based on a logical test.

The**_if_** and **_if-else_**, as well as the switch control structures are used to make certain selections  
The simplest selection control structure is the if, where if the logical test is true (i.e. non zero), then the following statement (or statements in curly braces) is (are) executed. Otherwise the statement (or statements) is (are) skipped and the statement after the if control structure is executed.  
 _if (logical test)_  
 _statement ;_

**_if-else if-...-else_** control structure provides several alternative actions. (It is more efficient to put the most probable selection first to reduce the chances of multiple checks)  
 _if (logical test)_ (if-else if -else provides alternative actions)  
 _{_  
 _statements_ (executed if (logical test) is true)  
 _}_  
 _else if  (another logical test)_ (checked  if (logical test) is false)  
 _{_  
 _statements_  
 _}_  
 _else_ (executed if not any (logical test) is true)  
 _{_  
 _statements_  
 _}_

The**_switch()_** control structure is useful when there are many different selections. It consists of multiple selection cases and an optional default case. Only constant integral expressions can be checked in _switch()_ cases. The controlling expression in the parentheses determines which of the cases should be executed and starts executing statements in that case continuing until the closing brace of the switch control structure, or until a break is reached. The break causes the program to exit the switch structure and execute the next statement after it.  
 _switch (x)_  
 _{_  
 _case 1:_  
 _statements_  
 _break;_  
 _case 2: case ’b’: case ’B’:_  
 _statements_  
 _break;_  
 _case 3:_  
 _case ’c’:_  
 _statements_  
 _break;_  
 _........_  
 _default:_  
 _........._  
 _}_  
 

**_while_**, **_do/while_**, and **_for_** are the **repetition control structures** of C++, i.e. are used when iterations are required.

The statements of the **_while_** control structure are executed repeatedly as long as the logical test is true, and, at each iteration when the closing brace is reached, control is passed back at the beginning of the while loop. The while loop is continuously repeated until the logical test becomes false (i.e. equal to zero)  
 _while(logical test)_  
 _{_  
 _statements_    // statements executed repeatedly as  
                                       // long as the logical test is true  
 _}_

The **_do/while_** is similar to while with the only difference that its body is executed at least once since the check is done at the end.  
 _do_  
 _{_  
 _statements_ // executed repeatedly as long as the logical test  
 _} while(logical test);             //_ is true but always executed at least once

The **_for_** control structure is used for repetitions, when we have a regular incrementing. First, expr1 is evaluated, which is usually used to initialize the loop variables. Then, the logical test (which is a loop continuation condition) is evaluated, and if it is true (i.e. nonzero), the following statements, within the curly braces, are executed. Finally, expr3 is executed (usually providing an increment or decrement of the control variable), and then the procedure from evaluation of the logical test is repeated, as long as it is true (i.e. non zero.) expr1 and expr2 can be comma separated lists of expressions, which are executed from left to right. All three expressions are optional, although the two semicolon are always required.  
 _for (expr1 ;  logical test ; expr3)_  
 _{_  
 _statements in body of for loop_  
 _}_

Finally, the following control structure is the **_conditional operator_** which produces a value based on the logical test. Therefore, it can be placed inside another expression. The first expression after the question mark is executed if the logical test is true. Otherwise, the expression after the colon is executed.  
 _( logical test)  ?  when\_true\_statement : when\_false\_statement ;_

e.g.:   _max = (x>y) ? x : y ;_  
 _(i%2) ? cout \<\< i \<\< " is an odd integer" : cout \<\< i \<\< " is an even integer" ;_

The **_break_** statement is typically used to skip the remainder of the switch statement. It is also used to exit repetition control structures (i.e. _while_, _do/while_ and _for_). In all these cases execution continues with the first statement after the terminated control structure. The break statement exits the innermost loop, or switch statement.

The **_continue_** statement is used to skip the current iteration of a repetition control structure and continue with the next iteration, if there is one, i.e. the current iteration only is terminated and execution continues with the evaluation of the logical test of the next iteration. It goes to the next iteration of the innermost loop.