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

Jackrabbit Status March 2007
============================
_From the [minutes](http://www.apache.org/foundation/records/minutes/2007/board_minutes_2007_03_28.txt) of the Apache board meeting on March 28th, 2007:_

Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
We released three versions of Apache Jackrabbit; 1.2.1 in January, 1.2.2 in
February, and 1.2.3 in March.

The 1.2 release candidate needed to be cancelled and repackaged as 1.2.1
due to a last-minute issue that was raised during the release vote. This
prompted a discussion on release candidates and versioning, which in turn
resulted in some improvements to our release process.

We are currently working on the 1.3 release.


Community
---------
Przemyslaw Pakulski was added as a committer and PMC member.

The user mailing list that was launched last year has reached the activity
level of the development list and continues steady growth. The total
mailing list activity is now higher than ever before.

One session and one tutorial on JCR/Jackrabbit have been scheduled for the
upcoming ApacheCon EU. We are also planning to organize a Jackrabbit BOF
during the conference.

Based on the experiences from last summer, we are proposing a Google Summer
of Code 2007 project to build a JCR demo application based on Apache
Jackrabbit.

There is interest in starting a new incubating content analysis toolkit
project named Tika. Hopefully the project will as a side effect build more
bridges between the Lucene and Jackrabbit communities.


Development
-----------
The 1.2 releases include a new beta-level clustering feature that is
attracting much interest. Many corner cases are being ironed out based on
feedback and bug reports from the user community, and it seems that we can
soon declare the feature stable.

The main new feature in the 1.3 release is a set of "bundle persistence
manager" components contributed by Day. These components bring a major
performance boost to many Jackrabbit user cases. The contributed IP has
been cleared and is now being integrated into the Jackrabbit codebase.

There have been a number of cases where users have suggested some internal
changes to better handle specific performance and other requirements.
Unfortunately few of such discussions have resulted in proposed patches. We
should do better to encourage patch submissions.


Infrastructure
--------------
The Solaris zone we requested is now up and running. We have a Continuum
installation doing nightly builds and continuous integration tests for all
the Jackrabbit release components. So far we've seen zero build-breaking
commits.
