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
Apache Jackrabbit: Board Report June 2020 (draft)
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
There are no issues requiring board attention at this time.
   
## Activity: 
Apache Jackrabbit Oak receives most attention nowadays. All 
maintenance branches and the main development branch are 
continuously seeing moderate to high activity.

We continue making regular feature releases of Jackrabbit Oak. The
most recent release was Jackrabbit Oak 1.30.0 that was made available
on May 27th.  

A vulnerability report was sent to the security list on June 4th.
The Jackrabbit team is discussing the report and will likely reject
it (https://s.apache.org/7qhh5).

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

On March 26th the team retired the Apache Jackrabbit 2.8 branch.
Users of Apache Jackrabbit are encouraged to upgrade to 2.20 for
Java 8, 2.14 for Java 7 or 2.12 for Java 6.

On March 31st the team retired the Apache Jackrabbit Oak 1.0 branch.
Users of Apache Jackrabbit Oak are encouraged to upgrade to 1.26.0
for Java 8, 1.6.20 for Java 7 or 1.2.31 for Java 6.

On April 6th the team retired the Apache Jackrabbit Oak 1.10 branch.
Users of Apache Jackrabbit Oak are encouraged to upgrade to the
latest release of the newest maintenance branch (1.22.3).

## Health report: 
The project is healthy with a continuous stream of traffic on all 
mailing lists reflecting the activity of the respective component. 

There is a wide range of topics being discussed on the dev and user
lists as well as on the various JIRA issues. 

Commit activity is moderate to high mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

The report about a potential vulnerability to the security mailing
list revealed that only a small group of mostly passive PMC members
are subscribed to the security list. The PMC members were asked to
subscribe to the security list in order to add active members to
the list. 

In the last 3 months the project added two new committers and PMC
members. 

Martijn Hendriks contacted the PMC and expressed his desire to resign.
His resignation from the PMC and committer base became effective
on June 5th after his confirmation that he also wants to be removed
as a committer.

## PMC changes:

 - Currently 56 PMC members.
 - Martijn Hendriks resigned on 2020-06-05
 - Vinod Holani was added to the PMC on 2020-05-11
 - Fabrizio Fortino was added to the PMC on 2020-05-22 

## Committer base changes:

 - Currently 56 committers.
 - Martijn Hendriks resigned on 2020-06-05
 - Vinod Holani was added as committer on 2020-05-09
 - Fabrizio Fortino was added as committer on 2020-05-21 

## Releases:

 - jackrabbit-2.18.5 was released on 2020-03-06
 - jackrabbit-oak-1.22.2 was released on 2020-03-16
 - jackrabbit-oak-1.8.21 was released on 2020-03-23
 - jackrabbit-oak-1.26.0 was released on 2020-03-25
 - jackrabbit-2.16.6 was released on 2020-04-07
 - jackrabbit-oak-1.22.3 was released on 2020-04-21
 - jackrabbit-2.21.1 was released on 2020-05-11
 - jackrabbit-oak-1.8.22 was released on 2020-05-23
 - jackrabbit-oak-1.30.0 was released on 2020-05-27

## JIRA activity:

 - 224 JIRA tickets created in the last 3 months 
 - 236 JIRA tickets closed/resolved in the last 3 months 