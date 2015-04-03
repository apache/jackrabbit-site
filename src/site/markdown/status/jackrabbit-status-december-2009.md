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

Jackrabbit Status December 2009
===============================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170 and 283).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
Jackrabbit 2.0 reached beta status with the following releases:

* Apache Jackrabbit 2.0 alpha11 on September 23rd
* Apache Jackrabbit 2.0 beta1 on October 30th
* Apache Jackrabbit 2.0 beta3 on November 25th
* Apache Jackrabbit 2.0 beta4 on December 12th

We also made two releases from the old 1.4 maintenance branch:

* jackrabbit-core 1.4.10 on September 15th
* jackrabbit-core 1.4.11 on September 23rd

We made two releases of the Jackrabbit parent POM:

* org.apache.jackrabbit:jackrabbit:4 on September 14th
* org.apache.jackrabbit:jackrabbit:5 on October 4th


Legal
-----
We're tracking the [LEGAL-50](https://issues.apache.org/jira/browse/LEGAL-50)
and [LEGAL-62|https://issues.apache.org/jira/browse/LEGAL-62]
issues for further comments, but currently we have no open legal action
items.

We are interested in figuring out how the new trademark policy affects our
logo, website and releases, and what steps we need to take to meet the
policy.


Community / Development
-----------------------
Jackrabbit participated in the Content Technology track and the !NoSQL
meetup at ApacheCon US 2009.

The development branch related to database connection pooling has been
merged back to Jackrabbit trunk and the results are included in the
Jackrabbit 2.0 beta4 release.

We've discussed with Apache Sling about taking over some !OSGi bundling
code they've written for Jackrabbit. On the other hand there is some code
in Jackrabbit that's only being used by Sling and that might end up being
adopted by them. We're considering making parts of our svn tree writable by
members of both projects to simplify such cooperation.


Infrastructure
--------------
We received some spam through Nabble on our dev@ list, and have asked
Nabble to disable posts through the web interface.

We reconfigured the Jackrabbit entry on Ohloh to get code statistics for
the Git mirror at git.apache.org since the svn history seen by Ohloh didn't
include the time when Jackrabbit was still incubating.
