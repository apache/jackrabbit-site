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
Apache Jackrabbit: Board Report September 2025 (draft)
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
foundation of modern world-class websites and other demanding 
content applications. In contrast to its predecessor, Oak does not 
implement all optional features from the JSR specifications, and it 
is not a reference implementation. 

## Project Status: 
Current project status: Ongoing with moderate activity

Issues for the board: none

## Membership Data:
Apache Jackrabbit was founded 2006-03-15 (19 years ago).

There are currently 60 committers and 60 PMC members in this project.
The Committer-to-PMC ratio is 1:1, because all committers automatically
become PMC members.

Community changes, past quarter:
- Alejandro Moratinos was added to the PMC on 2025-08-27
- Alejandro Moratinos was added as committer on 2025-08-27

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

The team is further reducing usage of Google's Guava library and
Jackrabbit Oak is now using Java features or Apache Commons alternatives
where possible. The long term goal is to remove the dependency on Guava. 

Jackrabbit Oak release 1.84.0 updated the MongoDB driver from 3.12.14 to
5.2.1. This update required many code changes because the new MongoDB
driver version is not backward compatible. The new driver version ensures
compatibility with future MongoDB server versions and officially supports
Java 21.

Early July a security vulnerability (CVE-2025-53689) was reported. The
team released fixes for multiple versions of Jackrabbit on July 14th.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-oak-1.82.0 was released on 2025-07-03
- jackrabbit-2.20.17 was released on 2025-07-14
- jackrabbit-2.22.1 was released on 2025-07-14
- jackrabbit-2.23.2-beta was released on 2025-07-14
- jackrabbit-filevault-4.0.0 was released on 2025-07-31
- jackrabbit-2.22.2 was released on 2025-08-01
- jackrabbit-oak-1.84.0 was released on 2025-08-14

## JIRA activity:

- 187 JIRA tickets created in the last 3 months
- 158 JIRA tickets closed/resolved in the last 3 months
