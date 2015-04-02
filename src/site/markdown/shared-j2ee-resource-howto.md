Title: Shared J2EE Resource HOWTO
This document describes how to use a Jackrabbit content repository in the
deployment model 2: Shared J2EE Resource. In this deployment model, a
central content repository resource managed by an application server is
used by multiple different applications. See the [JCR client application HOWTO](jcr-client-application-howto.html)
 for instructions on how to use the configured content repository.

This how-to contains instructions for Tomcat versions 4.x and 5.x. It
should be easy to modify the instructions for other container environments.

<a name="SharedJ2EEResourceHOWTO-Tomcatinstructions"></a>
## Tomcat instructions

Follow the steps below to setup a model 2 Jackrabbit deployment for your
Tomcat 4.x or 5.x installation. Example code for both versions of Tomcat is
included after this overview.

1. Place the Jackrabbit jar file and all the dependencies (including the JCR
API jar file) under _Tomcat folder_/common/lib.
1. Register the bindable repository factory as a global resource.
1. Link the global resource to a context scoped JNDI address.

<a name="SharedJ2EEResourceHOWTO-Step2-Resourceconfiguration"></a>
### Step 2 - Resource configuration

Note: This step is essentially the same as step 2 in the Model 1 HOWTO. The
only differences are in the (arbitrary) naming of the resource and placing
of the configuration elements. The difference in the end result is that the
configured repository is bound to the global JNDI context instead of a
local one. In Tomcat 4.x and 5.0, add the following snippet in server.xml
under the GlobalNamingResources element.


    <Resource name="jcr/globalRepository"
    	  auth="Container"
    	  type="javax.jcr.Repository"/>
    
    <ResourceParams name="jcr/globalRepository">
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


In Tomcat 5.5, add the following snippet in server.xml under the
GlobalNamingResources element.


    <Resource name="jcr/globalRepository"
        auth="Container"
        type="javax.jcr.Repository"
        factory="org.apache.jackrabbit.core.jndi.BindableRepositoryFactory"
        configFilePath="[full path to repository.xml"
        repHomeDir="[full path to the repository home folder]
    "/>


<a name="SharedJ2EEResourceHOWTO-Step3-Resourcelink"></a>
### Step 3 - Resource link

In Tomcat versions 4.x and 5.0, add the following snippet in server.xml
under the Context element of your web application. In Tomcat version 5.5,
add the snippet in your application's context.xml or
$CATALINA_HOME/conf/_enginename_/_hostname_/_webappname_.xml. If you prefer
central configuration, you can add the configuration to
$CATALINA_HOME/conf/context.xml.


    <ResourceLink 
        name="jcr/repository"
        global="jcr/globalRepository"
        type="javax.jcr.Repository"/>

