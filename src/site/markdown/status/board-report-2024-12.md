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
Apache Jackrabbit: Board Report December 2024 (draft)
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
Apache Jackrabbit was founded 2006-03-15 (19 years ago).

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

The team reduced usage of Google's Guava library significantly and
Jackrabbit Oak is now using Java features where possible. The long
term goal is to remove the dependency on Guava.

Work on migrating Jackrabbit Oak from Azure SDK 8.x to 12.x has been
picked up again and is ongoing. Azure SDK 8.x is no longer supported
and a migration to 12.x is now required.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

In November, a vote was started to add a new committer and PMC member
to the project. The vote was canceled due to lack of votes. Concerns
raised on the private mailing list mentioned that the candidate has
not been active in the project long enough. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-oak-1.22.21 was released on 2024-09-12
- jackrabbit-filevault-3.8.2 was released on 2024-09-25
- filevault-package-maven-plugin-1.4.0 was released on 2024-10-01
- jackrabbit-oak-1.70.0 was released on 2024-10-01
- jackrabbit-2.23.1-beta was released on 2024-10-12
- jackrabbit-oak-1.72.0 was released on 2024-11-14

## JIRA activity:

- 226 JIRA tickets created in the last 3 months
- 190 JIRA tickets closed/resolved in the last 3 months
