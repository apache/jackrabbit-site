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

Jackrabbit Status March 2008
============================
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.


Releases
--------
Apache Jackrabbit 1.4 was released in January.

We are considering switching to releasing individual components in a more
frequent and fine-grained manner. So far Jackrabbit releases have contained
new versions of all Jackrabbit components.

The first component release, jackrabbit-core 1.4.1, was made in February.


Legal
-----
Apache Jackrabbit uses or bundles no cryptographic code, so there is no
need for export control notifications.

We have identified a minor license violation by an external party bundling
Jackrabbit code without meeting all the ALv2 requirements (no NOTICE file,
etc.). With help from the legal team, we have notified the party in
question and expect the issue to be resolved soon.


Community
---------
The Jackrabbit PMC has voted to invite Esteban Franqueiro to be a
Jackrabbit committer and PMC member. We are waiting for the CLA to proceed
with the committer account and other administrative bits.

We are planning to have a JCR community gathering event right next to the
ApacheCon EU next month in Amsterdam.


Development
-----------
The 1.4 release was well received, and with increased usage we've also seen
many requests to make the default installation and out-of-the-box
experience smoother for new users. We're working on addressing those needs.

The ongoing work towards the JCR 2.0 reference implementation continues,
and with major new features and changes entering the codebase we may see
some instability of the trunk during the months ahead. On the other hand
there's recently been much focus on improving test coverage and more test
automation, which should help us maintain stability of the codebase.

Some of our users are not yet ready to upgrade from 1.3 to 1.4, so we are
working on the 1.3 maintenance branch to produce a 1.3.4 release with
selected bug fixes and improvements from newer releases.


Infrastructure
--------------
Our web site is now managed using Confluence.

We have had problems with our private Continuum installation in the
Jackrabbit zone, and so we are currently migrating our CI builds to the
Hudson zone.
