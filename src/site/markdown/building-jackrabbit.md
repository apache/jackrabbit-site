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
The easiest way to use Jackrabbit is to [download](https://jackrabbit.apache.org/download.cgi)
a binary release, but if you want to access the latest development
version, you need to get the Jackrabbit sources and build them using the 
[Maven 3](https://maven.apache.org/) build environment.

The first step in building Jackrabbit is to clone the Jackrabbit
sources from the [Git](https://git-scm.com/)
source repository at <https://github.com/apache/jackrabbit>. 

The default branch is named `trunk` (for historical reasons) and contains the reactor Maven project and a number of [components](jackrabbit-components.html) in Maven modules. See the `README.txt` files within each subdirectory for a brief description of the according component. 

There is also a [sandbox](http://svn.apache.org/repos/asf/jackrabbit/sandbox/)
directory hosted in Subversion with miscellaneous contributions that are not (yet) a part of the
official Jackrabbit releases and the mostly outdated [commons](http://svn.apache.org/repos/asf/jackrabbit/commons/)/. 


Cloning the repository with Git
----------------------------------------
You need a [Git](https://git-scm.com/)
client to access the Jackrabbit source repository. You can clone the main Jackrabbit source tree with the
following command (or its equivalent in the client you are using):

    git clone https://github.com/apache/jackrabbit

The above checkout will create a subdirectory that
contains the latest Jackrabbit sources. 


Building the sources with Maven
-------------------------------
Jackrabbit uses [Maven 3](https://maven.apache.org/)
as the build system and the component sources are mostly organized
according to the Maven [Standard Directory Layout](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).
The standard build environment is Maven 3 with the Java Development Kit
(JDK) 11 for trunk.

See the [Running Maven](https://maven.apache.org/run-maven/index.html)
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
