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
Apache Jackrabbit: Board Report September 2026 (draft)
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

Two more Jackrabbit Oak 2.x feature releases were cut in this period,
Oak 2.4.0 in July and Oak 2.6.0 in August, continuing the regular
release cadence on the current Java 17 baseline. The oak-blob-azure
module gained support for the Azure SDK V12, a large change
that modernizes the Azure blob storage integration. The build was also
updated to Apache Parent POM 39, and Groovy was upgraded to 4.0.33 so
that the project builds on Java 26. Routine dependency maintenance
continued at a steady pace across the MongoDB, AWS, Netty, Jackson,
Tomcat and testing libraries.

Query processing and indexing again saw the most concentrated work,
mostly on the Elasticsearch backend. Improvements covered index
provisioning and more graceful handling of missing indexes, reduced
document counts for dynamic boost, and better use of thread pools for
async response processing. Fulltext indexing was made more robust
around indexing-rule changes, overlong facet properties and other
query edge cases.

Work on the caching layer continued the migration towards Caffeine,
with cache maintenance now running asynchronously, precomputed element
count and weight in the persistent disk cache, a fixed bound for the
disk cache and a new cache for service lookups. Several obsolete
feature toggles were removed as the features they guarded became the
default (full GC, embedded verification and the prefetch code path,
among others). In addition, a project-level security threat model was
contributed and wired for automated discoverability through
THREAT_MODEL.md and the AGENTS.md / SECURITY.md chain.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-2.23.5-beta was released on 2026-07-06
- jackrabbit-oak-2.4.0 was released on 2026-07-14
- jackrabbit-2.22.4 was released on 2026-08-06
- jackrabbit-oak-2.6.0 was released on 2026-08-24

## JIRA activity:

- 166 JIRA tickets created in the last 3 months
- 123 JIRA tickets closed/resolved in the last 3 months
