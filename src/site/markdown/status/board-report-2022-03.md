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
Apache Jackrabbit: Board Report March 2022 (draft)
==========================================

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

Apache Jackrabbit was founded 2006-03-15 (16 years ago)
There are currently 57 committers and 57 PMC members in this project.
The Committer-to-PMC ratio is 1:1.

Community changes, past quarter:

- Felix Meschberger was removed from the PMC on 2022-01-10
- Tobias Bocanegra was removed from the PMC on 2022-02-11
- Jose Andrés Cordero was added to the PMC on 2022-02-22
- Felix Meschberger was removed as committer on 2022-01-10
- Tobias Bocanegra was removed as committer on 2022-02-11
- Jose Andrés Cordero was added as committer on 2022-02-22

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

We continue making regular feature releases of Jackrabbit Oak. The
most recent release was Jackrabbit Oak 1.42.0 made available on
January 12th.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

Impact of the Log4j vulnerability on Jackrabbit modules was moderate.
Only vault-cli used Log4j for logging. With JCRVLT-573 this module
now also switched to logback and there is no more dependency on
Log4j. As precaution even some transitive test dependencies on Log4j
have been excluded (OAK-9639 and OAK-9645).

## Community Health:
The project is healthy with a continuous stream of traffic mostly on
the JIRA issues and GitHub pull requests reflecting the activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

 - jackrabbit-2.21.9 was released on 2021-12-10
 - jackrabbit-filevault-3.5.8 was released on 2021-12-22
 - jackrabbit-2.16.9 was released on 2022-01-07
 - jackrabbit-oak-1.42.0 was released on 2022-01-12
 - jackrabbit-oak-1.22.10 was released on 2022-01-24
 - jackrabbit-oak-1.8.26 was released on 2022-02-04
 - jackrabbit-2.21.10 was released on 2022-02-10
 - jackrabbit-oak-1.22.11 was released on 2022-02-24
 - jackrabbit-filevault-3.6.0 was released on 2022-03-02

## JIRA activity:

 - 137 JIRA tickets created in the last 3 months 
 - 108 JIRA tickets closed/resolved in the last 3 months
 