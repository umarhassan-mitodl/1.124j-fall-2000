---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Shape Example
uid: c6123d4d-4502-1a86-7b77-30fc94e894d0
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

**Topics**

1.  [Point.java](#1)
2.  [Shape.java](#2)
3.  [Circle.java](#3)
4.  [Square.java](#4)
5.  [Main.java](#5)

**{{< anchor "1" >}}{{< /anchor >}}1\. Point.java**

 _public class Point_  
_{_  
 _private float mfX, mfY;_

 _public Point() {_  
 _mfX = mfY = 0.0f;_  
 _}_

 _public Point(float fX, float fY) {_  
 _mfX = fX;_  
 _mfY = fY;_  
 _}_

 _public Point(Point p) {_  
 _mfX = p.mfX;_  
 _mfY = p.mfY;_  
 _}_

 _// You will generally not need to write a finalizer. Member variables that_  
 _// are of reference type will be automatically garbage collected once they_  
 _// are no longer in use. Finalizers are only for cleaning up system resources,_  
 _// e.g. closing files._  
 _protected void finalize() throws Throwable {_  
 _System.out.print("In Point finalizer: ");_  
 _print();_  
 _super.finalize();  // If you have to write a finalizer, be sure to do this._  
 _}_

 _public void print() {_  
 _System.out.println("Point print: (" + mfX + "," + mfY + ")");_  
 _}_  
_}_

**{{< anchor "2" >}}{{< /anchor >}}2\. Shape.java**

 _public abstract class Shape_  
_{_  
 _private Point mCenter;_  
 _protected static int miCount = 0;  // An example of a static member variable._

 _public Shape() {_  
 _mCenter = new Point();_  
 _}_

 _public Shape(Point p) {_  
 _mCenter = new Point(p);_  
 _}_

 _// You will generally not need to write a finalizer. Member variables that_  
 _// are of reference type (i.e. mCenter) will be automatically garbage collected_  
 _// once they are no longer in use. Finalizers are only for cleaning up system_  
 _// resources, e.g. closing files._  
 _protected void finalize() throws Throwable {_  
 _System.out.print("In Shape finalizer: ");_  
 _print();_  
 _super.finalize();  // If you have to write a finalizer, be sure to do this._  
 _}_

 _public void print() {_  
 _System.out.print("Shape print: mCenter = ");_  
 _mCenter.print();_  
 _}_

 _// An example of a static member function._  
 _public static int getCount() {_  
 _return miCount;  // Can only access static members in static functions._  
 _}_  
_}_

**{{< anchor "3" >}}{{< /anchor >}}3\. Circle.java**

 _public class Circle extends Shape_  
_{_  
 _private float mfRadius;_

 _public Circle() {_  
 _super();  // Call the base class constructer._  
 _mfRadius = 0.0f;_  
 _miCount++;  // Can access this because it is protected in base class._  
 _}_

 _public Circle(float fX, float fY, float fRadius) {_  
 _super(new Point(fX, fY));  // Call the base class constructer._  
 _mfRadius = fRadius;_  
 _miCount++;_  
 _}_

 _public Circle(Point p, float fRadius) {_  
 _super(p);  // Call the base class constructer._  
 _mfRadius = fRadius;_  
 _miCount++;_  
 _}_

 _// You will generally not need to write a finalizer. Member variables that_  
 _// are of reference type (i.e. mCenter) will be automatically garbage collected_  
 _// once they are no longer in use. Finalizers are only for cleaning up system_  
 _// resources, e.g. closing files._  
 _protected void finalize() throws Throwable {_  
 _System.out.print("In Circle finalizer: ");_  
 _print();_  
 _super.finalize();  // If you have to write a finalizer, be sure to do this._  
 _}_

 _public void print() {_  
 _System.out.print("Circle print: mfRadius = " + mfRadius + " ");_  
 _super.print();_  
 _}_  
_}_

**{{< anchor "4" >}}{{< /anchor >}}4\. Square.java**

 _public class Square extends Shape_  
_{_  
 _private float mfLength;_

 _public Square() {_  
 _super();  // Call the base class constructer._  
 _mfLength = 0.0f;_  
 _miCount++;  // Can access this because it is protected in base class._  
 _}_

 _public Square(float fX, float fY, float fLength) {_  
 _super(new Point(fX, fY));  // Call the base class constructer._  
 _mfLength = fLength;_  
 _miCount++;_  
 _}_

 _public Square(Point p, float fLength) {_  
 _super(p);  // Call the base class constructer._  
 _mfLength = fLength;_  
 _miCount++;_  
 _}_

 _// You will generally not need to write a finalizer. Member variables that_  
 _// are of reference type (i.e. mCenter) will be automatically garbage collected_  
 _// once they are no longer in use. Finalizers are only for cleaning up system_  
 _// resources, e.g. closing files._  
 _protected void finalize() throws Throwable {_  
 _System.out.print("In Square finalizer: ");_  
 _print();_  
 _super.finalize();  // If you have to write a finalizer, be sure to do this._  
 _}_

 _public void print() {_  
 _System.out.print("Square print: mfLength = " + mfLength + " ");_  
 _super.print();_  
 _}_  
_}_

**{{< anchor "5" >}}{{< /anchor >}}5\. Main.java**

 _public class Main_  
_{_  
 _final static int MAX = 3;  // An example of a constant class member variable._

 _public static void main(String\[\] args)_  
 _{_  
 _// Create some Point objects._  
 _Point a;_  
 _a = new Point();_  
 _a.print();_

 _Point b;_  
 _b = new Point(2,3);_  
 _b.print();_

 _Point c = new Point(b);_  
 _c.print();_

 _// Print out the total number of Shapes created so far. At this point,_  
 _// no Shapes have been created, however, we can still access static member_  
 _// function Shape.getCount()._  
 _System.out.println("Total number of Shapes = " + Shape.getCount());_

 _// Create a Circle object and hold on to it using a Shape reference._  
 _Shape s;_  
 _s = new Circle(a,1);_  
 _s.print(); // This will call the print method in Circle._

 _// Create an array of Shapes._  
 _Shape\[\] shapeArray;_  
 _shapeArray = new Shape\[MAX\];  // An array of Shape references._

 _shapeArray\[0\] = new Square();_  
 _shapeArray\[1\] = new Circle(4,5,2);_  
 _shapeArray\[2\] = new Square(3,3,1);_

 _// Print out the array of Shapes. The length member gives the array size._  
 _for (int i = 0; i \< shapeArray.length; i++) {_  
 _shapeArray\[i\].print();_  
 _}_

 _// Print out the total number of Shapes created so far. At this point,_  
 _// 4 Shapes have been created._  
 _System.out.println("Total number of Shapes = " + Shape.getCount());_

 _// We can mark the objects for destruction by removing all references to_  
 _// them. Normally, we do not need to call the garbage collector explicitly._  
 _// Note: here we have not provided a way to decrement the Shape counter._  
 _a = b = c = null;_  
 _s = null;_  
 _for (int i = 0; i \< shapeArray.length; i++) {_  
 _shapeArray\[i\] = null;_  
 _}_  
 _shapeArray = null;_  
 _}_  
_}_