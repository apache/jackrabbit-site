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

Jackrabbit Status September 2009
================================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
The big news this quarter is the release of Jackrabbit 1.6.0:

* Apache Jackrabbit 1.6.0 on August 11th

The following patch releases were made from earlier maintenance branches:

* Apache Jackrabbit 1.5.7 on August 3rd
* jackrabbit-core 1.4.10 on September 15th

We made two internal releases of the Jackrabbit parent POM:

* org.apache.jackrabbit:parent:3 on June 26th
* org.apache.jackrabbit:parent:4 on September 15th

We also continued releasing Jackrabbit 2.0 alphas:

* Apache Jackrabbit 2.0 alpha3 on July 3rd
* Apache Jackrabbit 2.0 alpha4 on July 14th
* Apache Jackrabbit 2.0 alpha7 on August 10th
* Apache Jackrabbit 2.0 alpha8 on August 18th
* Apache Jackrabbit 2.0 alpha9 on August 26th


Legal
-----
We have asked (see [LEGAL-50](https://issues.apache.org/jira/browse/LEGAL-50)) 
the legal team to review the terms under which we are redistributing the
JCR API jar. The purpose of this is to complete the legal records, and this
issue is not a blocker to our current releases.

Recent legal discussions regarding the contents of the NOTICE files (see
for example [LEGAL-62](https://issues.apache.org/jira/browse/LEGAL-62)) 
suggest that we have been including some unnecessary information in our
NOTICEs. We will review our NOTICE files before the 2.0 release to comply
with the consensus on legal-discuss@.


Community / Development
-----------------------
Sébastien Launay joined the Jackrabbit team as a committer and PMC member.

With the 1.6 release our JCR 1.0 work has entered maintenance mode and
we're focusing on releasing Jackrabbit 2.0 shortly after JCR 2.0 becomes
available. We reached JCR 2.0 feature-completeness with the 2.0 alpha9
release, and that release was also used for the JCR 2.0 RI and TCK
candidates. The JSR 283 final approval ballot has just passed, and we
expect the final JCR 2.0 release to follow soon.

The main author of the JCROM project that implements an alternative to the
Jackrabbit OCM (object content mapping) component contacted us about
bringing the JCROM code to Jackrabbit and possibly merging with our
existing OCM code.


Infrastructure
--------------
We are now using the Nexus server at repository.apache.org for staging and
deploying our releases to the central Maven repository.

The monthly Google Analytics reports we set up earlier this year don't seem
to be reaching the dev@ list anymore. To work around this we're now sharing
the reports via svn and our web site.
