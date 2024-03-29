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

Jackrabbit Status June 2010
===========================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170 and 283).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
Jackrabbit 2.1 was released in April:

* Apache Jackrabbit 2.1.0 on April 22nd

We also made maintenance releases from the 1.6 and 1.4 branches:

* Apache Jackrabbit 1.6.2 on June 7th
* jackrabbit-core 1.4.12 on June 7th


Legal
-----
The question in [LEGAL-50](https://issues.apache.org/jira/browse/LEGAL-50)
 about redistribution of the standard JCR API jar has now been officially
resolved. Thanks to the legal team for the closure on this! With LEGAL-50
resolved, we have no open legal issues.

We use RAT for automatic license header checks as a part of our normal
Hudson CI builds, and the accuracy of our LICENSE and NOTICE files is
manually reviewed before each release.


Community / Development
-----------------------
No new committers were added in this quarter. This is our third consequitive
quarter with no new committers. It looks like we need to pay more attention
to helping out and mentoring contributors. We have traditionally maintained
relatively high entry criteria for new committers.

Community diversity remains an issue we pay attention to, as the bulk of
Jackrabbit development is still done by one company. In this quarter we've
had eight people committing to Jackrabbit trunk, six of whom are employees
of Day Software. We satisfy the criteria of at least three independent
active committers and the community is healthy. Thus I don't see diversity
as an immediate problem for Jackrabbit, but it's a topic we are aware of
especially in light of the few new committers we've recently attracted.


Infrastructure
--------------
The Confluence upgrade caused some breakage on our web site and required
manual fixing. We are not too happy with our current Confluence auto-export
setup, and are considering other options.

Some of our Hudson builds have been failing due to generic Hudson problems.
We're hoping that the new master server will solve these issues. We're also
looking forward to a chance to set up a Sonar instance for Apache projects.
