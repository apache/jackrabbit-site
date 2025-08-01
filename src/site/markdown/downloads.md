<!--
   Licensed to the Apache Software Foundation (ASF) under one or more
   contributor license agreements.  See the NOTICE file distributed with
   this work for additional information regarding copyright ownership.
   The ASF licenses this file to You under the Apache License, Version 2.0
   (the "License"); you may not use this file except in compliance with
   the License.  You may obtain a copy of the License at

       https://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
-->

Downloads
=========

Use the links below to download Apache Jackrabbit releases from one of our
mirrors. You should [verify the integrity](#verify) of the files using
the signatures and checksums available from this page.

Please note that some mirrors might not be up-to-date shortly after a
release; in this case wait 12-24 hours until the distribution becomes available
on your preferred mirror.

* Latest stable releases:
    * [Apache Jackrabbit 2.22.x](#v2.22) (Java 11 and later)
    * [Apache Jackrabbit 2.20.x](#v2.20) (Java 8 and later)
    * [Apache Jackrabbit Oak 1.82.0](#latest) (Java 11 and later)
* Latest unstable releases (from trunk):
    * [Apache Jackrabbit 2.23.x](#v2.23) (Java 11 and later)
* Maintenance releases:
    * [Apache Jackrabbit Oak 1.22.x](#oak1.22) (Java 8 to Java 13)
* Latest stable OCM release: [Apache Jackrabbit OCM 2.0.0](#ocm)
* Latest stable FileVault releases:
    * [Apache Jackrabbit FileVault 4.0.0](#vlt) (Java 11 and later)
    * [Apache Jackrabbit FileVault 3.8.4](#vlt8) (Java 8 and later)
    * [Apache Jackrabbit FileVault 3.2.8](#vltjava7) (Java 7 and later)
* Latest stable FileVault Plugin release: [Apache Jackrabbit FileVault Package Maven Plugin 1.4.0](#vltplg)
* [Release Archive](#archive)

Apache Jackrabbit releases are available under the [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
See the `NOTICE.txt` file contained in each release artifact for applicable copyright attribution notices.
Some Jackrabbit components contain external code with licenses that meet [Apache licensing policies](https://www.apache.org/legal/resolved.html).
See the `LICENSE.txt` file contained in each release artifact for applicable licenses.



<a class='anchor' name='v2.22'></a>
Apache Jackrabbit 2.22.2 (2025-08-01)
-------------------------------------
Apache Jackrabbit 2.22.2 is an incremental feature release based on
and compatible with earlier stable Jackrabbit 2.x releases. Jackrabbit
2.22.x releases are considered stable and targeted for production use.

See the [full release notes](https://downloads.apache.org/jackrabbit/2.22.2/RELEASE-NOTES.txt) for more details.

* [jackrabbit-2.22.2-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/2.22.2/jackrabbit-2.22.2-src.zip)
    (13M, source zip, [pgp](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-2.22.2-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-2.22.2-src.zip.sha512))

* [jackrabbit-standalone-2.22.2.jar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.22.2/jackrabbit-standalone-2.22.2.jar)
    (100M, standalone server, [pgp](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-standalone-2.22.2.jar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-standalone-2.22.2.jar.sha512))

* [jackrabbit-webapp-2.22.2.war](https://www.apache.org/dyn/closer.lua/jackrabbit/2.22.2/jackrabbit-webapp-2.22.2.war)
    (45M, web application, [pgp](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-webapp-2.22.2.war.asc), [sha512](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-webapp-2.22.2.war.sha512))

* [jackrabbit-jca-2.22.2.rar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.22.2/jackrabbit-jca-2.22.2.rar)
    (43M, JCA resource adapter, [pgp](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-jca-2.22.2.rar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.22.2/jackrabbit-jca-2.22.2.rar.sha512))




<a class='anchor' name='vlt'></a>
Apache Jackrabbit FileVault 4.0.0 (July 31st, 2025)
----------------------------------------------------
Jackrabbit FileVault 4.0.0 is the latest stable release of the repository content synchronization tool. This version is only compatible with Java 11 or newer. The OSGi bundles depend on Jackrabbit 2.20.17+ (JCR Commons, SPI, SPI Commons), Oak Jackrabbit API 1.22.4+, Commons IO 2.7+, Commons Collections 4.1+ and SLF4J 1.7+.

See the [full release notes](https://downloads.apache.org/jackrabbit/filevault/4.0.0/RELEASE-NOTES.txt) for more details.

* [jackrabbit-filevault-4.0.0-source-release.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/filevault/4.0.0/jackrabbit-filevault-4.0.0-source-release.zip)
    (3M, source zip, [pgp](https://downloads.apache.org/jackrabbit/filevault/4.0.0/jackrabbit-filevault-4.0.0-source-release.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/filevault/jackrabbit-filevault-4.0.0-source-release.zip.sha512))
* Binaries (and also sources) are provided via [Maven Central](https://central.sonatype.org/) with [group id `org.apache.jackrabbit.vault`](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/)

Also see the Jackrabbit FileVault [documentation](/filevault/index.html) for more information about this project.





<a class='anchor' name='v2.20'></a>
Apache Jackrabbit 2.20.17 (2025-07-14)
--------------------------------------
Apache Jackrabbit 2.20.17 is an incremental feature release based on
and compatible with earlier stable Jackrabbit 2.x releases. Jackrabbit
2.20.x releases are considered stable and targeted for production use.

See the [full release notes](https://downloads.apache.org/jackrabbit/2.20.17/RELEASE-NOTES.txt) for more details.

* [jackrabbit-2.20.17-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/2.20.17/jackrabbit-2.20.17-src.zip)
    (13M, source zip, [pgp](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-2.20.17-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-2.20.17-src.zip.sha512))

* [jackrabbit-standalone-2.20.17.jar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.20.17/jackrabbit-standalone-2.20.17.jar)
    (105M, standalone server, [pgp](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-standalone-2.20.17.jar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-standalone-2.20.17.jar.sha512))

* [jackrabbit-webapp-2.20.17.war](https://www.apache.org/dyn/closer.lua/jackrabbit/2.20.17/jackrabbit-webapp-2.20.17.war)
    (48M, web application, [pgp](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-webapp-2.20.17.war.asc), [sha512](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-webapp-2.20.17.war.sha512))

* [jackrabbit-jca-2.20.17.rar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.20.17/jackrabbit-jca-2.20.17.rar)
    (46M, JCA resource adapter, [pgp](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-jca-2.20.17.rar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.20.17/jackrabbit-jca-2.20.17.rar.sha512))



<a class='anchor' name='v2.23'></a>
Apache Jackrabbit 2.23.2-beta (2025-07-14)
--------------------------------------------------
Apache Jackrabbit 2.23.2-beta is an unstable release cut directly from
Jackrabbit trunk, with a focus on new features and other
improvements. For production use we recommend the latest stable 2.22.x
release.

See the [full release notes](https://downloads.apache.org/jackrabbit/2.23.2-beta/RELEASE-NOTES.txt) for more details.

* [jackrabbit-2.23.2-beta-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/2.23.2-beta/jackrabbit-2.23.2-beta-src.zip)
    (13M, source zip, [pgp](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-2.23.2-beta-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-2.23.2-beta-src.zip.sha512))

* [jackrabbit-standalone-2.23.2-beta.jar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.23.2-beta/jackrabbit-standalone-2.23.2-beta.jar)
    (100M, standalone server, [pgp](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-standalone-2.23.2-beta.jar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-standalone-2.23.2-beta.jar.sha512))

* [jackrabbit-webapp-2.23.2-beta.war](https://www.apache.org/dyn/closer.lua/jackrabbit/2.23.2-beta/jackrabbit-webapp-2.23.2-beta.war)
    (45M, web application, [pgp](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-webapp-2.23.2-beta.war.asc), [sha512](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-webapp-2.23.2-beta.war.sha512))

* [jackrabbit-jca-2.23.2-beta.rar](https://www.apache.org/dyn/closer.lua/jackrabbit/2.23.2-beta/jackrabbit-jca-2.23.2-beta.rar)
    (43M, JCA resource adapter, [pgp](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-jca-2.23.2-beta.rar.asc), [sha512](https://downloads.apache.org/jackrabbit/2.23.2-beta/jackrabbit-jca-2.23.2-beta.rar.sha512))




<a class='anchor' name='latest'></a>
Apache Jackrabbit Oak 1.82.0 (2025-07-03)
-----------------------------------------
Apache Jackrabbit Oak 1.82.0 is an incremental feature release based
on and compatible with earlier stable Jackrabbit Oak 1.x
releases. This release is considered stable and targeted for
production use.

See the [full release notes](https://downloads.apache.org/jackrabbit/oak/1.82.0/RELEASE-NOTES.txt) for more details.

* [jackrabbit-oak-1.82.0-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/oak/1.82.0/jackrabbit-oak-1.82.0-src.zip)
    (20M, source zip, [pgp](https://downloads.apache.org/jackrabbit/oak/1.82.0/jackrabbit-oak-1.82.0-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/oak/1.82.0/jackrabbit-oak-1.82.0-src.zip.sha512))



<a class='anchor' name='oak1.22'></a>
Apache Jackrabbit Oak 1.22.22 (March 27th, 2025)
----------------------------------------------------
Apache Jackrabbit Oak 1.22.22 is an incremental feature release based on
and compatible with earlier stable Jackrabbit Oak 1.22.x
releases. Jackrabbit Oak 1.22.x releases are considered stable and
targeted for production use.

See the [full release notes](https://downloads.apache.org/jackrabbit/oak/1.22.22/RELEASE-NOTES.txt) for more details.

* [jackrabbit-oak-1.22.22-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/oak/1.22.22/jackrabbit-oak-1.22.22-src.zip)
    (17M, source zip, [pgp](https://downloads.apache.org/jackrabbit/oak/1.22.22/jackrabbit-oak-1.22.22-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/oak/1.22.22/jackrabbit-oak-1.22.22-src.zip.sha512))




<a class='anchor' name='vlt8'></a>
Apache Jackrabbit FileVault 3.8.4 (March 28th, 2025)
----------------------------------------------------
Jackrabbit FileVault 3.8.4 is the latest stable release of the repository content synchronization tool. This version is only compatible with Java 8 or newer. The OSGi bundles depend on Jackrabbit 2.20.8+ (JCR Commons, SPI, SPI Commons), Oak Jackrabbit API 1.22.4+, Commons IO 2.7+, Commons Collections 4.1+ and SLF4J 1.7+.

See the [full release notes](https://downloads.apache.org/jackrabbit/filevault/3.8.4/RELEASE-NOTES.txt) for more details.

* [jackrabbit-filevault-3.8.4-source-release.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/filevault/3.8.4/jackrabbit-filevault-3.8.4-source-release.zip)
    (3M, source zip, [pgp](https://downloads.apache.org/jackrabbit/filevault/3.8.4/jackrabbit-filevault-3.8.4-source-release.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/filevault/3.8.4/jackrabbit-filevault-3.8.4-source-release.zip.sha512))
* Binaries (and also sources) are provided via [Maven Central](https://central.sonatype.org/) with [group id `org.apache.jackrabbit.vault`](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/)

Also see the Jackrabbit FileVault [documentation](/filevault/index.html) for more information about this project.




<a class='anchor' name='vltjava7'></a>
Apache Jackrabbit FileVault 3.2.8 (March 21st, 2019)
--------------------------------------------------
Jackrabbit FileVault 3.2.8 is the latest stable release of repository content synchronization tool still compatible with Java 7. If possible use FileVault 3.4.0 or newer which requires Java 8.

See the [full release notes](https://downloads.apache.org/jackrabbit/filevault/3.2.8/RELEASE-NOTES.txt) for more details.

* [jackrabbit-filevault-3.2.8-src.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/filevault/3.2.8/jackrabbit-filevault-3.2.8-src.zip)
    (1.5M, source zip, [pgp](https://downloads.apache.org/jackrabbit/filevault/3.2.8/jackrabbit-filevault-3.2.8-src.zip.asc), [sha512](https://downloads.apache.org/jackrabbit/filevault/3.2.8/jackrabbit-filevault-3.2.8-src.zip.sha512))
* Binaries (and also sources) are provided via [Maven Central](https://central.sonatype.org/) with [group id `org.apache.jackrabbit.vault`](https://repo1.maven.org/maven2/org/apache/jackrabbit/vault/)

Also see the Jackrabbit FileVault [documentation](/filevault/index.html) for more information about this project.




<a class='anchor' name='vltplg'></a>
Apache Jackrabbit FileVault Package Maven Plugin 1.4.0 (October 1st, 2024)
------------------------------------------------------------------------
Jackrabbit FileVault Package Maven Plugin 1.4.0 is the latest stable release of the FileVault content package Maven plugin.

See the [full release notes](https://downloads.apache.org/jackrabbit/filevault-package-maven-plugin/1.4.0/RELEASE-NOTES.md) for more details.

* [filevault-package-maven-plugin-1.4.0-source-release.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/filevault-package-maven-plugin/1.4.0/filevault-package-maven-plugin-1.4.0-source-release.zip)
    (1.5M, source zip, [PGP signature](https://downloads.apache.org/jackrabbit/filevault-package-maven-plugin/1.4.0/filevault-package-maven-plugin-1.4.0-source-release.zip.asc))
    * [SHA512 checksum](https://downloads.apache.org/jackrabbit/filevault-package-maven-plugin/1.4.0/filevault-package-maven-plugin-1.4.0-source-release.zip.sha512)

Also see the Jackrabbit FileVault Package Maven Plugin [documentation](/filevault-package-maven-plugin/index.html) for more information about this project.




<a class='anchor' name='ocm'></a>
Apache Jackrabbit OCM 2.0.0 (10-July-2012)
------------------------------------------
Apache Jackrabbit OCM 2.0.0  is release that contains fixes and improvements over Jackrabbit OCM 1.5.
Apart from the test classes, it does not depend on Apache Jackrabbit core, but only on the JCR 2.0 specification

See the [full release notes](https://downloads.apache.org/jackrabbit/ocm/2.0.0/RELEASE-NOTES.txt) for more details.

* [jackrabbit-ocm-2.0.0-source-release.zip](https://www.apache.org/dyn/closer.lua/jackrabbit/ocm/2.0.0/jackrabbit-ocm-2.0.0-source-release.zip)
    (518K, source zip, [PGP signature](https://downloads.apache.org/jackrabbit/ocm/2.0.0/jackrabbit-ocm-2.0.0-source-release.zip.asc), [sha1](https://downloads.apache.org/jackrabbit/ocm/2.0.0/jackrabbit-ocm-2.0.0-source-release.zip.sha1))


<a class='anchor' name='archive'></a>
Release Archive
---------------
Only current recommended releases are available on the main distribution
site and its mirrors. Older releases are available from the [archive download site](http://archive.apache.org/dist/jackrabbit/).


<a class='anchor' name='verify'></a>
Verify
------

It is essential that you verify the integrity of the downloaded files using the PGP signatures or SHA512 checksums.
Please read [Verifying Apache HTTP Server Releases](http://httpd.apache.org/dev/verification.html) for more information
on why you should verify our releases.

The PGP signatures can be verified using PGP or GPG. First download the [KEYS](https://downloads.apache.org/jackrabbit/KEYS)
file as well as the `.asc` signature files for the relevant release packages. Make sure you get these files from
the [main distribution directory](https://downloads.apache.org/jackrabbit/), rather than from a mirror.

Then verify the signatures using

    % pgpk -a KEYS
    % pgpv jackrabbit-X.Y.Z-src.zip.asc

or

    % pgp -ka KEYS
    % pgp jackrabbit-X.Y.Z-src.zip.asc

or

    % gpg --import KEYS
    % gpg --verify jackrabbit-X.Y.Z-src.zip.asc jackrabbit-X.Y.Z-src.zip


Alternatively, you can verify the SHA512 checksums on the files. For checking the SHA512 checksums, use the program
called `sha512sum` ([GNU core utilities](http://www.gnu.org/software/coreutils/)), or, alternatively, `openssl`.
Windows users can use 'CertUtil` ([doc](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/certutil))
or use the equivalent *nix tools as part of their Cygwin or Linux subsystems.
