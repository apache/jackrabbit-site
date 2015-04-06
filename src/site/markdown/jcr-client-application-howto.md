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

JCR client application HOWTO
============================
This document describes the common configuration and initialization code of
a client application that uses a JCR content repository. The application
setup does not depend on the underlying deployment model, implementation,
or configuration of the content repository.

The instructions in this document apply to a J2EE web application that uses
JNDI to access the content repository. It should however be easy to modify
the instructions for other container environments.


J2EE web application instructions
---------------------------------
Follow the steps below to access a JNDI-bound content repository within a
J2EE web application. Example code is included after this overview. See the
deployment model howtos for instructions on how to create the JNDI bindings
for the standard deployment models.

1. Place the JCR API jar in the `WEB-INF/lib` subdirectory of your web application.
1. Declare the JNDI address under which you will request the repository instance in the deployment descriptor.
1. Code your application to use the resource.

Note that that none of your code or configuration needs to depend on the
underlying repository implementation or deployment model. All those details
are handled by the container and can easily be changed without modifying
your application. Just make sure that you have documented the JCR
repository level and optional features your application requires so that
your application can be deployed in an appropriate environment.

### Step 2 - Deployment descriptor
Add the following snippet in your web.xml deployment descriptor to declare
your application's use of a content repository resource.

    <resource-env-ref>
      <description>Content Repository</description>
      <resource-env-ref-name>jcr/repository</resource-env-ref-name>
      <resource-env-ref-type>javax.jcr.Repository</resource-env-ref-type>
    </resource-env-ref>

Note that the `java:comp/env/jcr` subcontext is the preferred naming context
for JCR content repository resources.

### Step 3 - Java code
Use the following Java code snippet to get a reference to the configured
content repository instance.

    InitialContext context = new InitialContext();
    Context environment = (Context) context.lookup("java:comp/env");
    Repository repository = (Repository) environment.lookup("jcr/repository");

