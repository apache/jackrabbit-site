Title: Basic OCM operations
When you have created a new [Object Content Manager](object-content-manager.html)
 in your application, you can use this component to insert, update, delete
and retrieve objects. The class 'Folder' used in the following sections has
to be annoted or defined in a xml file class descriptor.

This page describes only the main [Object Content Manager](object-content-manager.html)
 methods. You can see the javadoc to get more information on the API.
You can also read the tutorial [5' with Jackrabbit OCM](5'-with-jackrabbit-ocm.html)
 to get more information on how to initialize the [Object Content Manager]
 (ocm).

<a name="BasicOCMoperations-Insert"></a>
## Insert


    Folder folder =  new Folder();
    folder.setPath("/myfolder");
    folder.set...(); // call the setter methods
    
    ocm.insert(myFolder);


<a name="BasicOCMoperations-Retrieveandupdateanobject"></a>
## Retrieve and update an object


    Folder folder = (Folder) persistenceManager.getObject(Folder.class,
"/myfolder");
    folder.set...(); // call the setter methods
    
    ocm.update(myFolder);


<a name="BasicOCMoperations-Delete"></a>
## Delete


    ocm.remove("/test");


<a name="BasicOCMoperations-Savelastchanges"></a>
## Save last changes

After some inserts, deletes and/or updates, you can call the method
*ocm.save()* to apply your changes into the JCR repository.
