---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Custom Graphics
uid: 8ee0e91e-a113-9da9-244a-5d801314bf8d
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Custom Painting](#1) 
2.  [Simple 2D Graphics](#2) 
3.  [A Graphics Example](#3) 

{{< anchor "1" >}}{{< /anchor >}}1\. Custom Painting
----------------------------------------------------

### _(Ref. [Java® Tutorial](http://java.sun.com/docs/books/tutorial/uiswing/painting/index.html))_

So far, we have seen user interface components that display static content. The individual components posessed sufficient knowledge to draw themselves and so we did not have to do anything special beyond creating the components and describing their layout. If a component is obscured by some other window and then uncovered again, it is the job of the window system to make sure that the component is properly redrawn.

There are instances, however, where we will want to change the appearance of a component e.g. we may wish to draw a graph, display an image or even display an animation within the component. This requires the use of custom painting code. The recommended way to implement custom painting is to extend the _JPanel_ class. We will need to be concerned with two methods:

*   The _paintComponent()_ method specifies what the component should draw. We can override this method to draw text, graphics, etc. The _paintComponent()_ method should never be called directly. It will be called indirectly, either because the window system thinks that the component should draw itself or because we have issued a call to _repaint()_.
*   The _repaint()_ method forces the screen to update as soon as possible. It results in a call to the _paintComponent()_ method. _repaint()_ behaves asynchronously i.e. it returns immediately without waiting for the _paintComponent()_ method to complete.

The following code illustrates how custom painting works. A _JPanel_ subclass is used to listen to mouse events and then display a message at the location where the mouse is pressed or released.

_import javax.swing.\*;_  
_import java.awt.\*;_  
_import java.awt.event.\*;_

_class Main {_  
 _public static void main(String\[\] args0) {_  
 _JFrame frame = new JFrame();_  
 _frame.setSize(400, 400);_

 _DrawingArea drawingArea = new DrawingArea();_  
 _frame.getContentPane().add(drawingArea);_

 _frame.addWindowListener(new WindowAdapter() {_  
 _public void windowClosing(WindowEvent e) {_  
 _System.exit(0);_  
 _}_  
 _});_  
 _frame.setVisible(true);_  
 _}_  
_}_

_class DrawingArea extends JPanel {_  
 _private String mText;_  
 _private static String mStr1 = "The mouse was pressed here!";_  
 _private static String mStr2 = "The mouse was released here!";_  
 _private int miX, miY;_

 _// The constructor simply registers the drawing area to receive mouse events from itself._  
 _public DrawingArea() {_  
 _addMouseListener(new MouseAdapter() {_  
 _public void mousePressed(MouseEvent e) {_  
 _miX = e.getX();_  
 _miY = e.getY();_  
 _mText = mStr1;_  
 _repaint();_  
 _}_  
 _public void mouseReleased(MouseEvent e) {_  
 _miX = e.getX();_  
 _miY = e.getY();_  
 _mText = mStr2;_  
 _repaint();_  
 _}_  
 _});_  
 _}_

 _// The paint method.  This gets called in response to repaint()._  
 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);           // This paints the background._  
 _if (mText != null)_  
 _g.drawString(mText, miX, miY);_  
 _}_  
_}_

Note that prior to the introduction of the Swing package, one would override the _paint()_ method to implement custom painting. In Swing applications, however, we override the  _paintComponent()_ method instead. The _paintComponent()_ method will be called by the _paint()_ method in class _JComponent_. The _JComponent_'s _paint()_ method also implements features such as double buffering, which are useful in animation.

{{< anchor "2" >}}{{< /anchor >}}2\. Simple 2D Graphics
-------------------------------------------------------

The _paintComponent()_ method gives us a graphics context, which is an instance of a _Graphics_ subclass. A graphics context bundles information such as the area into which we can draw, the font and color to be used, the clipping region, etc. Note that we do not instantiate the graphics context in our program; in fact the _Graphics_ class itself is an abstract class. The _Graphics_ class provides methods for drawing simple graphics primitives, like lines, rectangles, ovals, arcs and polygons. It also provides methods for drawing text, as we saw above.

This program illustrates how to draw some basic shapes.

_import javax.swing.\*;_  
_import java.awt.\*;_  
_import java.awt.event.\*;_

_class Main {_  
 _public static void main(String\[\] args0) {_  
 _JFrame frame = new JFrame();_  
 _frame.setSize(400, 400);_

 _DrawingArea drawingArea = new DrawingArea();_  
 _frame.getContentPane().add(drawingArea);_  
 _frame.addWindowListener(new WindowAdapter() {_  
 _public void windowClosing(WindowEvent e) {_  
 _System.exit(0);_  
 _}_  
 _});_  
 _frame.setVisible(true);_  
 _}_  
_}_

_class DrawingArea extends JPanel {_  
 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);_

 _// Draw some simple geometric primitives._  
 _g.setColor(Color.red);_  
 _g.drawLine(10, 10, 40, 50);                                            // x1, y1, x2, y2_

 _g.setColor(Color.green);_  
 _g.drawRect(100, 100, 40, 30);                                        // x, y, width, height_

 _g.setColor(Color.yellow);_  
 _g.drawOval(100, 200, 30, 50);                                        // x, y, width, height_

 _g.setColor(Color.blue);_  
 _g.drawArc(200, 200, 50, 30, 45, 90);                             // x, y, width, height, start angle, arc angle_

 _int x1\_points\[\] = {100, 130, 140, 115, 90};_  
 _int y1\_points\[\] = {300, 300, 340, 370, 340};_  
 _g.setColor(Color.black);_  
 _g.drawPolygon(x1\_points, y1\_points, x1\_points.length);   // x array, y array, length_

 _int x2\_points\[\] = {300, 330, 340, 315, 290};_  
 _int y2\_points\[\] = {300, 300, 340, 370, 340};_  
 _g.setColor(Color.cyan);_  
 _g.drawPolyline(x2\_points, y2\_points, x2\_points.length);    // x array, y array, length_

 _g.setColor(Color.orange);_  
 _g.fillRect(300, 100, 40, 30);                                             // x, y, width, height_

 _g.setColor(Color.magenta);_  
 _g.fill3DRect(300, 200, 40, 30, true);                                // x, y, width, height, raised_  
 _}_  
_}_

The [Java® 2D API](http://java.sun.com/docs/books/tutorial/2d/index.html) provides a range of advanced capabilities, such as stroking and filling, affine transformations, compositing and transparency.

{{< anchor "3" >}}{{< /anchor >}}3\. A Graphics Example
-------------------------------------------------------

Here is a complete program that allows you to interactively define points, lines and polygon using mouse input. This program can be run either as an application or as an applet.

_// This is a Java graphics example that can be run either as an applet or as an application._  
_// Created by Kevin Amaratunga 10/17/1997.  Converted to Swing 10/17/1999._

_import javax.swing.\*;_  
_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import java.util.\*;_

_// In order to run as an applet, class Geometry must be declared as a public class.  Note that there_  
_// cannot  be more than one public class in a .java file.  Also, the public class must have the same_  
_// same name as the .java file._  
 _public class Geometry extends JApplet {_  
 _JTextArea mTextArea;_  
 _DrawingArea mDrawingArea;_

 _public Geometry() {_  
 _// Get the applet's container._  
 _Container c = getContentPane();_

 _// Choose a layout manager.  BorderLayout is a straightforward one to use._  
 _c.setLayout(new BorderLayout());_

 _// Create a drawing area and add it to the center of the applet._  
 _mDrawingArea = new DrawingArea(this);_  
 _c.add("Center", mDrawingArea);_

 _// Create a read only text area to be used for displaying_  
 _// information.  Add it to the bottom of the applet._  
 _mTextArea = new JTextArea();_  
 _JScrollPane scrollPane = new JScrollPane(mTextArea);_  
 _scrollPane.setPreferredSize(new Dimension(600, 100));_  
 _mTextArea.setEditable(false);_  
 _c.add("South", scrollPane);_  
 _}_

 _public JTextArea getTextArea() {_  
 _return mTextArea;_  
 _}_

 _public static void main(String args\[\]) {_  
 _// Create the applet object._  
 _Geometry geomApplet = new Geometry();_

 _// Create a frame.  Then set its size and title._  
 _JFrame frame = new JFrame();_  
 _frame.setSize(600, 600);_  
 _frame.setTitle(geomApplet.getClass().getName());_

 _// Make the frame closable._  
 _WindowListener listener = new WindowAdapter() {_  
 _// An anonymous class that extends WindowAdapter._  
 _public void windowClosing(WindowEvent e) {_  
 _System.out.println("Window closing");_  
 _System.exit(0);_  
 _}_  
 _};_  
 _frame.addWindowListener(listener);_

 _// Add the applet to the center of the frame._  
 _frame.getContentPane().add("Center", geomApplet);_

 _// Initialize the applet._  
 _geomApplet.init();_

 _// Make the frame visible._  
 _frame.setVisible(true);_

 _// Start the applet._  
 _geomApplet.start();_  
 _}_  
_}_  
 

_// The drawing area is the area within all the objects will be drawn._  
_class DrawingArea extends JPanel implements MouseListener {_  
 _// Parent and child widgets._  
 _Geometry mGeomApplet;                     // The parent applet._  
 _JPopupMenu mPopupMenu;                 // Popup menu for creating new objects._

 _// Object lists._  
 _Vector mPointList;                             // List of all Point objects._  
 _Vector mLineList;                               // List of all Line objects._  
 _Vector mPolygonList;                         // List of all Polygon objects._

 _// Constants that indicate which kind of object (if any) is currently being created._  
 _static final int NO\_OBJECT = 0;_  
 _static final int POINT\_OBJECT = 1;_  
 _static final int LINE\_OBJECT = 2;_  
 _static final int POLYGON\_OBJECT = 3;_

 _// Miscellaneous state variables._  
 _int miLastButton = 0;                        // Last button for which an event was received._  
 _int miAcceptingInput = 0;                  // Type of object (if any) that we are currently creating._  
 _int miPointsEntered = 0;                   // Number of points entered for this object so far._  
 _Object mCurrentObject = null;           // The object that we are currently creating._  
 

 _// DrawingArea constructor._  
 _DrawingArea(Geometry geomApplet) {_  
 _JMenuItem menuItem;_

 _mGeomApplet = geomApplet;_

 _// Set the background color._  
 _setBackground(Color.white);_

 _// Register the drawing area to start listening to mouse events._  
 _addMouseListener(this);_

 _// Create a popup menu and make it a child of the drawing area, but don't show it just yet._  
 _mPopupMenu = new JPopupMenu("New Object");_  
 _menuItem = new JMenuItem("Point");_  
 _menuItem.addActionListener(new PointActionListener(this));_  
 _mPopupMenu.add(menuItem);_  
 _menuItem = new JMenuItem("Line");_  
 _menuItem.addActionListener(new LineActionListener(this));_  
 _mPopupMenu.add(menuItem);_  
 _menuItem = new JMenuItem("Polygon");_  
 _menuItem.addActionListener(new PolygonActionListener(this));_  
 _mPopupMenu.add(menuItem);_  
 _add(mPopupMenu);_

 _// Create the object lists with a reasonable initial capacity._  
 _mPointList = new Vector(10);_  
 _mLineList = new Vector(10);_  
 _mPolygonList = new Vector(10);_  
 _}_  
 

 _// The paint method._  
 _public void paintComponent(Graphics g) {_  
 _int i;_

 _// Paint the background._  
 _super.paintComponent(g);_

 _// Draw all objects that are stored in the object lists._  
 _for (i = 0; i \< mPointList.size(); i++) {_  
 _Point point = (Point)mPointList.elementAt(i);_  
 _g.fillRect(point.x-1, point.y-1, 3, 3);_  
 _}_

 _for (i = 0; i \< mLineList.size(); i++) {_  
 _Line line = (Line)mLineList.elementAt(i);_  
 _line.draw(g);_  
 _}_

 _for (i = 0; i \< mPolygonList.size(); i++) {_  
 _Polygon polygon = (Polygon)mPolygonList.elementAt(i);_  
 _int j;_

 _g.setColor(Color.red);_  
 _g.drawPolygon(polygon);_  
 _g.setColor(Color.black);_  
 _for (j = 0; j \< polygon.npoints; j++) {_  
 _g.fillRect(polygon.xpoints\[j\], polygon.ypoints\[j\], 3, 3);_  
 _}_  
 _}_

 _// Draw as much of the current object as available._  
 _switch (miAcceptingInput) {_  
 _case LINE\_OBJECT:_  
 _Line line = (Line)mCurrentObject;_  
 _if (line.mb1 && !line.mb2)_  
 _g.fillRect(line.mEnd1.x-1, line.mEnd1.y-1, 3, 3);_  
 _break;_

 _case POLYGON\_OBJECT:_  
 _Polygon polygon = (Polygon)mCurrentObject;_  
 _int j;_  
 _g.setColor(Color.red);_  
 _g.drawPolyline(polygon.xpoints, polygon.ypoints, polygon.npoints);_  
 _g.setColor(Color.black);_  
 _for (j = 0; j \< polygon.npoints; j++) {_  
 _g.fillRect(polygon.xpoints\[j\], polygon.ypoints\[j\], 3, 3);_  
 _}_  
 _break;_

 _default:_  
 _break;_  
 _}_

 _// Draw some text at the top of the drawing area._  
 _int w = getSize().width;_  
 _int h = getSize().height;_  
 _g.drawRect(0, 0, w - 1, h - 1);_  
 _g.setFont(new Font("Helvetica", Font.PLAIN, 15));_  
 _g.drawString("Drawing area", (w - g.getFontMetrics().stringWidth("Drawing area"))/2, 10);_  
 _}_  
 

 _// The next five methods are required, since we implement the_  
 _// MouseListener interface.  We are only interested in mouse pressed_  
 _// events._  
 _public void mousePressed(MouseEvent e) {_  
 _int iX = e.getX();  // The x and y coordinates of the_  
 _int iY = e.getY();  // mouse event._  
 _int iModifier = e.getModifiers();_

 _if ((iModifier & InputEvent.BUTTON1\_MASK) != 0) {_  
 _miLastButton = 1;_

 _// If we are currently accepting input for a new object,_  
 _// then add the current point to the object._  
 _if (miAcceptingInput != NO\_OBJECT)_  
 _addPointToObject(iX, iY);_  
 _}_  
 _else if ((iModifier & InputEvent.BUTTON2\_MASK) != 0) {_  
 _miLastButton = 2;_

 _}_  
 _else if ((iModifier & InputEvent.BUTTON3\_MASK) != 0) {_  
 _miLastButton = 3;_

 _if (miAcceptingInput == NO\_OBJECT) {_  
 _// Display the popup menu provided we are not accepting_  
 _// any input for a new object._  
 _mPopupMenu.show(this, iX, iY);_  
 _}_  
 _else if (miAcceptingInput == POLYGON\_OBJECT) {_  
 _// If current object is a polygon, finish it._  
 _mPolygonList.addElement(mCurrentObject);_  
 _String str = "Finished creating polygon object.\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _mGeomApplet.repaint();_  
 _miAcceptingInput = NO\_OBJECT;_  
 _miPointsEntered = 0;_  
 _mCurrentObject = null;_  
 _}_  
 _}_  
 _}_

 _public void mouseClicked(MouseEvent e) {}_

 _public void mouseEntered(MouseEvent e) {}_

 _public void mouseExited(MouseEvent e) {}_

 _public void mouseReleased(MouseEvent e) {}_

 _public void getPointInput() {_  
 _miAcceptingInput = POINT\_OBJECT;_  
 _mCurrentObject = (Object)new Point();_  
 _mGeomApplet.getTextArea().append("New point object: enter point.\\n");_  
 _}_

 _public void getLineInput() {_  
 _miAcceptingInput = LINE\_OBJECT;_  
 _mCurrentObject = (Object)new Line();_  
 _mGeomApplet.getTextArea().append("New line: enter end points.\\n");_  
 _}_

 _public void getPolygonInput() {_  
 _miAcceptingInput = POLYGON\_OBJECT;_  
 _mCurrentObject = (Object)new Polygon();_  
 _mGeomApplet.getTextArea().append("New polygon: enter vertices ");_  
 _mGeomApplet.getTextArea().append("(click right button to finish).\\n");_  
 _}_

 _void addPointToObject(int iX, int iY) {_  
 _String str;_

 _miPointsEntered++;_  
 _switch (miAcceptingInput) {_  
 _case POINT\_OBJECT:_  
 _str = "Point at (" + iX + "," + iY + ")\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _Point point = (Point)mCurrentObject;_  
 _point.x = iX;_  
 _point.y = iY;_  
 _mPointList.addElement(mCurrentObject);_  
 _str = "Finished creating point object.\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _mGeomApplet.repaint();_  
 _miAcceptingInput = NO\_OBJECT;_  
 _miPointsEntered = 0;_  
 _mCurrentObject = null;_  
 _break;_

 _case LINE\_OBJECT:_  
 _if (miPointsEntered \<= 2) {_  
 _str = "End " + miPointsEntered + " at (" + iX + "," + iY + ")";_  
 _str += "\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _}_  
 _Line line = (Line)mCurrentObject;_  
 _if (miPointsEntered == 1) {_  
 _line.setEnd1(iX, iY);_  
 _mGeomApplet.repaint();_  
 _}_  
 _else {_  
 _if (miPointsEntered == 2) {_  
 _line.setEnd2(iX, iY);_  
 _mLineList.addElement(mCurrentObject);_  
 _str = "Finished creating line object.\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _mGeomApplet.repaint();_  
 _}_  
 _miAcceptingInput = NO\_OBJECT;_  
 _miPointsEntered = 0;_  
 _mCurrentObject = null;_  
 _}_  
 _break;_

 _case POLYGON\_OBJECT:_  
 _str = "Vertex " + miPointsEntered + " at (" + iX + "," + iY + ")";_  
 _str += "\\n";_  
 _mGeomApplet.getTextArea().append(str);_  
 _Polygon polygon = (Polygon)mCurrentObject;_  
 _polygon.addPoint(iX, iY);_  
 _mGeomApplet.repaint();_  
 _break;_

 _default:_  
 _break;_  
 _}                           // End switch._  
 _}_  
_}_  
 

_// Action listener to create a new Point object._  
_class PointActionListener implements ActionListener {_  
 _DrawingArea mDrawingArea;_

 _PointActionListener(DrawingArea drawingArea) {_  
 _mDrawingArea = drawingArea;_  
 _}_

 _public void actionPerformed(ActionEvent e) {_  
 _mDrawingArea.getPointInput();_  
 _}_  
_}_  
 

_// Action listener to create a new Line object._  
_class LineActionListener implements ActionListener {_  
 _DrawingArea mDrawingArea;_

 _LineActionListener(DrawingArea drawingArea) {_  
 _mDrawingArea = drawingArea;_  
 _}_

 _public void actionPerformed(ActionEvent e) {_  
 _mDrawingArea.getLineInput();_  
 _}_  
_}_  
 

_// Action listener to create a new Polygon object._  
_class PolygonActionListener implements ActionListener {_  
 _DrawingArea mDrawingArea;_

 _PolygonActionListener(DrawingArea drawingArea) {_  
 _mDrawingArea = drawingArea;_  
 _}_

 _public void actionPerformed(ActionEvent e) {_  
 _mDrawingArea.getPolygonInput();_  
 _}_  
_}_  
 

_// A line class._  
_class Line {_  
 _Point mEnd1, mEnd2;_  
 _boolean mb1, mb2;_

 _Line() {_  
 _mb1 = mb2 = false;_  
 _mEnd1 = new Point();_  
 _mEnd2 = new Point();_  
 _}_

 _void setEnd1(int iX, int iY) {_  
 _mEnd1.x = iX;_  
 _mEnd1.y = iY;_  
 _mb1 = true;_  
 _}_

 _void setEnd2(int iX, int iY) {_  
 _mEnd2.x = iX;_  
 _mEnd2.y = iY;_  
 _mb2 = true;_  
 _}_

 _void draw(Graphics g) {_  
 _g.fillRect(mEnd1.x-1, mEnd1.y-1, 3, 3);_  
 _g.fillRect(mEnd2.x-1, mEnd2.y-1, 3, 3);_  
 _g.setColor(Color.green);_  
 _g.drawLine(mEnd1.x, mEnd1.y, mEnd2.x, mEnd2.y);_  
 _g.setColor(Color.black);_  
 _}_  
_}_