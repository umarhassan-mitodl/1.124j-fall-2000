---
content_type: page
description: Recitation notes about Exceptions, Threads, I/O, and Java GUI and Swing
draft: false
learning_resource_types:
- Recitations
ocw_type: CourseSection
parent_title: Recitations
parent_type: CourseSection
parent_uid: 08c0c758-213b-77ad-faca-c379a74d5283
title: Recitation 8
uid: c1780287-d0f8-a77d-3b3f-715b457172f9
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---
These notes were prepared by [Petros Komodromos](mailto:komodromos@ucy.ac.cy).

## Topics

1. [**Exceptions**](#1)
2. [**Threads**](#2)
3. [**I/O**](#3)
4. [**Introduction to Java® GUI and Swing**](#4)

## {{< anchor "1" >}}{{< /anchor >}}1\. Exceptions

Java® provides ways to manage *exceptions*, i.e. errors that may occur during the execution of a program that disrupt the normal flow of instructions. When an unexpected error condition happens during runtime a Java program "*throws*" an exception. This can avoid the premature termination of the program, which in some cases is not necessary. A function that detects an error throws an exception, which can be caught by an *exception handler*. The exception object contains information about the exception, e.g. its type and the state of the program when the error had occurred.

The runtime system tries to find some code to handle the error, i.e. an *exception handler*. The exception causes a search through the call stack to find an appropriate handler to handle the exception. The Java® runtime system searches backwards through the call stack to find any methods that are interested in handling a particular exception. The corresponding, or the default, exception handler catches the exception and may throw a new exception or attempt to handle the exception. If the runtime system, after an exhaustive search of all the methods on the call stack, cannot find an encompassing exception handler the exception is caught by a default exception handler. The latter, usually, prints information about the thrown exception, e.g. where it was thrown, and, then, the runtime system, and, consequently, the Java® program, terminate. An exception handler can catch an exception based on its group or general type by specifying any of the exception's superclasses in the catch statement.

An exception in Java® is an object which is a subclass of the class *Throwable*, and, in most cases, it is derived by the class *Exception*, which is a subclass of *Throwable*. The *Throwable*  class is the superclass of all errors and exceptions in the Java® language. Only objects that are instances of this class, or of one of its subclasses, can be *thrown* by the Java® VM, or by a Java® *throw* statement.

In Java®, exceptions are managed by first trying something in a *try{….}* compound block. The code that might throw an exception is placed in a *try* block. If an error occurs in that block an exception is thrown. Then, a *catch{…..} block* is used to catch any exception that is thrown. Zero or more *catch* blocks may follow the try block. The code that may provide the action that must be taken in the case of a certain exception occurs is provided in a *catch* block that follows the *try* block. Each *catch* block specifies the type of exception it can catch. Only the *Throwable* class or one of its subclasses can be the argument type in a *catch* clause. An optional *finally {….}* block, which follows the last *catch* block or the try block when there are no *catch* blocks, provides code that is executed in any case, i.e. regardless whether an exception occurs or not.

**Example**

*class Exceptions1*   
*{*   
*public static void main(String args\[\])*   
*{*   
*double d\[\] = new double\[4\];*   
*for(int j=0 ; j\<d.length ; j++)*   
*d\[j\] = j\*7.15 + 2.19 ;*

*for(int j=0 ; j\<=d.length ; j++)*   
*{*   
*try{*   
*System.out.print( "  d\[" + j + "\] / " + j + " = ");*   
*if(j==0)*   
*& #160;  throw new DivideByZeroException();*   
*System.out.println(d\[j\]/j);*   
*}*   
*catch(ArrayIndexOutOfBoundsException e)*   
*{*   
*System.out.println("Exception: " + e.getMessage());*   
*System.out.print("e.printStackTrace(): ");*   
*e.printStackTrace();*   
*}*   
*catch(DivideByZeroException e)*   
*{*   
*System.out.println("Exception: " + e.getMessage());*   
*}*   
*finally*   
*{*   
*System.out.println("Inside finally()\\n");*   
*}*   
*}*

*System.out.println( "\\n  Program exiting \\n");*   
*}*   
*}*

*class DivideByZeroException extends ArithmeticException*   
*{*   
*DivideByZeroException()*   
*{*   
*super("Trying to divide by zero");*   
*}*   
*}*   
 

***Output:***

*d\[0\] / 0 = Exception: Trying to divide by zero*   
*Inside finally()*

*d\[1\] / 1 = 9.34*   
*Inside finally()*

*d\[2\] / 2 = 8.245000000000001*   
*Inside finally()*

*d\[3\] / 3 = 7.880000000000002*   
*Inside finally()*

*d\[4\] / 4 = Exception: null*   
*e.printStackTrace(): java.lang.ArrayIndexOutOfBoundsException*   
*at Exceptions1.main(Compiled Code)*   
*Inside finally()*

*Program exiting*   
 

A *checked exception* requires the specification of the way that the exception should be handled. If a function may result in a *checked exception*, this must be defined using the keyword *throws* at the definition of the class, after its name. A method can only throw checked exceptions that have been specified in its declaration. Java® requires that a method should either catch, or specify all checked exceptions that can be thrown within the scope of that method.

*Unchecked exceptions* are of type *RuntimeException*, *Error*, or subclasses of them, and can be thrown anywhere without the need to specify the possibility of such exceptions to be thrown. Classes *Exception* and *Error* are subclasses of the class *Throwable\_*,\_ as shown in the following figure, which was adapted from Sun's Java® Tutorial. Class *RuntimeException* is a subclass of the class *Exception*.

\<section data-uuid="f494f101-342f-990d-5567-57018b331777">\</section>

Any method (i.e. function) that may produce a non-RuntimeException should declare the type of exception that it can produce using the *throws* keyword, or that exception should be caught in a *try/catch* block in the method. The basic error type is class *Exception*, although there are more specific types of exceptions. When a checked exception occurs, the *throw* keyword may used to actually create the *Exception* object and either an exception handler should catch and handle the exception, or the function exits. Java® uses the "termination model of exception", since control cannot return to the *throw point,* when an exception is thrown.

Code that may produce an exception is placed within the try block of a *try-catch* statement. If the code within the *try* block fails, the code within a corresponding *catch* block, if exists, is executed. When an exception is thrown the control goes out of the *try* block and searches the *catch* blocks to find an appropriate handler. If the code succeeds, then control passes to the next statement following the *try-catch* statement or to the finally block. In the presence of a *finally* block, the latter is also executed irrespectively of whether an exception has occurred. If no exception handler is found for an exception, the search continues in the enclosing try block and a Java® application terminates if no exception handler is eventually found.

Class *Error*  is, also, provided in Java® to be used for serious problems that should not be caught. The *Error* class is a subclass of the *Throwable* class. *RuntimeExceptions* should be dealt directly rather than throw an exception.

The main advantages of using exception handling are that regular code is separated from error handling code making the code much more readable. Also, error types can be grouped together, and the errors can propagate up the call stack to find a proper exception handler.

However, use of exception handling for purposes other than error handling should be avoided since it can cause a performance overhead. Exception handling should be used only when a method is unable to detect and process an error and, thus, it throws an exception under an exceptional situation, instead of processing it locally. You should avoid using exception-handling for purposes other than error handling. The latter reduces clarity but also results in an execution time overhead imposed by the exception handling code. However, when an exception does not occur there is almost no execution overhead.

An exception handler can do several things such as try to recover and resume execution, rethrow an exception, throw a different type of exception. As soon as the exception handler begins execution the *try* block has expired, and control is in a different scope. If an exception occurs in a handler, it may be processed only by code outside the *try* block in which the original exception had been thrown. Similarly, a rethrown exception can be caught only by an exception handler after the next enclosing *try* block.

A subclass class overridden method can have in its *throws list* only the same with, or a subset of, its superclass's method throws list.

## {{< anchor "2" >}}{{< /anchor >}}2\. Threads

A *threat* is a single sequence of steps executed one at a time, i.e. a sequential flow of control, running within a program and taking advantage of the resources allocated for that program and its environment.

*Multithreading* allows to a program to perform several tasks, i.e. to use more than one flow of control, concurrently. All threads of a multithreading Java® program share the same data and system resources, running at the same time and performing different tasks. Since most computers have only one CPU, threads share the CPU with other threads.

Threats can be used by one of the following ways:

By providing a subclass of the *Thread* class

By providing a class that implements the *Runnable* interface.

 1. Providing a subclass of the *Thread* class:

We need to provide a subclass of the *Thread* class. This subclass should override the *run()* method of class *Thread*. The latter must contain all code that is to be executed within the thread. An instance of the subclass can then be allocated and started.

*class MyThreadClass extends Thread*   
*{*

*public void run()*   
*{*   
*// Code to be executed within the thread*   
*}*

*}*   
 

Then, we can create a new thread by instantiating a subclass of the *Thread* class. Then, we can configure the thread, e.g. by setting its initial priority, name, etc. Finally, we can run it, by calling the *start()* method that is inherited from the class *Thread,* which invokes the new thread's *run()* method.

> *MyThreadClass x = new MyThreadClass();*   
> *x.start();*

However, using this approach is not possible when we need to extend some other class, since Java® does not allow multiple inheritance.

**Example**

*class MyThreadClass extends Thread*   
*{*   
*String name;*

*MyThreadClass(String str)*   
*{*   
*name = str;*   
*}*

*public void run()*   
*{*   
*for(int i=0; i\<5;i++)*   
*{*   
*System.out.println("Thread: " + name);*   
*try*   
*{*   
*Thread.sleep((int) (Math.random()\*1000));*   
*}*   
*catch(InterruptedException e)*   
*{*   
*System.out.println("Catch: " + getName());*   
*}*   
*}*   
*}*

*}*

*class ThreadExample1*   
*{*   
*public static void main(String args\[\])*   
*{*   
*MyThreadClass  th1 = new MyThreadClass("Thread-1");*   
*MyThreadClass  th2 = new MyThreadClass("Thread-2");*   
*MyThreadClass  th3 = new MyThreadClass("Thread-3");*   
 

*th3.start();*   
*th1.start();*   
*th2.start();*

*}*   
*}*

*Output: *   > java ThreadExample1

> *Thread: Thread-3*   
> *Thread: Thread-1*   
> *Thread: Thread-2*   
> *Thread: Thread-1*   
> *Thread: Thread-1*   
> *Thread: Thread-3*   
> *Thread: Thread-1*   
> *Thread: Thread-2*   
> *Thread: Thread-3*   
> *Thread: Thread-1*   
> *Thread: Thread-3*   
> *Thread: Thread-2*   
> *Thread: Thread-3*   
> *Thread: Thread-2*   
> *Thread: Thread-2*

2\. Implementing the Runnable Interface

The other way to create a thread is to declare a class that implements the *Runnable* interface. The *Runnable* interface requires the implementation of the *run()* method, in which all code that is to be executed within the thread should be placed. An instance of the class can then be allocated. Finally, a *Thread* object can be created passing as an argument the object of the class that implements the *Runnable* interface, and, then start the thread.

*class MyRunnableClass implements Runnable*   
*{*

*public void run()*   
*{*   
*//  Code to be executed within the thread*   
*}*

*}*

A new thread can by created by creating a *Thread* object using an object of type *MyRunnableClass*, and, then, by calling the *start()* method, of the *Threat* class, which runs the thread.

> *MyRunnableClass x = new MyRunnableClass();*   
> *Thread t = new Thread(x);*   
> *t.start();*

**Example**

*class MyRunnableClass implements Runnable*   
*{*   
*String name;*

*MyRunnableClass(String str)*   
*{*   
*name = str;*   
*}*

*public void run()*   
*{*   
*for(int i=0; i\<5;i++)*   
*{*   
*System.out.println("Thread: " + name);*   
*try*   
*{*   
*Thread.sleep((int) (Math.random()\*1000));*   
*}*   
*catch(InterruptedException e)*   
*{*   
*System.out.println("InterruptedException in " + name + " thread.");*   
*}*   
*}*   
*}*

*}*

*class ThreadExample2*   
*{*   
*public static void main(String args\[\])*   
*{*   
*MyRunnableClass  r1 = new MyRunnableClass("Thread-1");*   
*MyRunnableClass  r2 = new MyRunnableClass("Thread-2");*   
*MyRunnableClass  r3 = new MyRunnableClass("Thread-3");*

*Thread th1 = new Thread(r1);*   
*Thread th2 = new Thread(r2);*   
*Thread th3 = new Thread(r3);*

*th3.start();*   
*th1.start();*   
*th2.start();*

*}*   
*}*   
 

*Output:*      > java ThreadExample2

> *Thread: Thread-3*   
> *Thread: Thread-1*   
> *Thread: Thread-2*   
> *Thread: Thread-2*   
> *Thread: Thread-2*   
> *Thread: Thread-1*   
> *Thread: Thread-3*   
> *Thread: Thread-2*   
> *Thread: Thread-3*   
> *Thread: Thread-2*   
> *Thread: Thread-1*   
> *Thread: Thread-1*   
> *Thread: Thread-3*   
> *Thread: Thread-3*   
> *Thread: Thread-1*

States of a thread during its lifetime:

*New*: A new thread is one that has been created, i.e. using the new operator, but has not yet been started.

*Runnable (ready state)*: A thread becomes runnable once its *start()* method has been invoked, which means that the code in the *run()* method can execute whenever the thread receives CPU time from the operating system. A threat that had been set to sleep and the time interval has expired, a thread which was waiting and has been notified, a thread that had been suspended and it has been resumed, and a thread that had been blocked by an I/O request and the I/O has been completed are also in a runnable state.

*Not Runnable (blocked state)*: A thread can become not runnable if: the thread's *sleep()* method is invoked (in which case, the thread remains blocked for a specified number of milliseconds, giving a chance to lower-priority threads to run); the thread's *suspend()* method is invoked (in which case, the thread remains blocked until its *resume()* method is invoked); the thread calls the *wait()* method of an object (in which case, the thread remains blocked until either the object's *notify()* method or its *notifyAll()* method is called from another thread); the thread has blocked on an I/O operation (in which case the thread remains blocked until the I/O operation has been completed)

*Dead*: A thread can die either because the *run()* method has finished executing, i.e. has terminated, or because the thread's *stop()* method has been called. The latter should be avoided because it throws a *ThreadDeath* which is a subclass of *Error*.

The following diagram shows the possible life cycle of a thread:

{{< resource uuid="ae8a01ce-c067-8292-35c5-26a24e75c1e2" >}}

Note that the methods *stop(), suspend()*, and *resume()* have been *deprecated*, and, therefore, should be avoided to manage threads. Instead of using the *stop()* method, someone can modify some variable to indicate that the target thread should stop running. The target thread should check this variable regularly, and return from its run method as soon as this variable indicates that it is to stop running. A variable indicating the desired state of the thread can be used to specify whether it should be active or suspended, in order to avoid the *suspend()*, and *resume()* methods. When the desired state is suspended, the thread can wait using the *wait()* method. When the thread is resumed, the target thread is notified using the *notify()* method.

The *wait*() method makes a thread wait until some condition is satisfied. Actually *wait()* not only pauses the corresponding tread but also releases the lock on the object, which allows other threads to invoke synchronized code on that object. The notification methods *notify*() and *notifyAll*() can be used to inform waiting threads that there was some change that might have caused the satisfaction of that condition. Almost always the *notifyAll*() method is used to wake up all waiting threads, while *notify*() picks one of the waiting threads and wakes it up. Notifications affect only threads that have been waiting ahead of the notification, i.e. the *wait*() has been executed before the occurrence of the notification. The wait and notify methods can be invoked only from *synchronized* code, either directly or indirectly (through another method called from the *synchronized* code).

Typically *wait()* is used as follows. Note that the condition test should always be in a loop.

> *synchronized  returnType functionName()*   
> *{*   
> *while(!condition)*   
> *wait();*   
> *statements to be executed when the condition is true*   
> *notifyAll();*   
> *}*

The normal and cleanest way to end a thread's life is having the *run()* method return.

Method *interrupt*() can be used to interrupt a thread execution.

Every thread has a *priority,* which is a number between *Thread.MIN\_Priority* and *Thread.MAX\_Priority*. Threads with higher priority are executed in preference to threads with lower priority. When code running in some thread creates a new *Thread* object, the new thread has its priority initially set equal to the priority of the creating thread.

When multiple threads are runnable (i.e. ready to be executed), the runtime system chooses the runnable thread with the highest priority for execution. Only when that thread stops, yields, or becomes not runnable for some reason a lower priority thread will start executing.

Java® platforms that support time-slicing allow each thread of equal priority to run by providing to all threads a limited amount of the processor's time. On Java® platforms that do not support time-slicing a thread of a given priority runs to completion or until a higher (but not equal) priority thread becomes runnable. Method *yield*(), which is useful only on non-time-slicing systems, allows threads of the same priority to run.

Execution of multiple threads in some order is called *scheduling*. This is supported by  a very simple, deterministic scheduling algorithm (fixed priority scheduling) of the Java® runtime. This algorithm schedules threads based on their priority relative to other runnable threads. The Java® scheduler keeps the highest priority thread running at all times, and when time-slicing is supported allows equal high-priority threads to execute by giving slices of the processor time to them in sequence. In general, it is good practice to have the continuously running part of a program, or  threads that do frequent and continual updates set to MIN\_PRIORITY to avoid blocking other threads.

Threads on multiprocessor machines utilize the multiple processors. A number of the highest-priority threads equal to the number of the available processors execute.

Someone can set and get the name of a threat using the functions *setName()* and *getName()*, respectively, of the *Threat* class. The priority can be set and got using the methods set and get methods of the *Thread* class.

The thread object of the currently running thread can be obtained using the *currentThread()* method of the *Thread* class.

**Example**

*class MyRunnableClass implements Runnable*   
*{*   
*String name;*

*MyRunnableClass(String str)*   
*{*   
*name = str;*   
*}*

*public void run()*   
*{*   
*for(int i=0; i\<5;i++)*   
*{*   
*System.out.println("Thread: " + name);*   
*try*   
*{*   
*Thread.sleep((int) (Math.random()\*3));*   
*}*   
*catch(InterruptedException e)*   
*{*   
*System.out.println("InterruptedException in " + name + " thread.");*   
*}*   
*}*   
*}*

*}*

*class ThreadExample3*   
*{*   
*public static void main(String args\[\])*   
*{*   
*MyRunnableClass  r1 = new MyRunnableClass("Thread-1");*   
*MyRunnableClass  r2 = new MyRunnableClass("Thread-2");*   
*MyRunnableClass  r3 = new MyRunnableClass("Thread-3");*

*Thread th1 = new Thread(r1);*   
*Thread th2 = new Thread(r2);*   
*Thread th3 = new Thread(r3);*

*th2.setPriority(10);*   
*th3.setPriority(1);*

*System.out.println(" th1 priority: " + th1.getPriority());*   
*System.out.println(" th2 priority: " + th2.getPriority());*   
*System.out.println(" th3 priority: " + th3.getPriority() + "\\n");*

*th3.start();*   
*th1.start();*   
*th2.start();*

*}*   
*}*

*Output:*     > java ThreadExample3

> *th1 priority: 5*   
> *th2 priority: 10*   
> *th3 priority: 1*
> 
> > *Thread: Thread-2*   
> > *Thread: Thread-2*   
> > *Thread: Thread-2*   
> > *Thread: Thread-2*   
> > *Thread: Thread-2*   
> > *Thread: Thread-1*   
> > *Thread: Thread-1*   
> > *Thread: Thread-1*   
> > *Thread: Thread-3*   
> > *Thread: Thread-1*   
> > *Thread: Thread-1*   
> > *Thread: Thread-3*   
> > *Thread: Thread-3*   
> > *Thread: Thread-3*   
> > *Thread: Thread-3*

Java®'s garbage collector runs as a low-priority thread when processor time is available and when there are no higher-priority runnable threads.

Each thread may or may not be marked as a *daemon*. A daemon thread is a thread that runs in the background (when the processor is available) for the benefit of other threads. An example of a daemon thread is the garbage collector. When code running in some thread creates a new *Thread* object, the new thread is a *daemon* thread if and only if the creating thread is a *daemon*. Daemon threads do not prevent a program from terminating, since the program exits when only daemon threads remain in it. The Java® VM exits when the only threads running are all daemon threads. The function *setDaemon(boolean on)* can be used, before the thread is started, to mark a thread as a daemon thread or a user thread. If the argument to the *setDaemon(boolean on)* is true, the thread is marked as a daemon thread.

A s\_elfish thread\_ is a thread that never voluntarily gives up the control of the CPU, continuing running until either the thread's run() method terminates, or until the thread is preempted by a higher priority thread. Time-slicing systems do not allow to a selfish thread to keep the control when there are other multiple runnable threads of equal priority, allowing the other threads to run.

In particular, someone should never rely on time-sharing and should write well behaved threads that periodically give up, voluntarily, the control of the CPU, giving to other threads an opportunity to run.

*Race hazard*, or *race condition*, is the situation in which two or more threads can modify the same data in a way that the data can be corrupted by inconsistent changes.

*Starvation* is an indefinite postponement of the execution of lower-priority threads due to higher-priority threads which do not give them the chance to run. Starvation occurs when one (or more threads) in a program cannot progress because it is blocked from gaining access to a certain resource.

*Deadlock* is the worst case of starvation, which occurs when two or more threads are waiting on a condition that cannot be satisfied, e.g. when two (or more) threads are each waiting for the action of the other(s). Race conditions can arise from multiple, asynchronously executing threads that are trying to access a single object (data) at the same time which may result on a wrong result and inconsistencies. Synchronization can be used to avoid such race problems.

When several concurrent threads are competing for resources, *starvation* and *deadlock* should be prevented. Each thread should get enough access to limited resource in order to reasonably progress without causing problems to the other threads or corrupting common data.

*Synchronization*

In some cases separate, concurrently running threads share data in a way that they must take into account the state of other threads. An example of such a case is the so-called *producer/consumer* scenario in which the "producer" thread generates data that are consumed by a "consumer" thread.

In such cases, problems can be avoided using *synchronization,* which allows a thread to lock an object and in case of another thread trying to invoke a synchronized method on the same object, the second thread will be blocked until the object is unlocked from the first thread. A lock is associated with every object that has *synchronized code*.

*Critical code sections* are code segments (e.g. a method) within a program that access the same data (e.g. object) from separate but concurrent threads. In the Java® language, the *synchronized* keyword is used to identify a critical section. Whenever a synchronized method of a class is invoked, the associated object is locked by that method. A synchronized method cannot be called on the same object until the object is unlocked, i.e. another thread cannot invoke a *synchronized* method on that object until the lock is released. When a synchronized method is invoked on an object it obtains its lock, not allowing any other thread to invoke any synchronized method until it releases the lock. A thread can voluntarily call *wait()*, which releases the lock and the processor, and wait in a queue while other threads are able to obtain the lock and invoke *synchronized* code. The methods *notify*() and *notifyAll()* can be used to signal to waiting threads to become ready again and attempt to obtain the lock. If waiting threads are not notified the threads will wait forever causing a deadlock.

Java® locks are *reentrant*, i.e. it is allowed to a thread to re-acquire a lock that it already holds. This avoids problems in which arise when a thread calls from a synchronized method of an object another synchronized method of the same object, which could lead into deadlock.

Static methods can also be *synchronized*. In that case a "class lock" for the corresponding class is used, which does not allow two threads to execute *synchronized* static methods on the same class at the same time.

A *synchronized statement* is an alternative, in some cases, way to execute synchronized code that locks the object so that no *synchronized* method can be invoked on that object, since it is locked.   
 

> *synchronized(objectTobeLocked)*   
> *{*   
> *statements*   
> *}*

## Thread Group

In Java® every Thread object is a member of a thread group, which allows to handle multiple threads, which belong in the same thread group, as a group. The *ThreadGroup* class is used to implement thread groups and allow to deal with the threads in a thread group as a group.

The Java® runtime system creates a ThreadGroup by default, named *main*, as soon as a Java® application starts. A newly created thread is placed in the same group with the thread group in which the thread that created it belongs. Therefore, unless specified otherwise, all new threads that are created become members of the main thread group by default. In an applet a newly created thread may belong to some other than main thread group depending on the browser. A thread cannot change thread group after its creation.

A *ThreadGroup*  can contain any number of threads, which usually, however, are related in some way, and even other ThreadGroup objects. The top-most ThreadGroup in a Java® application is the ThreadGroup named *main*, which is the default thread group.

Method *activeCount*() gives the number of active threads in a thread group plus those in all its child thread groups. The *ThreadGroup* class provides a variety of methods to manage, and operate *ThreadGroup* objects and the *Thread* objects that are members of those thread groups.   
 

## {{< anchor "3" >}}{{< /anchor >}}3\. I/O

The ***System*** class, which is a final class and has private constructors (i.e. not allowing its extension), provides several useful class variables and methods. For example *System.out* is a *PrintStream* object that implements the standard output stream, and *System.getProperty(String key)* is a static method that returns the system property indicated by the specified key.

The ***System*** class provides:

- *in*: the standard input stream to read input data (static *InputStream* object)
- *out*: the standard output stream to output results (static *PrintStream* object)
- *err*: the standard error stream to display error messages (static *PrintStream* object)

Both standard output and error, which are derived from the *PrintStream* class, can invoke one of the *PrintStream's* methods *print()*, *println()*, and *write()* to print text to the stream. The latter method, which is not that common is used to write non-ASCII data, i.e. to write bytes to the stream.

The *java*.io package provides a collection of stream classes that support reading from and writing to an external destination. The provided classes operate on either characters or byte data types.

The abstract superclasses for character streams in *java*.io are the *Reader* (abstract class for reading character streams) and the *Writer* (abstract class for writing to character streams) classes, which partially provide the functionality for the characters reader and writer stream classes, respectively. *\[The following inserted figures have been adapted from the on-line* [*Java® Tutorial*](http://java.sun.com/docs/books/tutorial/) *of SUN\]*

{{< resource uuid="1cbba491-40a5-7fb2-5b61-8b2b09f8ad7f" >}}
{{< resource uuid="dbddd749-9bde-d555-8b04-5f94dcea773b" >}}

In general, readers and writers should be preferred to read and write information since they can handle any character in the Unicode character set because they use 16-bits per character.

Similarly, the abstract superclasses for byte streams in *java.io* are the *InputStream* (abstract class for reading byte streams) and the *OutputStream* (abstract class for writing to byte streams) classes.

{{< resource uuid="1cbac8d9-2fb4-22ad-4bce-f2b8e530b55c" >}}
{{< resource uuid="3aa45619-1b51-aac0-7185-03a7d52afeed" >}}

*Reader* and *InputStream* provide methods for reading characters and bytes, respectively. They also provide methods for marking a location in the stream, skipping input, and resetting the current position. Similarly, *Writer* and *OutputStream* provide methods for writing characters and bytes, respectively.

All readers, input streams, writers, and output streams are automatically opened upon the creation of the corresponding objects. Although they are eligible to be closed by the garbage collector, as soon as they are not referenced in any way, they can be explicitly closed by calling their *close()* method.

The above stream classes can be categorized into two groups: one that deals with reading and writing data, and another that performs some kind of operation on the data while reading and writing. The former are the ones shown with gray color in the above figures, while the latter are the ones shown in white.

A useful class provided by the *java.io* package is the *StreamTokenizer* class. A *StreamTokenizer* object can be created using as argument to its constructor call an *InputStreamReader* object. Then, the *StreamTokenizer* object may be used on an input stream to parses it into tokens, which it reads one at a time.

## {{< anchor "4" >}}{{< /anchor >}}[4\. Introduction to Java® GUI and Swing](http://java.sun.com/docs/books/tutorial/uiswing/TOC.html)

[*Java® Foundation Classes(JFC)*](http://java.sun.com/products/jfc/index.html) provide features to facilitate the development of Graphical User Interfaces (*GUI\_s). Among other, JFC provides* **Swing***\_**,*** which includes several components that can be used for the development of GUIs, support for a choice on the look and feel that a program uses, and provides [*Java®2D*](http://java.sun.com/docs/books/tutorial/2d/index.html) for high quality 2D graphics. Finally, swing allows the specification which look and feel a program should use. This is done with the *setLookAndFeel()* method of the *UIManager* class. ***Swing*** is built on top of the *AWT* (Abstract Window Toolkit) using the AWT infrastructure. However, ***Swing*** provides its own graphical user interface (GUI) components, many of which have a close relation or correspondence to the *AWT* components. Essentially, ***Swing*** is an extension and improvement to the *AWT*.

JFC 1.1 (with Swing API 1.1) is built into *JDK 1.2\_*.\_ The latest JFC development is the JFC/Swing portion of JDK 1.3, which is code-named *Kestrel* and it was released this year.

The Swing API is provided in the following Swing packages:

-  *javax.swing*   (the main swing package)
-  *javax.swing.border*
- *javax.swing.colorchooser*
- *javax.swing.event*
- *javax.swing.filechooser*
- *javax.swing.plaf*
- *javax.swing.plaf.basic*
- *javax.swing.plaf.metal*
- *javax.swing.plaf.multi*
- *javax.swing.table*
- *javax.swing.text*
- *javax.swing.text.html*
- *javax.swing.text.html.parser*
- *javax.swing.text.rtf*
- *javax.swing.tree*
- *javax.swing.undo*

The *AWT* (Abstract Window Toolkit) was first used to develop GUI's in Java®, and provided the foundation on which the JFC and swing were built. The main difference between *AWT* and *Swing* is that the components of the latter are implemented without any native code. Because of this, swing components are called lightweight, while AWT components, which use native code, are called heavyweight components. Lightweight components are drawn entirely using Java®, while heavyweight components use native peers. Actually, *AWT* 1.1 also introduced some lightweight components, while earlier versions were based solely on heavyweight components. *Swing* components, in general, have much more capabilities than the AWT corresponding ones. For instance some Swing components (such as labels and buttons) can display icons, while the corresponding AWT components cannot. *Swing* provides a number of additional components that were not provided by AWT.

*Swing* provides several standard components (e.g. buttons, checkbuttons, radiobuttons, menus, lists, labels, and text areas) to create a program's GUI using one or more containers (e.g. frames, dialogs, windows and tool bars). Most Swing components that begin with J, except the top-level containers, are subclasses of the *JComponent* class. The letter J is used to differentiate the actual extra user interface classes provided by Swing from the support classes that it provides. Swing components inherit many features from the *JComponent* class, such as a configurable look and feel, borders, and tool tips, as well as many methods. In addition, some Swing components can display images on them. The *JComponent* class extends the *Container* class (provides support for adding and laying out components), which itself extends the *Component* class (provides support for  painting, events, layout etc.). *JComponent* is the base class for almost all lightweight J components. Therefore, all swing lightweight components (derived from the *JComponent* class) are subclasses of the *Container* class of *AWT*.

The following article, by Bill Harlan, provides some useful information about [***Improving Swing Performance.***](http://www.billharlan.com/papers/Improving_Swing_Performance.html)

## Containers

Every program with a *Swing* GUI contains at least one top-level Swing container, i.e., in general, an instance of a *JApplet*, *JFrame*, or *JDialog*, which enables the painting and event handling of the Swing components. The *JApplet*, *JFrame*, or *JDialog*, are considered top-level containers because they are used to provide an area in which the other containers and components can appear. Other containers, such as the *JPanel*, are used to facilitate the positioning and sizing of other containers and components. Between a top-level container and an intermediate container, a content pane (*JRootPane*), which is also an intermediate container, is indirectly provided. The content pane contains all of visible components of its GUI, except a menu bar. One of the *add()* methods of a container can be used to add a component to it. The component to be added is used as argument to the add method. In some cases another argument, which has to do with the layout, is used with the *add()* method.

Besides the *top-level* containers (*JApplet*, *JFrame*, *JDialog*, and *JWindow)* there are *special-purpose* containers (such as the *JInternalFrame*, *JLayeredPane*, and *JRootPane*) that are used for special purposes, and *general-purpose* containers (such as *JPanel*, *JScroll Pane*, *JSplitPane*, *JTabbedPane*, and *JToolBar*) that are used for other any general purpose.

The *JApplet* and *JFrame* classes should be used to implement Swing applets or applications, respectively. Both *JApplet* and *JFrame* classes are containers that contain an instance of the *JRootPane* class. The latter contains the content pane, which is a container, that contains all the components contained in the applet or application. Therefore, components should be added and layout managers should be set to the content pane.

## Atomic Components

There are many atomic components (i.e. components that exist as self-sufficient entities and not to hold other Swing components). Atomic components can be grouped into 3 categories:

- *Basic Controls*, which are components that can primarily be used to get input from the user (such as *JSlider\_*, \_ *JTextField\_*, \_ *JButton\_*, \_ *JComboBox\_*, \_ *JList\_*,\_ and *JMenu*)
- *Uneditable Information Displays,* which are used to display information to the user (such as *JProgressBar*, *JLabel\_*,*and \_JToolTip*)
- *Editable Displays of Formatted Information*, which are components that can be used to display formatted information that can be editable by the user (such as *JColorChooser\_*, \_ *JTextComponent\_*, \_ *JFileChooser\_*, \_ *JTable*, and *JTree*)

## Applets and Applications

*Swing applets* use the *JApplet* class which is a subclass of the *AWT* *Applet* class and implements the *Accessible* and *RootPaneContainer* interfaces. The following simple example shows an applet with a single component a *JLabel\_*.\_ The *BorderLayout* manager is used by the *JApplet* for its content pane (which is used in both Swing applets and applications), in contrast to the *FlowLayout* manager used by the *Applet* class.   
 

> SwingApplet1.java

> *import java.awt.\*;*   
> *import javax.swing.\*;*
> 
> *public class SwingApplet1 extends JApplet*   
> *{*   
> *public void init()*   
> *{*   
> *Icon icon = new ImageIcon("1.124.gif", "1.124 GIF");*   
> *JLabel label = new JLabel(" Test", icon, SwingConstants.CENTER);*   
> *getContentPane().add(label);*   
> *}*   
> *}*

The above applet can be executed using an html file like the following:

> SwingApplet1.html

> *\<html>*   
> *\<head>*   
> *\<title>JApplet Example # 1\</title>*   
> *\</head>*   
> *\<body>*
> 
> *\<center>*   
> *\<h2>*   
> *\<u>JApplet Example # 1\</u>\</h2>*   
> *\<hr>\<applet code="SwingApplet1.class" WIDTH="486" HEIGHT="94">\</applet>*   
> *\<hr>\</center>*
> 
> *\<p>\<br>*   
> *\</body>*   
> *\</html>*

Then, appletviewer (using the command: *appletviewer SwingApplet1.html*) displays the following window:

{{< resource uuid="e2e07bc1-49a4-0f71-39ec-550361e33d5d" >}}

Similarly, the *JFrame* class can be used to create a *Swing application* similar to the above applet. The *JFrame* class is a subclass of the *AWT*   *Frame* class and implements the *Accessible\_*,\_ *WindowConstants\_*,\_ and *RootPaneContainer* interfaces. It uses the *BorderLayout* manager for its content pane. The source code is presented below:

> SwingApplication1.java

> *import java.awt.\*;*   
> *import javax.swing.\*;*   
> *import java.awt.event.\*;*
> 
> *public class SwingApplication1 extends JFrame*   
> *{*
> 
> *public SwingApplication1()*   
> *{*   
> *super("Swing Application");*   
> *Icon icon = new ImageIcon("1.124.gif", "1.124 GIF");*   
> *JLabel label = new JLabel(" Test", icon, SwingConstants.CENTER);*   
> *getContentPane().add(label);*   
> *}*   
>  
> 
> *public static void main(String args\[\])*   
> *{*   
> *final JFrame jfr = new SwingApplication1();*
> 
> *jfr.setBounds(100,50,500,150);*   
> *jfr.setVisible(true);*
> 
> *jfr.setDefaultCloseOperation(DISPOSE\_ON\_CLOSE);*
> 
> *jfr.addWindowListener(new WindowAdapter()*   
> *& #160;       {*   
> *& #160;              public void windowClosed(WindowEvent e)*   
> *& #160;                   {*   
> *& #160;                     ; System.exit(0);*   
> *& #160;                   }*   
> *& #160;            }              );*   
> *}*
> 
> *}*

As any Java® application, a *main()* method must be provided. In *main()* a *JFrame* is instantiated, sized, and made visible. The default close operation is set to *DISPOSE\_ON\_CLOSE* (to dispose any native resources when the window is closed), and a window listener is added in order to exit the application as soon as the frame is closed.

Running the Java® interpreter (using *java* *SwingApplication1)* will execute the program and give the following window:

{{< resource uuid="78991a57-f994-7e6e-1fa6-17b608d9c421" >}}

Often, the source code file can be written in a way that it can be used both as an applet and an application. The above example is rewritten in way to facilitate such a use. The source code is provided below:

> AppletApplication1.java
> 
> *import java.awt.\*;*   
> *import javax.swing.\*;*   
> *import java.awt.event.\*;*
> 
> *public class AppletApplication1 extends JApplet*   
> *{*
> 
> *public void init()*   
> *{*   
> *Icon icon = new ImageIcon("1.124.gif", "1.124 GIF");*   
> *JLabel label = new JLabel(" Test", icon, SwingConstants.CENTER);*   
> *getContentPane().add(label);*   
> *}*   
>  
> 
> *public static void main(String args\[\])*   
> *{*   
> *final JFrame myFrame = new SwingApplication1();*   
> *JApplet myApplet = new AppletApplication1();*   
> *myApplet.init();*
> 
> *myFrame.setContentPane(myApplet.getContentPane());*   
> *myFrame.setBounds(100,50,500,150);*   
> *myFrame.setVisible(true);*
> 
> *myFrame.setDefaultCloseOperation(WindowConstants.DISPOSE\_ON\_CLOSE);*
> 
> *myFrame.addWindowListener(new WindowAdapter()*   
> *& #160;          {*   
> *& #160;             public void windowClosed(WindowEvent e)*   
> *& #160;                  {*   
> *& #160;                     ; System.exit(0);*   
> *& #160;                  }*   
> *& #160;          }                    );*   
> *}*
> 
> *}*

## Mixing AWT and Swing

Attention should be given when [mixing AWT and Swing](http://java.sun.com/products/jfc/tsc/swingdoc-archive/mixing.html) components, since when lightweight components overlap with heavyweight components, the heavyweight components are always painted on top. In general, it should [mixing AWT and Swing](http://java.sun.com/products/jfc/tsc/swingdoc-archive/mixing.html) components should not be mixed whenever possible. The "depth" at which components are displayed in a container is represented by the Z-order. The latter is determined by the order with which each component is added to the container, i.e. the first component to be added to a container has the highest Z-order which means that it is displayed in front of all other components added to that container. When lightweight and heavyweight components are mixed, the lightweight components, which need to reside in a heavyweight container, have the same Z-order of their container, and within it the order of each of the lightweight components is determined by the order in which they are added to the container. Note, that whenever a container is extended and the *paint()* method is overridden, the superclass *paint()* method should be explicitly invoked using *super.paint()* to force drawing of the lightweight components.

When *Swing* popup menus, which are lightweight, are mixed with a heavyweight component, the latter overlaps the former. This can be avoided by forcing the popup menus to be heavyweight using the method *setLightWeightPopupEnabled*() of the *JPopupMenu* class. A similar problem happens with a *JScrollPane* instance when any heavyweight components to it. Because there is no option of setting the *JScrollPane* as a heavyweight, the *AWT* ScrollPane can be used instead, which works fine with both lightweight and heavyweight components. Finally, heavyweight components should be avoided (i.e. not be added) to *Swing* internal frames, i.e. to a *JInternalFrame* instance.

## Layout Managers

Layout managers (such as the *BorderLayout\_*, \_ *BoxLayout\_*,\_ *GridLayout\_*, \_ *FlowLayout\_*, \_ *CardLayout\_*, \_ *GridBagLayout*) are used to determine the size and position of the components that are contained in a container. Each container is provided a default layout manager, which, however, can be changed using the *setLayout*() method and as an argument a newly created instance of the preferred layout manager. The minimum, preferred, and maximum sizes of a component can also be specified to the layout manager, as well as the preferred alignment.

## Painting System

The *AWT* painting system controls the painting of a Swing GUI, starting with the highest component that needs to be repainted and going down the hierarchy of containers, using the event-dispatching thread. The painting of swing components occurs whenever necessary. Swing uses double buffering to improve the efficiency and quality of the provided GUI. During painting, each component paints itself before any of the components that it contains. A Swing top-level container is painted on-screen using one of the methods: *setVisible(true)*, *show()*, or *pack()*. Painting starts with the highest component that needs to be repainted and moving down the containment hierarchy, i.e. each component paints itself before any of the components it contains.

Swing performs, by default, double-buffered to ensure smoothness and avoid flushing. Double buffering is essentially implemented by an offscreen buffer in which all painting takes place, and then it is flushed to the screen.

## Event Handling

The event handling features of the Swing (and AWT) components allow to a Java® program to respond to external events, such as the interaction of the user with the GUI. Events are handled by event handlers that are registered with event sources. Any *Swing* component can be notified for the occurrence of any event simply by implement the corresponding interface and registering it as an event listener on a relevant event source. The latter is usually component, e.g. a button. for each event there is a corresponding object which provides all the relevant information. An event handler is implemented by:

- either
    - implementing the corresponding listener interface, or
    - extending a class that implements that interface
- implement the method in the listener (interface or subclass)
- adding that kind of listener to a component

Sometimes, anonymous inner classes are used to keep the code clearer and the event handler closer to the point where it is registered. The event-handling code executes in the event-dispatching thread (single thread) ensuring that each event handler will execute in sequence allowing a previous event handler finish executing before the next one starts execution. Therefore, the code in the event handlers should be either very short and quick to execute, or another thread should be initiated to execute the code, in order to not harm the performance of the program. Otherwise, painting, which also executes on the event-dispatching thread, will not occur while an event is being handled.

## Threads

*Swing*, in general, is not thread safe, because a *Swing* component can be accessed by only one thread at a time, which, in general, is the *event-dispatching thread*. Because Swing is not thread safe, Swing components, in general, should be accessed only from the event-dispatching thread. The *event-dispatching thread* is the thread that invokes callback methods (e.g. *paint()* and *update()* functions) and event handler methods. Swing has been designed to be not thread safe in order to avoid the overhead of multithreading (e.g. obtaining and releasing locks) and to simplify the subclassing of its component. It is not allowed to access Swing components from any thread other than the event-dispatching thread.

However, some *Swing* components support multithread access. Actually after the realization of a *Swing* component code that might affect or depend on the state of that component should be executed in the event-dispatching thread. Realization of a component means after the component is available for painting on screen, after it is painted or become ready to be painted using one of the methods: *setVisible(true)*, *show()*, or *pack().*

The access only through the *event-dispatching thread* is not required in the following cases:

- when dealing with thread safe methods (as specified in the *Swing* API documentation) to construct and show a GUI in the main thread of  an application, as long as  no components have been realized in the current runtime environment
- constructing and manipulating the GUI in an applet's *init()* method, as long as the components have not been made visible, i.e. the method *show()* or *setVisible(true)* has never been called on the actual applet object
- methods *repaint()* and *revalidate()* are safe to call from any thread

In general, Swing it is not safe to access Swing components from any thread other than the event-dispatching thread. However, there are times that it is preferable to update Swing components from another thread, or perform time-consuming operations on a separate thread, and not use the *event-dispatching thread*. In those cases, *Swing* provides the methods *invokeLater*() and *invokeAndWait*() in the *SwingUtilities* class, which can be used to queue a runnable object on the event dispatch thread. They essentially allow a block of code from another thread to be invoked and executed by the event-dispatching thread. Both methods can be used to access Swing components from a thread other than the event-dispatching thread. Method *invokeLater()* queues the runnable object and returns immediately, while *invok eAndWait()* waits until the runnable object's *run()* method has started before returning. Only the *invokeLater*() (and not *invokeAndWait*()) method can be called from the event dispatching thread.