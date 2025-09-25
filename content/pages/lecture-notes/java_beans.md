---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Java Beans
uid: 2e8745e9-24d4-cbb4-bc68-de6ae4f922b2
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Introduction](#Intro)
2.  [The BeanBox](#Bean)
3.  [Creating a Java® Bean](#Java)
4.  [Support for Properties and Events](#Support)

Related Links
-------------

[Java® Beans trail in the Java® Tutorial](http://java.sun.com/docs/books/tutorial/javabeans/index.html)\- a good introduction to Java® Beans.  
[Java® Beans Development Kit (BDK)](http://www.cs.cmu.edu/afs/cs/academic/class/15612-s98/projects/NextGen/BDK/README.html)\- provides a basic development support tool (called the BeanBox) as well as several examples of Java® Bean components. This link also provides links to various commercial development environments for Java® Beans.  
[Java® Beans API](https://condor.depaul.edu/elliott/513/projects-archive/DS420Fall98/Paris/~ejones2.html)\- various interfaces, classes and exception types that you will encounter when developing Java® Beans.

{{< anchor "Intro" >}}{{< /anchor >}}1\. Introduction
-----------------------------------------------------

A Java® Bean is a reusable software component that can be manipulated visually in an application builder tool. The idea is that one can start with a collection of such components, and quickly wire them together to form complex programs without actually writing any new code.

Software components must, in general, adopt standard techniques for interacting with the rest of the world. For example, all GUI components inherit the java.awt.Component class, which means that one can rely on them to have certain standard methods like _paint()_, _setSize()_, etc. Java® Beans are not actually required to inherit a particular base class or implement a particular interface. However, they do provide support for some or all of the following key features:

*   Support for _introspection_. Introspection is the process by which an application builder discovers the properties, methods and events that are associated with a Java® Bean. 
*   Support for _properties_. These are basically member variables that control the appearance or behavior of the Java® Bean. 
*   Support for _customization_ of the appearance and behavior of a Java® Bean.
*   Support for _events_. This is a mechanism by which Java® Beans can communicate with one another.
*   Support for _persistent storage_. Persistence refers to the abilility to save the current state of an object, so that it can be restored at a later time.

{{< anchor "Bean" >}}{{< /anchor >}}2\. The BeanBox
---------------------------------------------------

This is a basic tool that Sun provides for testing Java® Beans. To run the BeanBox, your computer needs to have access to a [BDK](http://www.ecst.csuchico.edu/~amk/foo/advjava/notes/beans/BDK/) installation. To run the BeanBox, go to the _beans/beanbox_ subdirectory and then type _run_. This will bring up three windows:

*   The ToolBox window gives you a palette of sample Java® Beans to choose from.
*   The BeanBox window is a container within which you can visually wire beans together.
*   The Properties window allows you to edit the properties of the currently selected Java® Bean.

Try a simple example: choose _Juggler_ bean from the ToolBox and drop an instance in the BeanBox window. Also create two instances of _OurButton_. Edit the labels of the buttons to read _start_ and _stop_ using the Properties window. Now wire the start button to the juggler as follows. Select the start button, then go to Edit | Events | action | actionPerformed. Connect the rubber band to the juggler. You will now see an EventTargetDialog box with a list of _Juggler_ methods that could be invoked when the start button is pressed (these are the methods that either take an ActionEvent as an argument or have no arguments at all.) Choose _startJuggling_ as the target method and press OK. The BeanBox now generates an adaptor class to wire the start button to the juggler. Wire the stop button to the juggler's _stopJuggling_ method in a similar manner.

Now that the program has been designed, you can run it within the BeanBox. Simply press the start button to start juggling and press the stop button to stop juggling. If you wish, you can turn your program into an applet by choosing File | MakeApplet in the BeanBox. This will automatically generate a complete set of files for the applet, which can be run in the appletviewer. (Do not expect current versions of Netscape® and Internet Explorer to work with this applet.)

Let's take a closer look at how the BeanBox works. On start up, it scans the directory _beans/jars_ for files with the .jar extension that contain Java® Beans. These beans are displayed in the ToolBox window, from where they can be selected and dropped into the BeanBox window. Next, we edited the labels of the two instances of _OurButton_. The BeanBox determined that _OurButton_ has a member named _label_ by looking for setter and getter methods that follow standard naming conventions called _design patterns_. If you look at the source code in _beans\\demo\\sunw\\demo\\buttons\\OurButton.java_, you will see that OurButton has two methods named

     _public void setLabel(String newLabel) {_  
 _..._  
 _}_

     _public String getLabel() {_  
 _..._  
 _}_

Design patterns are an implicit technique by which builder tools can introspect a Java® Bean. There is also an explicit technique for exposing properties, methods and events. This involves writing a bean information class, which implements the _BeanInfo_ interface.

When we wired the start button to the juggler, the BeanBox set up the juggler to respond to action events generated by the start button. The BeanBox again used design patterns to determine the type of events that can be generated by an _OurButton_ object. The following design patterns indicate that _OurButton_ is capable of firing _ActionEvents_.

 _public synchronized void addActionListener(ActionListener l) {_  
 _..._  
 _}_

 _public synchronized void removeActionListener(ActionListener l) {_  
 _..._  
 _}_

By choosing Edit | Events | action | actionPerformed to connect the start button to the juggler, we were really registering an _ActionListener_ with the start button. The _Juggler_ bean itself is does not implement the _ActionListener_ interface. Instead the BeanBox generated an event hookup adaptor, which implements _ActionListener_ and simply calls the juggler's _startJuggling_ method in its _actionPerformed_ method:

 _// Automatically generated event hookup file._

 _package tmp.sunw.beanbox;_  
 _import sunw.demo.juggler.Juggler;_  
 _import java.awt.event.ActionListener;_  
 _import java.awt.event.ActionEvent;_

 _public class \_\_\_Hookup\_1474c0159e implements_  
 _java.awt.event.ActionListener, java.io.Serializable {_

 _public void setTarget(sunw.demo.juggler.Juggler t) {_  
 _target = t;_  
 _}_

 _public void actionPerformed(java.awt.event.ActionEvent arg0) {_  
 _target.startJuggling(arg0);_  
 _}_

 _private sunw.demo.juggler.Juggler target;_  
 _}_

A similar event hookup adaptor was generated when we wired the stop button to the juggler's _stopJuggling_ method.

Why not make _Juggler_ implement the _ActionListener_ interface directly? This is mainly a matter of convenience. Suppose that _Juggler_ implemented _ActionListener_ and that it was registered to receive _ActionEvent_s from both the start button and the stop button. Then the _Juggler_'s _actionPerformed_ method would need to examine incoming events to determine the event source, before it could know whether to call _startJuggling_ or _stopJuggling_.

{{< anchor "Java" >}}{{< /anchor >}}3\. Creating a Java® Bean
-------------------------------------------------------------

This example illustrates how to create a simple Java® Bean. Java Bean classes must be made serializable so that they support persistent storage. To make use of the default serialization capabilities in Java®, the class needs to implement the _Serializable_ interface or inherit a class that implements the _Serializable_ interface. Note that the _Serializable_ interface does not have any methods. It just serves as a flag to say that the designer has tested the class to make sure it works with default serialization. Here is the code:

 _**SimpleBean.java**_

 _import java.awt.\*;_  
 _import java.io.Serializable;_

 _public class SimpleBean extends Canvas implements Serializable {_  
 _//Constructor sets inherited properties_  
 _public SimpleBean() {_  
 _setSize(60,40);_  
 _setBackground(Color.red);_  
 _}_  
 _}_

Since this class extends a GUI component, _java.awt.Canvas_, it will be a visible Java® Bean. Java® Beans may also be invisible.

Now the Java® Bean must be compiled and packaged into a JAR file. First run the compiler:

    _javac SimpleBean.java_

Then create a manifest file

 **_manifest.tmp_**

    _Name: SimpleBean.class_  
 _Java-Bean: True_

Finally create the JAR file:

    _jar cfmv SimpleBean.jar manifest.tmp SimpleBean.class_

The JAR file can now be placed in the _beans/jars_ so that the BeanBox will find it on startup, or it can be loaded subsequently by choosing File | LoadJar.

{{< anchor "Support" >}}{{< /anchor >}}4.  Support for Properties and Events
----------------------------------------------------------------------------

This example builds on the SimpleBean class. It illustrates how to add customizable properties to a Java® Bean and how to generate and receive property change events.

 **_SimpleBean.java_**

    _import java.awt.\*;_  
 _import java.io.Serializable;_  
 _import java.beans.\*;_

 _public class SimpleBean extends Canvas implements Serializable,_  
 _java.beans.PropertyChangeListener {_

 _// Constructor sets inherited properties_  
 _public SimpleBean() {_  
 _setSize(60,40);_  
 _setBackground(Color.red);_  
 _}_

 _// This section illustrates how to add customizable properties to the Java Bean.  The names_  
 _// of the property setter and getter methods must follow specific design patterns that allow_  
 _// the BeanBox (or builder tool) to determine the name of the property variable upon_  
 _// introspection._

 _private Color beanColor = Color.green;_

 _public void setBeanColor(Color newColor) {_  
 _Color oldColor = beanColor;_  
 _beanColor = newColor;_  
 _repaint();_

 _// This relates to bound property support (see below)._  
 _changes.firePropertyChange("beanColor", oldColor, newColor);_  
 _}_

 _public Color getBeanColor() {_  
 _return beanColor;_  
 _}_

 _public void paint(Graphics g) {_  
 _g.setColor(beanColor);_  
 _g.fillRect(20,5,20,30);_  
 _}_

 _// This section illustrates how to implement bound property support.  Bound property_  
 _// support allows other objects to respond when a property change occurs in this Java_  
 _// Bean.  Remember that each property setter method must fire a property change event,_  
 _// so that registered listeners can be properly notified.  The addPropertyChangeListener_  
 _// and removePropertyChangeListener methods follow design patterns that indicate the_  
 _// ability of this Java Bean to generate property change events.  As it happens, these_  
 _// methods overide methods of the same names, which are inherited through java.awt.Canvas._

 _private PropertyChangeSupport changes = new PropertyChangeSupport(this);_

 _public void addPropertyChangeListener(PropertyChangeListener l) {_  
 _changes.addPropertyChangeListener(l);_  
 _}_

 _public void removePropertyChangeListener(PropertyChangeListener l) {_  
 _changes.removePropertyChangeListener(l);_  
 _}_

 _// This section illustrates how to implement a bound property listener, which will allow this_  
 _// Java Bean to register itself to receive property change events fired by other objects._  
 _// Registration simply involves making a call to the other object's addPropertyChangeListener_  
 _// method with this Java Bean as the argument.  If you are using the BeanBox, however, you_  
 _// will typically use the event hookup adaptor mechanism to receive the events.  In this case,_  
 _// you can set the target method to be the propertyChange method.  (Another word about the_  
 _// BeanBox: the Edit | bind property option is a useful way to make a property change in one_  
 _// object automatically trigger a property change in another object.  In this case, the BeanBox_  
 _// will invoke the correct property setter using code in sunw/beanbox/PropertyHookup.java._  
 _// An adaptor class will not be generated in this case.)_

 _public void propertyChange(PropertyChangeEvent evt) {_  
 _String propertyName = evt.getPropertyName();_  
 _System.out.println("Received property change event " + propertyName);_  
 _}_  
 _}_