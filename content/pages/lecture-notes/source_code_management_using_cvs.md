---
content_type: page
description: ''
learning_resource_types:
- Lecture Notes
ocw_type: CourseSection
parent_title: Lecture Notes
parent_type: CourseSection
parent_uid: dd846b6b-f0c7-fd62-35a9-4e87d772d0e9
title: Source Code Management Using CVS
uid: 3848cf7f-d910-16a7-0e67-d39e21a63f50
video_files:
  video_thumbnail_file: null
video_metadata:
  youtube_id: null
---

Topics
------

1.  [CVS Resources](#1)
    
2.  [Introduction](#2)
3.  [Environment Variable](#3)
4.  [Setting Up a New Repository](#4)
5.  [Importing a Project Into CVS](#5)
6.  [Routine CVS Operations on Source Files](#6)
7.  [Tagging, Branching and Merging](#7)

{{< anchor "1" >}}{{< /anchor >}}1\. CVS Resources
--------------------------------------------------

Where to get CVS

The latest version of CVS can be obtained by anonymous ftp:

[ftp://prep.ai.mit.edu/pub/gnu/](ftp://prep.ai.mit.edu/pub/gnu/)

_CVS references on the Web_
---------------------------

[Concurrent Versions System](http://www.cvshome.org/)

[CVS Index](http://www.catb.org/~esr/writings/version-control/cederqvist-1.11.22.html#SEC193)

{{< anchor "2" >}}{{< /anchor >}}2\. Introduction
-------------------------------------------------

CVS (Concurrent Versions System) is a version control system which allows multiple software developers to work on a project concurrently. It maintains a single master copy of the source-code, which is called the _source repository_. Individual developers may obtain a working copy by checking out a snapshot of the source repository. This working copy can be edited without affecting other developers, and once the changes are complete, CVS assists in merging the changes into the source repository. CVS supports parallel development efforts through _branches_, and it provides mechanisms for merging these branches back together when desired. It also provides the facility to _tag_ the state of the directory tree at any given point so that that state can be recreated at a later time.

CVS runs under both Unix® and Windows® 95/NT environments, and it can be run as a client-server application with the source repository residing on a central Unix® server and the clients running on either Unix® or Windows® machines. The source repository may be accessed using a command line interface or through a web interface. Security provisions include simple password protection as well as Kerberos encryption.

CVS is really a front end to the slightly more primitive RCS revision control system.

{{< anchor "3" >}}{{< /anchor >}}3\. Environment Variable
---------------------------------------------------------

The CVSROOT environment variable needs to be set up to point to the source repository e.g.

setenv CVSROOT /mit/1.124/mysrc

_Note_

For a CVS password server running on a remote machine with the source repository located in /mysrc, the environment variable is set as follows:

setenv CVSROOT :pserver:USER@HOSTNAME:/mysrc

in which case, the user must log in using

cvs login

For a Kerberos-authenticated server, we would need to use kserver instead of pserver.

{{< anchor "4" >}}{{< /anchor >}}4\. Setting Up a New Repository
----------------------------------------------------------------

Once the CVSROOT environment has been set to point to the desired location, we can create a new repository using

cvs init

This operation only needs to be done once.

{{< anchor "5" >}}{{< /anchor >}}5\. Importing a Project Into CVS
-----------------------------------------------------------------

A project which was previously not under CVS control can be imported into the CVS repository using the _cvs import_ command. Be sure to change directory to the top level project directory first.

e.g.

cd ~/MyProject  
cvs import -m"Importing project into CVS." Projects/MyProject vendortag releasetag

will create the directory $CVSROOT/Projects/MyProject in the CVS repository, and import the local project files into this directory. vendortag could be your name, and releasetag could be the string "start".

This operation only needs to be done once.

{{< anchor "6" >}}{{< /anchor >}}6\. Routine CVS Operations on Source Files
---------------------------------------------------------------------------

Checking out the Project

cvs co Projects/MyProject

will make a local working copy of the repository files, with the same directory structure. There are several variants on this command. For example, instead of checking out a directory, one can check out a CVS module, which defines a collection of files and directories. CVS modules are defined in the $CVSROOT/modules file.

One can also check out a specific revision or tag using the -r option e.g.

cvs co -r1.3 Project/MyProject/myfile.C

cvs co -rMyTag Project/MyProject

It is also possible to check out the project as of a particular date and time:

cvs co -D"11/23/97 16:00:00 EST" Project/MyProject

This command does not affect the source repository.

Updating a File
---------------

Before a set of changes can be committed to the source respository, all files must be brought up to date. Files can become out of date if someone else commited changes after the working copy was checked out. To update all files in the project, type

cd Project/MyProject  
cvs up

Individual files may also be updated e.g.

cvs up myfile.C

The update command will not throw away any local changes that have been made. Instead it will attempt to merge them with the changes that were retrieved from the repository. In some cases, thr merge will fail and CVS will report a conflict. If this happens, the conflicts will have to be resolved by editing the portions of the source file that are in conflict. Conflicts can be detected by searching for the \<\<\< sequence.

The -r option can also be used with the update command.

cvs up -r1.3 myfile.C

Note that the -r option to _cvs co_ or _cvs up_ will cause a sticky tag to be set (you can check using cvs stat.) To remove the sticky tag, and update to the latest revision, use

cvs up -A myfile.C

This command does not affect the source repository.

Looking at Differences
----------------------

You can examine the local changes you are about to commit using the _cvs diff_ command. e.g.

cvs diff myfile.C

This command does not affect the source repository.

Committing Changes to the Source Repository
-------------------------------------------

Once you are sure that your changes are ready to be committed, use the _cvs commit_ command. e.g.

cvs commit -m"This is my log message." myfile.C

This command affects the source repository!

Examining the Version History of a File
---------------------------------------

Use _cvs log_ to examine the log entries for a particular file. e.g.

cvs log myfile.C

This command does not affect the source repository.

Examining the Status of a File

The current status of a file can be examined using the _cvs stat_ command. This is useful for checking whether or not the file is up to date.

cvs stat myfile.C

This command does not affect the source repository.


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Adding a New File
-----------------

A new file can be added to the project using the _cvs add_ command. Unlike _cvs import_, the _cvs add_ command should be used when the project is already under CVS control, and has already been checked out. e.g.

cd Project/MyProject  
cvs add newfile.C   
cvs commit -m"Added a new file." newfile.C

This command affects the source repository!

Removing an Unwanted File
-------------------------

If a file is no longer necessary, it can be removed from the project using the _cvs rm_ command. e.g.

cd Project/MyProject   
cvs rm oldfile.C   
cvs commit -m"Removed an unwanted file." oldfile.C

This causes the file to be retired. It will still be kept in the source repository in a subdirectory called Attic, in case it ever needs to be resurrected.

This command affects the source repository!

{{< anchor "7" >}}{{< /anchor >}}7\. Tagging, Branching and Merging
-------------------------------------------------------------------

Tagging
-------

Once the source tree has reached a stable state, it is a good idea to tag the tree, so that the stable state can be recreated. e.g.

cd Project/MyProject   
cvs tag Release\_1\_0

The tree can then continue to be modified, but the stable state can always be recovered using

cvs co -rRelease\_1\_0 Project/MyProject

Branching
---------

A parallel branch can be created by using the _cvs tag_ command with the -b option. e.g.

cd Project/MyProject   
cvs tag BigExperiment\_BASE   
cvs tag -b BigExperiment\_BRANCH

Developers who wish to work on the branch will then check out the branch:

cvs co -rBigExperiment\_BRANCH Project/MyProject

All changes will then be committed to the branch. In the meantime, development can also proceed on the trunk by doing a normal check out without the -r option.

Merging
-------

The changes on the branch can be merged back with the trunk as follows:

cvs co Project/MyProject   
cvs tag BeforeBigMerge   
cvs up -jBigExperiment\_BRANCH   
\<Resolve any conflicts here.>   
cvs commit -m"Merged in the big experiment."

The merging process should be handled with care, since it is easy to make mistakes. It is possible to do more complicated merges, such as merging just a portion of the branch with the trunk. For more details, visit one of the CVS resources listed above.