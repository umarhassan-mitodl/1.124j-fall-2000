---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Java Basics (contd.)
uid: 1fb0b094-6d59-959f-123e-af70d2c33483
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Interfaces](#1)
2.  [Exceptions and Error Handling](#2)

{{< anchor "1" >}}{{< /anchor >}}1\. Interfaces
-----------------------------------------------

An interface declares a set of methods and constants, without actually providing an implementation for any of those methods. A class is said to _implement_ an interface if it provides definitions for all of the methods declared in the interface.

Interfaces provide a way to prescribe the behavior that a class must have. In this sense, an interface bears some resemblance to an abstract class. An abstract class may contain default implementations for some of its methods; it is an incomplete class that must be specialized by subclassing. By constrast, an interface does not provide default implementations for any of the methods. It is just a way of specifying the functions that a class should contain. There is no notion of specialization through function overriding.

Some points to note about interfaces:

A class may implement more than one interface, whereas it can only extend one parent class.

An interface is treated as a reference type.

Interfaces provide a mechanism for callbacks, rather like pointers to functions in C++.

An interface can extend another interface.

Here is an example of using an interface.

_import java.util.\*;_

_interface Collection {_  
 _final int MAXIMUM = 100;            // An interface can only have constant data._  
 _public void add(Object obj);_  
 _public void remove();_  
 _public void print();_  
_}_

_class Stack implements Collection {           // A last in first out (LIFO) process._  
 _Vector mVector;_

 _public Stack() {_  
 _mVector = new Vector(0);                // Create an empty vector._  
 _}_

 _// This adds an element to the top of the stack._  
 _public void add(Object obj) {_  
 _if (mVector.size() \< MAXIMUM)     // Restrict the size of the Stack._  
 _mVector.insertElementAt(obj, 0);_  
 _else_  
 _System.out.println("Reached maximum size");_  
 _}_

 _// This removes an element from the top of the stack._  
 _public void remove() {_  
 _mVector.removeElementAt(0);_  
 _}_

 _// This prints out the stack in order from top to bottom._  
 _public void print() {_  
 _System.out.println("Printing out the stack");_  
 _for (int i = 0; i \< mVector.size(); i++)_  
 _System.out.println(mVector.elementAt(i));_  
 _}_  
_}_

_class Queue implements Collection {           // A first in first out (FIFO) process._  
 _Vector mVector;_

 _public Queue() {_  
 _mVector = new Vector(0);                 // Create an empty vector._  
 _}_

 _// This adds an element to the bottom of the queue._  
 _public void add(Object obj) {_  
 _if (mVector.size() \< MAXIMUM)      // Restrict the size of the Queue._  
 _mVector.addElement(obj);_  
 _else_  
 _System.out.println("Reached maximum size");_  
 _}_

 _// This removes an element from the top of the queue._  
 _public void remove() {_  
 _mVector.removeElementAt(0);_  
 _}_

 _// This prints out the queue in order from top to bottom._  
 _public void print() {_  
 _System.out.println("Printing out the queue");_  
 _for (int i = 0; i \< mVector.size(); i++)_  
 _System.out.println(mVector.elementAt(i));_  
 _}_  
_}_  
 

_class Main {_  
 _public static void main(String\[\] args) {_

 _// Create a stack and add some objects to it.  The function CreateSomeObjects takes a_  
 _// reference to the Collection interface as an argument, so it does not need to know anything_  
 _// about the Stack class except that it supplies all the methods that the Collection interface_  
 _// requires.  This is an example of using callbacks._  
 _Stack s = new Stack();_  
 _CreateSomeObjects(s);_

 _// Remove an element from the stack and then print it out._  
 _s.remove();_  
 _s.print();         // This will print out the elements 3,7,5._  
 

 _// Create a queue and add some objects to it._  
 _Queue q = new Queue();_  
 _CreateSomeObjects(q);_

 _// Remove an element from the queue and then print it out._  
 _q.remove();_  
 _q.print();         // This will print out the elements 7,3,4._  
 _}_  
 

 _// Create some objects and add them to a collection.  Class Integer allows us to create integer_  
 _// objects from the corresponding primitive type, int._  
 _public static void CreateSomeObjects(Collection c) {_  
 _c.add(new Integer(5));_  
 _c.add(new Integer(7));_  
 _c.add(new Integer(3));_  
 _c.add(new Integer(4));_  
 _}_  
_}_

{{< anchor "2" >}}{{< /anchor >}}2\. Exceptions and Error Handling
------------------------------------------------------------------

What happens when a program encounters a run-time error? Should it exit immediately or should it try to recover? The behavior that is desired may vary depending on how serious the error is. A "file not found" error may not be a reason to terminate the program, whereas an "out of memory error" may. One way to keep track of errors is to return an error code from each function. Exceptions provide an alternative way to handle errors.

The basic idea behind exceptions is as follows. Any method with the potential to produce a remediable error should declare the type of error that it can produce using the _throws_ keyword. The basic remediable error type is class _Exception_, but one may be more specific about the type of exception that can be thrown e.g. _IOException_ refers to an exception thrown during an input or output operation. When an exception occurs, we use the _throw_ keyword to actually create the _Exception_ object and exit the function.

Code that has the potential to produce an exception should be placed within the _try_ block of a _try-catch_ statement. If the code succeeds, then control passes to the next statement following the _try-catch_ statement. If the code within the _try_ block fails, then the code within the _catch_ block is executed. The following example illustrates this.  
 

_class LetterTest {_  
 _char readLetter() throws Exception {        // Indicates type of exception thrown._  
 _int k;_

 _k = System.in.read();_  
 _if (k \< 'A' || k > 'z') {_  
 _throw new Exception();                  // Throw an exception._  
 _}_

 _return (char)k;_  
 _}_

 _public static void main(String\[\] args) {_  
 _LetterTest a = new LetterTest();_

 _try {_  
 _char c = a.readLetter();_  
 _String str;_  
 _str = "Successfully read letter " + c;_  
 _System.out.println(str);_  
 _}_  
 _catch (Exception e) {                           // Handle the exception._  
 _System.out.println("Failed to read letter.");_  
 _}_  
 _}_  
_}_  
 

Note: in addition to the _Exception_ class, Java® also provides an _Error_ class, which is reserved for those kinds of problems that a reasonable program should not try to catch.