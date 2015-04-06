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

A simple OCM Project with Maven and Eclipse
===========================================
This tutorial explains how to start a new OCM project with Maven 2 & Eclipse. 
It is based on the tutorial [5' with Jackrabbit OCM](5-with-jackrabbit-ocm.html).


Install Maven 2 & Eclipse
-------------------------
This tutorial assumes that you have installed correctly Maven 2 & Eclipse.
If it is not the case, here is the instructions to install both products :

* Download Maven 2 (http://maven.apache.org/download.html). See the installation instructions on this page.
* Download Eclipse from http://www.eclipse.org
* In Eclipse, you have to create a new classpath variable called M2_REPO 
  which references the maven 2 repository (by default, it is the directory _$user home/.m2/repository_).


Download the OCM project
------------------------
You can download the OCM project from [here](5minutes.zip).


Install the project
-------------------

* Extract the project distribution anywhere on your local machine.
* Open a command terminal and change the current directory to the project root folder.
* Execute "mvn clean compile". This is an optional step to check if the code can be compiled correctly.


Get ready for Eclipse
---------------------
* Execute "mvn eclipse:eclipse" from the project root folder. By this way, you project can be imported into Eclipse.
* Start Eclipse and import the project (menu File/import, select general/existing project in the workspace,
  than select the project root directory).

Now you are ready to modify the project from Eclipse.


Review the project
------------------
This project is a standalone java application (see the 
class org.apache.jackrabbit.ocm.Main) which is creating, retrieving and deleting a 
PressRelease (see the class org.apache.jackrabbit.ocm.model.PressRelease).For simplicity 
reason, this application is using a TransientRepository but  you can change the repository 
configuration from the class RepositoryUtil. 


You can read the tutorial [5' with Jackrabbit OCM](5-with-jackrabbit-ocm.html) to get more 
information on how to  initialize the _Object Content Manager_ and how to persist the 
PressRelease Object.
