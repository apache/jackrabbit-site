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

Jackrabbit Status June 2009
===========================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
We made the following releases from the 1.5 branch:

* Apache Jackrabbit 1.5.4 on April 7th
* Apache Jackrabbit 1.5.5 on April 28th
* Apache Jackrabbit 1.5.6 on June 4th

We also made the first alpha release of the upcoming Jackrabbit 2.0:

* Apache Jackrabbit 2.0 alpha1 on June 4th


Legal
-----
The current Jackrabbit trunk and the 2.0 alpha1 release have a system
dependency to an early "for review only" version of the JCR 2.0 API jar
from JSR 283. No major concerns were raised when this case was discussed on
the legal-discuss@ mailing list.


Community / Development
-----------------------
Jackrabbit was present at the ApacheCon EU where we also organized a quite
successful JCR meetup.

The CMIS effort that started in the Jackrabbit sandbox has now become the
Apache Chemistry project in the Incubator. The other podling with
Jackrabbit as the sponsoring PMC, Apache Sling, is just about to graduate
into a standalone TLP.

The JCR 2.0 specification (JSR 283) is expected to become final in a few
months, as soon as we've completed the required RI and TCK work in
Jackrabbit trunk. We're producing source-only alpha releases of the 2.0
codebase to give people a chance to review all the new features and to
better track our progress.

We are also planning to release Jackrabbit 1.6 as the last minor release
from the 1.x branch that's still based on the JCR 1.0 API.


Infrastructure
--------------
We are about to start using the Nexus installation at repository.apache.org
for staging and deploying our releases to the Maven repository.
