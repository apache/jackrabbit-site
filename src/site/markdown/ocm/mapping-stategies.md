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

Mapping Strategies
=================
We are calling "Mapping strategy" the algorithm used by the Persistence
Manager to map a Java class into JCR nodes and/or properties.


The Object Model
----------------
In order to explain the basic mapping strategies, we will use the following
simple object model :

* A page contains a path (of course), a pageInfo and a collection of paragraphs.
* The PageInfo class contains the title and the page description. We are
    using the pageInfo here to see all mapping features (see the
    bean-descriptors). In real application, this class is not necessary :-)
* Each paragraph contains a path and a text field.

{center}!sample-model-doc.png!{center}

This object model could be too simple for real applications and it is just
used here to simplify the description of the different mapping strategies.


The Java Classes
----------------
Based on that object model, we can define the following Java classes:

**Page.java**

    public class Page
    {
      String path;
      PageInfo pageInfo;
      Collection paragraphs;
    
      /*  Add here the getter and setter methods */
    
      public void addParagraph(Paragraph paragraph)
      {
        if (paragraphs == null)
        {
          paragraphs = new ArrayList();
        }
    
        paragraphs.add(paragraph);
      }
    }

**PageInfo.java**

    public class PageInfo
    {
      String path;
      String title;
      String description;
    
      /*  Add here the getter and setter methods */
    
    }


**Paragraph.java**
    
    public class Paragraph
    {
      private String path;
      private String text;
    
      /* Add here the getter and setter methods */
    
    }



The JCR Structure
-----------------
Here is the resulting JCR structure if the page is stored on the path
"/mysite/mypage1" and contains 2 paragraphs:


    /mysite/page1
      /mysite/page1/pageInfo
        my:title = "This is my page title"
        my:description = "This is my page description"
      /mysite/page1/paragraphs
        /mysite/page1/paragraphs/paragraph1
          my:text = "This is the content of para1"
        /mysite/page1/paragraphs/paragraph2
          my:text = "This is the content of para2"

 
It is possible to have another kind of jcr structure by using other mapping
strategies. See the sections [Mapping Atomic Fields](mapping-atomic-fields.html)
, [Mapping Bean Fields]
, [Mapping Collection Fields]
 to get more information on that.


The Class Descriptors
---------------------
When you decide to map a bean class, you have to create a new class
descriptor entry in the Persistence Manager descriptor file. Let's start
with the simplest class-descriptor:

This class descriptor maps the class
"org.apache.jackrabbit.ocm.testmodel.Paragraph" into the JCR type
"nt:unstructured". Each field-descriptor maps one bean field into a JCR
property. For example, the first field descriptor maps the java bean field
"text" into the jcr property called "myjcrtext". The second
field-descriptor is a specific case because it maps the jcr node path into
a bean field called "path" (see below the section "The Path Field").

You can find more information on the field-descriptors in the page [Mapping Atomic Fields](mapping-atomic-fields.html).

It is also possible to map a bean class to a particular JCR node type by
specifying the desired type in the attribute jcrType. The following
class-descriptor map the class
"org.apache.jackrabbit.ocm.testmodel.Paragraph" into the node type
"my:paragraph".

Here are the class-descriptors required to map the classes Page, PageInfo
and Paragraph:

In order to use correctly our example class with Apache Jackrabbit, you
should import the following node type definitions with the Jackrabbit API.

Of course, node types "my:Page" and "my:PageInfo" are also required.

We are currently building a node type management tools which can import the
node types from the class-descriptors.


The Path Field
--------------
Each mapped class contains a mandatory field called the "path field". It
contains the JCR path associated to the object. For example, the following
descriptor specify the bean field "myPath" as the path field.


    <field-descriptor fieldName="myPath" path="true" />

