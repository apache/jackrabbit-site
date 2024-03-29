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

Object Content Mapping
======================

> The Jackrabbit OCM documentation is still in progress. We advise you also
> to review  [the unit tests](http://svn.apache.org/viewvc/jackrabbit/trunk/jackrabbit-ocm/src/test/)
> to get an overview on current OCM features.


* [Object Content Manager](ocm/object-content-manager.html)
    * [Basic OCM operations](ocm/basic-ocm-operations.html)
    * [OCM Search](ocm/ocm-search.html)
    * [OCM Version Management](ocm/ocm-version-management.html)
    * [OCM Locking](ocm/ocm-locking.html)
* Tutorials
    * [5' with Jackrabbit OCM](ocm/5-with-jackrabbit-ocm.html)
    * [A simple OCM project with Maven & Eclipse](ocm/a-simple-ocm-project-with-maven--eclipse.html)
    * [How to map associations between objects](ocm/how-to-map-associations-between-objects.html)
* [Mapping Strategies](ocm/mapping-stategies.html) (obsolete doc)
    * [Mapping Atomic Fields](ocm/mapping-atomic-fields.html) (obsolete doc)
    * [Mapping Bean Fields](ocm/mapping-bean-fields.html) (obsolete doc)
    * [Mapping Collection Fields](ocm/mapping-collection-fields.html) (obsolete doc)
    * [Advanced Mapping Strategies](ocm/advanced-mapping-strategies.html) (obsolete doc)

Jackrabbit OCM is a framework used to persist java objects (pojos) in a JCR
repository including association, inheritance, polymorphism, composition,
and the Java collections framework. It offers also features like version
support, object locking and express queries with Java-based criteria, as
well as with JCR query languages.

In order to easily support the JCR specification, any content application
managing an high level object model can use this framework. For example, a
classic Forum application contains objects like "Forum", "Topic" and
"Post". Now, the data objects (pojo) can be managed by our JCR mapping
tools in order to persist them into a JCR compliant repository.


Why an ocm?
-----------
The object content mapping framework was created for the following
different reasons:

* Sometimes it is very convenient to be able to just access the JCR nodes
    and properties directly from your presentation-layer for very simple things
    (mostly generic display). When a lot of "business logic" are involved, the
    JCR API can be too low level and real business objects (pojo) are more
    appreciate in such cases.
* The OCM framework provides more abstraction on the technologies used to
    persist your content. The different application layers are less dependent
    on the JCR API.
* ORM tools like OJB or Hibernate are not appropriate for content oriented application.


Prerequisite
------------
Before using this OCM framework, you should review the JCR specification
and implementations like Apache Jackrabbit.
