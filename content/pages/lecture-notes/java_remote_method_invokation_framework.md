---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Java Remote Method Invokation Framework
uid: e20527da-f358-a3c0-6544-650b3dff8917
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [Java® RMI](#1)
2.  [The RMI Client](#2)
3.  [The RMI Server](#3)
4.  [How to Compile and Run](#4)

{{< anchor "1" >}}{{< /anchor >}}1\. Java® RMI
----------------------------------------------

(Ref: Just Java® 1.2 Ch 16)

The Java® Remote Method Invokation (RMI) framework provides a simple way for Java® programs to communicate with each other. It allows a client program to call methods that belong to a remote object, which lives on a server located elsewhere on the network. The client program can pass arguments to the methods of the remote object and obtain return values, as seamlessly as invoking a method of a local object.

The operation of a remote method call is as follows. The client program actually calls into a dummy method, called a _stub_, which resides locally. The stub gets the function arguments, serializes them and then sends them over the network to the server. On the server side, a corresponding bare-bones method (called a _skeleton_) deserializes the argument objects and passes them onto the real server method. This process is reversed in order to send the result back to the client.

The Interface to the Remote Object
----------------------------------

Both the client and the server must agree on a common interface, which describes the methods that are to be invoked on the server. For example:

_**WeatherIntf.java**_

_// An interface that describes the service we will be accessing remotely._  
 _public interface WeatherIntf extends java.rmi.Remote {_  
 _public String getWeather() throws java.rmi.RemoteException;_  
_}_

{{< anchor "2" >}}{{< /anchor >}}2\. The RMI Client
---------------------------------------------------

Here is the example code for the client. The call to _Naming.lookup()_ returns a reference to a _Remote_ object that is available on the server (_localhost_ in this case) under the service name _/WeatherServer_. Before we can access its methods, the _Remote_ object must be cast to the appropriate interface type (_WeatherIntf_ in this case).

_RMIdemo.java_

_import java.rmi.\*;_

 _public class RMIdemo {_  
 _public static void main(String\[\] args) {_  
 _try {_  
 _// Obtain a reference to an object that lives remotely on a server._  
 _// The object is published under the service name WeatherServer and_  
 _// it is known to implement interface WeatherIntf.  We cast to this_  
 _// interface in order to access the object's methods._  
 _Remote robj = Naming.lookup("//localhost/WeatherServer");_  
 _WeatherIntf weatherServer = (WeatherIntf)robj;_

 _// Access the services provided by the remote object._  
 _while (true) {_  
 _String forecast = weatherServer.getWeather();_  
 _System.out.println("The weather will be " + forecast);_  
 _Thread.sleep(500);_  
 _}_  
 _}_  
 _catch (Exception e) {_  
 _System.out.println(e.getMessage());_  
 _}_  
 _}_  
_}_

{{< anchor "3" >}}{{< /anchor >}}3\. The RMI Server
---------------------------------------------------

Here is the example code for the server. The server makes its services available to the client by registering them with the RMI registry using a call to _Naming.rebind()_. In this code, the server side object is made available under the name _/WeatherServer_.

_WeatherServer.java_

_import java.rmi.\*;_  
_import java.rmi.server.UnicastRemoteObject;_

 _public class WeatherServer extends UnicastRemoteObject implements WeatherIntf {_  
 _public WeatherServer() throws java.rmi.RemoteException {_  
 _super();_  
 _}_

 _// The method that will be invoked by the client._  
 _public String getWeather() throws RemoteException {_  
 _return Math.random() > 0.5 ? "sunny" : "rainy";_  
 _}_

 _public static void main(String\[\] args) {_  
 _// We need to set a security manager since this is a server._  
 _// This will allow us to customize access priviledges to_  
 _// remote clients._  
 _System.setSecurityManager(new RMISecurityManager());_

 _try {_  
 _// Create a WeatherServer object and announce its service to the_  
 _// registry._  
 _WeatherServer weatherServer = new WeatherServer();_  
 _Naming.rebind("/WeatherServer", weatherServer);_  
 _}_  
 _catch (Exception e) {_  
 _System.out.println(e.getMessage());_  
 _}_  
 _}_  
_}_

{{< anchor "4" >}}{{< /anchor >}}4\. How to Compile and Run

*   Compile all three _.java_ files using _javac_:  
     _javac \*.java_ 
*   Generate the stub and the skeleton classes for the server:  
     _rmic WeatherServer_ 
*   Put the class files in a location that the JDK knows about e.g. the current directory or _$JAVAHOME/jre/classes_. 
*   Start the RMI registry:  
    _rmiregistry_ 
*   Create a permissions file for the server:   
    _**permit**_
    
        _grant {_  
     _permission java.net.SocketPermission "\*", "connect";_  
     _permission java.net.SocketPermission "\*", "accept";_  
     _// Here is how you could set file permissions:_  
     _// permission java.io.FilePermission "/tmp/\*", "read";_  
     _};_
    
*   Start the server using the security policy prescribed by the permissions file:   
     _java -Djava.security.policy=permit WeatherServer_  
*   Start the client:  
    _java RMIdemo_

The client will now communicate with the server to find out the current weather.


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------