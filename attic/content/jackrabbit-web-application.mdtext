Title: Jackrabbit Web Application
This is the Web Application component of the Apache Jackrabbit project.
This component provides servlets used to access a Jackrabbit repository:
* [RepositoryAccessServlet.java](http://jackrabbit.apache.org/api/1.4/org/apache/jackrabbit/j2ee/RepositoryAccessServlet.html)
* [LoggingServlet.java](http://jackrabbit.apache.org/api/1.4/org/apache/jackrabbit/j2ee/LoggingServlet.html)
* [RepositoryStartupServlet.java](http://jackrabbit.apache.org/api/1.4/org/apache/jackrabbit/j2ee/RepositoryStartupServlet.html)

In addition, the project contains 2 different WebDAV servlets:
* [SimpleWebdavServlet.java](http://jackrabbit.apache.org/api/1.4/org/apache/jackrabbit/webdav/simple/SimpleWebdavServlet.html)
* [JCRWebdavServerServlet.java](http://jackrabbit.apache.org/api/1.4/org/apache/jackrabbit/webdav/jcr/JCRWebdavServerServlet.html)

All servlets are configured in the [web.xml](https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbit-webapp/src/main/webapp/WEB-INF/web.xml)
 of the jackrabbit-webapp. It provides a good overview of the available
options.

<a name="JackrabbitWebApplication-SimpleWebdavServer"></a>
### Simple Webdav Server

Adds WebDAV support (DAV 1,2 and DeltaV) to your jackrabbit repository.

The servlet configuration goes along with a [config.xml](https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbit-webapp/src/main/webapp/WEB-INF/config.xml)
 that provides additional configuration options for the WebDAV resources
including import and export behaviour for both resources and their
properties, mime type and nodetype mappings and simple item filters.

<a name="JackrabbitWebApplication-JCRWebdavServer"></a>
### JCR Webdav Server

A servlet used to remote JSR170 calls via webDAV.

IMPORTANT: Please note, that this servlet is not intended to provide common
WebDAV support to the repository. Instead the primary goal is to remote
JSR170 calls.

For the corresponding JCR client see JCR to SPI and the _SPI to WebDAV_
contribution inside the Jackrabbit sandbox.
