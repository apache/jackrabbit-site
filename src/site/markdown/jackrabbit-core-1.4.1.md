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

jackrabbit-core 1.4.1
=====================
Release Notes -- Apache Jackrabbit Core -- Version 1.4.1


Introduction
------------
This is the 1.4.1 patch release of the jackrabbit-core component of Apache
Jackrabbit, a fully conforming implementation of the Content Repository for
Java Technology API (JCR).

This release fixes a binary property regression (JCR-1346) as well as other
issues reported against the Apache Jackrabbit 1.4 release. See below for a
full list of changes in this release.

See the Apache Jackrabbit website at http://jackrabbit.apache.org/ for more
information.


Release Contents
----------------
Unlike previous Jackrabbit releases that contained a full set of
components, this patch release only contains the jackrabbit-core component.
The component is distributed both as a source archive and a pre-compiled
binary.

### Source archive (jackrabbit-core-1.4.1-src.jar)

The source archive contains the full source code of this release in a
"jackrabbit-core-1.4.1" directory. Use the following commands (or the
equivalent in your environment) to build the component with Maven 2 and
Java 1.4 or higher:


    $ jar xf jackrabbit-core-1.4.1-src.jar
    $ cd jackrabbit-1.4.1
    $ mvn install


### Pre-compiled binary (jackrabbit-core-1.4.1.jar)

Core of the Apache Jackrabbit content repository implementation.

See the included README.txt file for more information.

Each release file is accompanied by SHA1 and MD5 checksums and a PGP
signature. The public key used for the signatures can be found in the KEYS
file.


Changes and known issues in this release
----------------------------------------
All the changes and known issues in this release are listed below. The
issue identifier and title is listed for each change and known issue. You
can look up individual issues for more details in the Jackrabbit issue
tracker at http://issues.apache.org/jira/browse/JCR


### Bug fixes
* \[[JCR-1046](https://issues.apache.org/jira/browse/JCR-1046)] Non-versionable children of a versionable node should not be ...
* \[[JCR-1227](https://issues.apache.org/jira/browse/JCR-1227)] Restore of empty multivalue property always changes property ...
* \[[JCR-1305](https://issues.apache.org/jira/browse/JCR-1305)] JNDI data sources with BundleDbPersistenceManager: ...
* \[[JCR-1318](https://issues.apache.org/jira/browse/JCR-1318)] Repository Home locked not released despite ...
* \[[JCR-1322](https://issues.apache.org/jira/browse/JCR-1322)] Cluster information is not persisted to database when ...
* \[[JCR-1323](https://issues.apache.org/jira/browse/JCR-1323)] When using QueryImpl.setLimit() and QueryImpl.setOffset(), ...
* \[[JCR-1332](https://issues.apache.org/jira/browse/JCR-1332)] CLONE -Aggregate include ignored if no primaryType set
* \[[JCR-1341](https://issues.apache.org/jira/browse/JCR-1341)] Cluster Journal directory should be created automatically
* \[[JCR-1346](https://issues.apache.org/jira/browse/JCR-1346)] InternalValue.createCopy for binary properties (jcr:data) ...
* \[[JCR-1358](https://issues.apache.org/jira/browse/JCR-1358)] Cluster revision file not closed on repository shutdown.
* \[[JCR-1372](https://issues.apache.org/jira/browse/JCR-1372)] \[PATCH] Fix possible Null Ptr exception in ConnectionFactory
* \[[JCR-1374](https://issues.apache.org/jira/browse/JCR-1374)] \[PATCH] DbDataStore: Make sure streams are closed
* \[[JCR-1376](https://issues.apache.org/jira/browse/JCR-1376)] SearchIndex parameter cacheSize is ignored
* \[[JCR-1379](https://issues.apache.org/jira/browse/JCR-1379)] AbstractExcerpt uses wrong logger
* \[[JCR-1380](https://issues.apache.org/jira/browse/JCR-1380)] CachingHierarchyManager synchronization problem
* \[[JCR-1389](https://issues.apache.org/jira/browse/JCR-1389)] setProperty("name", new Value\[0], PropertyType.LONG) loses ...

### Known issues
* \[[JCR-43](https://issues.apache.org/jira/browse/JCR-43)] Restore on nodes creates same-name-sibling of ...
* \[[JCR-320](https://issues.apache.org/jira/browse/JCR-320)] BinaryValue equals fails for two objects with ...
* \[[JCR-392](https://issues.apache.org/jira/browse/JCR-392)] Querying element by number does not work
* \[[JCR-435](https://issues.apache.org/jira/browse/JCR-435)] Node.update() does not work correct for SNS
* \[[JCR-449](https://issues.apache.org/jira/browse/JCR-449)] inconsistency in internal version items during commits
* \[[JCR-517](https://issues.apache.org/jira/browse/JCR-517)] Reserved status of namespace jcr not enforced
* \[[JCR-522](https://issues.apache.org/jira/browse/JCR-522)] XPath parser too tolerant
* \[[JCR-537](https://issues.apache.org/jira/browse/JCR-537)] Failure to remove a versionable node
* \[[JCR-538](https://issues.apache.org/jira/browse/JCR-538)] failing Node.checkin() or Node.checkout() might leave ...
* \[[JCR-566](https://issues.apache.org/jira/browse/JCR-566)] Versioning bug with restore and transactions
* \[[JCR-575](https://issues.apache.org/jira/browse/JCR-575)] unicode escapes in files generated by JJTree
* \[[JCR-591](https://issues.apache.org/jira/browse/JCR-591)] XPath position function does not work
* \[[JCR-639](https://issues.apache.org/jira/browse/JCR-639)] Allow modification of OPV=IGNORE items even if parent ...
* \[[JCR-643](https://issues.apache.org/jira/browse/JCR-643)] Own AccessManager + VersionManager : AccessDenied problem
* \[[JCR-690](https://issues.apache.org/jira/browse/JCR-690)] Nodes' and properties' names with invalid XML ...
* \[[JCR-709](https://issues.apache.org/jira/browse/JCR-709)] ArrayStoreException is thrown when jcr:deref() is used ...
* \[[JCR-777](https://issues.apache.org/jira/browse/JCR-777)] Order by clause using child axis does not throw ...
* \[[JCR-843](https://issues.apache.org/jira/browse/JCR-843)] XPath does not work with sub-axes
* \[[JCR-908](https://issues.apache.org/jira/browse/JCR-908)] Unable to properly restore a previous version of a node that ...
* \[[JCR-932](https://issues.apache.org/jira/browse/JCR-932)] Lossy SQL parsing
* \[[JCR-935](https://issues.apache.org/jira/browse/JCR-935)] ConcurrentModificationException during logout (cont'd)
* \[[JCR-936](https://issues.apache.org/jira/browse/JCR-936)] Using Oracle bundle PM throws SQL exception (cannot insert NULL)
* \[[JCR-983](https://issues.apache.org/jira/browse/JCR-983)] fn:upper accepted in too many places
* \[[JCR-1002](https://issues.apache.org/jira/browse/JCR-1002)] QueryManager does not throw exception if property name ...
* \[[JCR-1075](https://issues.apache.org/jira/browse/JCR-1075)] Error with predicate in query with multiple jcr:deref()
* \[[JCR-1117](https://issues.apache.org/jira/browse/JCR-1117)] Bundle cache is not rolled back when the storage of a ...
* \[[JCR-1135](https://issues.apache.org/jira/browse/JCR-1135)] boolean value constraints exposed in custom format
* \[[JCR-1173](https://issues.apache.org/jira/browse/JCR-1173)] Session scoped lock has no effect on other cluster nodes
* \[[JCR-1187](https://issues.apache.org/jira/browse/JCR-1187)] Asking a property twice for it's stream returns the same ...
* \[[JCR-1211](https://issues.apache.org/jira/browse/JCR-1211)] QueryManager does not throw exception if jcr:deref is used in ...
* \[[JCR-1223](https://issues.apache.org/jira/browse/JCR-1223)] Occasional NPE on node checkin
* \[[JCR-1248](https://issues.apache.org/jira/browse/JCR-1248)] ParseException if search string ends with '!'
* \[[JCR-1275](https://issues.apache.org/jira/browse/JCR-1275)] NullPointerException in AbstractVersionManager....
* \[[JCR-1334](https://issues.apache.org/jira/browse/JCR-1334)] Deadlock with XA enabled
* \[[JCR-1354](https://issues.apache.org/jira/browse/JCR-1354)] Repository shutdown reposts ERROR: failed to close connection
* \[[JCR-1359](https://issues.apache.org/jira/browse/JCR-1359)] Adding nodes from concurrently running sessions cause exceptions
* \[[JCR-1360](https://issues.apache.org/jira/browse/JCR-1360)] Parsing built-in CND and XML nodetypes does not result in ...
* \[[JCR-1362](https://issues.apache.org/jira/browse/JCR-1362)] DatabaseJournal improperly finds tables in external schemas ...
* \[[JCR-1367](https://issues.apache.org/jira/browse/JCR-1367)] Exception when closing connection under db2
* \[[JCR-1387](https://issues.apache.org/jira/browse/JCR-1387)] Lock token not removed from session when node is removed
