Title: Jackrabbit JCR Server
This is the JCR Server component of the Apache Jackrabbit project. This
component contains two WebDAV based JCR server implementations:
* Simple Webdav Server
* JCR Webdav Server

<a name="JackrabbitJCRServer-SimpleWebdavServer"></a>
### Simple Webdav Server

WebDAV (conformance levels 1, 2, and 3) and DeltaV compliant WebDAV server
implementation to access a JSR170 repository.

Futher information such as configuration as well as the
_SimpleWebdavServlet.java_ itself can be found in the [Jackrabbit Web Application](jackrabbit-web-application.html)
 project.
* Packages:
<table>
<tr><td> org.apache.jackrabbit.server </td><td> Common server functionality </td></tr>
<tr><td> org.apache.jackrabbit.server.io </td><td> Import and export facilities </td></tr>
<tr><td> org.apache.jackrabbit.webdav.simple </td><td> Server side WebDAV implementation
(DavResource, ResourceConfig,...). </td></tr>
* Servlet:
<tr><td> org.apache.jackrabbit.j2ee.SimpleWebdavServlet.java </td><td> see [Jackrabbit Web Application](jackrabbit-web-application.html)
 </td></tr>
</table>

Note thatn when run on top of a JCR 2.0 implementation that also supports
shareable nodes, the WebDAV BIND specification
([http://tools.ietf.org/html/draft-ietf-webdav-bind](http://tools.ietf.org/html/draft-ietf-webdav-bind)
) is also supported.

<a name="JackrabbitJCRServer-JCRWebdavServer"></a>
### JCR Webdav Server

Server used to remote JSR170 calls via WebDAV.

The client counterpart of this server is represented by the JCR to SPI
project in combination with the _SPI to WebDAV_ SPI implementation that can
be found in the [Jackrabbit SPI to DAV](jackrabbit-spi-to-dav.html)
 project. Easy to use setup of both components can be found in [Jackrabbit JCR to DAV]
 and [Jackrabbit JCR Client]
, respectively.
* Packages:
<table>
<tr><td> org.apache.jackrabbit.server </td><td> Common server functionality </td></tr>
<tr><td> org.apache.jackrabbit.server.jcr </td><td> JCR-Server </td></tr>
<tr><td> org.apache.jackrabbit.webdav.jcr </td><td> Server side WebDAV implementation
(DavResources, Reports, Properties) </td></tr>
* Servlet:
<tr><td> org.apache.jackrabbit.j2ee.JCRServerServlet.java </td><td> see [Jackrabbit Web Application](jackrabbit-web-application.html)
</td></tr>
</table>

Further reading:
* http://jackrabbit.apache.org/JCR_Webdav_Protocol.doc
