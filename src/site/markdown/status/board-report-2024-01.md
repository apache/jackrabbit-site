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
Apache Jackrabbit: Board Report January 2024 (draft)
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
Apache Jackrabbit was founded 2006-03-15 (18 years ago)
There are currently 59 committers and 59 PMC members in this project.
The Committer-to-PMC ratio is 1:1, because all committers automatically
become PMC members.

Community changes, past quarter:
- Nuno Santos was added to the PMC on 2023-11-14
- Nuno Santos was added as committer on 2023-11-13

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

In October a significant code contribution to Jackrabbit Oak was made
by a non-committer (Lucas Weitzendorf). The contribution adds support
for parallel compaction of a segment store.

Throughout the last quarter the indexing component of Jackrabbit Oak
has seen a lot of activity. The team has been working on a more efficient
way to index large repositories.

Migration to Jakarta APIs saw some progress with good collaboration
between different Apache project teams. However, the migration requires
many changes while the team also wants to keep modules compatible with
the current version of the Servlet API.

In December the classic Jackrabbit code base was migrated from SVN to
Git. The only remaining module in SVN is the project website, but there
are plans to migrate that as well.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-2.20.12 was released on 2023-09-08
- jackrabbit-oak-1.22.17 was released on 2023-09-15
- jackrabbit-2.21.20 was released on 2023-10-11
- jackrabbit-oak-1.58.0 was released on 2023-10-16
- jackrabbit-filevault-3.7.2 was released on 2023-11-04
- jackrabbit-2.20.13 was released on 2023-11-07
- filevault-package-maven-plugin-1.3.6 was released on 2023-11-16
- jackrabbit-oak-1.22.18 was released on 2023-12-01
- jackrabbit-oak-1.60.0 was released on 2023-12-06
- jackrabbit-2.21.21 was released on 2023-12-12
- jackrabbit-2.21.22 was released on 2023-12-19

## JIRA activity:

- 140 JIRA tickets created in the last 3 months
- 131 JIRA tickets closed/resolved in the last 3 months
