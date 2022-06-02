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

Jackrabbit Web Application
==========================
This is the Web Application component of the Apache Jackrabbit project.
This component provides servlets used to access a Jackrabbit repository:

* [RepositoryAccessServlet.java](/api/trunk/org/apache/jackrabbit/j2ee/RepositoryAccessServlet.html)
* [RepositoryStartupServlet.java](/api/trunk/org/apache/jackrabbit/j2ee/RepositoryStartupServlet.html)

In addition, the project contains 2 different WebDAV servlets:

* [SimpleWebdavServlet.java](/api/trunk/org/apache/jackrabbit/webdav/simple/SimpleWebdavServlet.html)
* [JCRWebdavServerServlet.java](/api/trunk/org/apache/jackrabbit/webdav/jcr/JCRWebdavServerServlet.html)

All servlets are configured in the [web.xml](https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbit-webapp/src/main/webapp/WEB-INF/web.xml)
of the jackrabbit-webapp. It provides a good overview of the available options.


Simple Webdav Server
--------------------
Adds WebDAV support (DAV 1,2 and DeltaV) to your jackrabbit repository.

The servlet configuration goes along with a [config.xml](https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbit-webapp/src/main/webapp/WEB-INF/config.xml)
that provides additional configuration options for the WebDAV resources
including import and export behaviour for both resources and their
properties, mime type and nodetype mappings and simple item filters.


JCR Webdav Server
-----------------
A servlet used to remote JSR170 calls via webDAV.

IMPORTANT: Please note, that this servlet is not intended to provide common
WebDAV support to the repository. Instead the primary goal is to remote
JSR170 calls.

For the corresponding JCR client see JCR to SPI and the _SPI to WebDAV_
contribution inside the Jackrabbit sandbox.
