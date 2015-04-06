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

Advanced Mapping Strategies
===========================

Inheritance
-----------
TODO


Interface
---------
TODO


Components
----------
A component is an entity that cannot live by its own, but has a logical
meaning. Take for example an Address. It may live alone, but doesn't make
much sense in some systems. Once associated with an User it starts making
sense. Now, as in RDBMS you can choose the persist this as a record in a
separate table with a 1-1 relation, or you may choose to persist Address
field along with the User.

Now, returning to JCR, the component is fitting perfectly the mixin notion.
A mixin cannot live by its own in the repository. It is associated with
some node. It's properties are added to the set of original node.


Group some bean attributes into a subnode
-----------------------------------------
TODO


Map to another node structure
-----------------------------
Sometime, it should be interesting to map to a different jcr node
structure. Here is an example, for a class "File", we can have:


    public class File
    {
      private String mimeType;
      private String encoding;
      private InputStream data;
      private Calendar lastModified;
      // Add getters/setters
    }


and in terms of JCR structure, we can have:


    nt:file
      jcr:content
        jcr:mimeType
        jcr:encoding
        jcr:data
        jcr:lastModified


So, the jcr:content node is an extra node to specify in the mapping file.
