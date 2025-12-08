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
Apache Jackrabbit: Board Report December 2025 (draft)
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
Apache Jackrabbit was founded 2006-03-15 (20 years ago).

There are currently 60 committers and 60 PMC members in this project.
The Committer-to-PMC ratio is 1:1, because all committers automatically
become PMC members.

Community changes, past quarter:
- No new PMC members. Last addition was Alejandro Moratinos on 2025-08-27.
- No new committers. Last addition was Alejandro Moratinos on 2025-08-27.

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

Jackrabbit Oak release 1.88.0 updated a first module to use the new AWS
SDK for Java 2.x version. The previous version 1.x will be end-of-life
by the end of 2025. Additional work is ongoing to update remaining usage
of AWS SDK 1.x in future Jackrabbit Oak releases.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-oak-1.86.0 was released on 2025-09-22
- jackrabbit-oak-1.22.23 was released on 2025-10-03
- jackrabbit-filevault-4.1.4 was released on 2025-10-24
- jackrabbit-oak-1.88.0 was released on 2025-11-04

## JIRA activity:

- 174 JIRA tickets created in the last 3 months
- 148 JIRA tickets closed/resolved in the last 3 months
