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

Embedded Repository
===================
You can run Jackrabbit in embedded mode inside your application if you only
(or mostly) access a repository from that one application. In this
deployment model the Jackrabbit dependencies are included directly in your
classpath and your application is in full control of the repository
lifecycle. To use this deployment model you need to add the appropriate
dependencies to your application and include a few lines of
Jackrabbit-specific code to start and stop a repository. You can then use
the standard JCR API to access and manage content inside the repository.

This page describes how to embed Jackrabbit in your application.

Jackrabbit dependencies
-----------------------
To use Jackrabbit in embedded mode you need to make sure that the JCR API
and all required Jackrabbit libraries are included in your classpath. If
you use [Maven 2](http://maven.apache.org/)
, you can achieve this by specifying the following dependencies.


    <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
      <version>1.0</version>
    </dependency>
    <dependency>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>jackrabbit-core</artifactId>
      <version>1.5.0</version>
      <exclusions>
        <exclusion>
          <groupId>commons-logging</groupId>
          <artifactId>commons-logging</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>jcl-over-slf4j</artifactId>
      <version>1.5.3</version>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.5.3</version>
    </dependency>


The jcr dependency includes the JCR 1.0 API in your classpath. You need to
explicitly declare this dependency as in jackrabbit-core the JCR API
dependency scope is _provided_ to work better in deployment models where
the JCR API is shared between multiple applications.

The jackrabbit-core dependency pulls in the Jackrabbit content repository
implementation and a set of transitive dependencies needed by Jackrabbit.
See the [Downloads](downloads.html)
 page for the latest available version.

Jackrabbit uses the [SLF4J](http://www.slf4j.org/)
 for logging and leaves it up to the embedding application to decide which
underlying logging library to use. In the example above we use the
slf4j-log4j12 library which uses [log4j 1.2](http://logging.apache.org/log4j/1.2/)
 for handling the log messages. Note that the commons-logging dependency
(which is a transitive dependency from [Apache POI](http://poi.apache.org/)
) is explicitly replaced with the jcl-over-slf4j dependency that routes
also all [Commons Logging](http://commons.apache.org/logging/)
 log messages through the selected SLF4J implementation. Jackrabbit 1.5.x
uses SLF4J version 1.5.3.

The full set of compile-scope dependencies included by the above
declaration is shown below. If you use a build tool like [Ant](http://ant.apache.org/)
 where you need to explicitly include all dependencies, you can use this
list to correctly configure your classpath.


    +- javax.jcr:jcr:jar:1.0:compile
    +- org.apache.jackrabbit:jackrabbit-core:jar:1.5.0:compile
    |  +- concurrent:concurrent:jar:1.3.4:compile
    |  +- commons-collections:commons-collections:jar:3.1:compile
    |  +- commons-io:commons-io:jar:1.4:compile
    |  +- org.apache.jackrabbit:jackrabbit-api:jar:1.5.0:compile
    |  +- org.apache.jackrabbit:jackrabbit-jcr-commons:jar:1.5.0:compile
    |  +- org.apache.jackrabbit:jackrabbit-spi-commons:jar:1.5.0:compile
    |  +- org.apache.jackrabbit:jackrabbit-spi:jar:1.5.0:compile
    |  +- org.apache.jackrabbit:jackrabbit-text-extractors:jar:1.5.0:compile
    |  |  +- org.apache.poi:poi:jar:3.0.2-FINAL:compile
    |  |  +- org.apache.poi:poi-scratchpad:jar:3.0.2-FINAL:compile
    |  |  +- pdfbox:pdfbox:jar:0.7.3:compile
    |  |  |  +- org.fontbox:fontbox:jar:0.1.0:compile
    |  |  |  \- org.jempbox:jempbox:jar:0.2.0:compile
    |  |  \- net.sourceforge.nekohtml:nekohtml:jar:1.9.7:compile
    |  |	 \- xerces:xercesImpl:jar:2.8.1:compile
    |  |	    \- xml-apis:xml-apis:jar:1.3.03:compile
    |  +- org.slf4j:slf4j-api:jar:1.5.3:compile
    |  +- org.apache.lucene:lucene-core:jar:2.3.2:compile
    |  \- org.apache.derby:derby:jar:10.2.1.6:compile
    +- org.slf4j:jcl-over-slf4j:jar:1.5.3:compile
    \- org.slf4j:slf4j-log4j12:jar:1.5.3:compile
       \- log4j:log4j:jar:1.2.14:compile


Note that some of the transitive dependencies listed above may conflict
with some other dependencies of our application. In such cases you may want
to consider switching to a deployment model that uses separate class
loaders for your application and the Jackrabbit content repository.

Starting the repository
-----------------------
Once you have your classpath configured you can start the repository with
the following piece of code.

    import javax.jcr.Repository;
    import org.apache.jackrabbit.core.RepositoryImpl;
    import org.apache.jackrabbit.core.config.RepositoryConfig;
    
    String xml = "/path/to/repository/configuration.xml";
    String dir = "/path/to/repository/directory";
    RepositoryConfig config = RepositoryConfig.create(xml, dir);
    Repository repository = RepositoryImpl.create(config);

    
See the [Jackrabbit Configuration]
page for more information on repository configuration. See the [RepositoryConfig](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/config/RepositoryConfig.html)
and [RepositoryImpl](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/RepositoryImpl.html)
javadocs for more details on these classes.
    
Shutting down the repository
----------------------------
When your application no longer needs the content repository, you can shut it down with the following code.
    
    ((RepositoryImpl) repository).shutdown();

This will forcibly close all open sessions and make sure that all
repository content is safely stored on disk.


The TransientRepository class
-----------------------------
Jackrabbit comes with a [TransientRepository](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/TransientRepository.html)
 class that makes it even easier to get started with a content repository.
This class is especially handy for quick prototyping, but using the
RepositoryImpl class as described above gives you better control over the
repository lifecycle and is typically a better alternative for production
code.

    import javax.jcr.Repository;
    import org.apache.jackrabbit.core.TransientRepository;
    
    Repository repository = new TransientRepository();

    
This creates a repository instance that starts up when the first session is
created and automatically shuts down when the last session is closed. By
default the repository will be created in a "jackrabbit" subdirectory using
a default configuration file in `jackrabbit/repository.xml`. See the
TransientRepository javadocs for the ways to override these defaults.
    

Enabling remote access
----------------------
Even if you mostly use the content repository in embedded mode within your
application, it may occasionally be useful to be able to access the
repository for example from an external administration tool while your
application is still running. You can use the jackrabbit-jcr-rmi library to
make this possible. To do this, you first need to add the appropriate
dependency.
    
    <dependency>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>jackrabbit-jcr-rmi</artifactId>
      <version>1.5.0</version>
    </dependency>


Make sure that you have [rmiregistry](http://java.sun.com/j2se/1.5.0/docs/tooldocs/solaris/rmiregistry.html)
 running, and use the following code to export the repository. Note that
you need to include the JCR API and the jackrabbit-jcr-rmi libraries in the
rmiregistry classpath for the binding to work without extra RMI codebase
settings.

    import java.rmi.Naming;
    import org.apache.jackrabbit.rmi.server.RemoteAdapterFactory;
    import org.apache.jackrabbit.rmi.server.RemoteRepository;
    import org.apache.jackrabbit.rmi.jackrabbit.JackrabbitRemoteAdapterFactory;
    
    String url = "//localhost/javax/jcr/Repository"; // RMI URL of the
    repository
    RemoteAdapterFactory factory = new JackrabbitRemoteAdapterFactory();
    RemoteRepository remote = factory.getRemoteRepository(repository);
    Naming.bind(url, remote);

    
Use the following code to remote the repository binding from the RMI
registry before you shutdown the repository.
    
    Naming.unbind(url);

You need to keep a direct reference to the RemoteRepository instance in
your code until you call Naming.unbind as otherwise it could get garbage
collected before a remote client connects to it.

_Note_: RMI access is deprecated and will be removed in version 2.22.x
(see [JCR-4792](https://issues.apache.org/jira/browse/JCR-4972) for details).

See the [Repository Server](repository-server.html)
page for instructions on how to access such a remote repository.


Embedded repository in a web application
----------------------------------------
If your want to embed Jackrabbit in a web application, you can use the
classes in the jackrabbit-jcr-servlet library to avoid the above startup
and shutdown code. To do this, you first need to include
jackrabbit-jcr-servlet as a dependency.


    <dependency>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>jackrabbit-jcr-servlet</artifactId>
      <version>1.5.0</version>
    </dependency>


Then you can instruct the servlet container to automatically start and stop
the repository as a part of your webapp lifecycle by including the
following servlet configuration in your web.xml file.


    <servlet>
        <servlet-name>ContentRepository</servlet-name>
        <servlet-class>org.apache.jackrabbit.servlet.jackrabbit.JackrabbitRepositoryServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>


See the [JackrabbitRepositoryServlet](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/servlet/jackrabbit/JackrabbitRepositoryServlet.html)
 javadocs for the available configuration options.

You can then access the repository in your own servlet classes using the
following piece of code without worrying about the repository lifecycle.

    import javax.jcr.Repository;
    import org.apache.jackrabbit.servlet.ServletRepository;

Repository repository = new ServletRepository(this); // "this" is the
containing servlet

The benefit of this approach over directly using the RepositoryImpl or
TransientRepository classes as described above is that you can later on
switch to a different deployment model without any code changes simply by
modifying the servlet configuration in your web.xml.
    
With this approach it is also easier to make your repository remotely
available. Add the following configuration to your web.xml and your
repository is automatically made available as a remote repository at
.../rmi in the URL space of your webapp.
    
    <servlet>
        <servlet-name>RemoteRepository</servlet-name>
        <servlet-class>org.apache.jackrabbit.servlet.remote.RemoteBindingServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>RemoteRepository</servlet-name>
        <url-pattern>/rmi</url-pattern>
    </servlet-mapping>

Note that you also need the jackrabbit-jcr-rmi dependency in your
application for the above configuration to work.
