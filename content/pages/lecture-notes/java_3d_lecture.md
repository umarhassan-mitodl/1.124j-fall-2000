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

1. {{% resource_link "1fdb45c1-b7dc-44c9-b51a-332ea678b6bf" "Introduction to Java® 3D" %}}
2. {{% resource_link "1368f056-1a53-468c-9975-9247c1101f86" "Java® 3D References" %}}
3. {{% resource_link "f2b179de-5a76-4557-904d-b97b672015d2" "Examples and Applications" %}}
4. {{% resource_link "d4a06f5e-d710-4085-a738-78f7ed9e553b" "Scene Graph Structure and basic Java® 3D concepts and classes" %}}
5. {{% resource_link "68697870-dacf-48c6-9c17-92b2916134c3" "A simple Java® 3D program" %}}
6. {{% resource_link "7ea60274-3072-4f43-837a-37a74a52d273" "Performance of Java® 3D" %}}

{{\< anchor "1" >}}{{\< /anchor >}}1. Introduction to Java® 3D

*Java® 3D* is a general-purpose, platform-independent, object-oriented API for 3D-graphics that enables high-level development of Java® applications and applets with 3D interactive rendering capabilities. With *Java® 3D*, 3D scenes can be built programmatically, or, alternatively, 3D content can be loaded from VRML or other external files. *Java® 3D*, as a part of the *Java® Media APIs*, integrates well with the other {{% resource_link "5d1993f4-5720-44f6-bb87-a06e6eebe258" "Java® technologies and APIs" %}}. For example, {{% resource_link "d3d45e8d-c76e-4e43-b920-08121f760b37" "*Java® 2D*" %}} API can be used to plot selected results, while the {{% resource_link "dde52564-681e-4849-b0e7-c0f28a7cc3d2" "*Java® Media Framework (JMF)*" %}} API can be used to capture and stream audio and video.

Java® 3D is based on a directed acyclic graph-based scene structure, known as scene graph, that is used for representing and rendering the scene. The scene structure is a tree-like diagram that contains nodes with all the necessary information to create and render the scene. In particular, the {{% resource_link "d4a06f5e-d710-4085-a738-78f7ed9e553b" "scene graph" %}} contains the nodes that are used to represent and transform all objects in the scene, and all viewing control parameters, i.e. all objects with information related to the viewing of the scene. The scene graph can be manipulated very easily and quickly allowing efficient rendering by following a certain optimal order and bypassing hidden parts of objects in the scene.

Java® 3D API has been developed under a joint collaboration between Intel, Silicon Graphics, Apple, and Sun, combining the related knowledge of these companies. It has been designed to be a platform-independent API concerning the host's operating system (PC/Solaris/Irix/HPUX/Linux) and graphics (OpenGL/Direct3D) platform, as well as the input and output (display) devices. The implementation of Java® 3D is built on top of OpenGL, or Direct3D. The high level Java® 3D API allows rapid application development which is very critical, especially nowadays.

However, Java® 3D has some weaknesses such as the performance, which is inferior to that of OpenGL, and the limited access to the rendering pipeline details. It is also still under development and several bugs need to be fixed. Although Java® 3D cannot achieve peak performance, portability and rapid development advantages may overweigh the slight performance penalty for many applications.

The current version of the Java® 3D API is the Version 1.2, which works together with the {{% resource_link "17f29cdf-7a5e-4a44-94b2-c8b9de529bd0" "Java® 2 Platform" %}}. Both APIs can be downloaded for free from the {{% resource_link "5d1993f4-5720-44f6-bb87-a06e6eebe258" "Java® products page of Sun" %}}.

 

{{\< anchor "2" >}}{{\< /anchor >}}2. Java® 3D References

The following list includes many links related to the Java® 3D API

- {{% resource_link "6d65d7c8-ee1f-45a9-a55d-ed665469cb30" "*Java® 3D 1.2 API Documentation*" %}}  
- {{% resource_link "48ee7a5d-fbc8-4b1c-9d34-ecbbf2f41755" "*Java® 3D 1.2 Specification*" %}}  
- Java® 3D Tutorial (PDF format):       
      
    - {{% resource_link "42a1af77-8935-4647-a720-4c6f73db102e" "*Chapter 0*" %}} , Preface, Appendices, and Glossary
    - {{% resource_link "4c7891c5-063b-4687-9246-bfef845413d2" "*Chapter 1*" %}} , Getting Started
    - {{% resource_link "b6599323-9512-41b6-b994-a448c9b78c6d" "*Chapter 2*" %}} , Creating Content
    - {{% resource_link "b4c8d3a4-a982-4849-a71c-9a09ddb837b6" "*Chapter 3*" %}} , Easier Content Creation
    - {{% resource_link "63a7a464-02e4-4d26-86db-ed9f4294e2d0" "*Chapter 4*" %}} , Interaction
    - {{% resource_link "5e4dc85e-e49e-4a81-8952-63120e8ce5a9" "*Chapter 5*" %}} , Animation
    - {{% resource_link "197b30e6-7e93-4644-b6cb-1094f8e21908" "*Chapter 6*" %}} *,* Lights
    - {{% resource_link "e5d76911-f4ba-4fc6-8ddc-ee4581130b95" "*Chapter 7*" %}} , Textures        
         
- {{% resource_link "55a5d056-f9ce-4584-ace0-0e807253b4ec" "*Raw J3D*" %}}
- {{% resource_link "ce05983c-21e6-461c-85a9-66e5d8354e6d" "*Java® 3D: For Developers and End-User*" %}}
- *A Fourth generation Java® 3D graphics API*
- *Java® 3D FAQ at Sun*
- {{% resource_link "ff8f4f8a-c95d-4daa-bce0-bc3e2dd68779" "*Java® 3D Community FAQ*" %}}
- *Extensive Java® 3D FAQ at Sun*
- *Java® 3D Group at NCSA*
- {{% resource_link "b478e17c-25db-4e48-85ac-953b59417597" "*Java® 3D Community site*" %}}
- *The Java® 3D and VRML Working group*
- *VRML and Java® 3D Information Center*
- *Web 3D consortium*
- {{% resource_link "3b0dadcf-99d4-418f-9b67-8396dc7d9d41" "*Java® 3D Loader Archive*" %}}

Java® 3D is specified in the packages: {{% resource_link "8d48c77e-ca19-48db-ac0e-9ae933907e74" "*javax.media.j3d*" %}} and {{% resource_link "17e47468-a9ef-4406-8184-a027ab60f4d7" "*javax.vecmath*" %}}. Supporting classes and utilities are provided in the *com.sun.j3d* packages.

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
- {{% resource_link "5594491c-f583-4157-a2c9-059e02187ab2" "*Collaborative Visualization Space Science and Engineering Center (SSEC)*" %}}
- {{% resource_link "9effa2d3-8c52-45d0-a139-4d7fbeddeb37" "*Java® 3D API Customer Success Stories*" %}}

{{\< anchor "4" >}}{{\< /anchor >}}4. Scene Graph Structure and Basic Java® 3D Concepts and Classes

*Scene graph: Content-View Branches*

A Java® 3D scene is created as a tree-like graph structure, which is traversed during rendering. The scene graph structure contains nodes that represent either the actual objects of the scene, or, specifications that describe how to view the objects. Usually, there are two  branches in Java® 3D, the **content branch**, which contains the nodes that describe the actual objects in the scene, and  the **view branch**, which contains nodes that specify viewing related conditions. Usually, the content branch contains much larger number of nodes than the view branch.

The following image shows a basic Java® 3D graph scene, where the content branch is located on the left and the view branch on the right side of the graph:

{{< resource uuid="cb6b58f7-abe0-910f-9d4c-1a4e758995c5" >}}

Java® 3D applications construct individual graphic components as separate objects, called nodes, and connects them together into a tree-like scene graph, in which the objects and the viewing of them can easily be manipulated. The scene graph structure contains the description of the virtual universe, which represents the entire scene. All information concerning geometric objects, their attributes, position and orientation, as well as the viewing information are all contained into the scene graph.

The above scene graph consists of superstructure components, in particular a {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}} and a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} object, and a two {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} objects, which are attached to the superstructure. The one branch graph, rooted at the left {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} node, is a content branch, containing all the relevant to the contents of the scene objects. The other branch, known as view branch, contains all the information related to the viewing and the rendering details of the scene.

The state of a shape node, or any other leaf node, is defined, during rendering, by the nodes that lie in the direct path between that node and the root node, i.e. the {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}}. For example, a {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node in a path between a leaf node and the scene's root can change the position, orientation, and scale of the object represented by the leaf node.

{{% resource_link "c1450e15-ad79-4555-8715-a422cb4c7916" "*SceneGraphObject*" %}} Hierarchy

The Java® 3D node objects of a Java® 3D scene graph, which are instances of the {{% resource_link "b1cf9a12-dd53-4bd2-ac2b-9ff2006cbd3f" "*Node*" %}} class, may reference node component objects, which are instances of the class NodeComponent. The {{% resource_link "b1cf9a12-dd53-4bd2-ac2b-9ff2006cbd3f" "*Node*" %}} and {{% resource_link "a306bb25-9ba4-490a-aca3-1e75c471676d" "*NodeComponent*" %}} classes are subclasses of the {{% resource_link "6d22810e-72b4-4602-8c37-f14c14b7aacf" "*SceneGraphObject*" %}} abstract class. Almost all objects that may be included in a scene graph are instances of subclasses of the {{% resource_link "6d22810e-72b4-4602-8c37-f14c14b7aacf" "*SceneGraphObject*" %}} class. A scene graph object is constructed by instantiating the corresponding class, and then, it can be accessed and manipulated using the provided set and get methods.

The following graph shows the class hierarchy of the major subclasses of the {{% resource_link "6d22810e-72b4-4602-8c37-f14c14b7aacf" "*SceneGraphObject*" %}} class:

{{< resource uuid="d718435c-535c-ef73-9917-b89c8413f90f" >}}

*Class* {{% resource_link "b1cf9a12-dd53-4bd2-ac2b-9ff2006cbd3f" "*Node*" %}} *and its subclasses*

The abstract Class {{% resource_link "b1cf9a12-dd53-4bd2-ac2b-9ff2006cbd3f" "*Node*" %}} is the base class for almost all objects that constitute the scene graph. It has two subclasses the {{% resource_link "2b073c70-7626-4286-b542-37a3a22c291f" "*Group*," %}} and {{% resource_link "b67c71a8-0c21-44c5-b4c4-a3d4b71efdb5" "*Leaf*" %}} classes, which have many useful subclasses. Class {{% resource_link "6c1ee2d0-d705-4fa8-be9c-f112f47e2a90" "*Group*" %}} is a superclass of, among others, the classes {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} and {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*." %}} Class {{% resource_link "b67c71a8-0c21-44c5-b4c4-a3d4b71efdb5" "*Leaf*" %}}, which is used for nodes with no children, is a superclass of, among others, the classes {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}}, {{% resource_link "a0d20e1a-8d92-4f1c-a46a-e6f71cf762a7" "*Light*" %}}, {{% resource_link "c21acf18-2ffe-43d9-a5f7-d691e7270423" "*Shape3D*" %}}, and {{% resource_link "cd45e890-40d9-4bf7-bc5e-62f2c146c510" "*ViewPlatform*" %}}. The {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node is used to define from where the scene is viewed. In particular, it can be used to specify the location and the orientation of the point of view.

*Class* {{% resource_link "a306bb25-9ba4-490a-aca3-1e75c471676d" "*NodeComponent*" %}} *and its subclasses*

Class {{% resource_link "a306bb25-9ba4-490a-aca3-1e75c471676d" "*NodeComponent*" %}} is the base class for classes that represent attributes associated with the nodes of the scene graph. It is the superclass of all scene graph node component classes, such as the {{% resource_link "cd13f080-9ce3-4d28-b1a4-7267040c2d37" "*Appearance*" %}}, {{% resource_link "514f459c-5743-40ef-9690-d26cbeed73ec" "*Geometry*" %}}, {{% resource_link "bcbb1f04-046e-49e8-9362-9c468a66863e" "*PointAttributes*" %}}, and {{% resource_link "d162c482-100d-4c7a-a9aa-a7aa5db54be9" "*PolygonAttributes*" %}} classes. {{% resource_link "a306bb25-9ba4-490a-aca3-1e75c471676d" "*NodeComponent*" %}} objects are used to specify attributes for a node, such as the color and geometry of a shape node, i.e. a {{% resource_link "c21acf18-2ffe-43d9-a5f7-d691e7270423" "*Shape3D*" %}} node. In particular, a {{% resource_link "c21acf18-2ffe-43d9-a5f7-d691e7270423" "*Shape3D*" %}} node uses an {{% resource_link "cd13f080-9ce3-4d28-b1a4-7267040c2d37" "*Appearance*" %}} and a {{% resource_link "514f459c-5743-40ef-9690-d26cbeed73ec" "*Geometry*" %}} objects, where the {{% resource_link "cd13f080-9ce3-4d28-b1a4-7267040c2d37" "*Appearance*" %}} object is used to control how the associated geometry should be rendered by Java® 3D.

The geometry component information of a {{% resource_link "c21acf18-2ffe-43d9-a5f7-d691e7270423" "*Shape3D*" %}} node, i.e. its geometry and topology, can be specified in an instance of a subclass of the abstract {{% resource_link "514f459c-5743-40ef-9690-d26cbeed73ec" "*Geometry*" %}} class. A Geometry object is used as a component object of a {{% resource_link "c21acf18-2ffe-43d9-a5f7-d691e7270423" "*Shape3D*" %}} leaf node. Geometry objects consist of the following four generic geometric types. Each of these geometric types defines a visible object, or a set of objects.

- {{% resource_link "81aae594-634b-4b27-99d2-c9048b6fbbd7" "*CompressedGeometry*" %}}
- {{% resource_link "eea80d91-aa81-488d-9427-aed6e1ffa090" "*GeometryArray*" %}}
- {{% resource_link "414426cd-9555-431f-9d96-a3502cbaa7c9" "*Raster*" %}}
- {{% resource_link "e6f4a63d-8453-4d44-93f6-7c22ab7edc40" "*Text3D*" %}}

For example, the {{% resource_link "eea80d91-aa81-488d-9427-aed6e1ffa090" "*GeometryArray*" %}} is a subclass of the class {{% resource_link "514f459c-5743-40ef-9690-d26cbeed73ec" "*Geometry*" %}}, which itself extends the {{% resource_link "a306bb25-9ba4-490a-aca3-1e75c471676d" "*NodeComponent*" %}} class, that is extended to create the various primitive types such as lines, triangle strips and quadrilaterals.

{{< resource uuid="d404ba55-8789-1a59-f627-8f8ae65b49b3" >}}

The {{% resource_link "b08e8e5f-6a81-4b57-b1ab-dc53586be400" "*IndexedGeometryArray*" %}} object above contains separate integer arrays that index, among others, into arrays of positional coordinates specifying how vertices are connected to form geometry primitives. This class is extended to create the various indexed primitive types, such as {{% resource_link "7d9d3ccc-cba3-42ed-988d-06766803e738" "*IndexedLineArray*" %}}, {{% resource_link "f03cf827-8a35-4bf9-a039-01a56f345159" "*IndexedPointArray*" %}}, and {{% resource_link "9bbb7dbc-9117-417d-a276-acc474bf108f" "*IndexedQuadArray*" %}}.

Vertex data may be passed to the geometry array either by copying the data into the array using the existing methods, which is the default mode, or by passing a reference to the data.

The methods for setting positional coordinates, colors, normals, and texture coordinates, such as the method {{% resource_link "a9c8a782-f0b0-4d70-b690-930a5601de03" "*setCoordinates*()" %}}, copy the data into the {{% resource_link "eea80d91-aa81-488d-9427-aed6e1ffa090" "*GeometryArray*" %}}, which offers much flexibility in organizing the data.

Another set of methods allows data to be passed and accessed by reference, such as the {{% resource_link "d138c895-d4ec-4543-a0e5-3b7047a0c2d0" "*setCoordRef3d*()" %}} method, set a reference to user-supplied data, e.g. coordinate arrays. In order to enable the passing of data by reference, the {{% resource_link "25177563-4ff5-462f-b58d-53ead1f00085" "*BY*\_\_REFERENCE\_" %}} bit in the {{% resource_link "19b60ba3-3077-41c6-9e5f-71214118f5be" "*vertexFormat*" %}} field of the constructor for the corresponding {{% resource_link "eea80d91-aa81-488d-9427-aed6e1ffa090" "*GeometryArray*" %}} must be set accordingly. Data in any array that is referenced by a live or compiled {{% resource_link "eea80d91-aa81-488d-9427-aed6e1ffa090" "*GeometryArray*" %}} object may only be modified using the {{% resource_link "2e5ad484-c7a7-4871-ac1d-e57c9627bc66" "*updateData*" %}} method assuming that the {{% resource_link "6f232577-4921-4f11-9c41-edb1e012efc3" "*ALLOW\_REF\_DATA\_WRITE*" %}} capability bit is set accordingly, which can be done using the {{% resource_link "eabd8d8b-21f7-49e0-8a4b-021c34835219" "*setCapability*" %}} method.

The {{% resource_link "cd13f080-9ce3-4d28-b1a4-7267040c2d37" "*Appearance*" %}} object defines all rendering state that control the way the associated geometry should be rendered. The rendering state consists of the following:

- Point attributes: a {{% resource_link "bcbb1f04-046e-49e8-9362-9c468a66863e" "*PointAttributes*" %}} object defines attributes used to define points, such as the size to be used
- Line attributes: using a {{% resource_link "d24b26ac-168a-4d16-bf52-a90bb5f34a5c" "*LineAttributes*" %}} object attributes used to define lines, such as the width and pattern, can be defined
- Polygon attributes: using a {{% resource_link "d162c482-100d-4c7a-a9aa-a7aa5db54be9" "*PolygonAttributes*" %}} object the attributes used to define polygons, such as rasterization mode (i.e.. filled, lines, or points) are defined
- Coloring attributes: a {{% resource_link "4de39697-d60f-45ed-b7a3-0d3e3ce6dc50" "*ColoringAttributes*" %}} object is used to defines attributes used in color selection and shading.
- Rendering attributes: defines rendering operations, such as whether invisible objects are rendered, using a {{% resource_link "438f9427-659e-423c-bc19-ba07d876d0c4" "*RenderingAttributes*" %}} object.
- Transparency attributes: a {{% resource_link "975dea8d-8f74-45e8-88cf-8ceaa0c95038" "*TransparencyAttributes*" %}} defines the attributes that affect transparency of the object
- Material: a {{% resource_link "85e0bf68-feec-4148-b134-0985de878198" "*Material*" %}} object defines the appearance of an object under illumination, such as the ambient color, specular color, diffuse color, emissive color, and shininess. It is used to control the color of the shape.
- Texture: the texture image and filtering parameters used, when texture mapping is enabled, can be defined in a {{% resource_link "520b9584-888e-4ab0-99d5-07857e8c7103" "*Texture*" %}} object.
- Texture attributes: a {{% resource_link "3420fb00-98df-40f3-8ef5-96717730ed8e" "*TextureAttributes*" %}} object can be used to define the attributes that apply to texture mapping, such as the texture mode, texture transform, blend color, and perspective correction mode.
- Texture coordinate generation: the attributes that apply to texture coordinate generation can be defined in a {{% resource_link "c1d7d36d-9673-44ba-b41a-40f18f304721" "*TexCoordGeneration*" %}} object.
- Texture unit state: array that defines texture state for each of N separate texture units allowing multiple textures to be applied to geometry. Each {{% resource_link "3426b10a-cc1d-4846-ba8d-3eb34910f532" "*TextureUnitState*" %}} object contains a Texture object, TextureAttributes, and TexCoordGeneration object for one texture unit.

{{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "***VirtualUniverse***" %}}

and {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}}

After constructing a subgraph, it can be attached to a {{% resource_link "3d1fcd42-046c-4790-9729-0d7c97895ba7" "*VirtualUniverse*" %}} object through a high-resolution {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} object, which is itself attached to the virtual universe. The {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}} is the root of all Java® 3D scenes, while {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} objects are used for basic spatial placement. The attachment to a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} object makes all objects in the attached subgraph live (i.e. drawable), while removing it from the locale reverses the effect. Any node added to a live scene graph becomes live. However, in order to be able to modify a live node the corresponding {{% resource_link "eabd8d8b-21f7-49e0-8a4b-021c34835219" "*capability* bits" %}} should be set accordingly.

Typically, a Java® 3D program has only one {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}} which consists of one, or more, {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} objects that may contain collections of subgraphs of the scene graph that are rooted by {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} nodes, i.e. a large number of  branch graphs. Although a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} has no explicit children, it may reference an arbitrary number of {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} nodes. The subgraphs contain all the scene graph nodes that exist in the universe. A {{% resource_link "83d91078-5ba2-49fa-a3ad-5c64c315b906" "*Locale*" %}} node is used to accurately position a branch graph in a universe specifying a location within the virtual universe using high-resolution coordinates ({{% resource_link "80e345d1-7b0c-49f7-b9d5-596d7ec76075" "*HiResCoord*" %}}), which represent 768 bits of floating point values. A {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} is positioned in a single {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}} node using one of its constructors.

The {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}} and {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} classes, as well as the {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} class, are subclasses of the basic superclass {{% resource_link "90b2b0d1-3749-4c57-a880-cbe030d09af0" "***Object***" %}}, as shown below:

{{< resource uuid="e45316c9-a420-f0b0-66d3-544026497bcd" >}}

 

Branch Graphs

A branch graph is a scene graph rooted in a {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} node and can be used to point to the root of a scene graph branch. A graph branch can be added to the list of branch graphs of a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} node using its {{% resource_link "d4f9f623-3d0b-4be2-aa60-3c581a680e0a" "*addBranchGraph*(*BranchGroup* bg)" %}} method. {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} objects are the only objects that can be inserted into a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}}*'s* list of objects.

A {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} may be compiled by calling its compile method, which causes the entire subgraph to be compiled including any {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} nodes that may be contained within the subgraph. A graph branch, rooted by a  {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} *node,* becomes live when inserted into a virtual universe by attaching it to a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}}. However, if a {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} is contained in another subgraph as a child of some other group node, it may not be attached to a {{% resource_link "0e423f53-3c86-42de-b9b4-ed3f380b635a" "*Locale*" %}} node.

Capability Bits, Making Live and Compiling

Certain optimizations can be done to achieve better performance by compiling a subgraph into an optimized internal format, prior to its attachment to a virtual universe. However, many *set* and *get* methods of objects that are part of a live or compiled scene graph cannot be accessed. In general, the *set* and *get* methods can be used only during the creation of a scene graph, except where explicitly allowed, in order to allow certain optimizations during rendering. The set and get methods that can be used when the object is live or compiled should be specified using a set of capability bits, which by default are disabled, prior to compiling or making live the object. The methods {{% resource_link "6b872630-bf8b-47a1-aa3e-a5ab490232ec" "*isCompiled()*" %}} and {{% resource_link "f5cc1935-96e8-43e6-a7e9-e052b9997745" "*isLive()*" %}} can be used to find out whether a scene graph object is compiled or live. The methods {{% resource_link "eabd8d8b-21f7-49e0-8a4b-021c34835219" "*setCapability*()" %}} and {{% resource_link "2a24779d-d967-46f3-b4aa-d7ea777daa93" "*getCapability*()" %}} can be used to set properly the capability bits to allow access to the object's methods. However, the less the capability bits that are enabled, the more optimizations can be performed during rendering.

Viewing Branch: {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}}*,*  {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}}*,* {{% resource_link "10bc50a1-b4d7-4750-b881-e9383263b325" "*Screen3D*" %}}

The view branch has usually the following structure, consisting of nodes that control the viewing of the scene.

{{< resource uuid="be7231df-1539-a99c-6e1a-611c255912f1" >}}

The view branch contains some scene graph viewing objects that can be used to define the viewing parameters and details, such as the {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}}, {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}}, {{% resource_link "10bc50a1-b4d7-4750-b881-e9383263b325" "*Screen3D*" %}}, {{% resource_link "1f0c58b4-f6b9-4e80-8398-928c7e830407" "*PhysicalBody*" %}}, and {{% resource_link "0480a80e-eb18-45ba-99f0-58788faeb602" "*PhysicalEnvironment*" %}} classes.

Java® 3D uses a viewing model that can be used to transform the position and direction of the viewing while the content branch remains unmodified. This is achieved with the use of the {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} and the {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} classes, to specify from where and how, respectively, the scene is being viewed.

The {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node controls the position, orientation and scale of the viewer. A viewer can navigate through the virtual universe by changing the transformation in the scene graph hierarchy above the {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node. The location of the viewer can be set using a {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node above the {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node. The {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node has an activation radius that is used together with the bounding volumes of {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}}, {{% resource_link "36936584-4457-4464-b177-4b05d2c3540b" "*Background*" %}} and other nodes in order to determine whether the latter nodes should be scheduled, or turned on, respectively. The method {{% resource_link "0e813421-467a-462c-afea-27126d81f5fe" "*setActivationRadius*()" %}} can be used to set the activation radius.

A {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} object connects to the {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node in the scene graph, and specifies all viewing parameters of the rendering process of a 3D scene. Although it exists outside of the scene graph, it attaches to a {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} leaf node in the scene graph, using the method {{% resource_link "5ce74645-e400-4ef5-a103-656b60cea4b8" "*attachViewPlatform*(*ViewPlatform* vp)" %}}. A {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} object contains references to a {{% resource_link "1f0c58b4-f6b9-4e80-8398-928c7e830407" "*PhysicalBody*" %}} and a {{% resource_link "0480a80e-eb18-45ba-99f0-58788faeb602" "*PhysicalEnvironment*" %}} object, which can be set using the methods {{% resource_link "afbfe09e-43c9-4536-b49b-916760b0906d" "*setPhysicalBody*()" %}} and {{% resource_link "641f3a59-aefd-40ef-badf-045398de9c89" "*setPhysicalEnvironment*()" %}}*, respectively*.

A {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} object contains a list of {{% resource_link "24354722-eb5e-4c01-b868-8919c0d5d8a2" "*Canvas3D*" %}} objects where rendering of the view is done. The method {{% resource_link "b2da139f-51a6-4057-8222-404dae042d47" "*addCanvas3D*(Canvas3D c)" %}} of the class {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "*View*" %}} can be used to add the provided {{% resource_link "24354722-eb5e-4c01-b868-8919c0d5d8a2" "*Canvas3D*" %}} object to the list of canvases of the {{% resource_link "79f74c13-5566-468a-804a-115313a12b8e" "View" %}} object.

{{< resource uuid="962db16a-d746-33a5-7a2a-a1311a65fb65" >}}

Class {{% resource_link "b8cac54c-70ff-4912-9bae-b7198eee25aa" "*Canvas3D*" %}} extends the heavyweight class {{% resource_link "fac7aed5-5a45-4cf6-8506-9575f3b5003c" "*Canvas*" %}} in order to achieve hardware acceleration, since a low rendering library, such as OpenGL, requires the rendering to be done in a native window to enable hardware acceleration.

Finally, all {{% resource_link "b8cac54c-70ff-4912-9bae-b7198eee25aa" "*Canvas3D*" %}} objects on the same physical display device refer to a {{% resource_link "10bc50a1-b4d7-4750-b881-e9383263b325" "*Screen3D*" %}} object, which contains all information about that particular display device. {{% resource_link "10bc50a1-b4d7-4750-b881-e9383263b325" "*Screen3D*" %}} can be obtained from the {{% resource_link "b8cac54c-70ff-4912-9bae-b7198eee25aa" "*Canvas3D*" %}} using the {{% resource_link "27874840-8dc9-47d7-ad1d-582da7356e1b" "*getScreen3D*()" %}} method.

Default Coordinate System

The default coordinate system is a right-handed Cartesian coordinate system centered on the screen with the x and y-axes directed towards the right and top of the screen, respectively. The z-axis is, by default directed out of the screen towards the viewer, as shown below. The default distances are in meter and the angles in radians.        
 

{{< resource uuid="b4b7e83d-b897-f4fe-b33f-16f275d7751d" >}}

Transformations

Class {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} which extends the class {{% resource_link "2b073c70-7626-4286-b542-37a3a22c291f" "*Group*" %}} can be used to set a spatial transformation, such as positioning, orientation, and scaling of its children through the use of a {{% resource_link "143e93eb-d9a9-40b4-a6a2-474f2ac5b50f" "*Transform3D*" %}} object. A {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node enables the setting and use of a coordinate system relative to its parent coordinate system.

The {{% resource_link "143e93eb-d9a9-40b4-a6a2-474f2ac5b50f" "*Transform3D*" %}} object of a {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} object can be set using the method {{% resource_link "2e8c8ef0-b0fe-497e-b799-4b8ee2f7b6e8" "*setTransform*(Transform3D  t)" %}}, which is used to set the transformation components of the {{% resource_link "143e93eb-d9a9-40b4-a6a2-474f2ac5b50f" "*Transform3D*" %}} object to the ones of the passed parameter.

A {{% resource_link "143e93eb-d9a9-40b4-a6a2-474f2ac5b50f" "*Transform3D*" %}} object is a 4x4 double-precision matrix that is used to determine the transformations of a {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node, as shown in the following equation. The elements T{{\< sub "00" >}}, T{{\< sub "01" >}}, T{{\< sub "02" >}}, T{{\< sub "10" >}}, T{{\< sub "11" >}}, T{{\< sub "12" >}},T{{\< sub "20" >}}, T{{\< sub "21" >}}, and T{{\< sub "22" >}} are used to set the rotation and scaling, and the T{{\< sub "03" >}}, T{{\< sub "13" >}}, and T{{\< sub "23" >}} are used to set the translation.

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

Since the {{% resource_link "b8cac54c-70ff-4912-9bae-b7198eee25aa" "*Canvas3D*" %}} extends the heavyweight AWT class *Canvas*, it should be handled with care if Swing is used. The information provided when {{% resource_link "352d18bc-bfd5-4495-88cd-c608bd3bab52" "*mixing AWT and Swing*" %}} components should be followed. The main problem is that there is one-to-one correspondence between heavyweight components and their window system peers, i.e. native OS window components. In contrast, a lightweight component expects to use the peer of its enclosing container since it does not have a peer.

When lightweight components overlap with heavyweight components, the heavyweight components are always painted on top. In general, the heavyweight {{% resource_link "b8cac54c-70ff-4912-9bae-b7198eee25aa" "*Canvas3D*" %}} of Java® 3D should be kept apart from lightweight Swing components using different containers to avoid problems.

To avoid heavyweight components overlapping *Swing* popup menus, which are lightweight, the popup menus  can be forced to be heavyweight using the method *setLightWeightPopupEnabled()* of the *JPopupMenu* class.

Similarly, problems with tooltips can be avoided by invoking the following method

*ToolTipManager.sharedInstance().setLightWeightPopupEnabled(false)*

Behaviors

Behaviors are essentially Java® methods that are scheduled to run only when certain requirements are satisfied according to wakeup conditions. Although a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object is connected to the scene it is kept in a separate area of the Java® 3D runtime environment and it is not considered part of the scene graph. The runtime environment treats a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object differently ensuring that certain actions take place. All behaviors in Java® 3D extend the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class, which is an abstract class that itself extends the {{% resource_link "b67c71a8-0c21-44c5-b4c4-a3d4b71efdb5" "*Leaf*" %}} class. The {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class provides a way to execute certain statements, provided in the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method, in order to modify the scene graph when specified criteria are satisfied.

The {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class has two major methods, in particular the {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method, which is called when the behavior becomes live, and the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method, which is called by the Java® 3D scheduler whenever appropriate,  and  a scheduling region. Typically, in order to create a custom behavior, the class {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} is extended and referenced by the scene graph from an appropriate place that should be able to effect. A custom behavior that extends the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class should implement the {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} and {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} methods, and provide other methods and constructors that may be needed. The {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class object contains the state information that is needed by its {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}}and the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} methods. A constructor or another method may be used to set references to the scene graph objects upon which the behavior acts. In addition, the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class is extended by the following three classes {{% resource_link "79b6c8a7-faf6-4e65-884f-c3f243c54057" "*Billboard*" %}}, {{% resource_link "009c098f-f9f5-45be-96ba-ea3dd31b5c2c" "*Interpolator*" %}}, and {{% resource_link "e1e49924-5938-4c97-9e59-b2ad6b61813a" "*LOD*" %}}.

The {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method is called once when the behavior becomes "live", i.e. when its {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} node is added to a {{% resource_link "61d5dc59-b956-4ff2-8e39-49ab93b2b207" "*VirtualUniverse*" %}}, to initialize this behavior. The Java® 3D behavior scheduler calls the {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method, which should never be called directly. The {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method is used to set a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object, which has been "added" to the scene graph, into a "known" condition and register the criteria to be used to decide on its execution. Classes that extend Behavior must provide their own {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method. The {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method allows a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object to initialize its internal state and specify its initial wakeup conditions. Java® 3D automatically invokes a behavior's initialize code when a {{% resource_link "83a59cec-1964-445d-9433-1ae0d46bf6f2" "*BranchGroup*" %}} node that contains the behavior is added to the virtual universe, i.e. becomes live. The {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method should return, since Java® 3D does not invoke the initialize method in a new thread, and therefore it must regain control. Finally, a wakeup condition must be set in order to be able to invoke the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method of the behavior.

However, a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object is considered active only when its scheduling bounds intersect the activation volume of a {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node. Therefore, the scheduling bounds should be provided for a behavior in order to be able to receive stimuli. The scheduling bounds of a behavior can be specified as a bounded spatial volume, such as a sphere, using the method {{% resource_link "4aa1acd1-cb26-4e34-ad46-958941586349" "*setSchedulingBounds(Bounds region)*" %}}. Bounds are used for selective scheduling to improve performance. Bounds are used to decide whether a behavior should be added to the list of scheduled behaviors.

The {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method is called whenever the wakeup criteria are satisfied and the ViewPlatform's activation region intersect with the Behavior's scheduling region. The method is called by the Java® 3D behavior scheduler when something happens that causes the behavior to execute. A stimulus, i.e. a notification, informs the behavior that it should execute its {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method. Therefore, applications should not call explicitly this method. Classes that extend the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class must provide their own  {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method. The scheduling region defines a spatial volume that serves to enable the scheduling of {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} nodes. A {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} node is active, i.e. it can receive stimuli, whenever its scheduling region intersects the activation volume of a {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}}.

The Java® 3D behavior scheduler invokes the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method of a Behavior node when its scheduling region intersects the  activation volume of a {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node and all wakeup criteria  of that behavior are satisfied. Then, the statements in the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method may perform any computations and actions, such as including the registration of state change information that could cause Java® 3D to wake other Behavior objects and modify node values within the scene graph, change the internal state of the behavior, specify its next wakeup conditions, and exit. It is allowed to a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object to change its next trigger event. The {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method, typically, manipulates scene graph elements, as long as the associated capabilities bits are set accordingly. For example, a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} node can be used to repeatedly modify a {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node in order to animate the associated with the {{% resource_link "decb0ada-866b-4bd9-918e-6706d4d5cead" "*TransformGroup*" %}} node objects.

The amount of work done in a {{% resource_link "11ac7a8e-0295-44f4-86da-afad8fb171aa" "*processStimulus()*" %}} method should be limited since the method may lower the frame rate of the renderer. Java® 3D assumes that {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} methods run to completion and if necessary they spawn threads.

The application must provide the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object with references to those scene graph elements that the Behavior object will manipulate. This is achieved by providing those references as arguments to the constructor of the behavior when the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object is created. Alternatively, the Behavior object itself can obtain access to the relevant scene graph elements either when Java® 3D invokes its {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} method or each time Java® 3D invokes its {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus()*" %}} method. Typically, the application provides references to the scene graph objects that a behavior should be able to access as arguments to its constructor when the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} is instantiated.

Java® 3D assumes that {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} methods always run to completion and that if needed they can spawn threads. The structure of each {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} method consists of the following parts:

- code to decode and extract references from the {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} enumeration that awoke the object
- code to perform the manipulations associated with the {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}}
- code to establish new {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} for this behavior
- a path to exit, so that execution returns to the Java® 3D behavior scheduler

The {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} class is an abstract class that specifies a single wakeup condition. It is specialized to 14 different {{% resource_link "78b6b5cb-b789-4f17-9638-d08deeaf9a84" "*WakeupCriterion*" %}} subclasses and to 4 subclasses that can be used to create complex wakeup conditions using boolean logic combinations of individual  {{% resource_link "78b6b5cb-b789-4f17-9638-d08deeaf9a84" "*WakeupCriterion*" %}} objects. A Behavior node provides a {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} object to the Java® 3D behavior scheduler using its {{% resource_link "09cccdb8-32ac-49fc-a9ba-a0bcc16dc19a" "*wakeupOn()*" %}} method. When that {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} is satisfied, while the scheduling region intersects the activation volume of a {{% resource_link "fa669302-3cd1-4db5-98b8-831701e7ab08" "*ViewPlatform*" %}} node, the behavior scheduler passes that same {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} back to the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} via an enumeration.

Java® 3D provides the following wakeup criteria that {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} objects can use to specify a complex {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}}. All of the following are subclasses of the {{% resource_link "78b6b5cb-b789-4f17-9638-d08deeaf9a84" "*WakeupCriterion*" %}} class, which itself is a subclass of the {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} class.

- {{% resource_link "61d2ce83-5d60-4bcf-9692-9a22ff207205" "*WakeupOnViewPlatformEntry:*" %}} when the center of a ViewPlatform enters a specified region
- {{% resource_link "ec06402f-6c40-45e4-aeda-4dc6f5eb0747" "*WakeupOnViewPlatformExit:*" %}} when the center of a ViewPlatform exits a specified region
- {{% resource_link "693cc8e4-5670-47ec-9a89-bb5410fce294" "*WakeupOnActivation*" %}}: when a behavior is activated
- {{% resource_link "0b958390-829a-4d3a-bd29-f8815adc30a0" "*WakeupOnDeactivation*" %}}: when a behavior is deactivated
- {{% resource_link "9a47df90-01a5-40bd-a579-ccd9f334c60d" "*WakeupOnTransformChange*:" %}} when a specified TransformGroup node's transform changes
- {{% resource_link "41bcb42d-6bb6-4ec7-9293-d7ea7412a049" "*WakeupOnCollisionEntry*" %}}: when collision is detected between a specified Shape3D node's Geometry object and any other object
- {{% resource_link "e7c39d7f-92f0-4de8-8c22-381c94de1f2b" "*WakeupOnCollisionMovement*" %}}: when movement occurs between a specified Shape3D node's Geometry object and any other object with which it collides
- {{% resource_link "d9b13dcc-1e17-4fbb-9af1-113a3071cb36" "*WakeupOnCollisionExit*" %}}: when a specified Shape3D node's Geometry object no longer collides with any other object
- {{% resource_link "3367b20f-4cb3-4a1f-a615-53a025afbc11" "*WakeupOnBehaviorPost*" %}}: when a specified Behavior object posts a specific event
- {{% resource_link "39ddf2b2-7990-4298-aeb8-d1661718801f" "*WakeupOnAWTEvent*" %}}*:* when a specified AWT event occurs, such as. a mouse press
- {{% resource_link "efd8d1f9-8b9f-41c2-bc8a-b255522999c5" "*WakeupOnElapsedTime*" %}}: when a specified time interval elapses
- {{% resource_link "5158fd26-961e-4b29-830f-4f89ba266fff" "*WakeupOnElapsedFrames:*" %}} when a specified number of frames have been drawn
- {{% resource_link "d94478a6-d067-4083-a6b6-172083bfee02" "*WakeupOnSensorEntry:*" %}} when the center of a specified Sensor enters a specified region
- {{% resource_link "ec06402f-6c40-45e4-aeda-4dc6f5eb0747" "*WakeupOnSensorExit*" %}}: when the center of a specified Sensor exits a specified region

A {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object constructs a {{% resource_link "78b6b5cb-b789-4f17-9638-d08deeaf9a84" "*WakeupCriterion*" %}} by providing the appropriate arguments, such as a reference to some scene graph object and a region of interest.

Multiple criteria can be combined using the following classes to form complex wakeup conditions.

- {{% resource_link "a1a84df2-204c-4be2-bf07-ad1875d186df" "*WakeupOr*" %}}: specifies any number of wakeup conditions logically ORed together
- {{% resource_link "68c20c0a-1f7d-4198-8381-2260fc7e4b37" "*WakeupAnd*" %}}: specifies any number of wakeup conditions logically ANDed together
- {{% resource_link "951c850b-0b36-4207-bbf8-3a7d55d70e2f" "*WakeupOrOfAnds*" %}}: specifies any number of OR wakeup conditions logically ANDed together
- {{% resource_link "6a18a4c9-7902-4d38-9880-c3c5edb5ea59" "*WakeupAndOfOr:*" %}}  specifies any number of AND wakeup conditions logically ORed together

The class hierarchy of the {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} class is shown below:

{{< resource uuid="76163ee3-f63d-c91c-3d9f-88be97281f08" >}}

The following code provides an example of setting a {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} object

    *public void initialize()*        
*{*        
{{% resource_link "78b6b5cb-b789-4f17-9638-d08deeaf9a84" "*WakeupCriterion*" %}} *criteria\[\] = new WakeupCriterion\[2\];*        
*criteria\[0\] = new* {{% resource_link "ff6b42fb-b677-4398-bb62-4568aa40f2c3" "*WakeupOnElapsedFrames(3)*" %}}*;*        
*criteria\[0\] = new* {{% resource_link "b3f1e4cf-4c5a-4ece-8225-bd827731a692" "*WakeupOnElapsedTime(500)*" %}}*;*

{{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} *condition = new* {{% resource_link "a1a84df2-204c-4be2-bf07-ad1875d186df" "*WakeupOr*" %}}*(criteria);*        
{{% resource_link "09cccdb8-32ac-49fc-a9ba-a0bcc16dc19a" "*wakeupOn(*" %}}*condition);*        
*}*

A {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} node provides a {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}} object to the behavior scheduler via its {{% resource_link "09cccdb8-32ac-49fc-a9ba-a0bcc16dc19a" "*wakeupOn()*" %}} method and the behavior scheduler provides an enumeration of that {{% resource_link "9339912c-345b-407e-badc-fb8b2235bd91" "*WakeupCondition*" %}}. The {{% resource_link "09cccdb8-32ac-49fc-a9ba-a0bcc16dc19a" "*wakeupOn()*" %}} method should be called from the {{% resource_link "6c830b3d-e7af-42aa-9db9-c57b41b3030e" "*initialize()*" %}} and {{% resource_link "06627900-1eba-4733-a03a-aa8eb69b171b" "*processStimulus()*" %}} methods, just prior of exiting these methods.

In the current Java® 3D implementation the behavior scheduler, and, therefore, the {{% resource_link "06627900-1eba-4733-a03a-aa8eb69b171b" "*processStimulus*" %}} method of the {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} class as well, run concurrently with the rendering thread. However, a new thread will not start until both the renderer, which may be working on the previous frame, and the behavior scheduler are done.

Java® 3D guarantees that all behaviors with a {{% resource_link "5158fd26-961e-4b29-830f-4f89ba266fff" "*WakeupOnElapsedFrames*" %}} will be executed before the next frame starts rendering, i.e. the rendering thread will wait until all behaviors are done with their {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus*" %}} methods before drawing the next frame. In addition, Java® 3D guarantees that all scene graph updates that occur from within a single {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object will be reflected in the same frame for consistency purposes.

Finally, {{% resource_link "009c098f-f9f5-45be-96ba-ea3dd31b5c2c" "*Interpolator*" %}} objects can be used for simple behaviors where a parameter can be varied between a starting and an ending value during a certain time interval.

Lights

Lights can be used in order to achieve higher quality and realism of the graphics. Lighting capabilities is provided by the class Light and its subclasses. All light objects have a color, an on/off state, and a bounding volume that controls their illumination range. Java3D provides the following four types of lights, which are subclasses of the class {{% resource_link "a0d20e1a-8d92-4f1c-a46a-e6f71cf762a7" "*Light*" %}}:

- {{% resource_link "52fcd3f8-3c88-4826-b6d0-90c3b91e91f3" "*AmbientLight*" %}}: the rays from an ambient light source object come from all directions illuminating shapes evenly
- {{% resource_link "bac5c900-c512-40a9-9b42-248c489d590f" "*DirectionalLight*" %}}: a directional light source object has parallel rays of light aiming at a certain direction
- {{% resource_link "a8291754-1253-484e-99ba-194771218326" "*PointLight*" %}}: the rays from an point light source object are emitted radially from a point to all directions
- {{% resource_link "5191799e-379e-4bac-9aed-5371a48aa91e" "*SpotLight*" %}}: the rays from a spot light source object are emitted radially from a point to all directions but within a cone

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

Whenever a node of the scene graph is modified a message is generated with a value associated with it and any state necessary to reflect the specific changes, and queued with all other messages by the thread scheduler. At each iteration the messages are processed and the various structures are updated accordingly. The update time is very fast when the messages are very simple, which is typically the case. In the current implementation the rendering thread and the behavior thread can run concurrently. In particular, the behavior scheduler and therefore the {{% resource_link "26177be4-f81e-4595-ae87-1e3ed4a86217" "*processStimulus*" %}} method of a {{% resource_link "ef5817d6-e126-42b6-8ebd-a0805c309b0f" "*Behavior*" %}} object, can run concurrently with the renderer. However, a new frame will not start until both the rendering of the previous frame and the behavior scheduler are done.

Finally it offers level-of-detail ({{% resource_link "e1e49924-5938-4c97-9e59-b2ad6b61813a" "*LOD*" %}}) capabilities to further improve performance using a {{% resource_link "e1e49924-5938-4c97-9e59-b2ad6b61813a" "*LOD*" %}} object. An LOD leaf node is an abstract class that operates on a list of Switch group nodes to select one of the children of the Switch nodes. The {{% resource_link "e1e49924-5938-4c97-9e59-b2ad6b61813a" "*LOD*" %}} class is extended to implement various selection criteria, such as the {{% resource_link "46af42c1-c8b9-40e5-a2e0-91773efdfa4e" "*DistanceLOD*" %}} subclass.