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
Apache Jackrabbit: Board Report June 2024 (draft)
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
Apache Jackrabbit was founded 2006-03-15 (18 years ago).

There are currently 59 committers and 59 PMC members in this project.
The Committer-to-PMC ratio is 1:1, because all committers automatically
become PMC members.

Community changes, past quarter:
- No new PMC members. Last addition was Nuno Santos on 2023-11-14.
- No new committers. Last addition was Nuno Santos on 2023-11-13.

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

Steffen Van suggested introducing a code formatter for the Jackrabbit
Oak code base. The proposal sparked a discussion on the mailing list
and a corresponding pull request. Jackrabbit committers voiced concerns
about the impact on git diff readability and backporting of changes to
maintenance branches. No decision has been made yet.

A new revision garbage collection feature was added to Jackrabbit Oak.
The feature is disabled by default and can be enabled with a feature
toggle. Additional work is in progress to control the type of garbage
that is collected.

After some confusion about the Jackrabbit even/odd minor version scheme,
the team decided to add a -beta suffix to releases with an odd minor
version number. The first release with the new versioning scheme was
Jackrabbit 2.21.26-beta on March 28th.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-2.20.15 was released on 2024-03-11
- jackrabbit-oak-1.22.19 was released on 2024-03-14
- jackrabbit-2.21.26-beta was released on 2024-03-28
- jackrabbit-oak-1.62.0 was released on 2024-04-09
- jackrabbit-2.20.16 was released on 2024-05-13
- jackrabbit-oak-1.22.20 was released on 2024-05-13
- jackrabbit-oak-1.64.0 was released on 2024-05-27

## JIRA activity:

- 207 JIRA tickets created in the last 3 months
- 179 JIRA tickets closed/resolved in the last 3 months
