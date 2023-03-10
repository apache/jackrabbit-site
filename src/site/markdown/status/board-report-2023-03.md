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
Apache Jackrabbit: Board Report March 2023 (draft)
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
foundation of modern world-class websites and other demanding 
content applications. In contrast to its predecessor, Oak does not 
implement all optional features from the JSR specifications, and it 
is not a reference implementation. 
   
## Issues: 
There are no issues requiring board attention at this time.
   
## Membership Data:

Apache Jackrabbit was founded 2006-03-15 (17 years ago)
There are currently 58 committers and 58 PMC members in this project.
The Committer-to-PMC ratio is 1:1.

Community changes, past quarter:
- No new PMC members. Last addition was Joerg Hoh on 2022-07-01.
- No new committers. Last addition was Joerg Hoh on 2022-07-01.

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

The project team decided to require Java 11 as the minimum version
for new feature releases. Apache Jackrabbit Oak 1.48.0 is the last
release supporting Java 8.

A roadmap has been outlined how to update the Guava dependency. The
next Jackrabbit Oak release will make usage of deprecated APIs
exposing Guava more visible by logging warn and error messages.
Later this year the team plans to introduce a wrapped Guava version
for Jackrabbit Oak internal use and then remove deprecated APIs.

## Community Health:
The project is healthy with a continuous stream of traffic mostly on
JIRA issues and GitHub pull requests reflecting activity of the
respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- filevault-package-maven-plugin-1.3.2 was released on 2022-12-16
- jackrabbit-oak-1.46.0 was released on 2022-12-21
- jackrabbit-2.20.8 was released on 2023-01-09
- jackrabbit-filevault-3.6.8 was released on 2023-01-10
- jackrabbit-oak-1.22.14 was released on 2023-01-19
- jackrabbit-oak-1.48.0 was released on 2023-01-27
- jackrabbit-2.21.15 was released on 2023-02-10
- jackrabbit-2.20.9 was released on 2023-03-10

## JIRA activity:

- 168 JIRA tickets created in the last 3 months
- 146 JIRA tickets closed/resolved in the last 3 months
 