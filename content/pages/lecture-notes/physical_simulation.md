---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Physical Simulation
uid: cab4f67e-ebcd-c2e6-24c2-67ad391b0b21
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Physical Simulation Example
---------------------------

The following example shows how you might integrate a numerical simulation with a Java® animation. Here, we have considered a simple spring-mass-damper system of the form

    d{{< sup "2" >}}x/dt{{< sup "2" >}} + 2xw{{< sub "0" >}}dx/dt + w{{< sub "0" >}}{{< sup "2" >}} x = 0

and computed the solution numerically using an explicit Forward Euler time-stepping scheme. Try increasing the size of the time step and notice that the simulation becomes unstable when the growth factors become larger than 1. When using explicit time integration, we must therefore choose our time step to be smaller than the critical time step.

Now try using an implicit Backward Euler time-stepping scheme. In this case, the simulation remains stable even for large time steps because the growth factors are always smaller than 1. You may also wish to determine the exact solution to the differential equation and compare it to the numerical solution.

_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import javax.swing.\*;_

_class Vec2D {_  
 _private float\[\] vec;_

 _public Vec2D(float fX, float fV) {_  
 _vec = new float\[2\];_  
 _vec\[0\] = fX;_  
 _vec\[1\] = fV;_  
 _}_

 _public void translate(float fDx) {_  
 _vec\[0\] += fDx;_  
 _}_

 _public void setPos(float fX) {_  
 _vec\[0\] = fX;_  
 _}_

 _public void setVel(float fV) {_  
 _vec\[1\] = fV;_  
 _}_

 _public float getPos() {_  
 _return vec\[0\];_  
 _}_

 _public float getVel() {_  
 _return vec\[1\];_  
 _}_  
_}_

_class Matrix2D {_  
 _private float\[\]\[\] mat;_

 _public Matrix2D(float a11, float a12, float a21, float a22) {_  
 _mat = new float\[2\]\[2\];_  
 _mat\[0\]\[0\] = a11;_  
 _mat\[0\]\[1\] = a12;_  
 _mat\[1\]\[0\] = a21;_  
 _mat\[1\]\[1\] = a22;_  
 _}_

 _public void multiply(Vec2D vec) {_  
 _float fX = mat\[0\]\[0\] \* vec.getPos() + mat\[0\]\[1\] \* vec.getVel();_  
 _float fV = mat\[1\]\[0\] \* vec.getPos() + mat\[1\]\[1\] \* vec.getVel();_  
 _vec.setPos(fX);_  
 _vec.setVel(fV);_  
 _}_

 _public void invert() {_  
 _float det = mat\[0\]\[0\]\*mat\[1\]\[1\]-mat\[0\]\[1\]\*mat\[1\]\[0\];_  
 _float tmp = mat\[0\]\[0\];_  
 _mat\[0\]\[0\] = mat\[1\]\[1\] / det;_  
 _mat\[1\]\[1\] = tmp / det;_  
 _mat\[0\]\[1\] = -mat\[0\]\[1\] / det;_  
 _mat\[1\]\[0\] = -mat\[1\]\[0\] / det;_  
 _}_  
_}_

_class Ball {_  
 _Vec2D mXState;  // x position and velocity._  
 _Vec2D mYState;  // y position and velocity._  
 _Matrix2D mMatrix;_  
 _int miRadius;_  
 _int miWindowWidth, miWindowHeight;_

 _public Ball(int iRadius, int iW, int iH) {_  
 _miRadius = iRadius;_  
 _mXState = new Vec2D(0.0f, 0.0f);_  
 _mYState = new Vec2D(0.0f, 0.0f);_  
 _miWindowWidth = iW;_  
 _miWindowHeight = iH;_  
 _}_

 _public void setPosition(float fXPos, float fYPos) {_  
 _mXState.setPos(fXPos);_  
 _mYState.setPos(fYPos);_  
 _}_

 _public void setVelocity(float fXVel, float fYVel) {_  
 _mXState.setVel(fXVel);_  
 _mYState.setVel(fYVel);_  
 _}_

 _public void setParams(float fXi, float fW0, float fDt, boolean explicit) {_  
 _float fReal1 = 0.0f, fImag1 = 0.0f;  // First eigenvalue._  
 _float fReal2 = 0.0f, fImag2 = 0.0f;  // Second eigenvalue._  
 _float G1, G2;  // Growth factors._

 _// Determine the eigenvalues._  
 _if (fXi \< 1.0f) {_  
 _fReal1 = fReal2 = -fW0\*fXi;_  
 _fImag1 = (float)(fW0\*Math.sqrt(1-fXi\*fXi));_  
 _fImag2 = -fImag1;_  
 _System.out.println("System is underdamped.");_  
 _System.out.println("Eigenvalues are: " + fReal1 + " +/- " + fImag1 + "i");_  
 _}_  
 _else {_  
 _fReal1 = -fW0\*(fXi + (float)Math.sqrt(fXi\*fXi-1));_  
 _fReal2 = -fW0\*(fXi - (float)Math.sqrt(fXi\*fXi-1));_  
 _System.out.println("System is overdamped or critically damped.");_  
 _System.out.println("Eigenvalues are: " + fReal1 + " and " + fReal2 + "i");_  
 _}_

 _if (explicit) {_  
 _// Forward Euler._  
 _mMatrix = new Matrix2D(1.0f, fDt, -fW0\*fW0\*fDt, 1-2\*fXi\*fW0\*fDt);_

 _G1 = (float)Math.sqrt(Math.pow(1+fReal1\*fDt,2.0) + Math.pow(fImag1\*fDt,2.0));_  
 _G2 = (float)Math.sqrt(Math.pow(1+fReal2\*fDt,2.0) + Math.pow(fImag2\*fDt,2.0));_  
 _}_  
 _else {_  
 _// Backward Euler._  
 _mMatrix = new Matrix2D(1.0f, -fDt, fW0\*fW0\*fDt, 1+2\*fXi\*fW0\*fDt);_  
 _mMatrix.invert();_

 _G1 = (float)(1.0/Math.sqrt(Math.pow(1-fReal1\*fDt,2.0) + Math.pow(fImag1\*fDt,2.0)));_  
 _G2 = (float)(1.0/Math.sqrt(Math.pow(1-fReal2\*fDt,2.0) + Math.pow(fImag2\*fDt,2.0)));_  
 _}_  
 _System.out.println("Growth factors are " + G1 + " and " + G2);_  
 _}_

 _public int getXPos() {_  
 _return (int)mXState.getPos();_  
 _}_

 _public int getYPos() {_  
 _return (int)mYState.getPos();_  
 _}_

 _public void draw(Graphics g) {_  
 _g.setColor(Color.red);_  
 _g.fillOval(miWindowWidth/2+(int)mXState.getPos()-miRadius,_  
 _miWindowHeight/2+(int)mYState.getPos()-miRadius,_  
 _2\*miRadius, 2\*miRadius);_  
 _}_

 _// Update the position of the ball._  
 _void move() {_  
 _mMatrix.multiply(mYState);_  
 _}_  
_}_

_public class Animation extends JApplet implements Runnable, ActionListener {_  
 _int miFrameNumber = 0;_  
 _int miTimeStep;_  
 _Thread mAnimationThread;_  
 _boolean mbIsPaused = false;_  
 _Button mButton;_  
 _Ball ball;_

 _public void init() {_  
 _// Time step in milliseconds._  
 _miTimeStep = 20; // Try changing this to (a) 50 ms and (b) 60 ms._

 _// Initialize the parameters of the ball.  The parameters refer to the_  
 _// differential equation:  d^2 x/dt^2 + 2 xi w0 dx/dt + w0^2 x = 0_

 _int iRadius = 15;_  
 _float fXPos = 0.0f;      // Initial x displacement_  
 _float fYPos = 100.0f;    // Initial y displacement_  
 _float fXVel = 0.0f;      // Initial x velocity_  
 _float fYVel = 0.0f;      // Initial y velocity_  
 _float fXi = 0.05f;       // xi_  
 _float fW0 = 2.0f;        // w0_  
 _boolean explicit = true; // true: forward Euler, false: backward Euler_

 _ball = new Ball(iRadius, getSize().width, getSize().height);_  
 _ball.setPosition(fXPos, fYPos);_  
 _ball.setVelocity(fXVel, fYVel);_  
 _ball.setParams(fXi, fW0, miTimeStep/1000.0f, explicit);_

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

 _// Draw the rubber band._  
 _g.drawLine(getSize().width/2, 0,_  
 _getSize().width/2+ball.getXPos(),_  
 _getSize().height/2+ball.getYPos());_

 _// Draw the ball._  
 _ball.draw(g);_  
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
 _// Draw the next frame._  
 _repaint();_

 _// Advance the animation frame._  
 _miFrameNumber++;_

 _// Update the position of the ball._  
 _ball.move();_

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
_}_