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

Jackrabbit Configuration
========================

Apache Jackrabbit needs two pieces of information to set up a runtime
content repository instance:

* **Repository home directory**   
    The filesystem path of the directory
    containing the content repository accessed by the runtime instance of
    Jackrabbit. This directory usually contains all the repository content,
    search indexes, internal configuration, and other persistent information
    managed within the content repository. Note that this is not absolutely
    required and some persistence managers and other Jackrabbit components may
    well be configured to access files and even other resources (like remote
    databases) outside the repository home directory. A designated repository
    home directory is however always needed even if some components choose to
    not use it. Jackrabbit will automatically fill in the repository home
    directory with all the required files and subdirectories when the
    repository is first instantiated.

* **Repository configuration file**   
    The filesystem path of the repository
    configuration XML file. This file specifies the class names and properties
    of the various Jackrabbit components used to manage and access the content
    repository. Jackrabbit parses this configuration file and instantiates the
    specified components when the runtime content repository instance is
    created.

These two configuration parameters are passed either directly to Jackrabbit
when creating a repository instance or indirectly through settings for a
JNDI object factory or some other component management system.

Note that since Jackrabbit 2.22.1, JNDI is disabled by default. If you want to
use JNDI, you need to set the system property `jackrabbit.jndi.enabled` to `true`.

For each workspace that was created, there will also be a `workspace.xml`
file created inside the workspace home directory that will be used for the
workspace - these files have to be changed, too, because the
workspace-specific configuration inside repository.xml is only used as a
template for new workspaces, ie. if you use the `createWorkspace()`
method of the Jackrabbit API, the `workspace.xml` is just a copy of the [Workspace](#workspace-configuration)
element inside `repository.xml`. You can also manually create the workspace
folder with a workspace.xml file to create a new workspace yourself (Please
note that depending on the [persistence manager](#persistence-configuration)
you will also have to setup a database and configure the access to it).


Repository configuration
------------------------
The repository configuration file, typically called `repository.xml`,
specifies global options like security, versioning and clustering settings.
A default workspace configuration template is also included in the
repository configuration file. The exact format of this XML configuration
file is defined in the following document type definition (DTD) files
published by the Apache Jackrabbit project.

* [-//The Apache Software Foundation//DTD Jackrabbit 1.5//EN](http://jackrabbit.apache.org/dtd/repository-1.5.dtd)
* [-//The Apache Software Foundation//DTD Jackrabbit 1.4//EN](http://jackrabbit.apache.org/dtd/repository-1.4.dtd)
* [-//The Apache Software Foundation//DTD Jackrabbit 1.2//EN](http://jackrabbit.apache.org/dtd/repository-1.2.dtd)
* [-//The Apache Software Foundation//DTD Jackrabbit 1.0//EN](http://jackrabbit.apache.org/dtd/repository-1.0.dtd)

All Jackrabbit 1.x versions are fully backwards compatible, so you can use
a recent Jackrabbit version without having to modify your existing
repository configuration. Of course you will need to make configuration
changes if you want to enable new features like the data store introduced
in Jackrabbit 1.4.

The top-level structure of the repository configuration file is shown
below. The `<!DOCTYPE>` declaration is optional, but if you include it
Jackrabbit 1.5 will use XML validation to make sure that the configuration
file is correctly formatted.

    <!DOCTYPE Repository
    	  PUBLIC "-//The Apache Software Foundation//DTD Jackrabbit 1.5//EN"
    	  "http://jackrabbit.apache.org/dtd/repository-1.5.dtd">
    <Repository>
      <FileSystem .../>
      <Security .../>
      <Workspaces .../>
      <Workspace .../>
      <Versioning .../>
      <SearchIndex .../>  <!-- optional -->
      <Cluster .../>	  <!-- optional, available since 1.2 -->
      <DataStore .../>	  <!-- optional, available since 1.4 -->
    </Repository>


Starting with Jackrabbit 1.5, the order of the configuration elements below
`<Repository/>` is now fixed.

The repository configuration elements are:

* [FileSystem](#file-system-configuration): The virtual file system used by the repository to store things like registered namespaces and node types.
* [Security](#security-configuration): Authentication and authorization configuration.
* [Workspaces](#workspace-configuration): Configuration on where and how workspaces are managed.
* [Workspace](#workspace-configuration): Default workspace configuration template.
* [Versioning](#versioning-configuration):  Configuration of the repository-wide version store.
* [SearchIndex](#search-configuration): Configuration of the search index that covers the repository-wide `/jcr:system` content tree. 
* [Cluster](#cluster-configuration): Clustering configuration.
* [DataStore](#data-store-configuration): Data store configuration.

See the Jackrabbit 1.5 [default configuration](repository.xml) , for an example repository configuration file.

> It is a good idea to place the `repository.xml` file _inside_ the
> repository home directory. This keeps your repository and its configuration
> nicely contained within a single directory tree.

### Bean configuration elements
Most of the entries in the configuration file are based on the following
generic JavaBean configuration pattern. Such configuration specifies that
the repository should use an instance of the specified class with the
specified properties for the named functionality.

    <ConfigurationElement class="fully.qualified.ClassName">
      <param name="property1" value="...">
      <param name="property2" value="...">
    <ConfigurationElement>


### Configuration variables
Jackrabbit supports configuration variables of the form `${name}`. These
variables can be used to avoid hardcoding specific options in the
configuration files. The following variables are available in all
Jackrabbit versions:

* `${rep.home}`: Repository home directory.
* `${wsp.name}`: Workspace name. Only available in workspace configuration.
* `${wsp.home}`: Workspace home directory. Only available in workspace configuration.

Since Jackrabbit 1.4 (see [JCR-1304](https://issues.apache.org/jira/browse/JCR-1304)) 
it has been possible to use system properties or any application-specific
settings as configuration variables.

<a name="security-configuration"></a>
Security configuration
-----------------------
The security configuration element is used to specify authentication and
authorization settings for the repository. The structure of the security
configuration element is:

    <Security appName="Jackrabbit">
      <SecurityManager .../>     <!-- optional, available since 1.5 -->
      <AccessManager .../>	 <!-- mandatory until 1.4, optional since 1.5 -->
      <LoginModule .../>	 <!-- optional -->
    </Security>


By default Jackrabbit uses the [Java Authentication and Authorization Service](http://java.sun.com/j2se/1.4.2/docs/guide/security/jaas/JAASRefGuide.html)
(JAAS) to authenticate users who try to access the repository. The
`appName` parameter in the `<Security/>` element is used as the JAAS
application name of the repository.

If JAAS authentication is not available or (as is often the case) too
complex to set up, Jackrabbit allows you to specify a repository-specific
JAAS [LoginModule](http://java.sun.com/j2se/1.4.2/docs/api/javax/security/auth/spi/LoginModule.html)
that is then used for authenticating repository users. The default [SimpleLoginModule](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/security/SimpleLoginModule.html)
class included in Jackrabbit implements a trivially simple authentication
mechanism that accepts any username and any password as valid
authentication credentials.

Once a user has been authenticated, Jackrabbit will use the configured [AccessManager](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/security/AccessManager.html)
to control what parts of the repository content the user is allowed to
access and modify. The default [SimpleAccessManager|http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/security/SimpleAccessManager.html]
class included in Jackrabbit implements a trivially simple authorization
mechanism that grants full read access to all users and write access to
everyone except anonymous users.

The slightly more advanced [SimpleJBossAccessManager](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/security/SimpleJBossAccessManager.html)
class was added in Jackrabbit 1.3 (see [JCR-650](https://issues.apache.org/jira/browse/JCR-650)). 
This class is designed for use with the [JBoss Application Server](http://www.jboss.org/jbossas/), 
where it maps JBoss roles to Jackrabbit permissions.

<a name="workspace-configuration"></a>
Workspace configuration
-----------------------
A Jackrabbit repository contains one or more workspaces that are each
configured in a separate `workspace.xml` configuration file. The
`Workspaces` element of the repository configuration specifies where and
how the workspaces are managed. The repository configuration also contains
a default workspace configuration template that is used to create the
`workspace.xml` file of a new workspace unless more specific
configuration is given when the workspace is created. See the
`createWorkspace` methods in the [JackrabbitWorkspace](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/api/JackrabbitWorkspace.html)
interface for more details on workspace creating workspaces.

The workspace settings in the repository configuration file are:

    <Workspaces rootPath="${rep.home}/workspaces"
        defaultWorkspace="default"
        configRootPath="..."  <!-- optional -->
        maxIdleTime="..."/>   <!-- optional -->
    <Workspace .../>   <!-- default workspace configuration template -->

The following global workspace configuration options are specified in the `Workspaces` element:

* `rootPath`:   
    The native file system directory for workspaces. A
    subdirectory is automatically created for each workspace, and the path of
    that subdirectory can be used in the workspace configuration as the `${wsp.path}` variable.
* `defaultWorkspace`:   
    Name of the default workspace. This workspace is
    automatically created when the repository is first started.
* `configRootPath`:   
    By default the configuration of each workspace is
    stored in a *workspace.xml* file within the workspace directory within
    the `rootPath` directory. If this option is specified, then the workspace
    configuration files are stored within the specified path in the virtual
    file system (see above) configured for the repository.
* `maxIdleTime`:   
    By default Jackrabbit only releases resources
    associated with an opened workspace when the entire repository is closed.
    This option, if specified, sets the maximum number of seconds that a
    workspace can remain unused before the workspace is automatically closed.

The workspace configuration template and all *workspace.xml*
configuration files have the following structure:

    <Workspace name="${wsp.name}">
        <FileSystem .../>
        <PersistenceManager .../>
        <SearchIndex .../>	      <!-- optional -->
        <ISMLocking .../>	      <!-- optional, available since 1.4 -->
    </Workspace>


The workspace configuration elements are:

* [FileSystem](#file-system-configuration): The virtual file system passed to the persistence manager and search index.
* [PersistenceManager](#persistence-configuration): Persistence configuration for workspace content.
* [SearchIndex](#search-configuration): Configuration of the workspace search index.
* [ISMLocking](#item-state-locking-configuration): Locking configuration for concurrent access to workspace content.

> To modify the configuration of an existing workspace, you need to change
> the `workspace.xml` file of that workspace. Changing the `<Workspace/>`
> element in the repository configuration file will not affect existing
> workspaces.

<a name="versioning-configuration"></a>
Versioning configuration
------------------------
The version histories of all versionable nodes are stored in a
repository-wide version store configured in the `Versioning` element of
the repository configuration. The versioning configuration is much like
workspace configuration as they are both used by Jackrabbit for storing
content. The main difference between versioning and workspace configuration
is that no search index is specified for the version store as version
histories are indexed and searched using the repository-wide search index.
Another difference is that there are no `${wsp.name}` or `${wsp.path}` 
variables for the versioning configuration. Instead the native file system 
path of the version store is explicitly specified in the configuration.

The structure of the versioning configuration is:

    <Versioning rootPath="${rep.home}/version">
      <FileSystem .../>
      <PersistenceManager .../>
      <ISMLocking .../>	      <!-- optional, available since 1.4 -->
    </Versioning>

The versioning configuration elements are:

* [FileSystem](#file-system-configuration): The virtual file system passed to the persistence manager.
* [PersistenceManager](#persistence-configuration): Persistence configuration for the version store.
* [ISMLocking](#item-state-locking-configuration): Locking configuration for concurrent access to workspace content.

<a name="search-configuration"></a>
Search configuration
--------------------
See the [Search](http://jackrabbit.apache.org/archive/wiki/JCR/Search_115513504.html) page on the Jackrabbit wiki.

<a name="persistence-configuration"></a>
Persistence configuration
-------------------------
The Persistence Manager is one of the most important parts of the
configuration, because it actually takes care of storing the nodes and
properties. There are various very different implementations, but most of
them are using databases to store the data. If you use a database PM and
like to connect to an external database, you might also have to setup the
database. This might include access rights for the Jackrabbit database user
to allow creation of tables, because the name of the table typically
depends on the workspace name (see the individual PM's javadoc for more
information).

For large binary properties there is the option to use the [DataStore](#data-store-configuration) 
instead of the Persistence Manager.

For more detailed information and an overview of available PMs, see the [PersistenceManagerFAQ](http://jackrabbit.apache.org/archive/wiki/JCR/PersistenceManagerFAQ_115513487.html)
page on the Jackrabbit wiki.

> If you use a database persistence manager, the configured database
> connection *must not* be under the control of an external transaction
> manager. Jackrabbit implements distributed XA transaction support on a
> higher level, and expects to be in full control of the underlying database
>connection.

<a name="filesystem-configuration"></a>
File system configuration
-------------------------
Early versions on Jackrabbit were designed to abstract their persistence
mechanism using a virtual file system layer defined in the [FileSystem](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/fs/FileSystem.html)
interface. This low-level approach didn't work that well in practice, and
so most of the persistence abstraction is now handled in a higher level.
However, certain parts of Jackrabbit still use this file system
abstraction.

A virtual file system is configured in a `<FileSystem/>` bean
configuration element. See the main file system implementations 
[LocalFileSystem](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/fs/local/LocalFileSystem.html), 
[DatabaseFileSystem](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/fs/db/DatabaseFileSystem.html) (including subclasses), 
and [MemoryFileSystem](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/core/fs/mem/MemoryFileSystem.html)
for the available options. The recommended alternative is to use the
`LocalFileSystem` implementation that simply maps abstract file system
accesses to the specified directory within the native file system.

<a name="cluster-configuration"></a>
Cluster configuration
---------------------
See the [Clustering](http://jackrabbit.apache.org/archive/wiki/JCR/Clustering_115513377.html) page on the Jackrabbit wiki.

<a name="datastore-configuration"></a>
Data store configuration
------------------------
See the [DataStore](http://jackrabbit.apache.org/archive/wiki/JCR/DataStore_115513387.html) page on the Jackrabbit wiki.

<a name="itemstatelocking-configuration"></a>
Item state locking configuration
--------------------------------
TODO

Passwords in configuration (as of Jackrabbit 2.3)
-------------------------------------------------
When using a database-backed persistence manager or another component, you
usually need to include the database password in Jackrabbit configuration.
If you don't want to store such passwords in plain text inside the
configuration file, you can encode the password in base64 and prefix it
with `{base64}`. Jackrabbit will automatically decode such a password
before passing it to the underlying database.

As an example, the following two password configuration parameters are
equivalent ("dGVzdA==" is the base64 encoding of "test"):

    <param name="password" value="test"/>
    <param name="password" value="{base64}dGVzdA=="/>

