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
Apache Jackrabbit: Board Report June 2019
=========================================

## Description: 
The Apache Jackrabbit™ content repository is a fully conforming
implementation of the Content Repository for Java™ Technology API
(JCR, specified in JSR 170 and 283). The Jackrabbit content 
repository is stable, largely feature complete and actively being
maintained. 
Jackrabbit Oak is an effort to implement a scalable and performant 
hierarchical content repository as a modern successor to the Apache
Jackrabbit content repository. It is targeted for use as the 
foundation of modern world-class web sites and other demanding  
content applications. In contrast to its predecessor, Oak does not 
implement all optional features from the JSR specifications and it 
is not a reference implementation. 
   
## Issues: 
There are no issues requiring board attention at this time   
   
## Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the unstable development branch are 
continuously seeing moderate to high activity.

We made our 7th feature release of Jackrabbit Oak (1.14) in June. 

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

We changed the release strategy for Jackrabbit Oak. The aim is to reduce
the number of maintained branches in the long run and deliver new features
to users more frequently. Feature releases are now planned roughly ever
two months. See https://s.apache.org/9SYQ on oak-dev for details.

A hackathon was held in Basel this quarter (https://s.apache.org/LRn6).
Various topics were discussed during the hackathon, including the
planned Apache MoinMoin Wiki decommission, making it easier for
developers to run proposed changes through a CI/CD pipeline and a
prototype for asynchronous commits.

As part of the hackathon the Apache Jackrabbit MoinMoin Wiki was archived
(https://s.apache.org/7rDN) and the project will no longer use a Wiki
system.

## Health report: 
The project is healthy with a continuous stream of traffic on all 
mailing lists reflecting the activity of the respective component. 

There is a wide range of topics being discussed on the dev and user
lists as well as on the various JIRA issues. 

Commit activity is moderate to high mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

## PMC changes: 
   
 - Currently 52 PMC members. 
 - No new PMC members added in the last 3 months 
 - Last PMC addition was Woonsan Ko on Tue Sep 25 2018
 - The PMC elected Marcel Reutegger as the new chair effective April 17th.
   
## Committer base changes: 
   
 - Currently 52 committers. 
 - No new committers added in the last 3 months 
 - Last committer addition was Woonsan Ko at Tue Sep 25 2018 
   
## Releases: 
   
 - jackrabbit-2.14.7 was released on Tue Jun 04 2019 
 - jackrabbit-2.16.4 was released on Wed May 01 2019 
 - jackrabbit-2.18.1 was released on Fri Apr 12 2019 
 - jackrabbit-2.18.2 was released on Thu May 23 2019 
 - jackrabbit-2.19.2 was released on Fri Apr 05 2019 
 - jackrabbit-2.19.3 was released on Mon May 06 2019 
 - jackrabbit-oak-1.10.2 was released on Mon Mar 18 2019 
 - jackrabbit-oak-1.12.0 was released on Tue Apr 09 2019 
 - jackrabbit-oak-1.14.0 was released on Wed Jun 05 2019 
 - jackrabbit-oak-1.6.17 was released on Mon Apr 08 2019 
 - jackrabbit-oak-1.8.13 was released on Mon May 06 2019 
 - jackrabbit-filevault-3.2.8 was released on Fri Mar 22 2019 
   
   
## JIRA activity: 
   
 - 301 JIRA tickets created in the last 3 months 
 - 270 JIRA tickets closed/resolved in the last 3 months 