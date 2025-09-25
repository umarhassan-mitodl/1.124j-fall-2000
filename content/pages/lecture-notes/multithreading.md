---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Multithreading
uid: 559b3cf8-ad34-b681-28e7-73a083ddf9f0
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Threads, Processes and Multitasking](#1)
2.  [How to Create Threads](#2)
3.  [The LifeCycle of a Thread](#3)
4.  [Animations](#4)

{{< anchor "1" >}}{{< /anchor >}}1\. Threads, Processes and Multitasking
------------------------------------------------------------------------

_Multitasking_ is the ability of a computer's operating system to run several programs (or _processes_) concurrently on a single CPU. This is done by switching from one program to another fast enough to create the appearance that all programs are executing simultaneously. There are two types of multitasking:

_Preemptive multitasking._ In preemptive multitasking, the operating system decides how to allocate CPU time slices to each program. At the end of a time slice, the currently active program is _forced_ to yield control to the operating system, whether it wants to or not. Examples of operating systems that support premptive multitasking are Unix®, Windows® 95/98, Windows® NT and the planned release of Mac® OS X.

_Cooperative multitasking._ In cooperative multitasking, each program controls how much CPU time it needs. This means that a program must cooperate in yielding control to other programs, or else it will hog the CPU. Examples of operating systems that support cooperative multitasking are Windows® 3.1 and Mac® OS 8.5.

_Multithreading_ extends the concept of multitasking by allowing individual programs to perform several tasks concurrently. Each task is referred to as a _thread_ and it represents a separate flow of control. Multithreading can be very useful in practical applications. For example, if a web page is taking too long to load in a web browser, the user should be able interrupt the loading of the page by clicking on the stop button. The user interface can be kept responsive to the user by using a separate thread for the network activity needed to load the page.

What then is the difference then between a _process_ and a _thread_? The answer is that each process has its own set of variables, whereas threads share the same data and system resources. A multithreaded program must therefore be very careful about the way that threads access and modify data, or else unpredictable behavior may occur.

{{< anchor "2" >}}{{< /anchor >}}2\. How to Create Threads
----------------------------------------------------------

_(Ref. [Java® Tutorial](http://java.sun.com/developer/codesamples/thrds.html))_

We can create a new thread using the _Thread_ class provided in the _java.lang_ package. There are two ways to use the _Thread_ class.

*   By creating a subclass of _Thread_.
*   By writing a class that implements the _Runnable_ interface.

Subclassing the _Thread_ class
------------------------------

In this approach, we create a subclass of the _Thread_ class. The _Thread_ class has a method named _run()_, which we can override in our subclass. Our implementation of the _run()_ method must contain all code that is to be executed within the thread.

_class MyClass extends Thread {_  
 _// ..._

 _public void run() {_  
 _// All code to be executed within the thread goes here._  
 _}_  
_}_  
 

We can create a new thread by instantiating our class, and we run it by calling the _start()_ method that we inherited from class _Thread_.

_MyClass a = new MyClass();_  
_a.start();_

This approach for creating a thread works fine from a technical standpoint. Conceptually, however, it does not make that much sense to say that _MyClass_ "is a" _Thread_. All that we are really interested in doing is to provide a _run()_ method that the _Thread_ class can execute. The next approach is geared to do exactly this.

Implementing the _Runnable_ Interface
-------------------------------------

In this approach, we write a class that implements the _Runnable_ interface. The _Runnable_ interface requires us to implement a single method named _run()_, within which we place all code that is to be executed within the thread.

_class MyClass implements Runnable {_  
 _// ..._

 _public void run() {_  
 _// All code to be executed within the thread goes here._  
 _}_  
_}_  
 

We can create a new thread by creating a _Thread_ object from an object of type _MyClass_. We run the thread by calling the _Thread_ object's _start()_ method.

_MyClass a = new MyClass;_  
_Thread t = new Thread(a);_  
_t.start();_

{{< anchor "3" >}}{{< /anchor >}}3\. The LifeCycle of a Thread
--------------------------------------------------------------

_(Ref. [Java® Tutorial](http://java.sun.com/developer/codesamples/thrds.html))_

A thread can be in one of four states during its lifetime:

*   _new_ - A new thread is one that has been created (using the _new_ operator), but has not yet been started.
*   _runnable_ - A thread becomes runnable once its _start()_ method has been invoked. This means that the code in the _run()_ method can execute whenever the thread receives CPU time from the operating system.
*   _blocked_ - A thread can become blocked if one of the following events occurs:
    *   The thread's _sleep()_ method is invoked. In this case, the thread remains blocked until the specified number of milliseconds elapses.
    *   The thread calls the _wait()_ method of an object. In this case, the thread remains blocked until either the object's _notify()_ method or its _notifyAll()_ method is called from another thread. The calls to _wait()_, _notify()_ and _notifyAll()_ are typically found within _synchronized_ methods of the object.
    *   The thread has blocked on an input/output operation. In this case, the thread remains blocked until the i/o operation has completed.  
          
        
*   _dead_ - A thread typically dies when the _run()_ method has finished executing.

Note: The following methods in the _java.lang.Thread_ class should no longer be used, since they can lead to unpredicable behavior: _stop()_, _suspend()_ and _resume()_.

The following example illustrates various thread states. The _main_ thread in our program creates a new thread, _Thread-0_. It then starts _Thread-0_, thereby making _Thread-0_ runnable so that it prints out an integer every 500 milliseconds. We call the _sleep()_ method to enforce the 500 millisecond delay between printing two consecutive integers. In the meantime, the _main_ thread proceeds to print out an integer every second only. The output from the program shows that the two threads are running in parallel. When the _main_ thread finishes its _for_ loop, it stops _Thread-0_.

We maintain a variable, _myThread_, which initially references _Thread-0_. This variable is polled by the _run()_ method to make sure that it is still referencing _Thread-0_. All we have to do to stop the thread is to set _myThread_ to _null_. This will cause the _run()_ method to terminate normally.

_class MyClass implements Runnable {_  
 _int i;_  
 _Thread myThread;_

 _public MyClass() {_  
 _i = 0;_  
 _}_

 _// This will terminate the run() method._  
 _public void stop() {_  
 _myThread = null;_  
 _}_

 _// The run() method simply prints out a sequence of integers, one every half second._  
 _public void run() {_  
 _// Get a handle on the thread that we are running in._  
 _myThread = Thread.currentThread();_

 _// Keep going as long as myThread is the same as the current thread._  
 _while (Thread.currentThread() == myThread) {_  
 _System.out.println(Thread.currentThread().getName() + ": " + i);_  
 _i++;_

 _try {_  
 _Thread.sleep(500); // Tell the thread to sleep for half a second._  
 _}_  
 _catch (InterruptedException e) {}_  
 _}_  
 _}_  
_}_  
 

_class Threadtest {_  
 _public static void main(String\[\] args) {_  
 _MyClass a = new MyClass();_  
 _Thread t = new Thread(a);_

 _// Start another thread.  This thread will run in parallel to the main thread._  
 _System.out.println(Thread.currentThread().getName() + ": Starting a separate thread");_  
 _t.start();_

 _// The main thread proceeds to print out a sequence of integers of its own, one every second._  
 _for (int i = 0; i \< 6; i++) {_  
 _System.out.println(Thread.currentThread().getName() + ": " + i);_  
 _// Tell the main thread to sleep for a second._  
 _try {_  
 _Thread.sleep(1000);_  
 _}_  
 _catch (InterruptedException e) {}_  
 _}_

 _// Stop the parallel thread.  We do this by setting myThread to null in our runnable object._  
 _System.out.println(Thread.currentThread().getName() + ": Stopping the thread");_  
 _a.stop();_  
 _}_  
_}_

{{< anchor "4" >}}{{< /anchor >}}4\. Animations
-----------------------------------------------

Here is an example of a simple animation. We have used a separate thread to control the motion of a ball on the screen.

_**anim.html**_

_\<HTML>_  
_\<BODY>_  
_\<APPLET CODE="Animation.class" WIDTH=300 HEIGHT=400>_  
_\</APPLET>_  
_\</BODY>_  
 

_**Animation.java**_

_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import javax.swing.\*;_

 _public class Animation extends JApplet implements Runnable, ActionListener {_  
 _int miFrameNumber = -1;_  
 _int miTimeStep;_  
 _Thread mAnimationThread;_  
 _boolean mbIsPaused = false;_  
 _Button mButton;_  
 _Point mCenter;_  
 _int miRadius;_  
 _int miDX, miDY;_

 _public void init() {_  
 _// Make the animation run at 20 frames per second.  We do this by_  
 _// setting the timestep to 50ms._  
 _miTimeStep = 50;_

 _// Initialize the parameters of the circle._  
 _mCenter = new Point(getSize().width/2, getSize().height/2);_  
 _miRadius = 15;_  
 _miDX = 4;  // X offset per timestep._  
 _miDY = 3;  // Y offset per timestep._

 _// Create a button to start and stop the animation._  
 _mButton = new Button("Stop");_  
 _getContentPane().add(mButton, "North");_  
 _mButton.addActionListener(this);_

 _// Create a JPanel subclass and add it to the JApplet.  All drawing_  
 _// will be done here, do we must write the paintComponent() method._  
 _// Note that the anonymous class has access to the private data of_  
 _// class Animation, because it is defined locally._  
 _getContentPane().add(new JPanel() {_  
 _public void paintComponent(Graphics g) {_  
 _// Paint the background._  
 _super.paintComponent(g);_

 _// Display the frame number._  
 _g.drawString("Frame " + miFrameNumber, getSize().width/2 - 40,_  
 _getSize().height - 15);_

 _// Draw the circle._  
 _g.setColor(Color.red);_  
 _g.fillOval(mCenter.x-miRadius, mCenter.y-miRadius, 2\*miRadius,_  
 _2\*miRadius);_  
 _}_  
 _}, "Center");_  
 _}_

 _public void start() {_  
 _if (mbIsPaused) {_  
 _// Don't do anything.  The animation has been paused._  
 _} else {_  
 _// Start animating._  
 _if (mAnimationThread == null) {_  
 _mAnimationThread = new Thread(this);_  
 _}_  
 _mAnimationThread.start();_  
 _}_  
 _}_

 _public void stop() {_  
 _// Stop the animating thread by setting the mAnimationThread variable_  
 _// to null.  This will cause the thread to break out of the while loop,_  
 _// so that the run() method terminates naturally._  
 _mAnimationThread = null;_  
 _}_

 _public void actionPerformed(ActionEvent e) {_  
 _if (mbIsPaused) {_  
 _mbIsPaused = false;_  
 _mButton.setLabel("Stop");_  
 _start();_  
 _} else {_  
 _mbIsPaused = true;_  
 _mButton.setLabel("Start");_  
 _stop();_  
 _}_  
 _}_

 _public void run() {_  
 _// Just to be nice, lower this thread's priority so it can't_  
 _// interfere with other processing going on._  
 _Thread.currentThread().setPriority(Thread.MIN\_PRIORITY);_

 _// Remember the starting time._  
 _long startTime = System.currentTimeMillis();_

 _// Remember which thread we are._  
 _Thread currentThread = Thread.currentThread();_

 _// This is the animation loop._  
 _while (currentThread == mAnimationThread) {_  
 _// Advance the animation frame._  
 _miFrameNumber++;_

 _// Update the position of the circle._  
 _move();_

 _// Draw the next frame._  
 _repaint();_

 _// Delay depending on how far we are behind._  
 _try {_  
 _startTime += miTimeStep;_  
 _Thread.sleep(Math.max(0,_  
 _startTime-System.currentTimeMillis()));_  
 _}_  
 _catch (InterruptedException e) {_  
 _break;_  
 _}_  
 _}_  
 _}_

 _// Update the position of the circle._  
 _void move() {_  
 _mCenter.x += miDX;_  
 _if (mCenter.x - miRadius \< 0 ||_  
 _mCenter.x + miRadius > getSize().width) {_  
 _miDX = -miDX;_  
 _mCenter.x += 2\*miDX;_  
 _}_

 _mCenter.y += miDY;_  
 _if (mCenter.y - miRadius \< 0 ||_  
 _mCenter.y + miRadius > getSize().height) {_  
 _miDY = -miDY;_  
 _mCenter.y += 2\*miDY;_  
 _}_  
 _}_  
_}_