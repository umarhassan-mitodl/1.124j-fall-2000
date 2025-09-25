---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Working With Images
uid: 868be7fa-4b57-691b-5d07-2b8c285a801e
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Loading and Displaying Images](#1)
2.  [Tracking Image Loading](#2)
3.  [Image Animations](#3)
4.  [Examples](#4)

{{< anchor "1" >}}{{< /anchor >}}1\. Loading and Displaying Images
------------------------------------------------------------------

_(Ref. [Java® Tutorial](http://java.sun.com/docs/books/tutorial/uiswing/painting/index.html)__)_

Images provide a way to augment the aethetic appeal of a Java program. Java® provides support for two common image formats: GIF and JPEG. An image that is in one of these formats can be loaded by using either a URL or a filename.

The basic class for representing an image is _java.awt.Image_. Packages that are relevant to image handling are _java.applet_, _java.awt_ and _java.awt.image_.  
 

Loading an Image
----------------

Images can be loaded using the _getImage()_ method. There are several versions of _getImage()_. When we create an applet by subclassing _javax.swing.JApplet_, we inherit the following methods from _java.awt.Applet_.

*   _Image getImage(URL url)_
*   _Image getImage(URL url, String name)_

These methods only work _after_ the applet's constructor has been called. A good place to call them is in the applet's _init()_ method. Here are some examples:

 _// In a method in an Applet subclass, such as the init() method:_  
 _Image image1 = getImage(getCodeBase(), "imageFile.gif");_  
 _Image image2 = getImage(getDocumentBase(), "anImageFile.jpeg");_  
 _Image image3 = getImage(new URL("http://java.sun.com/graphics/people.gif"));_

In the first example, the code base is the URL of the directory that contains the applets .class file. In the second example, the document base is the URL of the directory containing the HTML document that loads the applet.

Alternatively, we may use the _getImage()_ methods provided by the _Toolkit_ class.

*   _Image getImage(URL url)_
*   _Image getImage(String filename)_

This approach can be used either in an applet or an application. e.g.

 _Toolkit toolkit = Toolkit.getDefaultToolkit();_  
 _Image image1 = toolkit.getImage("imageFile.gif");_  
 _Image image2 = toolkit.getImage(new URL("http://java.sun.com/graphics/people.gif"));_

In general, applets cannot read files that are on the local machine for reasons of security. Thus, applets typically download any images they need from the server.

Note that _getImage()_ returns immediately without waiting for the image to load. The image loading process occurs lazily, in that the image doesn't start to load until the first time we try to display it.  
 

Displaying an Image
-------------------

Images can be displayed by calling one of the _drawImage()_ methods supplied by the _Graphics_ object that gets passed in to the _paintComponent()_ method.

This version draws an image at the specified position using its natural size:

 _boolean drawImage(Image img, int x, int y, ImageObserver observer)_

This version draws an image at the specified position, and scales it to the specified width and height:

 _boolean drawImage(Image img, int x, int y, int width, int height, ImageObserver observer)_

The _ImageObserver_ is a mechanism for tracking the loading of an image (see below). One of the uses for an _ImageObserver_ is to ensure that the image is properly displayed once it has finished loading. The return value from _drawImage()_ is rarely used: this value is _true_ if the image has been completely loaded and thus completely painted, and _false_ otherwise.

Here is a simple example of loading and displaying images.

_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import javax.swing.\*;_

_// This applet displays a single image twice,_  
_// once at its normal size and once much wider._

 _public class ImageDisplayer extends JApplet {_  
 _static String imageFile = "images/rocketship.gif";_

 _public void init() {_  
 _Image image = getImage(getCodeBase(), imageFile);_  
 _ImagePanel imagePanel = new ImagePanel(image);_  
 _getContentPane().add(imagePanel, BorderLayout.CENTER);_  
 _}_  
_}_

_class ImagePanel extends JPanel {_  
 _Image image;_

 _public ImagePanel(Image image) {_  
 _this.image = image;_  
 _}_

 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);  // Paint background_

 _// Draw image at its natural size first._  
 _g.drawImage(image, 0, 0, this); //85x62 image_

 _// Now draw the image scaled._  
 _g.drawImage(image, 90, 0, 300, 62, this);_  
 _}_  
_}_  
 

{{< anchor "2" >}}{{< /anchor >}}2\. Tracking Image Loading
-----------------------------------------------------------

The most frequent reason to track image loading is to find out when an image or group of images is fully loaded. At a minimum, we will want to make sure that each image is redrawn after it finishes loading, otherwise only a part of the image will be visible.  We may even wish to wait until image loading is complete, before attempting to do any drawingat all. There are two ways to track images: using the _MediaTracker_ class and by implementing the _ImageObserver_ interface.

Media Trackers
--------------

_(Ref. [Java® Tutorial](http://java.sun.com/docs/books/tutorial/uiswing/painting/index.html))_

The _MediaTracker_ class provides a relatively simple way to delay drawing until the image loading process is complete. We can modify the _ImageDisplayer_ applet to perform the following steps:

*   Create a _MediaTracker_ object.
*   Add the image to it using the _addImage()_ method. (If we had several images, they would all be added to the same _MediaTracker_.)
*   Use the _waitForAll()_ method to load the image data synchronously when the program starts up.
*   Use the _checkAll()_ method in the _paintComponent()_ method to test whether image loading is complete.

_import java.awt.\*;_  
_import java.awt.event.\*;_  
_import javax.swing.\*;_

_// This applet displays a single image twice,_  
_// once at its normal size and once much wider._

 _public class ImageDisplayer extends JApplet {_  
 _static String imageFile = "images/rocketship.gif";_

 _public void init() {_  
 _Image image = getImage(getCodeBase(), imageFile);_

 **_// Create a media tracker and add the image to it.  If we had several_**  
 **_// images to load, they could all be added to the same media tracker._**  
 **_MediaTracker tracker = new MediaTracker(this);_**  
 **_tracker.addImage(image, 0);_**

 **_// Start downloading the image and wait until it finishes loading._**  
 **_try {_**  
 **_tracker.waitForAll();_**  
 **_}_**  
 **_catch(InterruptedException e) {}_**

 _ImagePanel imagePanel = new ImagePanel(image, tracker);_  
 _getContentPane().add(imagePanel, BorderLayout.CENTER);_  
 _}_  
_}_

_class ImagePanel extends JPanel {_  
 _Image image;_  
 _MediaTracker tracker;_

 _public ImagePanel(Image image, MediaTracker tracker) {_  
 _this.image = image;_  
 _this.tracker = tracker;_  
 _}_

 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);  // Paint background_

 **_// Check that the image has loaded before trying to draw it._**  
 **_if (!tracker.checkAll()) {_**  
 **_g.drawString("Please wait...", 0, 0);_**  
 **_return;_**  
 **_}_**

 _// Draw image at its natural size first._  
 _g.drawImage(image, 0, 0, this); //85x62 image_

 _// Now draw the image scaled._  
 _g.drawImage(image, 90, 0, 300, 62, this);_  
 _}_  
_}_  
 

Image Observers
---------------

Image observers provide a way to track image loading even more closely. In order to track image loading, we must pass in an object that implements the _ImageObserver_ interface as the last argument to the _Graphics_ object's _drawImage()_ method. The _ImageObserver_ interface has a method named

 _imageUpdate(Image img, int flags, int x, int y, int width, int height)_

which will be called whenever an interesting milestone in the image loading process is reached. The _flags_ argument can be examined to determine exactly what this milestone is. The _ImageObserver_ interface defines the following constants, against which the _flags_ argument can be tested using the bitwise _AND_ operator:

 _public static final int WIDTH;_  
 _public static final int HEIGHT;_  
 _public static final int PROPERTIES;_  
 _public static final int SOMEBITS;_  
 _public static final int FRAMEBITS;_  
 _public static final int ALLBITS;_  
 _public static final int ERROR;_  
 _public static final int ABORT;_

The _java.awt.Component_ class implements the _ImageObserver_ interface and provides a default version of _imageUpdate()_, which calls _repaint()_ when the image has finished loading. The following example shows how we could modify the _ImageDisplayer_ applet, so that the _ImagePanel_ class provides its own version of _imageUpdate()_ instead of using the one that it inherits from _java.awt.Component_. Note that we pass _this_ as the last argument to _drawImage()_.  
 

_import java.awt.\*;_  
_import java.awt.event.\*;_  
**_import java.awt.image.ImageObserver;_**  
_import javax.swing.\*;_

_// This applet displays a single image twice,_  
_// once at its normal size and once much wider._

 _public class ImageDisplayer extends JApplet {_  
 _static String imageFile = "images/rocketship.gif";_

 _public void init() {_  
 _Image image = getImage(getCodeBase(), imageFile);_  
 _ImagePanel imagePanel = new ImagePanel(image);_  
 _getContentPane().add(imagePanel, BorderLayout.CENTER);_  
 _}_  
_}_

_class ImagePanel extends JPanel **implements ImageObserver** {_  
 _Image image;_

 _public ImagePanel(Image image) {_  
 _this.image = image;_  
 _}_

 _public void paintComponent(Graphics g) {_  
 _super.paintComponent(g);  // Paint background_

 _// Draw image at its natural size first._  
 _g.drawImage(image, 0, 0, **this**); //85x62 image_

 _// Now draw the image scaled._  
 _g.drawImage(image, 90, 0, 300, 62, **this**);_  
 _}_

 **_public boolean imageUpdate(Image image, int flags, int x, int y,_**  
 **_int width, int height) {_**  
 **_// If the image has finished loading, repaint the window._**  
 **_if ((flags & ALLBITS) != 0) {_**  
 **_repaint();_**  
 **_return false;  // Return false to say we don't need further notification._**  
 **_}_**  
 **_return true;       // Image has not finished loading, need further notification._**  
 **_}_**  
_}_  
 

{{< anchor "3" >}}{{< /anchor >}}3\. Image Animations
-----------------------------------------------------

_(Ref. Java® Tutorial: Moving an Image Across the Screen and Displaying a Sequence of Images)_

Moving an Image Across the Screen
---------------------------------

The simplest type of image animation involves moving a single frame image across the screen. This is known as _cutout animation_, and it is accomplished by repeatedly updating the position of the image in an animation thread, in a similar fashion to the bouncing ball animation we saw earlier.

Displaying a Sequence of Images
-------------------------------

Another type of image animation is _cartoon style animation_, in which a sequence of image frames is displayed in succession. The following example does this by creating an array of ten _Image_ objects and then incrementing the array index every time the _paintComponent()_ method is called.The portion of code that is of main interest is:

 _// In initialization code._  
 _Image\[\] images = new Image\[10\];_  
 _for (int i = 1; i \<= 10; i++) {_  
 _images\[i-1\] = getImage(getCodeBase(), "images/duke/T"+i+".gif");_  
 _}_

 _// In the paintComponent method._  
 _g.drawImage(images\[ImageSequenceTimer.frameNumber % 10\], 0, 0, this);_

This is a good example of why a _MediaTracker_  should be used to delay drawing until after all the images have loaded.   

{{< anchor "4" >}}{{< /anchor >}}4\. Examples
---------------------------------------------

Here are some more examples of image animation:

*   [Bouncing heads](http://java.sun.com/applets/other/BouncingHeads/index.html) 
*   [Tumbing duke](http://java.sun.com/applets/other/TumblingDuke/index.html) 

Check out [Code Samples and Applets](http://java.sun.com/applets/index.html) for other interesting applets.