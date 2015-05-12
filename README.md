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
The Jackrabbit site lives as Markdown files in `src/site/markdown` such
that it easy to view e.g. from GitHub. This project only generates the
content below `https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr`, otherwise
the scm-publish mechanism is too slow, checking out the entire site.

The Maven site plugin can be used to build and deploy a web site as follows:

1. In this project build the site with:

   ````
   $ mvn site
   ````

2. Review the site at `target/site/index.html`

3. Deploy the site to `http://jackrabbit.apache.org/jcr` using:

   ````
   $ mvn site-deploy
   ````

4. Finally review the site at `http://jackrabbit.apache.org/`.

Note: To skip the final commit use `-Dscmpublish.skipCheckin=true`. You can then
review all pending changes in `target/scmpublish-checkout` and follow
up with `svn commit` manually.


Note: Every committer should be able to deploy the site. No fiddling with
credentials needed since deployment is done via svn commit to
`https://svn.apache.org/repos/asf/jackrabbit/site/live/jcr`.

