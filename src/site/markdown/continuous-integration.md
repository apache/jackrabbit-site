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
Apache Jackrabbit 2 uses [Jenkins](https://www.jenkins.io/) for continuous integration builds while
Apache Jackrabbit Oak uses [GitHub Actions](https://github.com/features/actions).

Build targets and schedule
--------------------------
See the [Jenkins Jackrabbit page](https://ci-builds.apache.org/job/Jackrabbit/)
on the Jenkins server for the list of configured Jackrabbit builds and
their current status. For Jackrabbit Oak, refer to the [GitHub Actions page](https://github.com/apache/jackrabbit-oak/actions/workflows/build.yml).

The builds are configured to daily check the Git repository for updates
and to run builds whenever there are changes (in the relevant branches). Build and test errors are
reported on the dev@ mailing list.
