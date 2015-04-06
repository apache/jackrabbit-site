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

OCM Search
==========


Searching a single object
-------------------------

    QueryManager queryManager = ocm.getQueryManager();
    
    // Build the search filter
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.addEqualTo("text", "Para 1");   // Text is an attribute in the class Paragraph
    
    // Build the query
    Query query = queryManager.createQuery(filter);
    Paragraph paragraph = (Paragraph) ocm.getObject(query);


Searching a collection
----------------------

    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    Collection result = ocm.getObjects(query);


Searching with an iterator
--------------------------

    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    Iterator iterator = ocm.getObjectIterator(query);


Remove objects based on a query
-------------------------------

    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    ocm.remove(query);

