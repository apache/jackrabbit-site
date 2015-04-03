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

Jackrabbit Status December 2008
===============================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
We released Apache Jackrabbit 1.5.0 on December 8th.

We also made the following patch releases from the 1.4 branch:

* jackrabbit-core 1.4.6 on October 7th
* jackrabbit-classloader 1.4.1 on October 2nd
* jackrabbit-jcr-server 1.4.1 on September 30th


Legal
-----
We use Google Analytics to track usage of our web site. We posted a privacy
policy that mentions the Analytics use on our web site and continue to work
with legal-discuss@ to resolve concerns that were raised about the use of
Google Analytics.


Community
---------
Claus Koell joined the Jackrabbit team as a committer and PMC member.

The slump in community activity over late summer seems to be gone and we're
back to normal levels of mailing list and commit activity.

Based on interest to the CMIS implementation effort (see below), we have
extended write access in our sandbox area in svn to all Apache committers.

We are considering starting a "JCR Commons" subproject for managing the
development and release of a number of our components that are not tightly
coupled with the Jackrabbit content repository implementation. This
subproject would keep using our existing mailing lists but would have its
own web site (under http://jackrabbit.apache.org/commons/) and separate
issue trackers and release cycles for each component. See
http://markmail.org/message/qqlvlwpgi5oauak6 for more details.


Development
-----------
Development in trunk continues with post-1.5 features, and I expect us to
release Jackrabbit 1.6 early next year. Jackrabbit 2.0 (and the JSR 283
reference implementation) will probably be released later next year.

A new sandbox component was started for an effort to implement the proposed
Content Management Interoperability Services (CMIS) specification on top of
a JCR content repository.


Infrastructure
--------------
We created a new Jira project (JCRCMIS) for the CMIS implementation effort
and plan to create more assuming the JCR Commons subproject gets started.

We've enabled wiki markup and the patch-available workflow in the JCRCMIS
project. If these features work well, we will enable them also in our main
JCR project in Jira.
