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

Continuous Integration
======================
Apache Jackrabbit uses [Hudson](https://hudson.dev.java.net/)
for continuous integration builds. The Jackrabbit builds are a part of the [Hudson zone|http://hudson.zones.apache.org/hudson/]
in the Apache infrastructure. See the [Hudson wiki page](http://wiki.apache.org/general/Hudson)
for more information about the Hudson installation at Apache. The wiki
page also contains instructions on how to get an account if you're a member
of the [Jackrabbit Team](jackrabbit-team.html)
and want to modify the continuous integration settings.


Build targets and schedule
--------------------------
See the [Jackrabbit page](http://hudson.zones.apache.org/hudson/view/Jackrabbit/)
on the Hudson server for the list of configured Jackrabbit builds and
their current status.

The builds are configured to hourly check the Subversion server for updates
and to run builds whenever there are changes. Build and test errors are
reported on the dev@ mailing list.
