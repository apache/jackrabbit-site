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
Apache Jackrabbit: Board Report March 2026 (draft)
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

The oak-blob-azure module was upgraded from Azure SDK V8 to V12, a
major dependency and API change. The project also raised the minimum
Java version to 17 across build and CI (OAK-11952), and delivered
simplified index management (OAK-12010 / OAK-12110), introducing a new
index management path with diff index support and refinements across
multiple releases.

Segment store reliability saw important improvements. The
oak-segment-azure component received memory optimisations (UUID
and GCGeneration handling, structure changes), and test stability
fixes to address OutOfMemory issues by ensuring proper cleanup of
FileStores and closeable resources (OAK-12085). The GCGeneration
class was moved into an exported SPI package (OAK-12084), clarifying
the public API for segment and GC generation.

The ongoing effort to reduce dependence on Google Guava continued.
Guava’s Monitor, Guard, SettableFuture, Striped locks,
Uninterruptibles (await, sleep, join, drain), ThreadFactoryBuilder,
and related utilities were replaced with JDK or oak-commons
equivalents. Guava dependencies were removed from several modules as
part of the long-term goal to drop the Guava dependency.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component.

Commit activity is moderate, mirroring the activity on the
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-2.23.3-beta released on 2025-12-11
- jackrabbit-oak-1.90.0 was released on 2026-01-07
- jackrabbit-2.22.3 was released on 2026-01-16
- jackrabbit-filevault-4.2.0 was released on 2026-02-27
- jackrabbit-oak-1.92.0 was released on 2026-03-03

## JIRA activity:

- 129 JIRA tickets created in the last 3 months
- 108 JIRA tickets closed/resolved in the last 3 months
