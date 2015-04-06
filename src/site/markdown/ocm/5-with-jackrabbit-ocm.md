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

5' with Jackrabbit and OCM
==========================
This very small tutorial describes how to create an application with Jackrabbit OCM.
In short, you have to:

* Create one or more persistent classes. 
* Instantiate an _Object Content Manager_ component.
* Use the _Object Content Manager_ to persist your data.


Create a persistent class
-------------------------
This tutorial is using the annotation support to define a persistent class. 
Your data objects are simple pojos with some OCM annotations. 
Here is a example of a PressRelease class. 

    package org.apache.jackrabbit.ocm.model;
    
    import java.util.Date;
    
    import org.apache.jackrabbit.ocm.mapper.impl.annotation.Field;
    import org.apache.jackrabbit.ocm.mapper.impl.annotation.Node;
    
    @Node
    public class PressRelease 
    {
	@Field(path=true) String path;
	@Field String title; 
	@Field Date pubDate; 
	@Field String content;
	
	public String getPath() {
	    return path;
	}
	public void setPath(String path) {
	    this.path = path;
	}
	public String getContent() {
	    return content;
	}
	public void setContent(String content) {
	    this.content = content;
	}
	public Date getPubDate() {
	    return pubDate;
	}
	public void setPubDate(Date pubDate) {
	    this.pubDate = pubDate;
	}
	public String getTitle() {
	    return title;
	}
	public void setTitle(String title) {
	    this.title = title;
	}
    }


The annotation `@Node` has to be added on the top of the class.
Each persistent class must have a *path field* which will be mapped 
into the JCR Node path. This can be specify with the annotation. 
`@Field(path=true)` Other persistent fields can be defined with the 
annotation `@Field`

That's all for the class definition. In other tutorials, we will see 
how to map advanced fields like collections or custom objects. 


Instantiate an Object Content Manager component
-----------------------------------------------
In order to save a PressRelease object, you have to instantiate an _Object Content Manager_ component : 


    List<Class> classes = new ArrayList<Class>();	
    classes.add(PressRelease.class); // Call this method for each persistent class
		    
    Mapper mapper = new AnnotationMapperImpl(classes);
    ObjectContentManager ocm =  new ObjectContentManagerImpl(session, mapper);	


Use the Object Content Manager to persist your data
---------------------------------------------------
Now, you are ready to create a new PressRelease and use the _Object Content Manager_ to persist it into the JCR repository. 


    // Insert an object
    System.out.println("Insert a press release in the repository");
    PressRelease pressRelease = new PressRelease();
    pressRelease.setPath("/newtutorial");
    pressRelease.setTitle("This is the first tutorial on OCM");
    pressRelease.setPubDate(new Date());
    pressRelease.setContent("Many Jackrabbit users ask to the dev team to make a tutorial on OCM");
			    
    ocm.insert(pressRelease);
    ocm.save();
			    
    // Retrieve 
    System.out.println("Retrieve a press release from the repository");
    pressRelease = (PressRelease) ocm.getObject("/newtutorial");
    System.out.println("PressRelease title : " + pressRelease.getTitle());
			    
    // Delete
    System.out.println("Remove a press release from the repository");
    ocm.remove(pressRelease);
    ocm.save();

