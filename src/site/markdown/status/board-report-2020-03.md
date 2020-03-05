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
Apache Jackrabbit: Board Report March 2020 (draft)
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
most recent release was Jackrabbit Oak 1.24.0 that was made available
on January 28th.  

The upcoming Jackrabbit Oak 1.26.0 release will finally remove usage
of java.security.acl.Group, a deprecated interface that will be removed
in Java 14.

A security issue was reported on January 22nd on the private list.
The issue was very well handled by Angela Schreiber and Julian Reschke
and within a week new releases were made available that contained
a fix. The security issue was initially discovered by Andrew Khoury and
Russ Wright of Adobe. Details on the security issue are available in
https://issues.apache.org/jira/browse/OAK-8870 and
https://nvd.nist.gov/vuln/detail/CVE-2020-1940

Apache Jackrabbit itself is mostly in maintenance mode with most of 
the work going into bug fixing and tooling. New features are mainly
driven by dependencies from Jackrabbit Oak.

## Health report: 
The project is healthy with a continuous stream of traffic on all 
mailing lists reflecting the activity of the respective component. 

There is a wide range of topics being discussed on the dev and user
lists as well as on the various JIRA issues. 

Commit activity is moderate to high mirroring the activity on the 
JIRA issues and the desire of the individual contributors to bring
features and improvements in for the next Jackrabbit Oak release.

Jukka Zitting contacted the PMC and expressed his desire to go
emeritus. His resignation from the PMC and committer base became
effective after a 72 hour wait period on March 6th.

## PMC changes:

 - Currently 55 PMC members.
 - Jukka Zitting resigned on 2020-03-06
 - No new PMC members. Last additions were Mohit Kataria and Nitin
 Gupta on 2019-08-08.

## Committer base changes:

 - Currently 55 committers.
 - Jukka Zitting resigned on 2020-03-06
 - No new committers. Last additions were Mohit Kataria and Nitin
 Gupta on 2019-08-08. 

## Releases:

 - jackrabbit-oak-1.10.7 was released on 2019-12-12
 - jackrabbit-2.20.0 was released on 2020-01-07
 - jackrabbit-oak-1.6.19 was released on 2020-01-13
 - jackrabbit-oak-1.22.0 was released on 2020-01-16
 - jackrabbit-oak-1.4.25 was released on 2020-01-20
 - jackrabbit-oak-1.8.19 was released on 2020-01-23
 - jackrabbit-oak-1.24.0 was released on 2020-01-28
 - jackrabbit-oak-1.10.8 was released on 2020-01-28
 - jackrabbit-oak-1.8.20 was released on 2020-01-31
 - jackrabbit-oak-1.6.20 was released on 2020-02-05
 - jackrabbit-oak-1.22.1 was released on 2020-02-13
 - jackrabbit-2.21.0 was released on 2020-02-14
 - jackrabbit-oak-1.4.26 was released on 2020-02-19 

## JIRA activity:

 - 157 JIRA tickets created in the last 3 months 
 - 130 JIRA tickets closed/resolved in the last 3 months 