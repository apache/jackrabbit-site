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

Mapping Collection Fields
=========================
The collection-descriptor maps a collection attribute into JCR nodes or in
a multivalue property.

Based on our model defined here, the following collection-descriptor is
used to map the "paragraphs" field into the JCR node called "paragraphs".


    <class-descriptor
        className="org.apache.jackrabbit.ocm.testmodel.Page"
        jcrType="my:page">
      <collection-descriptor
          fieldName="paragraphs" jcrName="paragraphs"
          elementClassName="org.apache.jackrabbit.ocm.testmodel.Paragraph" />
      <!-- other field, bean and collection mapping here !-->
    </class-descriptor>
    
    <class-descriptor
        className="org.apache.jackrabbit.ocm.testmodel.Paragraph"
        jcrType="my:paragraph">
      <field-descriptor fieldName="path" path="true" />
      <field-descriptor fieldName="text" jcrName="my:text"/>
    </class-descriptor>


The collection-descriptor contains the elementClassName attribute which
specify the collection element class. A class descriptor for the element
class has also to be defined.


The JCR Structure
-----------------
Following our example, the resulting JCR structure is:


    /mysite/page1
      /mysite/page1/paragraphs
        /mysite/page1/paragraphs/collection-element1
          my:text = "This is the content of para1"
        /mysite/page1/paragraphs/collection-element2
          my:text = "This is the content of para2"
      ... other subnodes for page1 ...


By default, the persistence manager will create a subnode
(/mysite/page1/paragraphs). This one will contains the different
paragraphs.

As explained in the following sections, it is possible to map to another
JCR structure. It is also possible to use another name for the jcr node
names (see above).


Supported Collection and Map Types
----------------------------------
The OCM framework is supporting the following java types:

* *Collections* Collection, List, Set, ArrayList, Vector, HashSet
* *Maps* Map, HashMap


Using Another Collection or Map
-------------------------------
It is possible to support other Collection or Map types with the
ManageableCollection interface.


Using Another Collection Converter
----------------------------------
TODO


Predefined Collection Converters
--------------------------------
TODO


Building your own Collection Converters
---------------------------------------
TODO
