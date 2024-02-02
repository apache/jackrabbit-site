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

Website
=======

The [Apache Jackrabbit website](http://jackrabbit.apache.org/) is generated with the [maven-site-plugin](https://maven.apache.org/plugins/maven-site-plugin/) from Markdown sources in different Git repositories:

1. <https://github.com/apache/jackrabbit-site> for the path [`\jcr`](https://jackrabbit.apache.org/jcr/)
1. <https://github.com/apache/jackrabbit-oak/tree/trunk/oak-doc> for the path [`\oak`](https://jackrabbit.apache.org/oak/docs/)
1. <https://github.com/apache/jackrabbit-filevault> for the path [`\filevault`](https://jackrabbit.apache.org/filevault/)
1. <https://jackrabbit.apache.org/filevault-package-maven-plugin/> for the path [`\filevault-package-maven-plugin`](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
1. Every other path is maintained directly within <https://svn.apache.org/repos/asf/jackrabbit/site/live/> only.

Publishing works by committing the *generated* pages and assets to the dedicated SVN directory <https://svn.apache.org/repos/asf/jackrabbit/site/live/>.
From there the [svnpubsub mechanism from ASF](https://infra.apache.org/project-site.html#tools) publishes the content in <https://jackrabbit.apache.org>.

Only [Jackrabbit committers](jackrabbit-team.html) are allowed to modify the site content but contributions from anyone via pull requests are highly appreciated.

Usually each page also has an edit button next to the breadcrumb which everyone can use to easily contributes changes.

The website's usage is tracked through [Matomo](https://privacy.apache.org/matomo/) (without leveraging Cookies or collecting PII data). Everyone can inspect the metrics via <https://analytics.apache.org/index.php?module=CoreHome&action=index&date=yesterday&period=day&idSite=4>.

