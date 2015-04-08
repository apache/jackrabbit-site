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

Frequently Asked Questions
==========================


General
-------

### What is JCR?
JCR is the acronym of the Content Repository for Java technology API, a standard interface for accessing content repositories. 
JCR version 1.0 was specified in Java Specification Request 170 ([JSR 170](http://jcp.org/en/jsr/detail?id=170)), 
and version 2.0 is currently under work in [JSR 283|http://jcp.org/en/jsr/detail?id=283].

### What is a content repository?
A content repository is an information management system that provides
various services for storing, accessing, and managing content. In addition
to a hierarchically structured storage, common services of a content
repository are versioning, access control, full text searching, and event
monitoring. A content repository is not a content management system (CMS),
although most existing CMSs contain a custom content repository
implementation, often based on the file system or a relational database.

### What is Apache Jackrabbit?
Apache Jackrabbit is a fully featured content repository that implements
the entire JCR API.  The Jackrabbit project was started when Day Software,
the JSR-170 specification lead, licensed their initial implementation of
the JCR reference implementation. The Jackrabbit codebase was used for the
official reference implementation (RI) and technology compatibility kit
(TCK) released along with the final JCR API.

### What do I do if I have a question?
Please ask questions on the [Jackrabbit mailing lists](http://jackrabbit.apache.org/mailing-lists.html). 
There is the users list for questions around using JCR and Jackrabbit and
the dev list for the development of Jackrabbit itself and for people
starting to extend Jackrabbit or other advanced topics.


Building Jackrabbit
-------------------

### How do I build the Apache Jackrabbit sources?
See the [Building Jackrabbit](building-jackrabbit.html) page for detailed build instructions.


Using Jackrabbit
----------------

### How do I do X with JCR/Jackrabbit?
See the JCR specification, the JCR API documentation, or the Examples page
on the Jackrabbit wiki for information on how to perform various operation
using the JCR API.

For Jackrabbit features (like access control and node type management) not
covered by the JCR API, see the Examples page on the wiki, the Jackrabbit
javadocs, or contact the Jackrabbit mailing list.

### How do I use transactions with JCR?
See the mailing list announcement for a simple example on using the JTA
support in Jackrabbit. For a more complete explanation of the transaction
features, please	   see section 8.1 Transactions of the JCR
specification.

### How do I create new workspaces in Jackrabbit?
The JCR 2.0 API has two [Workspace.createWorkspace\(\)](http://www.day.com/maven/jsr170/javadocs/jcr-2.0/javax/jcr/Workspace.html#createWorkspace\(java.lang.String\)) methods for that.

The JCR 1.0 API does not contain features for creating or managing
workspaces, so you need to use Jackrabbit-specific functionality for
creating new workspaces. You can create a new workspace either manually or
programmatically.

The manual way is to create a new workspace directory within the repository
home directory and to place a new workspace.xml configuration file in that
folder. You can use the configuration file of an existing workspace as an
example, just remember to change the name of the workspace in the
Workspace name="..." tag. See the [Jackrabbit Configuration](jackrabbit-configuration.html)
page for configuration details. Note also that you need to restart the
repository instance to access the new workspace.

The programmatic way is to acquire a Workspace instance using the normal
JCR API and to cast the instance to the JackrabbitWorkspace interface. You
can then use the createWorkspace(String) method to create new workspaces.

### How do I delete a workspace in Jackrabbit?
There is currently no programmatic way to delete workspaces. You can delete
a workspace by manually removing the workspace directory when the
repository instance is not running.

### How do I deploy Jackrabbit into Tomcat?
* Download [jcr-1.0.jar](http://www.day.com/maven/javax.jcr/jars/jcr-1.0.jar) and put it into `<tomcat-install-dir>/shared/lib`.
* Get the WAR distribution from the [Downloads](downloads.html) page and deploy it into Tomcat.
* Point your browser to `http://localhost:8080/jackrabbit-webapp-<version>`


Access control
--------------

### How do I use LDAP, Kerberos, or some other authentication mechanism with Jackrabbit?

Jackrabbit uses the Java Authentication and Authorization Service (JAAS)
for authenticating users. You should be able to use any JAAS LoginModule 
implementation (e.g. the LoginModules in thecom.sum.security.auth.modulepackage) 
for authentication. See the JAAS documentation for configuration instructions.

### How do I manage the access rights of authenticated users?
The current JackrabbitSimpleAccessManager class only supports three access
levels: anonymous, normal, and system. Anonymous users have read
access while normal and system users have full read-write access.
You need to implement a custom AccessManager class to get more fine-grained
access control.


Persistence managers
--------------------

### What is a persistence manager?
A persistence manager (PM) is an internal Jackrabbit component
that handles the persistent storage of content nodes and
properties. Each workspace of a Jackrabbit content repository	       
uses a separate persistence manager to store the content in that	  
workspace. Also the Jackrabbit version handler uses a separate		
persistence manager.The persistence manager sits at the very bottom layer
of the Jackrabbit system architecture. Reliability, integrity and
performance of the PM are crucial to the overall	    
stability and performance of the repository. If e.g. the data	       
that a PM is based upon is allowed to change through external	       
means the integrity of the repository would be at risk (think of referential 
integrity / node references e.g.).

In practice, a persistence manager is any Java class that	   
implements the PersistenceManager interface and the associated
behavioural contracts. Jackrabbit contains a set of built-in
persistence manager classes that cover most of the deployment
needs. There are also a few contributed persistence managers that
give additional flexibility.

### What is a Jackrabbit file system?
A Jackrabbit file system (FS) is an internal component that	      
implements standard file system operations on top of some underlying	   
storage mechanism (a normal file system, a database, a webdav server,   
or a custom file format). A file system component is any Java class 
that implements the FileSystem interface and the
associated behavioral contracts. File systems are used in
Jackrabbit both as sub-components of the persistence managers and
for general storage needs (for example to store the full text
indexes).

### Can I use a persistence manager to access an existing data source?
No. The persistence manager interface was never intended as being	   
a general SPI that you could implement in order to integrate	      
external data sources with proprietary formats (e.g. a customers	  
database). The reason why we abstracted the PM interface was to
leave room for future performance optimizations that would not
affect the rest of the implementation (e.g. by storing the raw
data in a b-tree based database instead of individual file).

### How smart should a persistence manager be?

A persistence manager should not be intelligent, i.e. it should
not interpret the content it is managing. The only thing it
should care about is to efficiently, consistently, and reliably
store and read the content encapsulated in the passed NodeState
and PropertyState objects. Though it might be feasible to write a
custom persistence manager to represent existing legacy data in a
level-1 (read-only) repository, I don't think the same is
possible for a level-2 repository and I certainly would not
recommend it.

Query
-----

### I've configured textFilterClasses but my query still doesn't work, what's wrong?
Make sure you changed existing workspace.xml files as well. The workspace
element in `repository.xml only` acts as a template for new workspaces.

Verify that you also put the jar files into the classpath that jackrabbit
depends on for text extraction. You can find all required jar files inside
the jackrabbit-webapp war file (the *WEB-INF/lib* folder). 
Go to the [downloads](downloads.html) page to get the war file.

Some documents may still not be searchable for various reasons: the
document is corrupt, bug in one of the libraries that extract text,
document is encrypted or otherwise protected, etc.

### Why doesn't `//*\[jcr:contains(@jcr:data, 'foo')](jcr:contains(@jcr:data,-'foo').html)` return matches for binary content?
Extracted text from binary content is only indexed on the parent node of
the `@jcr:data property. Use jcr:contains()` on the nt:resource node.
Examples:

    //element(*, nt:resource)[jcr:contains(., 'foo')]
    //element(*, nt:file)[jcr:contains(jcr:content, 'foo')]


### Can I use the Lucene field syntax in `jcr:contains()` ?
No, you cannot. Even though Jackrabbit uses a Lucene index, the fields for
JCR properties do not map 1:1 to Lucene fields. Instead you can use the
following:

    //element(*, book)[jcr:contains(@title, 'jackrabbit') and jcr:contains(@text, 'query')]


### My XPath query returns no results when I add a path constraint, what's wrong?
You probably forgot to prefix your statement with */jcr:root*.

JSR 170 says in section 6.6.4.3:

> The context node of an XPath query is the XML node relative to which the
> query expression is evaluated.
> 
> A relative XPath statement (one that does not have a leading /) will be
> interpreted relative to the root node of the workspace, which, in the XML
> document view is the top-most XML element, <jcr:root>. This means that one
> should not include jcr:root as the first segment in a relative XPath
> statement, since that element is already the default context node.
> 
> An absolute XPath (one with a leading /), in contrast, will be interpreted
> relative to a position one level above <jcr:root>. This means that an
> absolute XPath must either begin with // or with /jcr:root in order to
> match anything at all.

### How do I force a consistency check on the search index?
Forcing a consistency check may be useful when you think the index is
inconsistent. You need to add two parameters to the SearchIndex section in
the workspace.xml configuration file:


    <param name="enableConsistencyCheck" value="true"/>
    <param name="forceConsistencyCheck" value="true"/>


Then restart Jackrabbit and watch the log file for possible repair
messages. Don't forget to remove the parameters again when you are done.

### Why is the size of my query result -1?
A JCR implementation may return -1 when the size is unknown. Starting with
2.0 Jackrabbit will return -1 for some query statements when there is
potential for a more optimized query execution. If you still want a size
information you can append an order by clause to your statement. This will
force Jackrabbit to calculate the result size.
