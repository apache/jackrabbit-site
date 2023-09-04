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
Apache Jackrabbit: Board Report September 2023 (draft)
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

## Project Status: 
The project is ongoing with moderate activity.

There are no issues requiring board attention at this time.

## Membership Data:

There are currently 58 committers and 58 PMC members in this project.
The Committer-to-PMC ratio is 1:1.

Community changes, past quarter:
- Dominique Pfister resigned on 2023-07-17
- No new committers. Last addition was Rishabh Daim on 2023-04-06.

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

The project team introduced a shaded version of Guava and replaced
usage of plain Guava with the shaded version. Only one transitive
dependency through an Azure SDK library is left. The plan is to remove
this final dependency in the next Jackrabbit Oak release. 

On June 29th a vulnerability was reported to the security mailing list.
The remote code execution in Jackrabbit RMI was handled with
CVE-2023-37895 and releases with a fix published on July 25th. 

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-oak-1.22.16 was released on 2023-07-17
- jackrabbit-filevault-3.7.0 was released on 2023-07-19
- jackrabbit-2.21.18 was released on 2023-07-24
- jackrabbit-2.20.11 was released on 2023-07-24
- filevault-package-maven-plugin-1.3.4 was released on 2023-07-24
- jackrabbit-oak-1.54.0 was released on 2023-07-24
- jackrabbit-2.21.19 was released on 2023-08-11
- jackrabbit-oak-1.56.0 was released on 2023-09-01

## JIRA activity:

- 156 JIRA tickets created in the last 3 months
- 118 JIRA tickets closed/resolved in the last 3 months
