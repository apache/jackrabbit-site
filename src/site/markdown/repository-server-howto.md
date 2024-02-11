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

Repository Server HOWTO
=======================
This document describes how to use a Jackrabbit content repository in the
deployment model 3: The Repository Server. In this deployment model, a
separate repository server is running outside the virtual machine the
client application is running in. A repository server can serve multiple
applications running on separate JVMs on separate network hosts. See the [JCR client application HOWTO](jcr-client-application-howto.html)
for instructions on how to use the configured content repository server.

Note that JCR specification defines no standard communication protocol for
inter-JVM repository access, and that Jackrabbit supports no such protocol
by default. However, Jackrabbit contains tools for using JCR content
repositories over the RMI and WebDAV protocols (see the jcr-rmi and the
jcr-server, webapp packages).

This how-to contains instructions for accessing a JCR-RMI server in Tomcat
versions 4.x and 5.x. It should be easy to modify the instructions for
other container environments and communication protocols.

In addition to the following the instructions in this document, you also
need to have an already running JCR-RMI server. See the JCR-RMI javadocs
for instructions on how to setup such a server.

Warning: The current JCR-RMI library is designed for simplicity, not
performance. You will probably experience major performance issues if you
try running any non-trivial applications on top of JCR-RMI.

_Note_: RMI access is deprecated and will be removed in version 2.22.x
(see [JCR-4792](https://issues.apache.org/jira/browse/JCR-4972) for details).

Tomcat instructions
-------------------
Follow the steps below to setup a model 3 JCR-RMI client deployment for
your web application in Tomcat 4.x or 5.x. Example code for both versions
of Tomcat is included after this overview.

Note that these instructions closely follow the Model 1 HOWTO instructions.
By making similar changes (change the factory class and parameters of the
repository) to the Model 2 HOWTO instructions, you can setup a shared
JCR-RMI client deployment for all applications in the container.

1. Place the JCR-RMI jar file and its dependencies (including the JCR API jar) under `$CATALINA_HOME/webapps/_your app_/WEB-INF/lib`.
2. Register the JCR-RMI client repository factory in the context scope.

### Step 2 - Context configuration
In Tomcat 4.x and 5.0, add the following snippet in `server.xml` under the
Context element of your web application.

    <Resource 
        name="jcr/repository" 
        auth="Container" 
        type="javax.jcr.Repository"
    />
    <ResourceParams name="jcr/repository">
        <parameter>
            <name>factory</name>
            <value>org.apache.jackrabbit.rmi.client.ClientRepositoryFactory</value>
        </parameter>
        <parameter>
            <name>url</name>
            <value>[The RMI URL of the repository] </value>
        </parameter>
    </ResourceParams>


In Tomcat 5.5, add the following snippet in your application's context.xml
file (or in the server.xml file if you prefer central configuration).

    <Resource 
        name="jcr/repository"
        auth="Container"
        type="javax.jcr.Repository" 
        factory="org.apache.jackrabbit.rmi.client.ClientRepositoryFactory" 
        url="[The RMI URL of the repository]"
    />

