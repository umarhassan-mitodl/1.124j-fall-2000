---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Applets and Applications
uid: 7377f250-f403-ddda-5d68-af923ca75434
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Programs that Function as Applets and as Applications
-----------------------------------------------------

The following example shows how you might write a Java® program, so that it can function either as an applet or as an application. The program can run as an applet because it inherits JApplet and it can run as an application because it has a main routine. The code creates the UI components within a JPanel and then sets this panel to be the content pane for a JApplet or a JFrame. When the program runs as an applet, the JApplet class is used as the top level container. When the program runs as an application, we create a JFrame and use this as the top level container.

_MyApp.java_

_import javax.swing.\*;_  
_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import javax.swing.event.\*;_

_// This class can be run either as an Applet or as an Application._  
 _public class MyApp extends JApplet {_  
 _// The RootPaneContainer interface is implemented by JApplet and by JFrame._  
 _// It specifies methods like setContentPane() and getContentPane().  The_  
 _// content pane is of type java.awt.Container or one of its subclasses._  
 _RootPaneContainer mRPC;_

 _// This contructor is used when we run as an applet._  
 _public MyApp() {_  
 _mRPC = this;_  
 _}_

 _// This contructor is used when we run as an application._  
 _public MyApp(JFrame frame) {_  
 _mRPC = frame;_  
 _}_

 _// The init method is the place to put the code to initialize the applet.  The code to set up the_  
 _// user interface usually goes here.  We avoid putting applet initialization code in applet constructors_  
 _// because an applet is not guaranteed to have a full environment until the init method is called._  
 _public void init() {_  
 _// We will put all our components in a JPanel and then set this panel_  
 _// as the content pane for the applet or application._  
 _JPanel panel = new JPanel();_  
 _panel.setLayout(new BorderLayout());_

 _JSlider slider = new JSlider(0,50,0);_  
 _panel.add(slider, BorderLayout.SOUTH);_  
 _final DrawingArea drawingArea = new DrawingArea();_  
 _panel.add(drawingArea, BorderLayout.CENTER);_

 _slider.addChangeListener(new ChangeListener() {_  
 _public void stateChanged(ChangeEvent e) {_  
 _JSlider source = (JSlider)e.getSource();_  
 _if (!source.getValueIsAdjusting()) {_  
 _int offset = (int)source.getValue();_  
 _drawingArea.setOffset(offset);_  
 _drawingArea.repaint();_  
 _}_  
 _}_  
 _});_

 _mRPC.setContentPane(panel);_  
 _}_

 _// The start method is the place to start the execution of the applet._  
 _// For example, this is where you would tell an animation to start running._  
 _public void start() {_  
 _}_

 _// The stop method is the place to stop the execution of the applet._  
 _// This is where you would tell an animation to stop running._  
 _public void stop() {_  
 _}_  
   
 _// The destroy method is where you would do any final cleanup that needs to be done.  The_  
 _// destroy method is rarely required, since most of the cleanup can usually be done in stop()._  
 _public void destroy() {_  
 _}_

 _public static void main(String\[\] args) {_  
 _JFrame frame = new JFrame();_  
 _final MyApp app = new MyApp(frame);_

 _frame.addWindowListener(new WindowAdapter() {_  
 _public void windowClosing(WindowEvent e) {_  
 _app.stop();_  
 _app.destroy();_  
 _System.exit(0);_  
 _}_  
 _});_

 _app.init();_

 _frame.setSize(400, 400);_  
 _frame.setVisible(true);_

 _app.start();_  
 _}_  
_}_  
 

_// A user interface component, which is to be added to the applet._  
_class DrawingArea extends JPanel {_  
 _private int mOffset;_

 _public DrawingArea() {_  
 _setBackground(Color.white);_  
 _}_

 _public void setOffset(int offset) {_  
 _mOffset = offset;_  
 _}_

 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);_  
 _g.setFont(new Font("Helvetica", Font.PLAIN, 24));_  
 _g.setColor(Color.green);_  
 _g.drawString("An Applet or an Application?", 10+mOffset, 50);_  
 _g.drawString("That is the question.", 10+mOffset, 100);_  
 _}_  
_}_

_mypage.html_

_\<HTML>_

_\<APPLET CODE=MyApp.class WIDTH=400 HEIGHT=400>_  
_\</APPLET>_