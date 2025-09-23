---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Makefile Primer
uid: 6d7097bb-1b92-3e77-7a6b-fe4a29d36d40
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

How to Use _make_
-----------------

Introduction
------------

_make_ is a command generator which generates a sequence of commands for execution by the UNIX® shell. These commands usually relate to the maintenance of a set of files in a software development project. We will use _make_ to help us organize our C++ and C source code files during the compilation and linking process. In particular, _make_ can be used to sort out the dependency relations among the various source files, object files and executables and to determine exactly how the object files and executables will be produced.

Invoking _make_ from the Command Line
-------------------------------------

_make_ may be invoked from the command line by typing:

make -f make filename program

Here, _program_ is the name of the **target** i.e. the program to be made. _makefilename_ is a **description file** which tells the _make_ utility how to build the target program from its various **components**. Each of these components could be a target in itself. _make_ would therefore have to build these targets, using information in the description file, before _program_ can be made. _program_ need not necessarily be the highest level target in the hierarchy, although in practice it often is.

It is not always necessary to specify the name of the description file when invoking _make_. For example,

make program

would cause _make_ to look in the current directory for a default description file named _makefile_ or _Makefile_, in that order.

Furthermore, it is not even necessary to specify the name of the final target. Simply typing

make

will build the first target found in the default description file, together with all of its components. On the other hand, it is also possible to specify multiple targets when invoking _make_.

_make_ Description Files (makefiles)
------------------------------------

Here is an example of a simple makefile:

_program: main.o iodat.o  
           cc -o program main.o iodat.o  
main.o: main.c  
           cc -c main.c  
iodat.o: iodat.c  
           cc -c iodat.c_

Each entry consists of a **dependency line** containing a colon, and one or more **command lines** each starting with a tab. Dependency lines have one or more **targets** to the left of the colon. To the right of the colon are the **component files** on which the target(s) depend.

A command line will be executed if any target listed on the dependency line does not exist, or if any of the component files are more recent than a target.

Here are some points to remember:

*   Comments start with a pound sign (#).
*   Continuation of a line is denoted by a backslash (\\).
*   Lines containing equals signs (=) are macro definitions (see next section).
*   Each command line is typically executed in a separate Bourne shell i.e. _sh_{{< sup "1" >}}.

To execute more than one command line in the same shell, type them on the same line, separated by semicolons. Use a \\ to continue the line if necessary. For example,

_program: main.o iodat.o  
          cd newdir; \\  
          cc -o program main.o iodat.o_

would change to the directory _newdir_ before invoking _cc_. (Note that executing the two commands in separate shells would not produce the required effect, since the _cd_ command is only effective within the shell from which it was invoked.)

The Bourne shell's pattern matching characters maybe used in command lines, as well as to the right of the colon in dependency lines e.g.

_program: \*.c  
           cc -o program \*.c_

Macros
------

_Macro Definitions in the Description File_

Macro definitions are of the form:

_name = string_

Subsequent references to $(_name_) or ${name} are then interpreted as _string_. Macros are typically grouped together at the beginning of the description file. Macros which have no string to the right of the equals sign are assigned the null string. Macros may be included within macro denitions, regardless of the order in which they are defined.

Here is an example of a macro:

_CC = /mit/gnu/arch/sun4x 57/bin/g++  
program: program.C  
           ${CC} -o program program.C  
  
_  
_Shell Environment Variables_

Shell variables that were part of the environment before make was invoked are available as macros within _make_. Within a _make_ description file, however, shell environment variables must be surrounded by parentheses or braces, unless they consist of a single character. For example, ${PWD} may be used in a description file to refer to the current working directory.

_Command Line Macro Definitions_

Macros can be defined when invoking _make_ e.g.

make program CC=/mit/gnu/arch/sun4x\_57/bin/g++  
  
_Internal Macros_

_make_ has a few predefined macros:

1.  $? evaluates to the list of components that are _younger_ than the current target. Can only be used in description file command lines.
2.  $@ evaluates to the current target name. Can only be used in description file command lines.
3.  $$@ also evaluates to the current target name. However, it can only be used on dependency lines.

**Example**

_PROGS = prog1 prog2 prog3  
${PROGS}: $$@.c  
           cc -o $@ $?_

This will compile the three files _prog1.c_, _prog2.c_ and _prog3.c_, unless any of them have already been compiled. During the compilation process, each of the programs becomes the current target in turn. In this particular example, the same effect would be obtained if we replaced the $? by $@.c

_Order of Priority of Macro Assignments_

The following is the order of priority of macro assignments, from least to greatest:

1.  Internal (default) macro definitions.
2.  Shell environment variables.
3.  Description file macro definitions.
4.  Command line macro definitions.

Items 2. and 3. can be interchanged by specifying the _\-e_ option to _make_.

_Macro String Substitution_

String substitutions may be performed on all macros used in description file shell commands. However, substitutions occur only at the end of the macro, or immediately before white space. The following example illustrates this:

               LETTERS = abcxyz xyzabc xyz  
               print:  
                         echo $(LETTERS:xyz=def)

This description file will produce the output

               abcdef xyzabc def

Suffix Rules

The existence of naming and compiling conventions makes it possible to considerably simplify description files. For example, the C compiler requires that C source files always have a .c suffix. Such naming conventions enable _make_ to perform many tasks based on **suffix rules**. _make_ provides a set of default suffix rules. In addition, new suffix rules can be defined by the user.

For example, the description file on page 2 can be simplified to

_program:_ _main.o iodat.o  
            cc -o program main.o iodat.o_

_make_ will use the following default macros and suffix rules to determine how to build the components _main.o_ and _iodat.o_.

_CC = cc  
CFLAGS = -O  
.SUFFIXES: .o .c  
.c.o:  
         ${CC} ${CFLAGS} $\<_

The entries on the .SUFFIXES line represent the suffixes which _make_ will consider **significant**. Thus, in building _iodat.o_ from the above description file, _make_ looks for a user-specified dependency line containing _iodat.o_ as a target. Finding no such dependency, _make_ notes that the .o suffix is significant and therefore it looks for another file in the current directory which can be used to make iodat.o. Such a file must

*   have the same name (apart from the suffix) as _iodat.o_.  
    
*   have a significant suffix.  
    
*   be able to be used to make _iodat.o_ according to an existing suffix rule.

_make_ then applies the above suffix rule which specifies how to build a _.o_ file from a _.c_ file. The $\< macro evaluates to the component that triggered the suffix rule i.e. _iodat.c_.

After the components _main.o_ and _iodat.o_ have been updated in this way (if necessary), the target _program_ will be built according to the directions in the description file.

_Internal Macros in Suffix Rules_

The following internal macros can only be used in suffix rules.

1.  $\< evaluates to the component that is being used to make the target.  
    
2.  $\* evaluates to the filename part (without any suffix) of the component that is being used to make the target.

Note that the $? macro cannot occur in suffix rules. The $@ macro, however, can be used.

_Null Suffixes_

Files with null suffixes (no suffix at all) can be made using a suffix rule which has only a single suffix e.g.

_.c:  
          ${CC} -o $@ $\<_

This suffix rule will be invoked to produce an executable called _program_ from a source file _program.c_, if the description file contains a line of the form.

          program:

Note that in this particular situation it would be incorrect to specify that _program_ depended on _program.c_, because _make_ would then consider the command line to contain a null command and would therefore not invoke the suffix rule. This problem does not arise when building a _.o_ file from a _.c_ file using suffix rules. A _.o_ file _can_ be specified to depend on a _.c_ file (and possibly some additional header files) because of the one-to-one relationship that exists betweeen _.o_ and _.c_ files.

_Writing Your Own Suffix Rules_

Suffix rules and the list of significant suffixes can be redefined. A line containing ._SUFFIXES_ by itself will delete the current list of significant suffixes e.g.

_.SUFFIXES:  
.SUFFIXES: .o .c  
.c.o:  
             ${CC} -o $@ $\<_


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

References
----------

\[1\] Talbot, S. "Managing Projects with Make." O'Reilly & Associates, Inc.