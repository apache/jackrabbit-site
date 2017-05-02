<!--
   Licensed to the Apache Software Foundation (ASF) under one or more
   contributor license agreements.  See the NOTICE file distributed with
   this work for additional information regarding copyright ownership.
   The ASF licenses this file to You under the Apache License, Version 2.0
   (the "License"); you may not use this file except in compliance with
   the License.  You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
-->

Building Jackrabbit
===================
The easiest way to use Jackrabbit is to [download](http://jackrabbit.apache.org/download.cgi)
a binary release, but if you want to access the latest development
version, you need to get the Jackrabbit sources and build them using the 
[Maven 3](http://maven.apache.org/) build environment.

The first step in building Jackrabbit is to check out the Jackrabbit
sources from the [Subversion](http://subversion.tigris.org/)
source repository at http://svn.apache.org/repos/asf/jackrabbit/. 

The source tree is divided in standard parts: [trunk](http://svn.apache.org/repos/asf/jackrabbit/trunk/), 
[branches](http://svn.apache.org/repos/asf/jackrabbit/branches/), 
[tags](http://svn.apache.org/repos/asf/jackrabbit/tags/) and 
[commons](http://svn.apache.org/repos/asf/jackrabbit/commons/)
([more info about commons](http://jackrabbit.apache.org/commons/)). 
The latest development version is found within trunk, while the other parts are
used to keep track of the source code of the Jackrabbit releases.

The trunk contains the top-level build environment and a number of [component projects](jackrabbit-components.html)
within subdirectories. See the `README.txt` files within each subdirectory
for a brief description of the component project. There is also a [sandbox](http://svn.apache.org/repos/asf/jackrabbit/sandbox/)
directory with miscellaneous contributions that are not yet a part of the
official Jackrabbit releases.


Checking out the sources with Subversion
----------------------------------------
You need a [Subversion](http://subversion.tigris.org/)
client to access the Jackrabbit source repository. Take a look at the [Subversion client list](http://subversion.tigris.org/project_links.html#clients)
unless you already have a one installed. Once you have the Subversion
client installed you can checkout the main Jackrabbit source tree with the
following command or its equivalent in the client you are using:

    svn checkout http://svn.apache.org/repos/asf/jackrabbit/trunk jackrabbit

The above checkout will create a subdirectory named jackrabbit that
contains the latest Jackrabbit sources. See the [Subversion book](http://svnbook.red-bean.com/)
or the documentation of your Subversion client for more information on how
to manage your source tree and keep it up to date with latest development.


Building the sources with Maven
-------------------------------
Jackrabbit uses [Maven 3](http://maven.apache.org/)
as the build system and the component sources are mostly organized
according to the Maven [Standard Directory Layout](http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).
The standard build environment is Maven 3 with the Java Development Kit
(JDK) 1.8 for trunk. Older branches use JDK 1.7 (2.14) and JDK 1.6 (2.12 and before).

See the [Running Maven](http://maven.apache.org/run-maven/index.html)
page and the related documentation on the Maven web site for instructions
on how to use Maven. You may also want to check for Maven integration
with your favourite Integrated Development Environment (IDE).

There are Maven project descriptors (POMs) within both the top level
jackrabbit directory you checked out above and all the
jackrabbit-<i>something</i> component subdirectories. The easiest way to build
Jackrabbit is to use the "multimodule" setup within the top level directory:

    $ cd /path/to/jackrabbit; mvn install

This will build and package all the component projects and place the
resulting artifacts within your local Maven repository. You can also find
the artifacts within the created target subdirectories of the component
projects.
