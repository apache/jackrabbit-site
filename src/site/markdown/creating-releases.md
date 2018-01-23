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

Creating Releases
=================
This is a how to document for creating Apache Jackrabbit releases. It
documents the current release process and needs to be updated as we move
forward.


Release planning
----------------
Jackrabbit releases are created based on user demand and the availability
of fixes and other requested changes. Any committer can declare their plan
to cut a release by sending a "Apache Jackrabbit x.y.z release plan"
message to the dev@ list. The plan should refer to Jira for the list of
fixes to be included in the release and give a rough estimate of the
release schedule. It's OK to revise the plan if needed. Optimally, link to
the candidate release notes.

If you're not a committer, you can send a message to the mailing list
asking for a new release to be made. Including the list of specific fixes
you need and a short rationale of why you need the release.


Prerequisites for release managers
----------------------------------
You need to be a Jackrabbit committer to prepare and perform a release, but
anyone is welcome to help test the release candidates and comment on the
release plans.

You should have a code signing key that is included in the Jackrabbit KEYS
file. See [Appendix A](#Appendix_A:_Create_and_add_your_key_to_the_Jackrabbit_KEYS_file) at the end of this page for more details.

You also need to tell Maven your Subversion credentials needed for
deploying artifacts to the Nexus server at https://repository.apache.org/.
See [Appendix B](#Appendix_B:_Maven_settings) for the required settings.


Release management tasks
------------------------
1. When releasing from trunk, consider checking the CVE database for vulnerabilities in dependencies, using `mvn org.owasp:dependency-check-maven:3.0.2:aggregate` (first run will be slow because CVE databases are downloaded and parsed). If dependencies need action, open tickets and make sure they are marked as candidate backports where applicable.        
2. Make sure that an appropriate version for the release is entered in Jira 
   ([Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page),
   [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page))
   and that all the related issues have been resolved. 
3. Create a new version in JIRA for the next release.
4. Create a `RELEASE-NOTES.txt` file in the root folder of the project to be released. 
    If such a file already exists, update it for the release. See a previous 
    release notes for examples of what to include. The release note report in Jira is a 
    useful source of required information: Open the [Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page)
    or [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page) page, 
    click on the release, then on the "Release Notes" link on the top.
    Double-check that all version numbers in the updated Release Notes are accurate.
    When done, commit the file.
5. If the branch is one that requires Java 8 or newer, make sure that the API docs can indeed be built with Java 8, using both `javadoc:javadoc` and `javadoc:jar`.
6. Build and deploy the release artifacts with Maven. See [below](#Steps_to_build_the_release_artifacts) for the exact steps.
7. Do a sanity check that the [staged repository](https://repository.apache.org/index.html#stagingRepositories) on repository.apache.org contains all artifacts (~19 projects for Jackrabbit).
8. Close the staged repository, giving it a meaningful name, such as "Apache Jackrabbit 2.x.y RC"
9. Upload the artifacts to https://dist.apache.org/repos/dist/dev/jackrabbit/ (instructions at the end of the build)

        # TARGET - where https://dist.apache.org/repos/dist/dev/jackrabbit/ is checked out
        # SOURCE - where the release was built
    
     For Jackrabbit:
        
        cd $TARGET
        scp -r $SOURCE/target/checkout/target/$version $version
        svn add $version
        svn commit -m "Apache Jackrabbit $version release candidate" $version

     For Oak:
        
        cd $TARGET
        scp -r $SOURCE/target/checkout/target/$version oak/$version
        svn add oak/$version
        svn commit -m "Apache Jackrabbit Oak $version release candidate" oak/$version

9. Find the vote template (`vote.txt`) generated by the Maven build and follow the instructions to verify the build yourself
10. Start the vote thread by emailing the applicable mailing list ([Jackrabbit](mailto:dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20x.y.z), [Oak](mailto:oak-dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20Oak%20x.y.z))
11. Wait 72 hours (we usually allow three business days, so be careful when a weekend is ahead)
12. Mark the version as released in Jira: [Jackrabbit Jira](https://issues.apache.org/jira/plugins/servlet/project-config/JCR/versions),
   [Oak Jira](https://issues.apache.org/jira/plugins/servlet/project-config/OAK/versions). You'll see all the defined project versions. From the settings menu, choose 'Release' on the version.
13. If the vote fails (easy case first) remove the tag from svn, drop the staged repository and revert the version release in Jira - done
14. If the vote is successful
    * close the vote by publishing the results
    * copy the release candidate from dev/jackrabbit to release/jackrabbit in https://dist.apache.org/repos/dist/ -- **be careful to properly set the version variable!!!**

        [ "x$version" = "x" ] || svn move -m "Apache Jackrabbit $version" \
        https://dist.apache.org/repos/dist/dev/jackrabbit/$version \
        https://dist.apache.org/repos/dist/release/jackrabbit/$version

    * delete any older releases from the same branch (they're automatically archived)
    * release the [staged repository](https://repository.apache.org/index.html#stagingRepositories) for synchronization to Maven central.
    * make sure the previous step actually succeeded (we have seen a case where it failed and a retry was needed)
    * close all the issues included in the release: [Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) or [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) -> Choose the released version -> select "View in Issue Navigator". From the issue list you have the option to bulk update all of the included issues. Just 'Transition Issues' from 'Resolved' to 'Closed' and you are done!

15. Update the Jackrabbit web site to point to the new release ([SVN](https://svn.apache.org/repos/asf/jackrabbit/site/trunk/)).
    1. index.md
    2. downloads.md (see [below](#Creating_Markdown_for_Downloads_Page)) - while doing so please a) remove obsoleted entries, and b) move new entries for Jackrabbit and/or Oak to the top)
16. Send a release announcement to the [applicable mailing lists](mailto:announce@apache.org,announce@jackrabbit.apache.org,users@jackrabbit.apache.org,dev@jackrabbit.apache.org,oak-dev@jackrabbit.apache.org?subject=%5BANNOUNCE%5D%20Apache%20Jackrabbit%20...%20released) once the web site and download mirrors have been synced (see [example](http://mail-archives.apache.org/mod_mbox/jackrabbit-announce/201712.mbox/%3C894e13d2-9e20-1819-4741-b09ed040be09%40apache.org%3E)). Please note the announce mails needs to be sent from an @apache.org address.
17. If the release was a Jackrabbit release used in Oak, make sure to also update the dependency in oak-parent/pom.xml (example: [OAK-4743](https://issues.apache.org/jira/browse/OAK-4743) - the current mapping is Jackrabbit 2.17 -> Oak trunk, Jackrabbit 2.16 -> Oak 1.8, Jackrabbit 2.14 -> Oak 1.6, Jackrabbit 2.12 -> Oak 1.4 and 1.2, Jackrabbit 2.8 -> Oak 1.0)
18. If the release was a stable release for which we publish API docs (such as Jackrabbit), consider updating the live site (https://svn.apache.org/repos/asf/jackrabbit/site/live/ - when producing the API docs, use a checkout of the actual release, specify an English locale (-Dlocale=en) and try to pick the right JDK version to minimize changes over the previously checked in docs).


Steps to build the release artifacts
------------------------------------
The release is built using the Maven release plugin (if your platform is Windows with Cygwin, see [Appendix C](#Appendix_C:_Cygwin)). See the [Performing a Maven Project Release](https://maven.apache.org/developers/release/maven-project-release-procedure.html) guide for more details. Make sure you have added the pgp key information in you maven settings file, especially if you have more than one key installed locally. See [Appendix B](#b) for the details.

In case you don't feel comfortable to keep the passwords in the file `~/.m2/settings.xml` forever, you need to set it now temporarily.

There have been some problems with certain combinations of Java and Maven versions. A known combinations where releasing was successful is Java 7 with Maven 3.2.2. In case you get an exception "Proxy Error" in the `release:perform`, see the [Apache Services Status Page](http://status.apache.org/), however it has been reported that the status page is not always accurate. In case you get an error with respect to API incompatibilities, try with an older Maven version or enforce use of a newer release plugin, such as with `mvn org.apache.maven.plugins:maven-release-plugin:2.5.3:prepare`.

1. Execute mvn `release:prepare`. This will update the POM files and tag the release in svn.
2. Execute mvn `release:perform`. This will build the tagged release and deploy the artifacts to a staging repository on repository.apache.org. The non-Maven release artifacts are automatically deployed to your home directory on people.apache.org. You only need to add the keyname if you have multiple keys and the code signing keys is not your default key.

After this is done, you can remove the passwords from the file `~/.m2/settings.xml` if you don't want to keep it there.


Creating Markdown for Downloads Page
------------------------------------
A [shell script](https://dist.apache.org/repos/dist/dev/jackrabbit/create-download-md.sh) is available for generating the downloads links for the mark down source,
to be run in a checkout of the [release folder](https://dist.apache.org/repos/dist/release/jackrabbit/).
Usage:

        $ cd path-of-jackrabbit-releases
        
For Jackrabbit:

        $ sh create-download-md.sh version
        
such as:                

        $ sh create-download-md.sh 2.14.4

For Oak:

        $ sh create-download-md.sh oak/version
   
such as:                

        $ sh create-download-md.sh oak/1.6.6



Related Links
-------------
* http://www.apache.org/dev/release.html
* http://www.apache.org/dev/release-signing.html
* http://wiki.apache.org/incubator/SigningReleases
* http://www.apache.org/dev/repository-faq.html


Appendix A: Create and add your key to the Jackrabbit KEYS file
---------------------------------------------------------------
Follow these instructions to generate your code signing key and to add it
to the Jackrabbit KEYS file.

1. [Generate a code signing key](http://www.apache.org/dev/release-signing.html#generate)
    using your @apache.org address as the email and "CODE SIGNING KEY" as the comment. Also make sure it has been sent to a public key server.
2. The Jackrabbit KEYS file is managed in https://dist.apache.org/repos/dist/release/jackrabbit/KEYS. To modify the file, first checkout the dist directory:
    
        svn checkout https://dist.apache.org/repos/dist/release/jackrabbit

3. See [instructions on how to append your key to the file](http://www.apache.org/dev/release-signing.html#keys-policy) (or, as an alternative, the beginning of the KEYS file).
4. Commit the change using:

        svn commit -m "Add code signing key" KEYS

5. See the changes on http://www.apache.org/dist/jackrabbit/KEYS (you may need to wait a few minutes).

You can (but don't need to) get your key [linked to the Apache web of trust](http://www.apache.org/dev/release-signing.html#apache-wot). Once other people have signed your key, you can update the KEYS file with the signatures you've received.

Appendix B: Maven settings
--------------------------
You need to change the `~/.m2/settings.xml` file as follows. PGP key id: this is the second part of your key in the KEYS file. For example, this is "F07CA77B" if the first line of your key in the KEYS file is "pub 4096R/F07CA77B 2014-07-31". In case you are not comfortable to keep passwords and key passphrases in human readable files, you can add them just before doing the release, and remove them just after the release. Instead of using the "gpg.passphrase" tag, you can try using `<gpg.executable>gpg2</gpg.executable>` (this should prompt you for the passphrase). For the server svn passwords, you could use the [Maven password encryption](http://maven.apache.org/guides/mini/guide-encryption.html).

    <settings>
      <profiles>
        <profile>
          <id>apache-release</id>
          <properties>
            <gpg.keyname><!-- PGP key id, see above --></gpg.keyname>
            <gpg.passphrase><!-- PGP key passphrase --></gpg.passphrase>
          </properties>
        </profile>
        ...
      </profiles>
      <servers>
        <!-- To deploy a Jackrabbit snapshot -->
        <server>
          <id>apache.snapshots.https</id>
          <username><!-- Apache svn user name --></username>
          <password><!-- Apache svn password --></password>
        </server>
        <!-- To stage a Jackrabbit release -->
        <server>
          <id>apache.releases.https</id>
          <username><!-- Apache svn user name --></username>
          <password><!-- Apache svn password --></password>
        </server>
        ...
      </servers>
    </settings>

Appendix C: Cygwin
------------------

The Subversion support in the release plugin assumes platform-specific path delimiters, and thus does not work properly if the "svn" executable is the Cygwin version. The easiest workaround for this problem is to install a Windows-native SVN version as well, and to modify the PATH variable for the mvn invocation so that it's found instead of the Cygwin variant.

Appendix D: Branching
---------------------

The following notes were collected while branching Jackrabbit 2.16:

Create a JIRA ticket for branching and the subsequent releases of new the branch and trunk; example: [JCR-4216](https://issues.apache.org/jira/browse/JCR-4216).

Create the branch:

    mvn release:branch -DbranchName=2.16 -DdevelopmentVersion=2.17.0-SNAPSHOT

Set the development version on the new branch:

    cd path-to-branch-checkout
    mvn release:update-versions -DautoVersionSubmodules=true -DdevelopmentVersion=2.16.0-SNAPSHOT
    
Open a ticket so that once the first release for the branch is made, the `comparisonVersion` for the `bundle:baseline` check is updated both in the branch and on trunk; example: [JCR-4218](https://issues.apache.org/jira/browse/JCR-4218).

Create release notes to include all of the changes accumulated - for 2.16.0 this means including all changes labeled with `fixVersion` set to `2.16`. Note that any change labeled with `fixVersion` set to any 2.15.* release should have `fixVersion: 2.16` as well, unless the change is irrelevant for the release notes.



