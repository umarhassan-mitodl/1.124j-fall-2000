---
content_type: page
description: Lecture notes and related links
draft: false
file_size: ''
file_type: ''
image_metadata:
  caption: ''
  credit: ''
  image-alt: ''
learning_resource_types:
- Lecture Notes
license: https://creativecommons.org/licenses/by-nc-sa/4.0/
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
resourcetype: Document
title: Java 3D Lecture
uid: c9c9104a-ac54-a054-d006-354e424ccb63
video_files:
  archive_url: ''
  video_captions_file: ''
  video_thumbnail_file: ''
  video_transcript_file: ''
video_metadata:
  video_speakers: ''
  video_tags: ''
  youtube_description: ''
  youtube_id: ''
---
This lecture is courtesy of Petros Komodromos.

Topics

1. [Introduction to Java® 3D](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#1)
2. [Java® 3D References](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#2)
3. [Examples and Applications](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#3)
4. [Scene Graph Structure and basic Java® 3D concepts and classes](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#4)
5. [A simple Java® 3D program](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#5)
6. [Performance of Java® 3D](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#6)

{{\< anchor "1" >}}{{\< /anchor >}}1. Introduction to Java® 3D

*Java® 3D* is a general-purpose, platform-independent, object-oriented API for 3D-graphics that enables high-level development of Java® applications and applets with 3D interactive rendering capabilities. With *Java® 3D*, 3D scenes can be built programmatically, or, alternatively, 3D content can be loaded from VRML or other external files. *Java® 3D*, as a part of the *Java® Media APIs*, integrates well with the other [Java® technologies and APIs](http://java.sun.com/products/). For example, [*Java® 2D*](http://java.sun.com/products/java-media/2D/index.html) API can be used to plot selected results, while the [*Java® Media Framework (JMF)*](http://java.sun.com/products/java-media/jmf/index.html) API can be used to capture and stream audio and video.

Java® 3D is based on a directed acyclic graph-based scene structure, known as scene graph, that is used for representing and rendering the scene. The scene structure is a tree-like diagram that contains nodes with all the necessary information to create and render the scene. In particular, the [scene graph](https://ocw-studio.odl.mit.edu/sites/1-124j-foundations-of-software-engineering-fall-2000/type/page/edit/c9c9104a-ac54-a054-d006-354e424ccb63/#4) contains the nodes that are used to represent and transform all objects in the scene, and all viewing control parameters, i.e. all objects with information related to the viewing of the scene. The scene graph can be manipulated very easily and quickly allowing efficient rendering by following a certain optimal order and bypassing hidden parts of objects in the scene.

Java® 3D API has been developed under a joint collaboration between Intel, Silicon Graphics, Apple, and Sun, combining the related knowledge of these companies. It has been designed to be a platform-independent API concerning the host's operating system (PC/Solaris/Irix/HPUX/Linux) and graphics (OpenGL/Direct3D) platform, as well as the input and output (display) devices. The implementation of Java® 3D is built on top of OpenGL, or Direct3D. The high level Java® 3D API allows rapid application development which is very critical, especially nowadays.

However, Java® 3D has some weaknesses such as the performance, which is inferior to that of OpenGL, and the limited access to the rendering pipeline details. It is also still under development and several bugs need to be fixed. Although Java® 3D cannot achieve peak performance, portability and rapid development advantages may overweigh the slight performance penalty for many applications.

The current version of the Java® 3D API is the Version 1.2, which works together with the [Java® 2 Platform](http://java.sun.com/j2se/). Both APIs can be downloaded for free from the [Java® products page of Sun](http://java.sun.com/products/).

 

{{\< anchor "2" >}}{{\< /anchor >}}2. Java® 3D References

The following list includes many links related to the Java® 3D API

- [*Java® 3D 1.2 API Documentation*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/index.html)  
- [*Java® 3D 1.2 Specification*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dguide/index.html)  
- Java® 3D Tutorial (PDF format):       
      
    - [*Chapter 0*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch0.pdf) , Preface, Appendices, and Glossary
    - [*Chapter 1*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch1.pdf) , Getting Started
    - [*Chapter 2*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch2.pdf) , Creating Content
    - [*Chapter 3*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch3.pdf) , Easier Content Creation
    - [*Chapter 4*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch4.pdf) , Interaction
    - [*Chapter 5*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch5.pdf) , Animation
    - [*Chapter 6*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch6.pdf) *,* Lights
    - [*Chapter 7*](http://java.sun.com/products/java-media/3D/collateral/j3d_tutorial_ch7.pdf) , Textures        
         
- [*Raw J3D*](https://www.oracle.com/java/technologies/javase/java-3d.html)
- [*Java® 3D: For Developers and End-User*](http://java.sun.com/developer/Books/Java3D/)
- *A Fourth generation Java® 3D graphics API*
- *Java® 3D FAQ at Sun*
- [*Java® 3D Community FAQ*](http://www.j3d.org/contact.html)
- *Extensive Java® 3D FAQ at Sun*
- *Java® 3D Group at NCSA*
- [*Java® 3D Community site*](http://www.j3d.org/)
- *The Java® 3D and VRML Working group*
- *VRML and Java® 3D Information Center*
- *Web 3D consortium*
- [*Java® 3D Loader Archive*](http://www.mail-archive.com/java3d-interest@java.sun.com/)

Java® 3D is specified in the packages: [*javax.media.j3d*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/package-summary.html) and [*javax.vecmath*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/vecmath/package-summary.html). Supporting classes and utilities are provided in the *com.sun.j3d* packages.

{{\< anchor "3" >}}{{\< /anchor >}}3. Examples and Applications

The following are examples provided by Java® 3D in directories with the names as follows under the subdirectory *java3d* of the directory *demo*.

- AlternateAppearance
- Appearance
- AppearanceMixed
- AWT\_Interaction: *java AWTInteraction*
- Background
- Billboard
- ConicWorld: *java  SimpleCylinder* ; *java  TexturedSphere*
- FourByFour: *appletviewer fbf.html*
- GearTest: *java GearBox*
- GeometryByReference
- GeometryCompression
- HelloUniverse
- Lightwave
- LOD
- ModelClip
- Morphing
- ObjLoad
- OffScreenCanvas3D
- OrientedShape3D
- PackageInfo
- PickTest
- PickText3D: *java PickText3DGeometry*
- PlatformGeometry
- PureImmediate
- ReadRaster
- Sound
- SphereMotion: *appletviewer SphereMotion.html*
- SplineAnim
- Text2D
- Text3D
- TextureByReference
- TextureTest
- TickTockCollision:  *java TickTockCollision*
- TickTockPicking
- VirtualInputDevice

For example, on a Sun Ultra 10 workstation the files for the *GearTest* example are located under the subdirectory:\_

mit/java\_v1.2ref/distrib/sun4x\_56/demo/java3d/GearTest\_

Similarly, if you download *Java® 3D* on your computer, the examples are typically stored in subdirectories in the subdirectory *demo\\java3d* of the directory where Java® has been downloaded, e.g. at *C:\\Java\\jdk1.3\\demo\\java3d*.

There are many fields in which Java® 3D can be used. The following are just a small selection of Java® 3D applications that are available on the net.

- *NCSA Astro3D*
- [*Collaborative Visualization Space Science and Engineering Center (SSEC)*](http://www.ssec.wisc.edu/~billh/visad.html#immersion)
- [*Java® 3D API Customer Success Stories*](http://java.sun.com/products/java-media/3D/in_action/)

{{\< anchor "4" >}}{{\< /anchor >}}4. Scene Graph Structure and Basic Java® 3D Concepts and Classes

*Scene graph: Content-View Branches*

A Java® 3D scene is created as a tree-like graph structure, which is traversed during rendering. The scene graph structure contains nodes that represent either the actual objects of the scene, or, specifications that describe how to view the objects. Usually, there are two  branches in Java® 3D, the **content branch**, which contains the nodes that describe the actual objects in the scene, and  the **view branch**, which contains nodes that specify viewing related conditions. Usually, the content branch contains much larger number of nodes than the view branch.

The following image shows a basic Java® 3D graph scene, where the content branch is located on the left and the view branch on the right side of the graph:

{{< resource uuid="cb6b58f7-abe0-910f-9d4c-1a4e758995c5" >}}

Java® 3D applications construct individual graphic components as separate objects, called nodes, and connects them together into a tree-like scene graph, in which the objects and the viewing of them can easily be manipulated. The scene graph structure contains the description of the virtual universe, which represents the entire scene. All information concerning geometric objects, their attributes, position and orientation, as well as the viewing information are all contained into the scene graph.

The above scene graph consists of superstructure components, in particular a [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html) and a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) object, and a two [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) objects, which are attached to the superstructure. The one branch graph, rooted at the left [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) node, is a content branch, containing all the relevant to the contents of the scene objects. The other branch, known as view branch, contains all the information related to the viewing and the rendering details of the scene.

The state of a shape node, or any other leaf node, is defined, during rendering, by the nodes that lie in the direct path between that node and the root node, i.e. the [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html). For example, a [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node in a path between a leaf node and the scene's root can change the position, orientation, and scale of the object represented by the leaf node.

[*SceneGraphObject*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/SceneGraphObject.html) Hierarchy

The Java® 3D node objects of a Java® 3D scene graph, which are instances of the [*Node*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Node.html) class, may reference node component objects, which are instances of the class NodeComponent. The [*Node*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Node.html) and [*NodeComponent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/NodeComponent.html) classes are subclasses of the [*SceneGraphObject*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html) abstract class. Almost all objects that may be included in a scene graph are instances of subclasses of the [*SceneGraphObject*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html) class. A scene graph object is constructed by instantiating the corresponding class, and then, it can be accessed and manipulated using the provided set and get methods.

The following graph shows the class hierarchy of the major subclasses of the [*SceneGraphObject*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html) class:

{{< resource uuid="d718435c-535c-ef73-9917-b89c8413f90f" >}}

*Class* [*Node*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Node.html) *and its subclasses*

The abstract Class [*Node*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Node.html) is the base class for almost all objects that constitute the scene graph. It has two subclasses the [*Group*,](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Group.html) and [*Leaf*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Leaf.html) classes, which have many useful subclasses. Class [*Group*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Group.html) is a superclass of, among others, the classes [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) and [*TransformGroup*.](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) Class [*Leaf*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Leaf.html), which is used for nodes with no children, is a superclass of, among others, the classes [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html), [*Light*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Light.html), [*Shape3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Shape3D.html), and [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/ViewPlatform.html). The [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node is used to define from where the scene is viewed. In particular, it can be used to specify the location and the orientation of the point of view.

*Class* [*NodeComponent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/NodeComponent.html) *and its subclasses*

Class [*NodeComponent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/NodeComponent.html) is the base class for classes that represent attributes associated with the nodes of the scene graph. It is the superclass of all scene graph node component classes, such as the [*Appearance*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Appearance.html), [*Geometry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Geometry.html), [*PointAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PointAttributes.html), and [*PolygonAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PolygonAttributes.html) classes. [*NodeComponent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/NodeComponent.html) objects are used to specify attributes for a node, such as the color and geometry of a shape node, i.e. a [*Shape3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Shape3D.html) node. In particular, a [*Shape3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Shape3D.html) node uses an [*Appearance*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Appearance.html) and a [*Geometry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Geometry.html) objects, where the [*Appearance*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Appearance.html) object is used to control how the associated geometry should be rendered by Java® 3D.

The geometry component information of a [*Shape3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Shape3D.html) node, i.e. its geometry and topology, can be specified in an instance of a subclass of the abstract [*Geometry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Geometry.html) class. A Geometry object is used as a component object of a [*Shape3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Shape3D.html) leaf node. Geometry objects consist of the following four generic geometric types. Each of these geometric types defines a visible object, or a set of objects.

- [*CompressedGeometry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/CompressedGeometry.html)
- [*GeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html)
- [*Raster*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Raster.html)
- [*Text3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Text3D.html)

For example, the [*GeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html) is a subclass of the class [*Geometry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Geometry.html), which itself extends the [*NodeComponent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/NodeComponent.html) class, that is extended to create the various primitive types such as lines, triangle strips and quadrilaterals.

{{< resource uuid="d404ba55-8789-1a59-f627-8f8ae65b49b3" >}}

The [*IndexedGeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/IndexedGeometryArray.html) object above contains separate integer arrays that index, among others, into arrays of positional coordinates specifying how vertices are connected to form geometry primitives. This class is extended to create the various indexed primitive types, such as [*IndexedLineArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/IndexedLineArray.html), [*IndexedPointArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/IndexedPointArray.html), and [*IndexedQuadArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/IndexedQuadArray.html).

Vertex data may be passed to the geometry array either by copying the data into the array using the existing methods, which is the default mode, or by passing a reference to the data.

The methods for setting positional coordinates, colors, normals, and texture coordinates, such as the method [*setCoordinates*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#setCoordinates_int__javax_vecmath_Point3d___), copy the data into the [*GeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html), which offers much flexibility in organizing the data.

Another set of methods allows data to be passed and accessed by reference, such as the [*setCoordRef3d*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#setCoordRef3d_javax_vecmath_Point3d___) method, set a reference to user-supplied data, e.g. coordinate arrays. In order to enable the passing of data by reference, the [*BY*\_\_REFERENCE\_](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#BY_REFERENCE) bit in the [*vertexFormat*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#GeometryArray_int__int_) field of the constructor for the corresponding [*GeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html) must be set accordingly. Data in any array that is referenced by a live or compiled [*GeometryArray*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html) object may only be modified using the [*updateData*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#updateData_javax_media_j3d_GeometryUpdater_) method assuming that the [*ALLOW\_REF\_DATA\_WRITE*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/GeometryArray.html#ALLOW_REF_DATA_WRITE) capability bit is set accordingly, which can be done using the [*setCapability*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html#setCapability_int_) method.

The [*Appearance*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Appearance.html) object defines all rendering state that control the way the associated geometry should be rendered. The rendering state consists of the following:

- Point attributes: a [*PointAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PointAttributes.html) object defines attributes used to define points, such as the size to be used
- Line attributes: using a [*LineAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/LineAttributes.html) object attributes used to define lines, such as the width and pattern, can be defined
- Polygon attributes: using a [*PolygonAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PolygonAttributes.html) object the attributes used to define polygons, such as rasterization mode (i.e.. filled, lines, or points) are defined
- Coloring attributes: a [*ColoringAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ColoringAttributes.html) object is used to defines attributes used in color selection and shading.
- Rendering attributes: defines rendering operations, such as whether invisible objects are rendered, using a [*RenderingAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/RenderingAttributes.html) object.
- Transparency attributes: a [*TransparencyAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransparencyAttributes.html) defines the attributes that affect transparency of the object
- Material: a [*Material*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Material.html) object defines the appearance of an object under illumination, such as the ambient color, specular color, diffuse color, emissive color, and shininess. It is used to control the color of the shape.
- Texture: the texture image and filtering parameters used, when texture mapping is enabled, can be defined in a [*Texture*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Texture.html) object.
- Texture attributes: a [*TextureAttributes*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TextureAttributes.html) object can be used to define the attributes that apply to texture mapping, such as the texture mode, texture transform, blend color, and perspective correction mode.
- Texture coordinate generation: the attributes that apply to texture coordinate generation can be defined in a [*TexCoordGeneration*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TexCoordGeneration.html) object.
- Texture unit state: array that defines texture state for each of N separate texture units allowing multiple textures to be applied to geometry. Each [*TextureUnitState*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TextureUnitState.html) object contains a Texture object, TextureAttributes, and TexCoordGeneration object for one texture unit.

[***VirtualUniverse***](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html)

and [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html)

After constructing a subgraph, it can be attached to a [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/VirtualUniverse.html) object through a high-resolution [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) object, which is itself attached to the virtual universe. The [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html) is the root of all Java® 3D scenes, while [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) objects are used for basic spatial placement. The attachment to a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) object makes all objects in the attached subgraph live (i.e. drawable), while removing it from the locale reverses the effect. Any node added to a live scene graph becomes live. However, in order to be able to modify a live node the corresponding [*capability* bits](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html#setCapability_int_) should be set accordingly.

Typically, a Java® 3D program has only one [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html) which consists of one, or more, [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) objects that may contain collections of subgraphs of the scene graph that are rooted by [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) nodes, i.e. a large number of  branch graphs. Although a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) has no explicit children, it may reference an arbitrary number of [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) nodes. The subgraphs contain all the scene graph nodes that exist in the universe. A [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Locale.html) node is used to accurately position a branch graph in a universe specifying a location within the virtual universe using high-resolution coordinates ([*HiResCoord*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/HiResCoord.html)), which represent 768 bits of floating point values. A [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) is positioned in a single [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html) node using one of its constructors.

The [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html) and [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) classes, as well as the [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) class, are subclasses of the basic superclass [***Object***](https://docs.oracle.com/javase/tutorial/java/IandI/objectclass.html), as shown below:

{{< resource uuid="e45316c9-a420-f0b0-66d3-544026497bcd" >}}

 

Branch Graphs

A branch graph is a scene graph rooted in a [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) node and can be used to point to the root of a scene graph branch. A graph branch can be added to the list of branch graphs of a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) node using its [*addBranchGraph*(*BranchGroup* bg)](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html#addBranchGraph_javax_media_j3d_BranchGroup_) method. [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) objects are the only objects that can be inserted into a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html)*'s* list of objects.

A [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) may be compiled by calling its compile method, which causes the entire subgraph to be compiled including any [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) nodes that may be contained within the subgraph. A graph branch, rooted by a  [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) *node,* becomes live when inserted into a virtual universe by attaching it to a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html). However, if a [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) is contained in another subgraph as a child of some other group node, it may not be attached to a [*Locale*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Locale.html) node.

Capability Bits, Making Live and Compiling

Certain optimizations can be done to achieve better performance by compiling a subgraph into an optimized internal format, prior to its attachment to a virtual universe. However, many *set* and *get* methods of objects that are part of a live or compiled scene graph cannot be accessed. In general, the *set* and *get* methods can be used only during the creation of a scene graph, except where explicitly allowed, in order to allow certain optimizations during rendering. The set and get methods that can be used when the object is live or compiled should be specified using a set of capability bits, which by default are disabled, prior to compiling or making live the object. The methods [*isCompiled()*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/SceneGraphObject.html#isCompiled__) and [*isLive()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html#isLive__) can be used to find out whether a scene graph object is compiled or live. The methods [*setCapability*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html#setCapability_int_) and [*getCapability*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SceneGraphObject.html#getCapability_int_) can be used to set properly the capability bits to allow access to the object's methods. However, the less the capability bits that are enabled, the more optimizations can be performed during rendering.

Viewing Branch: [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html)*,*  [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html)*,* [*Screen3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Screen3D.html)

The view branch has usually the following structure, consisting of nodes that control the viewing of the scene.

{{< resource uuid="be7231df-1539-a99c-6e1a-611c255912f1" >}}

The view branch contains some scene graph viewing objects that can be used to define the viewing parameters and details, such as the [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html), [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html), [*Screen3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Screen3D.html), [*PhysicalBody*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PhysicalBody.html), and [*PhysicalEnvironment*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PhysicalEnvironment.html) classes.

Java® 3D uses a viewing model that can be used to transform the position and direction of the viewing while the content branch remains unmodified. This is achieved with the use of the [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) and the [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) classes, to specify from where and how, respectively, the scene is being viewed.

The [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node controls the position, orientation and scale of the viewer. A viewer can navigate through the virtual universe by changing the transformation in the scene graph hierarchy above the [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node. The location of the viewer can be set using a [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node above the [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node. The [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node has an activation radius that is used together with the bounding volumes of [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html), [*Background*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Background.html) and other nodes in order to determine whether the latter nodes should be scheduled, or turned on, respectively. The method [*setActivationRadius*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html#setActivationRadius_float_) can be used to set the activation radius.

A [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) object connects to the [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node in the scene graph, and specifies all viewing parameters of the rendering process of a 3D scene. Although it exists outside of the scene graph, it attaches to a [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) leaf node in the scene graph, using the method [*attachViewPlatform*(*ViewPlatform* vp)](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html#attachViewPlatform_javax_media_j3d_ViewPlatform_). A [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) object contains references to a [*PhysicalBody*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PhysicalBody.html) and a [*PhysicalEnvironment*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PhysicalEnvironment.html) object, which can be set using the methods [*setPhysicalBody*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html#setPhysicalBody_javax_media_j3d_PhysicalBody_) and [*setPhysicalEnvironment*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html#setPhysicalEnvironment_javax_media_j3d_PhysicalEnvironment_)*, respectively*.

A [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) object contains a list of [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Canvas3D.html) objects where rendering of the view is done. The method [*addCanvas3D*(Canvas3D c)](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html#addCanvas3D_javax_media_j3d_Canvas3D_) of the class [*View*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) can be used to add the provided [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Canvas3D.html) object to the list of canvases of the [View](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/View.html) object.

{{< resource uuid="962db16a-d746-33a5-7a2a-a1311a65fb65" >}}

Class [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Canvas3D.html) extends the heavyweight class [*Canvas*](http://java.sun.com/j2se/1.3/docs/api/java/awt/Canvas.html) in order to achieve hardware acceleration, since a low rendering library, such as OpenGL, requires the rendering to be done in a native window to enable hardware acceleration.

Finally, all [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Canvas3D.html) objects on the same physical display device refer to a [*Screen3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Screen3D.html) object, which contains all information about that particular display device. [*Screen3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Screen3D.html) can be obtained from the [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Canvas3D.html) using the [*getScreen3D*()](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Canvas3D.html#getScreen3D__) method.

Default Coordinate System

The default coordinate system is a right-handed Cartesian coordinate system centered on the screen with the x and y-axes directed towards the right and top of the screen, respectively. The z-axis is, by default directed out of the screen towards the viewer, as shown below. The default distances are in meter and the angles in radians.        
 

{{< resource uuid="b4b7e83d-b897-f4fe-b33f-16f275d7751d" >}}

Transformations

Class [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) which extends the class [*Group*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Group.html) can be used to set a spatial transformation, such as positioning, orientation, and scaling of its children through the use of a [*Transform3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Transform3D.html) object. A [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node enables the setting and use of a coordinate system relative to its parent coordinate system.

The [*Transform3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Transform3D.html) object of a [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) object can be set using the method [*setTransform*(Transform3D  t)](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html#setTransform_javax_media_j3d_Transform3D_), which is used to set the transformation components of the [*Transform3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Transform3D.html) object to the ones of the passed parameter.

A [*Transform3D*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Transform3D.html) object is a 4x4 double-precision matrix that is used to determine the transformations of a [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node, as shown in the following equation. The elements T{{\< sub "00" >}}, T{{\< sub "01" >}}, T{{\< sub "02" >}}, T{{\< sub "10" >}}, T{{\< sub "11" >}}, T{{\< sub "12" >}},T{{\< sub "20" >}}, T{{\< sub "21" >}}, and T{{\< sub "22" >}} are used to set the rotation and scaling, and the T{{\< sub "03" >}}, T{{\< sub "13" >}}, and T{{\< sub "23" >}} are used to set the translation.

{{< resource uuid="339b4938-a492-82c1-5254-af6bded234ec" >}}

As the scene graph is traversed by the Java® 3D renderer, the transformations specified by any transformation nodes accumulate. The transformations closer to the geometry nodes executed prior to the ones closer to the virtual universe node.

{{\< anchor "5" >}}{{\< /anchor >}}5. A Simple Java® 3D Program

A Java® 3D program builds a scene graph, using Java® 3D classes and methods, that can be rendered onto the screen.

The following program creates 2 color cubes and a sphere as shown to the snapshot that follows the code.

*import java.awt.\*;*        
*import javax.swing.\*;*        
*import javax.media.j3d.\*;*        
*import javax.vecmath.\*;*        
*import java.awt.event.\*;*        
*import com.sun.j3d.utils.geometry.\*;*

*public class MyJava3D extends JFrame*        
*{*        
*//  Virtual Universe object.*        
*private VirtualUniverse universe;*

*//  Locale of the scene graph.*        
*private Locale locale;*        
 

*// BranchGroup for the Content Branch of the scene*        
*private BranchGroup contentBranch;*

*//  TransformGroup  node of the scene contents*        
*private TransformGroup contentsTransGr;*        
 

*// BranchGroup for the View Branch of the scene*        
*private BranchGroup viewBranch;*

*// ViewPlatform node, defines from where the scene is viewed.*        
*private ViewPlatform viewPlatform;*

*//  Transform group for the ViewPlatform node*        
*private TransformGroup vpTransGr;*

*//  View node, defines the View parameters.*        
*private View view;*

*// A PhysicalBody object can specify the user's head*        
*PhysicalBody body;*

*// A PhysicalEnvironment object can specify the physical*        
*// environment in which the view will be generated*        
*PhysicalEnvironment environment;*

*// Drawing canvas for 3D rendering*        
*private Canvas3D canvas;*

*// Screen3D Object contains screen's information*        
*private Screen3D screen;*

*private Bounds bounds;*        
 

*public MyJava3D()*        
*{*        
*super("My First Java3D Example");*

*// Creating and setting the Canvas3D*        
*canvas = new Canvas3D(null);*        
*getContentPane().setLayout( new BorderLayout( ) );*        
*getContentPane().add(canvas, "Center");*

*// Setting the VirtualUniverse and the Locale nodes*        
*setUniverse();*

*// Setting the content branch*        
*setContent();*

*// Setting the view branch*        
*setViewing();*

*// To avoid problems between Java3D and Swing*        
*JPopupMenu.setDefaultLightWeightPopupEnabled(false);*

*// enabling window closing*        
*addWindowListener(new WindowAdapter() {*        
*public void windowClosing(WindowEvent e)*        
*{System.exit(0); }   });*        
*setSize(600, 600);*        
*bounds = new BoundingSphere(new Point3d(0.0,0.0,0.0), Double.MAX\_VALUE);*        
*}*        
 

*private void setUniverse()*        
*{*        
*// Creating the VirtualUniverse and the Locale nodes*        
*universe = new VirtualUniverse();*        
*locale = new Locale(universe);*        
*}*

*private void setContent()*        
*{*        
*// Creating the content branch*

*contentsTransGr = new TransformGroup();*        
*contentsTransGr.setCapability(TransformGroup.ALLOW\_TRANSFORM\_WRITE);*

*setLighting();*

*ColorCube cube1 = new ColorCube(0.1);*

*Appearance appearance = new Appearance();*        
*cube1.setAppearance(appearance);*

*contentsTransGr.addChild(cube1);*        
 

*ColorCube cube2 = new ColorCube(0.25);*

*Transform3D t1 = new Transform3D();*        
*t1.rotZ(0.5);*        
*Transform3D t2 = new Transform3D();*        
*t2.set(new Vector3f(0.7f, 0.6f,-1.0f));*        
*t2.mul(t1);*        
*TransformGroup trans2 = new TransformGroup(t2);*        
*trans2.addChild(cube2);*        
*contentsTransGr.addChild(trans2);*        
 

*Sphere sphere = new Sphere(0.2f);*        
*Transform3D t3 = new Transform3D();*        
*t3.set(new Vector3f(-0.2f, 0.5f,-0.2f));*        
*TransformGroup trans3 = new TransformGroup(t3);*

*Appearance appearance3 = new Appearance();*

*Material mat = new Material();*        
*mat.setEmissiveColor(-0.2f, 1.5f, 0.1f);*        
*mat.setShininess(5.0f);*        
*appearance3.setMaterial(mat);*        
*sphere.setAppearance(appearance3);*        
*trans3.addChild(sphere);*        
*contentsTransGr.addChild(trans3);*        
 

*contentBranch = new BranchGroup();*        
*contentBranch.addChild(contentsTransGr);*        
*// Compiling the branch graph before making it live*        
*contentBranch .compile();*

*// Adding a branch graph into a locale makes its nodes live (drawable)*        
*locale.addBranchGraph(contentBranch);*        
*}*

*private void setLighting()*        
*{*        
*AmbientLight ambientLight =  new AmbientLight();*        
*ambientLight.setEnable(true);*        
*ambientLight.setColor(new Color3f(0.10f, 0.1f, 1.0f) );*        
*ambientLight.setCapability(AmbientLight.ALLOW\_STATE\_READ);*        
*ambientLight.setCapability(AmbientLight.ALLOW\_STATE\_WRITE);*        
*ambientLight.setInfluencingBounds(bounds);*        
*contentsTransGr.addChild(ambientLight);*

*DirectionalLight dirLight =  new DirectionalLight();*        
*dirLight.setEnable(true);*        
*dirLight.setColor( new Color3f( 1.0f, 0.0f, 0.0f ) );*        
*dirLight.setDirection( new Vector3f( 1.0f, -0.5f, -0.5f ) );*        
*dirLight.setCapability( AmbientLight.ALLOW\_STATE\_WRITE );*        
*dirLight.setInfluencingBounds(bounds);*        
*contentsTransGr.addChild(dirLight);*        
*}*

*private void setViewing()*        
*{*        
*// Creating the viewing branch*

*viewBranch = new BranchGroup();*

*// Setting the viewPlatform*        
*viewPlatform = new ViewPlatform();*        
*viewPlatform.setActivationRadius(Float.MAX\_VALUE);*        
*viewPlatform.setBounds(bounds);*

*Transform3D t = new Transform3D();*        
*t.set(new Vector3f(0.3f, 0.7f, 3.0f));*        
*vpTransGr = new TransformGroup(t);*

*// Node capabilities control (granding permission) read and write access*        
*//  after a node is live or compiled*        
*//  The number of capabilities small to allow more optimizations during compilation*        
*vpTransGr.setCapability(TransformGroup.ALLOW\_TRANSFORM\_WRITE);*        
*vpTransGr.setCapability( TransformGroup.ALLOW\_TRANSFORM\_READ);*

*vpTransGr.addChild(viewPlatform);*        
*viewBranch.addChild(vpTransGr);*

*// Setting the view*        
*view = new View();*        
*view.setProjectionPolicy(View.PERSPECTIVE\_PROJECTION );*        
*view.addCanvas3D(canvas);*

*body = new PhysicalBody();*        
*view.setPhysicalBody(body);*        
*environment = new PhysicalEnvironment();*        
*view.setPhysicalEnvironment(environment);*

*view.attachViewPlatform(viewPlatform);*

*view.setWindowResizePolicy(View.PHYSICAL\_WORLD);*

*locale.addBranchGraph(viewBranch);*        
*}*

*public static void main(String\[\] args)*        
*{*        
*JFrame frame = new MyJava3D();*        
*frame.setVisible(true);*

*}*        
*}*

{{< resource uuid="6b5587cd-656d-0bd0-fb79-7b5e50916d6c" >}}

 

A utility class, called *SimpleUniverse*, can alternatively be used to automatically build a common arrangement of a universe, locale, and viewing classes, avoiding the need to create explicitly the viewing branch. Then, a branch is added into the simple universe to make its nodes live (i.e. drawable).

*SimpleUniverse simpleUniverse = new SimpleUniverse(canvas);*        
*simpleUniverse.addBranchGraph(contentBranch);*

6\. More on Java® 3D

*Java® 3D and Swing*

Since the [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Canvas3D.html) extends the heavyweight AWT class *Canvas*, it should be handled with care if Swing is used. The information provided when [*mixing AWT and Swing*](http://java.sun.com/products/jfc/tsc/swingdoc-archive/mixing.html) components should be followed. The main problem is that there is one-to-one correspondence between heavyweight components and their window system peers, i.e. native OS window components. In contrast, a lightweight component expects to use the peer of its enclosing container since it does not have a peer.

When lightweight components overlap with heavyweight components, the heavyweight components are always painted on top. In general, the heavyweight [*Canvas3D*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Canvas3D.html) of Java® 3D should be kept apart from lightweight Swing components using different containers to avoid problems.

To avoid heavyweight components overlapping *Swing* popup menus, which are lightweight, the popup menus  can be forced to be heavyweight using the method *setLightWeightPopupEnabled()* of the *JPopupMenu* class.

Similarly, problems with tooltips can be avoided by invoking the following method

*ToolTipManager.sharedInstance().setLightWeightPopupEnabled(false)*

Behaviors

Behaviors are essentially Java® methods that are scheduled to run only when certain requirements are satisfied according to wakeup conditions. Although a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object is connected to the scene it is kept in a separate area of the Java® 3D runtime environment and it is not considered part of the scene graph. The runtime environment treats a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object differently ensuring that certain actions take place. All behaviors in Java® 3D extend the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class, which is an abstract class that itself extends the [*Leaf*](http://java.sun.com/products/java-media/3D/forDevelopers/j3dapi/javax/media/j3d/Leaf.html) class. The [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class provides a way to execute certain statements, provided in the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method, in order to modify the scene graph when specified criteria are satisfied.

The [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class has two major methods, in particular the [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method, which is called when the behavior becomes live, and the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method, which is called by the Java® 3D scheduler whenever appropriate,  and  a scheduling region. Typically, in order to create a custom behavior, the class [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) is extended and referenced by the scene graph from an appropriate place that should be able to effect. A custom behavior that extends the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class should implement the [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) and [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) methods, and provide other methods and constructors that may be needed. The [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class object contains the state information that is needed by its [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__)and the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) methods. A constructor or another method may be used to set references to the scene graph objects upon which the behavior acts. In addition, the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class is extended by the following three classes [*Billboard*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Billboard.html), [*Interpolator*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Interpolator.html), and [*LOD*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/LOD.html).

The [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method is called once when the behavior becomes "live", i.e. when its [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) node is added to a [*VirtualUniverse*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/VirtualUniverse.html), to initialize this behavior. The Java® 3D behavior scheduler calls the [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method, which should never be called directly. The [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method is used to set a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object, which has been "added" to the scene graph, into a "known" condition and register the criteria to be used to decide on its execution. Classes that extend Behavior must provide their own [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method. The [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method allows a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object to initialize its internal state and specify its initial wakeup conditions. Java® 3D automatically invokes a behavior's initialize code when a [*BranchGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/BranchGroup.html) node that contains the behavior is added to the virtual universe, i.e. becomes live. The [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method should return, since Java® 3D does not invoke the initialize method in a new thread, and therefore it must regain control. Finally, a wakeup condition must be set in order to be able to invoke the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method of the behavior.

However, a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object is considered active only when its scheduling bounds intersect the activation volume of a [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node. Therefore, the scheduling bounds should be provided for a behavior in order to be able to receive stimuli. The scheduling bounds of a behavior can be specified as a bounded spatial volume, such as a sphere, using the method [*setSchedulingBounds(Bounds region)*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#setSchedulingBounds_javax_media_j3d_Bounds_). Bounds are used for selective scheduling to improve performance. Bounds are used to decide whether a behavior should be added to the list of scheduled behaviors.

The [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method is called whenever the wakeup criteria are satisfied and the ViewPlatform's activation region intersect with the Behavior's scheduling region. The method is called by the Java® 3D behavior scheduler when something happens that causes the behavior to execute. A stimulus, i.e. a notification, informs the behavior that it should execute its [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method. Therefore, applications should not call explicitly this method. Classes that extend the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class must provide their own  [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method. The scheduling region defines a spatial volume that serves to enable the scheduling of [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) nodes. A [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) node is active, i.e. it can receive stimuli, whenever its scheduling region intersects the activation volume of a [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html).

The Java® 3D behavior scheduler invokes the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method of a Behavior node when its scheduling region intersects the  activation volume of a [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node and all wakeup criteria  of that behavior are satisfied. Then, the statements in the [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method may perform any computations and actions, such as including the registration of state change information that could cause Java® 3D to wake other Behavior objects and modify node values within the scene graph, change the internal state of the behavior, specify its next wakeup conditions, and exit. It is allowed to a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object to change its next trigger event. The [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method, typically, manipulates scene graph elements, as long as the associated capabilities bits are set accordingly. For example, a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) node can be used to repeatedly modify a [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node in order to animate the associated with the [*TransformGroup*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/TransformGroup.html) node objects.

The amount of work done in a [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus%28java.util.Enumeration%29#processStimulus_java_util_Enumeration_) method should be limited since the method may lower the frame rate of the renderer. Java® 3D assumes that [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) methods run to completion and if necessary they spawn threads.

The application must provide the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object with references to those scene graph elements that the Behavior object will manipulate. This is achieved by providing those references as arguments to the constructor of the behavior when the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object is created. Alternatively, the Behavior object itself can obtain access to the relevant scene graph elements either when Java® 3D invokes its [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) method or each time Java® 3D invokes its [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method. Typically, the application provides references to the scene graph objects that a behavior should be able to access as arguments to its constructor when the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) is instantiated.

Java® 3D assumes that [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) methods always run to completion and that if needed they can spawn threads. The structure of each [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) method consists of the following parts:

- code to decode and extract references from the [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) enumeration that awoke the object
- code to perform the manipulations associated with the [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html)
- code to establish new [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) for this behavior
- a path to exit, so that execution returns to the Java® 3D behavior scheduler

The [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) class is an abstract class that specifies a single wakeup condition. It is specialized to 14 different [*WakeupCriterion*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCriterion.html) subclasses and to 4 subclasses that can be used to create complex wakeup conditions using boolean logic combinations of individual  [*WakeupCriterion*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCriterion.html) objects. A Behavior node provides a [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) object to the Java® 3D behavior scheduler using its [*wakeupOn()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#wakeupOn_javax_media_j3d_WakeupCondition_) method. When that [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) is satisfied, while the scheduling region intersects the activation volume of a [*ViewPlatform*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/ViewPlatform.html) node, the behavior scheduler passes that same [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) back to the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) via an enumeration.

Java® 3D provides the following wakeup criteria that [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) objects can use to specify a complex [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html). All of the following are subclasses of the [*WakeupCriterion*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCriterion.html) class, which itself is a subclass of the [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) class.

- [*WakeupOnViewPlatformEntry:*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnViewPlatformEntry.html) when the center of a ViewPlatform enters a specified region
- [*WakeupOnViewPlatformExit:*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnViewPlatformExit.html) when the center of a ViewPlatform exits a specified region
- [*WakeupOnActivation*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnActivation.html): when a behavior is activated
- [*WakeupOnDeactivation*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnDeactivation.html): when a behavior is deactivated
- [*WakeupOnTransformChange*:](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnTransformChange.html) when a specified TransformGroup node's transform changes
- [*WakeupOnCollisionEntry*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnCollisionEntry.html): when collision is detected between a specified Shape3D node's Geometry object and any other object
- [*WakeupOnCollisionMovement*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnCollisionMovement.html): when movement occurs between a specified Shape3D node's Geometry object and any other object with which it collides
- [*WakeupOnCollisionExit*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnCollisionExit.html): when a specified Shape3D node's Geometry object no longer collides with any other object
- [*WakeupOnBehaviorPost*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnBehaviorPost.html): when a specified Behavior object posts a specific event
- [*WakeupOnAWTEvent*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnAWTEvent.html)*:* when a specified AWT event occurs, such as. a mouse press
- [*WakeupOnElapsedTime*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnElapsedTime.html): when a specified time interval elapses
- [*WakeupOnElapsedFrames:*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnElapsedFrames.html) when a specified number of frames have been drawn
- [*WakeupOnSensorEntry:*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnSensorEntry.html) when the center of a specified Sensor enters a specified region
- [*WakeupOnSensorExit*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnViewPlatformExit.html): when the center of a specified Sensor exits a specified region

A [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object constructs a [*WakeupCriterion*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCriterion.html) by providing the appropriate arguments, such as a reference to some scene graph object and a region of interest.

Multiple criteria can be combined using the following classes to form complex wakeup conditions.

- [*WakeupOr*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOr.html): specifies any number of wakeup conditions logically ORed together
- [*WakeupAnd*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupAnd.html): specifies any number of wakeup conditions logically ANDed together
- [*WakeupOrOfAnds*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOrOfAnds.html): specifies any number of OR wakeup conditions logically ANDed together
- [*WakeupAndOfOr:*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupAndOfOrs.html)  specifies any number of AND wakeup conditions logically ORed together

The class hierarchy of the [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) class is shown below:

{{< resource uuid="76163ee3-f63d-c91c-3d9f-88be97281f08" >}}

The following code provides an example of setting a [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) object

    *public void initialize()*        
*{*        
[*WakeupCriterion*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCriterion.html) *criteria\[\] = new WakeupCriterion\[2\];*        
*criteria\[0\] = new* [*WakeupOnElapsedFrames(3)*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnElapsedFrames.html#WakeupOnElapsedFrames_int_)*;*        
*criteria\[0\] = new* [*WakeupOnElapsedTime(500)*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnElapsedTime.html#WakeupOnElapsedTime_long_)*;*

[*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) *condition = new* [*WakeupOr*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOr.html)*(criteria);*        
[*wakeupOn(*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#wakeupOn_javax_media_j3d_WakeupCondition_)*condition);*        
*}*

A [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) node provides a [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html) object to the behavior scheduler via its [*wakeupOn()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#wakeupOn_javax_media_j3d_WakeupCondition_) method and the behavior scheduler provides an enumeration of that [*WakeupCondition*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupCondition.html). The [*wakeupOn()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#wakeupOn_javax_media_j3d_WakeupCondition_) method should be called from the [*initialize()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#initialize__) and [*processStimulus()*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus%28java.util.Enumeration%29) methods, just prior of exiting these methods.

In the current Java® 3D implementation the behavior scheduler, and, therefore, the [*processStimulus*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus%28java.util.Enumeration%29) method of the [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) class as well, run concurrently with the rendering thread. However, a new thread will not start until both the renderer, which may be working on the previous frame, and the behavior scheduler are done.

Java® 3D guarantees that all behaviors with a [*WakeupOnElapsedFrames*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/WakeupOnElapsedFrames.html) will be executed before the next frame starts rendering, i.e. the rendering thread will wait until all behaviors are done with their [*processStimulus*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) methods before drawing the next frame. In addition, Java® 3D guarantees that all scene graph updates that occur from within a single [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object will be reflected in the same frame for consistency purposes.

Finally, [*Interpolator*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Interpolator.html) objects can be used for simple behaviors where a parameter can be varied between a starting and an ending value during a certain time interval.

Lights

Lights can be used in order to achieve higher quality and realism of the graphics. Lighting capabilities is provided by the class Light and its subclasses. All light objects have a color, an on/off state, and a bounding volume that controls their illumination range. Java3D provides the following four types of lights, which are subclasses of the class [*Light*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Light.html):

- [*AmbientLight*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/AmbientLight.html): the rays from an ambient light source object come from all directions illuminating shapes evenly
- [*DirectionalLight*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/DirectionalLight.html): a directional light source object has parallel rays of light aiming at a certain direction
- [*PointLight*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/PointLight.html): the rays from an point light source object are emitted radially from a point to all directions
- [*SpotLight*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/SpotLight.html): the rays from a spot light source object are emitted radially from a point to all directions but within a cone

{{\< anchor "6" >}}{{\< /anchor >}}6. Performance of Java® 3D

Java® 3D aims at achieving high performance by utilizing the available graphics libraries (OpenGL/Direct3D), using 3D-graphics acceleration where available, and supporting some rendering optimizations (such as scene reorganization and content culling). It is optimized for performance rather than quality of image rendering. Compilation of branch groups and utilization of capability bits enable speed optimizations. It is as fast and high-level as Open Inventor and VRML (Virtual Reality Modeling Language), while it offers the portability of Java® and the direct access and well integration with all other available Java® APIs. Java® 3D uses native code of certain libraries, such as the OpenGL, at the final steps of rendering to achieve satisfactory performance levels. A scene reorganization and a content culling may be used by the renderer to optimize rendering by following an optimal order that bypasses hidden parts of the scene.

Java® 3D rendering is tuned to the underlying hardware utilizing a wide range of hardware and software platforms. Java® 3D is scalable, taking advantage of multithreading capabilities of Java® when multiple processors are available. The availability of multiple processors is automatically utilized by its independent and asynchronous components, such as the rendering thread and the behavior scheduler, that can be assigned to different processors. Also, branches of the scene tree-structure can be manipulated independently and concurrently utilizing multithreading and multiprocessing.

A thread scheduler was implemented inside the Java® 3D, providing to the Java® 3D architects full control of all threads and eliminating the need to deal with thread priorities. the underlying architecture uses messages to propagate scnegraph changes into certain structures that are used to optimize a particular functionality. There are two structures for geometric objects. The one organizes the geometry spatially enabling spatial queries on the scene graph, such as picking, collisions, culling etc. The other structure is a state snapshot of the scene graph, known as render bin, which is associated with each view and is used by the renderer thread. There is also a structure associated with behaviors that spatially organizes behavior nodes, and a behavior scheduler thread that executes behaviors that need to be executed.

The thread scheduler is essentially in a big infinite loop implemented inside the Java® 3D. For each iteration, the thread scheduler runs each thread that needs to be run once, waiting for all threads to be completed before entering the next iteration. The behavior and the rendering threads may run once in a single iteration. The following operations are conceptually performed within this infinite loop.

*while(true)*        
*{*        
*process input*

*if(there is a request for exit)*        
*break*

*perform any behaviors*

*transverse scene graph and render visible objects*        
*}*

Whenever a node of the scene graph is modified a message is generated with a value associated with it and any state necessary to reflect the specific changes, and queued with all other messages by the thread scheduler. At each iteration the messages are processed and the various structures are updated accordingly. The update time is very fast when the messages are very simple, which is typically the case. In the current implementation the rendering thread and the behavior thread can run concurrently. In particular, the behavior scheduler and therefore the [*processStimulus*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html#processStimulus_java_util_Enumeration_) method of a [*Behavior*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/Behavior.html) object, can run concurrently with the renderer. However, a new frame will not start until both the rendering of the previous frame and the behavior scheduler are done.

Finally it offers level-of-detail ([*LOD*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/LOD.html)) capabilities to further improve performance using a [*LOD*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/LOD.html) object. An LOD leaf node is an abstract class that operates on a list of Switch group nodes to select one of the children of the Switch nodes. The [*LOD*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/LOD.html) class is extended to implement various selection criteria, such as the [*DistanceLOD*](http://java.sun.com/products/java-media/3D/forDevelopers/J3D_1_2_API/j3dapi/javax/media/j3d/DistanceLOD.html) subclass.