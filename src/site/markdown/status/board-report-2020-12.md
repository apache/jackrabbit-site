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
Apache Jackrabbit: Board Report December 2020 (draft)
==============================================

## Description: 
The Apache Jackrabbit™ content repository is a fully conforming
implementation of the Content Repository for Java™ Technology API
(JCR, specified in JSR 170 and 283). The Jackrabbit content 
repository is stable, largely feature complete and actively being
maintained.
 
Jackrabbit Oak is an effort to implement a scalable and performant 
hierarchical content repository as a modern successor to the Apache
Jackrabbit content repository. It is targeted for use as the 
foundation of modern world-class web sites and other demanding 
content applications. In contrast to its predecessor, Oak does not 
implement all optional features from the JSR specifications and it 
is not a reference implementation. 
   
## Issues: 
There are no issues requiring board attention at this time.
   
## Membership Data:

Apache Jackrabbit was founded 2006-03-15 (15 years ago)
There are currently 58 committers and 58 PMC members in this project.
The Committer-to-PMC ratio is 1:1.

Community changes, past quarter:

 - Amrit Verma was added to the PMC on 2020-09-28
 - Miroslav Smiljanic was added to the PMC on 2020-10-27
 - Amrit Verma was added as committer on 2020-09-15
 - Miroslav Smiljanic was added as committer on 2020-10-27

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

We continue making regular feature releases of Jackrabbit Oak. The
most recent release was Jackrabbit Oak 1.36.0 that was made available
on November 17th.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

In October the team noticed security vulnerabilities with Apache
Solr versions in use by Apache Jackrabbit Oak (CVE-2020-13941,
CVE-2019-17558, CVE-2019-2386). The updated Solr versions with the
fixes required a change of the Java version supported by the
Jackrabbit Oak maintenance releases. So far Jackrabbit Oak 1.4.x
and 1.6.x releases were able to run on Java 7 or newer. With the
upgrade of Solr, the minimum version had to be lifted to Java 8
(https://s.apache.org/t40d0). 

Beginning of December the team decided to drop support and deprecate
the 2.18 branch of Apache Jackrabbit. Users are encouraged to upgrade
to the latest stable 2.20.x version (https://s.apache.org/llfe1).

## Community Health:
The project is healthy with a continuous stream of traffic on all 
mailing lists reflecting the activity of the respective component. 

There is a wide range of topics being discussed on the dev and user
lists as well as on the various JIRA issues. 

Commit activity is moderate mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

 - jackrabbit-2.12.11 was released on 2020-09-10
 - jackrabbit-oak-1.34.0 was released on 2020-09-10
 - jackrabbit-oak-1.22.5 was released on 2020-10-12
 - jackrabbit-2.21.4 was released on 2020-10-22
 - jackrabbit-2.20.2 was released on 2020-11-05
 - jackrabbit-1.36 was released on 2020-11-17
 - jackrabbit-oak-1.8.24 was released on 2020-12-08
 
## JIRA activity:

 - 121 JIRA tickets created in the last 3 months 
 - 121 JIRA tickets closed/resolved in the last 3 months
 