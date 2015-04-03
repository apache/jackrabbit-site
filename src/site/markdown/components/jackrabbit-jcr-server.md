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

Jackrabbit JCR Server
=====================
This is the JCR Server component of the Apache Jackrabbit project. 
This component contains two WebDAV based JCR server implementations:

* Simple Webdav Server
* JCR Webdav Server


Simple Webdav Server
--------------------
WebDAV (conformance levels 1, 2, and 3) and DeltaV compliant WebDAV server
implementation to access a JSR170 repository.

Further information such as configuration as well as the
`SimpleWebdavServlet.java` itself can be found in the [Jackrabbit Web Application](jackrabbit-web-application.html) project.

#### Packages:

|------------------------------------|----------------------------|
| org.apache.jackrabbit.server       | Common server functionality|
| org.apache.jackrabbit.server.io    | Import and export facilities|
| org.apache.jackrabbit.webdav.simple| Server side WebDAV implementation (DavResource, ResourceConfig,...)|

#### Servlet:

|-----------------------------------------------------|-------------------------------------------------------------------|
| org.apache.jackrabbit.j2ee.SimpleWebdavServlet.java | see [Jackrabbit Web Application](jackrabbit-web-application.html) |

Note that when run on top of a JCR 2.0 implementation that also supports shareable nodes, the WebDAV BIND specification
([http://tools.ietf.org/html/draft-ietf-webdav-bind](http://tools.ietf.org/html/draft-ietf-webdav-bind)) is also supported.


JCR Webdav Server
-----------------
Server used to remote JSR170 calls via WebDAV.

The client counterpart of this server is represented by the JCR to SPI
project in combination with the _SPI to WebDAV_ SPI implementation that can
be found in the [Jackrabbit SPI to DAV](jackrabbit-spi-to-dav.html) project. 
Easy to use setup of both components can be found in [Jackrabbit JCR to DAV]
and [Jackrabbit JCR Client], respectively.

#### Packages:

|------------------------------------|---------------------------|
| org.apache.jackrabbit.server       | Common server functionality |
| org.apache.jackrabbit.server.jcr   | JCR-Server |
| org.apache.jackrabbit.webdav.jcr   | Server side WebDAV implementation (DavResources, Reports, Properties) |

#### Servlet:

|-----------------------------------|---------------------------|
| org.apache.jackrabbit.j2ee.JCRServerServlet.java | see [Jackrabbit Web Application](jackrabbit-web-application.html) |


Further reading:

* http://jackrabbit.apache.org/JCR_Webdav_Protocol.doc
