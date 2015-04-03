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

Jackrabbit JCR-RMI
==================
This is the JCR-RMI component of the Apache Jackrabbit project. JCR-RMI is
a transparent Remote Method Invocation (RMI) layer for the Content
Repository for Java Technology API (JCR). The layer makes it possible to
remotely access JCR content repositories and is compatible with all JCR
implementations.


Setting up a remote repository
------------------------------
Setting up the server part of the JCR-RMI layer is quite straightforward.
After instantiating a local JCR repository you need to wrap it into a
remote adapter and create an RMI binding for the repository. A variation of
the following code is usually all that is needed in addition to the
standard RMI setup (starting rmiregistry, etc.):


    Repository repository = ...; // The local repository
    String name = ...; // The RMI URL for the repository
        
    RemoteAdapterFactory factory = new ServerAdapterFactory();
    RemoteRepository remote = factory.getRemoteRepository(repository);
    Naming.bind(name, remote);  // Make the RMI binding using java.rmi.Naming


Accessing a remote repository
-----------------------------
The ClientRepositoryFactory class provides a convenient mechanism for
looking up a remote JCR-RMI repository. The factory can be used either
directly or as a JNDI object factory.

The following example shows how to use the ClientRepositoryFactory directly:

    String name = ...; // The RMI URL of the repository
        
    ClientRepositoryFactory factory = new ClientRepositoryFactory();
    Repository repository = factory.getRepository(name);


The ClientRepositoryFactory can also be used via JNDI. The following
example settings and code demonstrate how to configure and use the
transparent JCR-RMI layer in a Tomcat 5.5 web application:

**context.xml**:

    <Resource name="jcr/Repository" auth="Container"
        type="javax.jcr.Repository"
        factory="org.apache.jackrabbit.rmi.client.ClientRepositoryFactory"
        url="..."/>


**web.xml**:

    <resource-env-ref>
      <description>The external content repository</description>
      <resource-env-ref-name>jcr/Repository</resource-env-ref-name>
      <resource-env-ref-type>javac.jcr.Repository</resource-env-ref-type>
    </resource-env-ref>


**...SomeServlet.java**:

    Context initial = new InitialContext();
    Context context = (Context) initial.lookup("java:comp/env");
    Repository repository = (Repository) context.lookup("jcr/Repository");


Note that in the example above only the context.xml configuration file
contains a direct references to the JCR-RMI layer. All other parts of the
web application can be implemented using the standard JCR interfaces. 
