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

Jackrabbit Status December 2006
===============================
_From the [minutes](http://www.apache.org/foundation/records/minutes/2006/board_minutes_2006_12_20.txt) of the Apache board meeting on December 20th, 2007:_

Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project has progressed nicely since the September
status report. We have no board-level issues at this time.


Releases
--------
We have released two versions of Apache Jackrabbit: 1.1 in October and
1.1.1 in December.

The 1.2 release is scheduled to happen by the end of the year.


Community
---------
No new committers have been added since September. One contributor was just
elected for committership, but the process is still pending on us receiving
the required CLAs.

The number of active contributors has grown lately, and I expect to see new
committers being elected in near future. Most notably we've seen a number
of contributions from employees of Cognifide, a consulting company with JCR
expertise. A CCLA has been requested.

There were two short Apache Jackrabbit presentations during the ApacheCon
US and some discussion on potential cooperation with other related Apache
projects.


Development
-----------
The Jackrabbit build environment was recently upgraded to Maven 2 along
with a restructuring of the Jackrabbit component projects.

An initial clustering implementation was added to Jackrabbit core and will
go out as a beta feature in the 1.2 release.

The Jackrabbit dependencies to Apache Lucene and Apache Derby were upgraded
to more recent versions.

A number of forward-looking design discussions have occurred on the mailing
list, often based on feedback from outside the core development group.


Infrastructure
--------------
We've requested a Solaris zone for setting up nightly builds and automating
integration tests and Maven reporting.
