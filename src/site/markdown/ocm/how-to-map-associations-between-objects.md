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

How to map associations between objects
=======================================

Overview
--------
This tutorial explains how to map associations between objects (1:1 and
1:n). You can find the tutorial code sample from [here](Beans_and_collections.zip)
. It is based on Maven and ready to be used inside Eclipse. If you have
some configuration issues, please review the tutorial "[A simple OCM
project with Maven & Eclipse]". 

The Content Model
-----------------
We will extend the content model created in the previous tutorial [5' with Jackrabbit OCM](5-with-jackrabbit-ocm.html). 
Each PressRelease is made by an Author and it is possible to add some
references (URL). 

So, we have to add 2 new associations in our model  : 

* An 1:1 association between a PressRelease and an Author.
* An 1:n association between PresseRelease and Url. 


Here is the main java class, the PressRelease : 


    @Node
    public class PressRelease
    {
        @Field(path=true) private String path;
        @Field  private String title;
        @Field  private Date pubDate;
        @Field  private String content;
        @Bean private Author author;
        @Collection  List<Url> urls;
        
        //if you want a map instead of a list, use the following declaration
        @Collection Map<String,Url> map;
        
     [... Add here getters & setters ...]
    
    }


Since the tutorial [5' with Jackrabbit OCM](5-with-jackrabbit-ocm.html), 
we can understand the goal of the annotations `@Node` and `@Field`. 
An association 1:1 can be specified with the annotation `@Bean` like 

    @Bean private Author author;


It is possible to set extra settings with this annotation but it is out of
the scope of this tutorial.You can review the code of the Author class
which is very simple. As you will see, it is not mandatory to add
annotation `@Field(path=true)` in the Author class because it is an
aggregation of a PressRelease.

An 1:n association can be specified with the annotation `@Collection` like 

    @Collection  List<Url> urls;


For this kind of association, you can also use a Map instead of a
Collection

    @Collection Map<String,Url> map;



Right now, the support of Map is limited to the usage of String for the key
because the map key will be used as the Node name.


How are those objects stored in the repository ?
------------------------------------------------
For this tutorial each java class is mapped into the "nt:unstructured" node
type. Making this kind of mapping is quite flexible because it does not
imply specific repository configuration. There is no constraints in the JCR
repository. All constrains are defined in the java code. 


> Note : It is possible to associate a specific node type to each java class
> but this imply more repository configurations. 
>       It is also possible to change the corresponding JCR node structure
> by using specific Bean or Collection converters. 
>       Later, we will add more tutorials on OCM converters. 


Following our example, the Author and Urls nodes will be created as
subnodes of a press release. 
Here is an example of the correspoding JCR structure : 


    - PressRelease_1 
    	* path : "/mypath/myrelease"
    	* title : "..."
    	* pubDate : 10/06/08
    	* content :  "...."
    	- Author
    		* firstName : "..."
    		* lastName : "..."
    	- urls
    		* url1 
    			* url : "http://...."
    			* caption : "..."
    			* description : "..."
    		* url2 
    			* url : "http://...."
    			* caption : "..."
    			* description : "..."
    		...
    	- map
    	   * Apache
    	       * url : "http://www.apache.org"
    	       * caption : "..."
    	       * description : "..."
                
    	   * Jackrabbit
    	      * url : "http://jackrabbit.apache.org"
    	      * caption : "..."
    	      * description : "..."
    		

Download the tutorial code
--------------------------
You can download the OCM project from [here](Beans_and_collections.zip)

