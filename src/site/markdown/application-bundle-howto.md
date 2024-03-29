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

Application Bundle HOWTO
========================
This document describes how to setup a Jackrabbit content repository in the 
deployment model 1; The (Web-) Application Bundle. In this deployment model, 
each application bundle uses its own local content repository that is not 
visible to other applications. See the [JCR client application HOWTO](jcr-client-architecture.html)
for instructions on how to use the configured content repository.

Note that it is also possible to bypass the JNDI mechanism by including all
the Jackrabbit startup and configuration code directly in your application.
This approach however makes a strong binding between your application and
the underlying repository implementation.

The instructions in this document apply to Tomcat versions 4.x and 5.x. It
should be easy to modify the instructions for other container environments.

Important: remember that two Jackrabbit instances should never read
from/write to the same physical storage. This setup is not supported and
will lead to corrupt data.


Tomcat instructions
----------------------
Follow the steps below to setup a model 1 Jackrabbit deployment for your
web application in Tomcat 4.x or 5.x. Example code for both versions of
Tomcat is included after this overview.

1. Place the Jackrabbit jar file and all the dependencies (including the JCR
    API jar file) under `$CATALINA_HOME/webapps/{your_app}/WEB-INF/lib`.
2. Register a bindable repository factory in the context scope. Configure
    the Java class name of the factory implementation, as well as the
    repository configuration file path and the repository home directory path.
    Use the full path in both cases.

Limitations: the application should not be redeployed during the same JVM
process to avoid creating duplicate Jackrabbit instances with the same
configuration. In case you want to redeploy your application be sure to
shutdown the repository when your application is undeployed. It can be done
by calling `RepositoryImpl.shutdown()` (e.g. in the `destroy()` method of a
servlet).


### Step 2 - Context configuration
In Tomcat 4.x and 5.0, add the following snippet in server.xml under the
Context element of your web application.


    <Resource 
        name="jcr/repository"
        auth="Container"
    	type="javax.jcr.Repository"
    />
    
    <ResourceParams name="jcr/repository">
      <parameter>
        <name>factory</name>
        <value>org.apache.jackrabbit.core.jndi.BindableRepositoryFactory</value>
      </parameter>
      <parameter>
        <name>configFilePath</name>
        <value>[full path to repository.xml]</value>
      </parameter>
      <parameter>
        <name>repHomeDir</name>
        <value>[full path to the repository home folder]</value>
      </parameter>
    </ResourceParams>


In Tomcat 5.5, add the following snippet in your application's
`WEB-INF/context.xml` or `$CATALINA_HOME/conf/_enginename_/_hostname_/_webappname_.xml`. 
If you prefer central configuration, you can add the configuration to the Host Context
section in the server.xml.

    <Resource 
        name="jcr/repository"
        auth="Container"
        type="javax.jcr.Repository"
        factory="org.apache.jackrabbit.core.jndi.BindableRepositoryFactory"
        configFilePath="[full path to repository.xml"
        repHomeDir="[full path to the repository home folder]"
    />
    
    
