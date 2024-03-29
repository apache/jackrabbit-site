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

First Hops
==========
Welcome to your first hops into the world of Jackrabbit! This introduction
gives you a hands-on experience with Jackrabbit and the JCR API. Once you
have finished hopping through this document, you should be all set to
continue on your own with the official JCR specification and the
documentation on this site. 


Hop 0: Getting started
----------------------
The easiest way to get started with Jackrabbit is to [download](downloads.html)
the runnable [Standalone Server](standalone-server.html) jar. In addition to 
running it, you can also put it in your classpath to quickly access all the classes 
and interfaces you need below. Alternatively, if you use the [Apache Maven](http://maven.apache.org/)
build system (which we recommend), you can set up your first hops project
with the following dependencies. 

    <dependencies> 
        <!-- The JCR API --> 
        <dependency> 
            <groupId>javax.jcr</groupId> 
            <artifactId>jcr</artifactId> 
            <version>2.0</version> 
        </dependency> 
        
        <!-- Jackrabbit content repository --> 
        <dependency> 
            <groupId>org.apache.jackrabbit</groupId> 
            <artifactId>jackrabbit-core</artifactId> 
            <version>2.12.1</version>
        </dependency> 
        
        <!-- Use Log4J for logging --> 
        <dependency> 
            <groupId>org.slf4j</groupId> 
            <artifactId>slf4j-log4j12</artifactId> 
            <version>1.5.11</version> 
        </dependency> 
    </dependencies> 


You probably have an error in your classpath settings if you get a
`ClassNotFoundException` message when trying to compile or run the
examples below. 


Hop 1: Logging in to Jackrabbit
-------------------------------
So let's get started. As a warm-up we'll create a Jackrabbit content
repository and start a login session for accessing it. The full example
application that does this is shown below, with line-by-line explanations
following shortly after. 

    import javax.jcr.GuestCredentials;
    import javax.jcr.Repository;
    import javax.jcr.Session; 
    import org.apache.jackrabbit.commons.JcrUtils;
    
    /** 
    * First hop example. Logs in to a content repository and prints a 
    * status message. 
    */ 
    public class FirstHop { 
    
        /** 
        * The main entry point of the example application. 
        * 
        * @param args command line arguments (ignored) 
        * @throws Exception if an error occurs 
        */ 
        public static void main(String[] args) throws Exception { 
            Repository repository = JcrUtils.getRepository();
            Session session = repository.login(new GuestCredentials());
            try { 
                String user = session.getUserID(); 
                String name = repository.getDescriptor(Repository.REP_NAME_DESC); 
                System.out.println( 
                "Logged in as " + user + " to a " + name + " repository."); 
            } finally { 
                session.logout(); 
            } 
        } 
    } 

You can also download the source file as `FirstHop.java`. If you have your
classpath set up, you can compile the application with javac `FirstHop.java`
and run it with java FirstHop to get the following output. 

    Logged in as anonymous to a Jackrabbit repository. 


In addition to producing the above status line the application copies a
default repository configuration file to `repository.xml` and creates an
initial Jackrabbit content repository in the `jackrabbit` subdirectory. You
can use the system properties `org.apache.jackrabbit.repository.conf` and
`org.apache.jackrabbit.repository.home` to set alternative configuration
file and repository directory locations. 

Read on for a detailed breakdown of the FirstHop application: 

    import javax.jcr.Repository; 
    import javax.jcr.Session; 


The JCR API interfaces are located in the javax.jcr package found in the
jcr-2.0.jar library. The promise of the JCR API is that if you only use
these interfaces in your content application, it should remain mostly
independent of the underlying content repository implementation. 

The [Repository](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Repository.html?is-external=true)
interface represents a given content repository instance and the [Session](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Session.html?is-external=true)
interface represents a single login session for accessing the repository.
A session is needed to access any content within a repository. 

Note that a Session instance is not guaranteed to be thread-safe so you
should start multiple sessions if you need to access repository content
simultaneously from different threads. This is especially important for
things like web applications. 

    import org.apache.jackrabbit.commons.JcrUtils;


The best practice for deploying Jackrabbit is to use JNDI or some other
configuration mechanism in a container environment to keep the application
code free of direct Jackrabbit dependencies, but since we are creating a
simple standalone application we can take a shortcut by using the [JcrUtils](http://jackrabbit.apache.org/api/2.10/org/apache/jackrabbit/commons/JcrUtils.html)
class from Jackrabbit commons.

    public class FirstHop 
    public static void main(String[] args) throws Exception 


The FirstHop example is a simple standalone application that fits nicely in
the `main()` method and lets the JVM take care of the possible exceptions.
More substantial content applications could also be written as web
application or EJB components with different setup and error handling
patterns. 

    Repository repository = JcrUtils.getRepository();


The `JcrUtils.getRepository()` method returns an object that implements the
JCR Repository interface. The actual implementation depends on the jar files
available on the classpath and in this example is a [TransientRepository](http://jackrabbit.apache.org/api/2.10/org/apache/jackrabbit/core/TransientRepository.html).
The implementation contains a utility feature that will take
care of the initial configuration and repository construction when the
first session is started. Thus there is no need for manual configuration
for now unless you want direct control over the repository setup. 

The `TransientRepository` implementation will automatically initialize the
content repository when the first session is started and shut it down when
the last session is closed. Thus there is no need for explicit repository
shutdown as long as all sessions are properly closed. Note that a
Jackrabbit repository directory contains a lock file that prevents it from
being accessed simultaneously by multiple processes. You will see
repository startup exceptions caused by the lock file if you fail to
properly close all sessions or otherwise shut down the repository before
leaving the process that accesses a repository. Normally you can just
manually remove the lock file in such cases but such cases always present a
chance of repository corruption especially if you use a non-transactional
persistence manager. 

    Session session = repository.login(new GuestCredentials());


The `Repository.login(Credentials)` method starts a repository session using the
default workspace and some user credentials. The FirstHop example uses [GuestCredentials](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/GuestCredentials.html?is-external=true)
and Jackrabbit maps it to the read-only anonymous user.

Since we use the `TransientRepository` class as the Repository
implementation, this step will also cause the repository to be initialized. 

    try { ... } finally { session.logout(); } 


It is a good practice to properly release all acquired resources, and the
JCR sessions are no exception. The try-finally idiom is a good way to
ensure that a resource really gets released, as the release method gets
called even if the intervening code throws an exception or otherwise jumps
outside the scope (for example using a return, break, or continue
statement). 

The `Session.logout()` method in the finally branch closes the session and
since this is the only session we have started, the TransientRepository is
automatically shut down. 

    String user = session.getUserID(); 


The username or identifier of the user associated with a session is
available using the `Session.getUserID()` method. Jackrabbit returns
`"anonymous"` by default. 

    String name = repository.getDescriptor(Repository.REP_NAME_DESC); 


Each content repository implementation publishes a number of string
descriptors that describe the various implementation properties, like the
implementation level and the supported optional JCR features. See the [Repository](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Repository.html?is-external=true)
interface for a list of the standard repository descriptors. The
`REP_NAME_DESC` descriptor contains the name of the repository
implementation, in this case `"Jackrabbit"`. 


Hop 2: Working with content
---------------------------
The main function of a content repository is allow applications to store
and retrieve content. The content in a JCR content repository consists of
structured or unstructured data modeled as a hierarchy of nodes with
properties that contain the actual data. 

The following example application first stores some content to the
initially empty content repository, then retrieves the stored content and
outputs it, and finally removes the stored content. 

    import javax.jcr.Repository; 
    import javax.jcr.Session; 
    import javax.jcr.SimpleCredentials; 
    import javax.jcr.Node; 
    import org.apache.jackrabbit.commons.JcrUtils;
    
    /** 
    * Second hop example. Stores, retrieves, and removes example content. 
    */ 
    public class SecondHop { 
        
        /** 
        * The main entry point of the example application. 
        * 
        * @param args command line arguments (ignored) 
        * @throws Exception if an error occurs 
        */ 
        public static void main(String[] args) throws Exception { 
        Repository repository = JcrUtils.getRepository();
            Session session = repository.login( 
            new SimpleCredentials("admin", "admin".toCharArray()));
            try { 
                Node root = session.getRootNode(); 
                
                // Store content 
                Node hello = root.addNode("hello"); 
                Node world = hello.addNode("world"); 
                world.setProperty("message", "Hello, World!"); 
                session.save(); 
                
                // Retrieve content 
                Node node = root.getNode("hello/world"); 
                System.out.println(node.getPath()); 
                System.out.println(node.getProperty("message").getString()); 
                
                // Remove content 
                root.getNode("hello").remove(); 
                session.save(); 
            } finally { 
                session.logout(); 
            } 
        } 
        
    } 


Like in the first hop, this example source is also available as
SecondHop.java. You can also compile and run this class just like you did
in the first hop example. Running this example should produce the following
output: 

    /hello/world 
    Hello, World! 


The basic structure of this example application is the same as in the First
Hop example, so let's just walk through the differences: 

    import javax.jcr.SimpleCredentials; 
    import javax.jcr.Node; 


These are two new classes we need for this example. The [SimpleCredentials](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/SimpleCredentials.html?is-external=true)
class is a simple implementation of the [Credentials](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Credentials.html?is-external=true)
interface used for passing explicit user credentials to the
`Repository.login(Credentials)` method. 

The [Node](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Node.html?is-external=true)
interface is used to manage the content nodes in a repository. There is a
related interface called [Property](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Property.html?is-external=true)
for managing content properties, but in this example we use the Property
interface only indirectly. 

    new SimpleCredentials("admin", "admin".toCharArray())


As discussed in the First Hop example, a login with `GuestCredentials`
returns an anonymous read-only session in the Jackrabbit default
configuration. To be able to store and remove content we need to create a
session with write access, and to do that we need to pass credentials with
a username and password to the

    Repository.login(Credentials credentials) method. 


The default Jackrabbit login mechanism accepts only username and password as
valid credentials for known users. A Jackrabbit repository with a default
configuration will create an admin user when it is first initialized. Thus we
need to construct and use a SimpleCredentials instance with the username and
initial default password of the admin user, in this case `"admin"` and `"admin"`.

The SimpleCredentials constructor follows the JAAS convention of
representing the username as a normal String, but the password as a
character array, so we need to use the `String.toCharArray()` method to
satisfy the constructor. 


    Node root = session.getRootNode(); 


Each JCR session is associated with a workspace that contains a single node
tree. A simple way to access the root node is to call the
`Session.getRootNode()` method. Having a reference to the root node allows us
to easily store and retrieve content in the current workspace. 

    Node hello = root.addNode("hello"); 
    Node world = hello.addNode("world"); 


New content nodes can be added using the `Node.addNode(String relPath)`
method. The method takes the name (or relative path) of the node to be
added and creates the named node in the transient storage associated with
the current session. Until the transient storage is persisted, the added
node is only visible within the current session and not within any other
session that is concurrently accessing the content repository. 

This code snippet creates two new nodes, called `"hello"` and `"world"`, with
`"hello"` being a child of the root node and `"world"` a child of the `"hello"`
node. 

    world.setProperty("message", "Hello, World!"); 


To add some content to the structure created using the `"hello"` and `"world"`
nodes, we use the `Node.setProperty(String name, String value)` method to add
a string property called `"message"` to the `"world"` node. The value of the
property is the string `"Hello, World!"`. 

Like the added nodes, also the property is first created in the transient
storage associated with the current session. If the named property already
exists, then this method will change the value of that property. 

    session.save(); 


Even though the rest of our example would work just fine using only the
transient storage of the single session, we'd like to persist the changes
we've made so far. This way other sessions could also access the example
content we just created. If you like, you could even split the example
application into three pieces for respectively storing, retrieving, and
removing the example content. Such a split would not work unless we
persisted the changes we make. 

The `Session.save()` method persists all pending changes in the transient
storage. The changes are written to the persistent repository storage and
they become visible to all sessions accessing the same workspace. Without
this call all changes will be lost forever when the session is closed. 

    Node node = root.getNode("hello/world"); 


Since we are still using the same session, we could use the existing hello
and world node references to access the stored content, but let's pretend
that we've started another session and want to retrieve the content that
was previously stored. 

The `Node.getNode(String relPath)` method returns a reference to the node at
the given path relative to this node. The path syntax follows common file
system conventions: a forward slash separates node names, a single dot
represents the current node, and a double dot the parent node. Thus the
path `"hello/world"` identifies the `"world"` child node of the `"hello"` child
node of the current node - in this case the root node. The end result is
that the method returns a node instance that represents the same content
node as the world instance created a few lines earlier. 

    System.out.println(node.getPath()); 


Each content node and property is uniquely identified by its absolute path
within the workspace. The absolute path starts with a forward slash and
contains all the names of the ancestor nodes in order before the name of
the current node or property. 

The path of a node or property can be retrieved using the Item.getPath()
method. The [Item](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Item.html?is-external=true)
interface is a superinterface of Node and Property, and contains all the
functionality shared by nodes and properties. 

The node variable references the `"world"` node, so this statement will
output the line `"/hello/world"`. 

    System.out.println(node.getProperty("message").getString()); 


Properties can be accessed using the `Node.getProperty(String relPath)`
method that returns an instance of the [Property](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/Property.html?is-external=true)
interface that represents the property at the given path relative to the
current node. In this case the "message" property is the one we created a
few lines earlier. 

A JCR property can contain either a single or multiple values of a given
type. There are property types for storing strings, numbers, dates, binary
streams, node references, etc. We just want the single string value, so we
use the `Property.getString()` method. The result of this statement is the
line `"Hello, World!"` being outputted. 

    root.getNode("hello").remove(); 


Nodes and properties can be removed using the`Item.remove()` method. The
method removes the entire content subtree, so we only need to remove the
topmost `"hello"` node to get rid of all the content we added before. 

Removals are first stored in the session-local transient storage, just like
added and changed content. Like before, the transient changes need to be
explicitly saved for the content to be removed from the persistent storage. 


Hop 3: Importing content
------------------------
TODO: Update to match the style of previous hops. 

To add content a bit more efficiently, you may want to try JCR's import
facilities, such as Session.importXML. The following XML document by
Elliotte Rusty Harold provides an interesting example that demonstrates a
repository's namespace capabilities: 

**test.xml**

    <xhtml:html xmlns:xhtml="http://www.w3.org/1999/xhtml" 
    xmlns:mathml="http://www.w3.org/1998/Math/MathML"> 
    <xhtml:head><xhtml:title>Three Namespaces</xhtml:title></xhtml:head> 
    <xhtml:body> 
    <xhtml:h1 align="center">An Ellipse and a Rectangle</xhtml:h1> 
    <svg:svg xmlns:svg="http://www.w3.org/2000/svg" 
    width="12cm" height="10cm"> 
    <svg:ellipse rx="110" ry="130" /> 
    <svg:rect x="4cm" y="1cm" width="3cm" height="6cm" /> 
    </svg:svg> 
    <xhtml:p>The equation for ellipses</xhtml:p> 
    <mathml:math> 
    <mathml:apply> 
    <mathml:eq/> 
    <mathml:cn> 1 </mathml:cn> 
    <mathml:apply> 
    <mathml:plus/> 
    <mathml:apply> 
    <mathml:divide/> 
    <mathml:apply> 
    <mathml:power/> 
    <mathml:ci> x </mathml:ci> 
    <mathml:cn> 2 </mathml:cn> 
    </mathml:apply> 
    <mathml:apply> 
    <mathml:power/> 
    <mathml:ci> a </mathml:ci> 
    <mathml:cn> 2 </mathml:cn> 
    </mathml:apply> 
    </mathml:apply> 
    <mathml:apply> 
    <mathml:divide/> 
    <mathml:apply> 
    <mathml:power/> 
    <mathml:ci> y </mathml:ci> 
    <mathml:cn> 2 </mathml:cn> 
    </mathml:apply> 
    <mathml:apply> 
    <mathml:power/> 
    <mathml:ci> b </mathml:ci> 
    <mathml:cn> 2 </mathml:cn> 
    </mathml:apply> 
    </mathml:apply> 
    </mathml:apply> 
    </mathml:apply> 
    </mathml:math> 
    <xhtml:hr/> 
    <xhtml:p>Last Modified January 10, 2002</xhtml:p> 
    </xhtml:body> 
    </xhtml:html> 


The third example application shown below will import the XML file called
`test.xml` from the current directory into a new content repository node
called `importxml`. Once the XML content is imported, the application
recursively dumps the contents of the entire workspace using the simple
`dump()` method. 

    import javax.jcr.*; 
    import java.io.FileInputStream;
    import org.apache.jackrabbit.commons.JcrUtils;

    /** 
    * Third Jackrabbit example application. Imports an example XML file 
    * and outputs the contents of the entire workspace. 
    */ 
    public class ThirdHop { 
    
        /**
        * The main entry point of the example application.
        *
        * @param args command line arguments (ignored)
        * @throws Exception if an error occurs
        */
        public static void main(String[] args) throws Exception { 
            Repository repository = JcrUtils.getRepository();
                Session session = repository.login( 
                new SimpleCredentials("admin", "admin".toCharArray()));
                try { 
                    Node root = session.getRootNode(); 
                    
                    // Import the XML file unless already imported 
                    if (!root.hasNode("importxml")) { 
                        System.out.print("Importing xml... "); 
                        
                        // Create an unstructured node under which to import the XML 
                        Node node = root.addNode("importxml", "nt:unstructured"); 
                        
                        // Import the file "test.xml" under the created node 
                        FileInputStream xml = new FileInputStream("test.xml");
                        session.importXML( 
                        node.getPath(), xml, ImportUUIDBehavior.IMPORT_UUID_CREATE_NEW); 
                        xml.close();
                        session.save(); 
                        System.out.println("done."); 
                    } 
                    
                    //output the repository content
                    dump(root); 
                } finally { 
                    session.logout(); 
                } 
            } 
        
        /** Recursively outputs the contents of the given node. */ 
        private static void dump(Node node) throws RepositoryException { 
            // First output the node path 
            System.out.println(node.getPath()); 
            // Skip the virtual (and large!) jcr:system subtree 
            if (node.getName().equals("jcr:system")) { 
                return; 
            } 
            
            // Then output the properties 
            PropertyIterator properties = node.getProperties(); 
            while (properties.hasNext()) { 
                Property property = properties.nextProperty(); 
                if (property.getDefinition().isMultiple()) { 
                    // A multi-valued property, print all values 
                    Value[] values = property.getValues(); 
                    for (int i = 0; i < values.length; i++) { 
                        System.out.println( 
                        property.getPath() + " = " + values[i] .getString()); 
                    } 
                } else { 
                    // A single-valued property 
                    System.out.println( 
                    property.getPath() + " = " + property.getString()); 
                } 
            } 
                
            // Finally output all the child nodes recursively 
            NodeIterator nodes = node.getNodes(); 
            while (nodes.hasNext()) { 
                dump(nodes.nextNode()); 
            } 
        } 
    } 


Running the ThirdHop class should produce output like the following: 


    Importing XML... done. 
    / 
    /jcr:primaryType=rep:root 
    /jcr:system 
    /importxml 
    /importxml/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html 
    /importxml/xhtml:html/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:head 
    /importxml/xhtml:html/xhtml:head/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:head/xhtml:title 
    /importxml/xhtml:html/xhtml:head/xhtml:title/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:head/xhtml:title/jcr:xmltext 
    /importxml/xhtml:html/xhtml:head/xhtml:title/jcr:xmltext/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:head/xhtml:title/jcr:xmltext/jcr:xmlcharacters=Three Namespaces 
    /importxml/xhtml:html/xhtml:body 
    /importxml/xhtml:html/xhtml:body/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:body/xhtml:h1 
    /importxml/xhtml:html/xhtml:body/xhtml:h1/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:body/xhtml:h1/align=center 
    /importxml/xhtml:html/xhtml:body/xhtml:h1/jcr:xmltext 
    /importxml/xhtml:html/xhtml:body/xhtml:h1/jcr:xmltext/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:body/xhtml:h1/jcr:xmltext/jcr:xmlcharacters=An Ellipse and a Rectangle 
    /importxml/xhtml:html/xhtml:body/svg:svg 
    /importxml/xhtml:html/xhtml:body/svg:svg/jcr:primaryType=nt:unstructured 
    /importxml/xhtml:html/xhtml:body/svg:svg/width=12cm 
    /importxml/xhtml:html/xhtml:body/svg:svg/height=10cm 
    . 
    . 
    . 


This hop has a lot of similarities with the Second Hop example: we create a
new session with write access by logging in, next we insert data into the
repository, this time by importing an xml file and finally we output the
entire repository content.

By now you should be familiar with logging into a repository
(Repository.login), creating a new node (Node.addNode) under the repository
root (Session.getRootNode) and saving the session so that our changes are
persisted (Session.save).

Let us look at the new methods used in this example, how to import xml
content:

    session.importXML(node.getPath(), xml, ImportUUIDBehavior.IMPORT_UUID_CREATE_NEW);


This deserializes an XML document and adds the resulting item subgraph as a
child of the node at the provided path.

The flag [ImportUUIDBehavior](https://s.apache.org/jcr-2.0-javadoc/javax/jcr/ImportUUIDBehavior.html?is-external=true)
governs how the identifiers of incoming nodes are handled. 

There are four options: 

* `ImportUUIDBehavior.IMPORT_UUID_CREATE_NEW`:  
    Incoming nodes are added in
    the same way that new node is added with Node.addNode. That is, they are
    either assigned newly created identifiers upon addition or upon save. In
    either case, identifier collisions will not occur. 

* `ImportUUIDBehavior.IMPORT_UUID_COLLISION_REMOVE_EXISTING`:  
    If an incoming
    node has the same identifier as a node already existing in the workspace
    then the already existing node (and its subgraph) is removed from wherever
    it may be in the workspace before the incoming node is added. Note that
    this can result in nodes "disappearing" from locations in the workspace
    that are remote from the location to which the incoming subgraph is being
    written. Both the removal and the new addition will be dispatched on save.

* `ImportUUIDBehavior.IMPORT_UUID_COLLISION_REPLACE_EXISTING`:  
    If an incoming
    node has the same identifier as a node already existing in the workspace,
    then the already-existing node is replaced by the incoming node in the same
    position as the existing node. Note that this may result in the incoming
    subgraph being disaggregated and "spread around" to different locations in
    the workspace. In the most extreme case this behavior may result in no node
    at all being added as child of parentAbsPath. This will occur if the
    topmost element of the incoming XML has the same identifier as an existing
    node elsewhere in the workspace. The change will be dispatched on save.

* `ImportUUIDBehavior.IMPORT_UUID_COLLISION_THROW`:  
    If an incoming node has
    the same identifier as a node already existing in the workspace then an
    ItemExistsException is thrown.


Another interesting method is 

    void dump(Node node)


This can be used as an example of how to do a recursive traversal of all
the repository, and check the properties of each node. 

Notice how we have to pay special attention to the multi-value properties,
because that impacts the way we use them:

    property.getDefinition().isMultiple()


if this yields true, then we are dealing with an array of values:

    Value[] values = property.getValues();


or else, we can use the provided api shortcuts, to get the desired value:

    property.getString()


which is equivalent to 

    property.getValue().getString()


A very good entry point for utilities related code examples is [JcrUtils](http://jackrabbit.apache.org/api/2.10/org/apache/jackrabbit/commons/JcrUtils.html).
