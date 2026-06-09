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
Apache Jackrabbit: Board Report June 2026 (draft)
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

Jackrabbit Oak 2.0.0 was released as the first major Oak release that
requires Java 17. This follows the earlier work to raise the minimum
Java version across build and CI, and gives the project a current Java
baseline for future development while maintenance branches continue to
serve older runtime requirements.

The ongoing effort to reduce dependence on Google's Guava library made
substantial progress. Oak introduced its own cache API and Caffeine based
implementations, added compatibility tests, and migrated cache usage in
document store, search, segment store, blob, S3 and Azure components.
Follow-up work refined cache statistics, eviction behaviour and exception
handling to preserve compatibility with existing Guava based behaviour.

Indexing and query processing continued to receive significant attention.
Changes improved index cost estimation, LIMIT aware index selection,
Lucene and Elastic index version handling, Elastic async response
processing, subtree deletion handling and diagnostics. Additional tests
were added for facets, KNN queries, deleted Lucene documents and related
query edge cases.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-2.23.4-beta was released on 2026-04-10
- jackrabbit-oak-2.0.0 was released on 2026-04-21
- jackrabbit-oak-1.22.24 was released on 2026-04-28
- jackrabbit-oak-2.2.0 was released on 2026-06-02

## JIRA activity:

- 131 JIRA tickets created in the last 3 months
- 101 JIRA tickets closed/resolved in the last 3 months
