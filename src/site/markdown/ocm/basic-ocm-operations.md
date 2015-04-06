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

Basic OCM operations
--------------------
When you have created a new [Object Content Manager](object-content-manager.html)
in your application, you can use this component to insert, update, delete
and retrieve objects. The class 'Folder' used in the following sections has
to be annotated or defined in a xml file class descriptor.

This page describes only the main [Object Content Manager](object-content-manager.html)
methods. You can see the javadoc to get more information on the API.
You can also read the tutorial [5' with Jackrabbit OCM](5-with-jackrabbit-ocm.html)
to get more information on how to initialize the [Object Content Manager](ocm).


Insert
------

    Folder folder =  new Folder();
    folder.setPath("/myfolder");
    folder.set...(); // call the setter methods
    
    ocm.insert(myFolder);


Retrieve and update an object
-----------------------------

    Folder folder = (Folder) persistenceManager.getObject(Folder.class, "/myfolder");
    folder.set...(); // call the setter methods
    
    ocm.update(myFolder);


Delete
------

    ocm.remove("/test");


Save last changes
-----------------
After some inserts, deletes and/or updates, you can call the method
`ocm.save()` to apply your changes into the JCR repository.
