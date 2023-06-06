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
Apache Jackrabbit: Board Report June 2023 (draft)
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
There are currently 59 committers and 59 PMC members in this project.
The Committer-to-PMC ratio is 1:1.

Community changes, past quarter:
- Rishabh Daim was added to the PMC on 2023-04-06
- Rishabh Daim was added as committer on 2023-04-06

## Project Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

The project team started to replace the plain Guava dependency in 
Jackrabbit Oak with a shaded version. This allows us to more easily
update Guava without interfering with users of Jackrabbit Oak.

Maintenance of Jackrabbit 2.16.x and Jackrabbit Oak 1.8.x ended in
May. Announcements have been sent to inform users to migrate to
more recent versions.

## Community Health:
The project is generally healthy with a continuous stream of traffic
mostly on JIRA issues and GitHub pull requests reflecting activity of
the respective component. 

Concerns were raised on the private email list about lack of or little
constructive participation by Jackrabbit committers on the FileVault
subproject. There is a split within the committers. Some would like to
actively evolve FileVault, while others are mostly happy with the status
quo and prefer fewer changes. 

Commit activity is moderate, mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## Releases:

- jackrabbit-oak-1.50.0 was released on 2023-03-23
- jackrabbit-2.21.16 was released on 2023-04-05
- jackrabbit-oak-1.22.15 was released on 2023-04-07
- jackrabbit-2.20.10 was released on 2023-05-08
- jackrabbit-oak-1.52.0 was released on 2023-05-15 

## JIRA activity:

- 167 JIRA tickets created in the last 3 months
- 134 JIRA tickets closed/resolved in the last 3 months
 