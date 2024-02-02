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

Jackrabbit Site Generation
==========================

[![Apache License, Version 2.0, January 2004](https://img.shields.io/github/license/apache/maven.svg?label=License)][license]
[![Jenkins Status](https://img.shields.io/jenkins/s/https/ci-builds.apache.org/job/Jackrabbit/job/jackrabbit-site/job/main.svg)][build]

This is the Git repository for the content of <https://jackrabbit.apache.org/jcr/>. 
Further information in [website](src/site/markdown/website.md).

The Jackrabbit site lives as Markdown files in `src/site/markdown` such
that it easy to view e.g. from GitHub. This project only generates the
content below <https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr>, otherwise
the scm-publish mechanism is too slow, checking out the entire site.

The Maven site plugin is used to build the web site as follows:

1. In this project's directory execute:

   ````
   $ mvn site
   ````

2. Review the site at `target/site/index.html`

3. Commit and push your changes to the source files

### Automatic Deployment

The `main` branch is automatically built on the [ASF Jenkins][build] after every commit and the results are automatically committed to <https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr> from where the Website is being populated.

### Manual Deployment

1. Build and deploy the site to <https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr> using:

   ````
   $ mvn site-deploy
   ````

2. Finally review the site at <https://jackrabbit.apache.org/jcr>.

Note: To skip the final commit use `-Dscmpublish.skipCheckin=true`. You can then
review all pending changes in `target/scmpublish-checkout` and follow
up with `svn commit` manually.


Note: Every committer should be able to deploy the site. Deployment is done via svn commit to
`https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr`. 
The credentials are retrieved from a server with `id` *apache.releases.https* from the [Maven Settings](https://maven.apache.org/settings.html). Alternatively
one can provide the credentials explicitly via `-Dpassword` and `-Dusername` ([maven-scm-publish-plugin:publish-scm](https://maven.apache.org/plugins/maven-scm-publish-plugin/publish-scm-mojo.html)).


[jira]: https://issues.apache.org/jira/projects/JCRSITE/
[license]: https://www.apache.org/licenses/LICENSE-2.0
[build]: https://ci-builds.apache.org/job/Jackrabbit/job/jackrabbit-site/job/main/
