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

### Part I: up to the release vote

1. Consider checking the CVE database for vulnerabilities in dependencies,
   using `mvn org.owasp:dependency-check-maven:5.3.2:aggregate` (first run will be slow because CVE
   databases are downloaded and parsed). If dependencies need action, open tickets and make sure they
   are marked as candidate backports where applicable.        
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
6. When releasing a Jackrabbit version that will be used in Oak, make sure it
   doesn't break Oak.
     * Check by building the applicable Oak version using `mvn clean install -PintegrationTesting -Djackrabbit.version=2.x.y-SNAPSHOT`
     * If the update does require changes in Oak, open JIRA tickets and link them to the JIRA tickets tracking the release activity.
7. If this is a stable branch, review changes to export versions which should be avoided (see [OAK-6346](https://issues.apache.org/jira/browse/OAK-6346) for context). If there are indeed changes (as in the example below), see [Appendix E](#Appendix_E:_Version_Changes).

        # Oak 1.8 as of November 2018
        svn diff https://svn.apache.org/repos/asf/jackrabbit/oak/tags/jackrabbit-oak-1.8.8 . | grep -i "@Version" -B 6
        -@Version("1.5.0")
        +@Version("1.6.0")
8. On the other hand, if this is a release from trunk, carefully review all
   export versions and check that no change introduces new dependencies on
   Guava (see [OAK-7182](https://issues.apache.org/jira/browse/OAK-7182))
9. If this is a release with Java 7 or older, make sure that your `MAVEN_OPTS` contain `-Dhttps.protocols=TLSv1.2`.
10. When doing "stable" release (even-numbered), check that we do not have
   dependencies to unstable releases. In particular, stable releases of Oak
   should not reference unstable Jackrabbit releases (if this is the case,
   a new stable Jackrabbit release might be required in order to proceed).
11. Build and deploy the release artifacts with Maven. See [below](#Steps_to_build_the_release_artifacts) for the exact steps.
12. Do a sanity check that the [staged repository](https://repository.apache.org/index.html#stagingRepositories) on repository.apache.org contains all artifacts (~19 projects for Jackrabbit).
13. Close the staged repository, giving it a meaningful name, such as "Apache Jackrabbit 2.x.y RC"
14. Upload the artifacts to https://dist.apache.org/repos/dist/dev/jackrabbit/ as follows:

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

15. Find the vote template (`./target/checkout/target/vote.txt`) generated by the Maven build and follow the instructions to verify the build yourself
16. Start the vote thread by emailing the applicable mailing list ([Jackrabbit](mailto:dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20x.y.z), [Oak](mailto:oak-dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20Oak%20x.y.z))
17. Mark the version as released in Jira: [Jackrabbit Jira](https://issues.apache.org/jira/plugins/servlet/project-config/JCR/versions),
   [Oak Jira](https://issues.apache.org/jira/plugins/servlet/project-config/OAK/versions). You'll see all the defined project versions. From the settings menu, choose 'Release' on the version.
18. Wait 72 hours (we usually allow three business days, so be careful when a weekend is ahead)

### Part II: after the release vote
   
If the vote fails (easy case first) remove the tag from svn, drop the staged repository, revert the version release in Jira, and announce that the vote has failed by replying to the vote email.

Otherwise:

1. Close the vote by publishing the results, replying to the original vote mail.
2. Copy the release candidate from dev/jackrabbit to release/jackrabbit in https://dist.apache.org/repos/dist/ (for Jackrabbit, `version` is just the version number, for Oak it is prefixed with `oak/`, reflecting the directory structure) -- **be careful to properly set the version variable!!!**

        [ "x$version" = "x" ] || svn move -m "Apache Jackrabbit $version" \
        https://dist.apache.org/repos/dist/dev/jackrabbit/$version \
        https://dist.apache.org/repos/dist/release/jackrabbit/$version

3. Delete any older releases from the same branch (they're automatically archived)
4. Release the [staged repository](https://repository.apache.org/index.html#stagingRepositories) for synchronization to Maven central.
    * make sure this step actually succeeded (we have seen a case where it failed and a retry was needed)
5. Close all the issues included in the release: [Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) or [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) -> Choose the released version -> select "View in Issue Navigator". From the issue list you have the option to bulk update all of the included issues. Just 'Transition Issues' from 'Resolved' to 'Closed' and you are done!
6. Update the Jackrabbit web site to point to the new release ([SVN](https://svn.apache.org/repos/asf/jackrabbit/site/trunk/)).
    * add an entry to `index.md`
    * update `downloads.md` (see [below](#Creating_Markdown_for_Downloads_Page)) - while doing so please a) remove obsoleted entries, and b) move new entries for Jackrabbit and/or Oak to the top)
    * don't forget to deploy the site (`mvn site-deploy`)
7. Send a release announcement to the [applicable mailing lists](mailto:announce@apache.org,announce@jackrabbit.apache.org,users@jackrabbit.apache.org,dev@jackrabbit.apache.org,oak-dev@jackrabbit.apache.org?subject=%5BANNOUNCE%5D%20Apache%20Jackrabbit%20...%20released) once the web site and download mirrors have been synced (template generated in `./target/checkout/target/announcement.txt`). Please note the announce mails needs to be sent from an @apache.org address.
8. If the release was a Jackrabbit release used in Oak, make sure to also update the dependency (and potentiall the Javadoc link) in oak-parent/pom.xml (example: [OAK-4743](https://issues.apache.org/jira/browse/OAK-4743) - the current mapping is Jackrabbit 2.20 -> Oak trunk and Oak 1.22, Jackrabbit 2.18 -> Oak 1.10, Jackrabbit 2.16 -> Oak 1.8, Jackrabbit 2.14 -> Oak 1.6, Jackrabbit 2.12 -> Oak 1.4 and 1.2)
9. If the release was an Oak release used in Jackrabbit (for jackrabbit-api), make sure to also update the dependency in jackrabbit-parent/pom.xml (example: [JCR-4492](https://issues.apache.org/jira/browse/JCR-4492) - the current mapping is Oak latest stable -> Jackrabbit trunk and 2.20)
10. If the release was a stable release for which we publish API docs (such as Jackrabbit), consider updating the live site (https://svn.apache.org/repos/asf/jackrabbit/site/live/ - when producing the API docs, use a checkout of the actual release, specify an English locale (-Dlocale=en) and try to pick the right JDK version to minimize changes over the previously checked in docs).
11. If the release was a stable release that is used for the baseline check in trunk (right now: Jackrabbit 2.20 and Oak 1.10), update trunk accordingly (example: [JCR-4312](https://issues.apache.org/jira/browse/JCR-4312))
12. Check that all subprojects now have the correct version; if not, fix them (for instance, oak-doc and oak-doc-railroad-macro are not in the reactor pom and therefore not updated)

Steps to build the release artifacts
------------------------------------
The release is built using the Maven release plugin (if your platform is Windows with Cygwin, see [Appendix C](#Appendix_C:_Cygwin)). See the [Performing a Maven Project Release](https://maven.apache.org/developers/release/maven-project-release-procedure.html) guide for more details. Make sure you have added the pgp key information in you maven settings file, especially if you have more than one key installed locally. See [Appendix B](#b) for the details.

In case you don't feel comfortable to keep the passwords in the file `~/.m2/settings.xml` forever, you need to set it now temporarily.

There have been some problems with certain combinations of Java and Maven versions. A known combinations where releasing was successful is Java 7 with Maven 3.2.2. In case you get an exception "Proxy Error" in the `release:perform`, see the [Apache Services Status Page](http://status.apache.org/), however it has been reported that the status page is not always accurate. In case you get an error with respect to API incompatibilities, try with an older Maven version or enforce use of a newer release plugin, such as with `mvn org.apache.maven.plugins:maven-release-plugin:2.5.3:prepare`.

1. Execute mvn `release:prepare`. This will update the POM files and tag the release in svn (see [Appendix F](#Appendix_F:_Version_Numbers) for how version numbers change).
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


Appendix E: Version Changes
---------------------------

**HERE BE DRAGONS**

In general, changes in stable branches should not change export versions, in order to avoid version conflicts with the ongoing development on the unstable branch. So avoid, avoid, avoid!

If the version change really is required, then it is mandatory to check that the new API is identical with the API in other release branches with the same version number.

To check, for example for a version change in Oak 1.6.13-SNAPSHOT:

1. Checkout Oak 1.8.

2. Edit the parent pom to use a comparisonVersion of "1.6.3-SNAPSHOT". Release branches normally use the default, so the property needs to be added to the maven bundle plugin configuration.

3. Build and watch for baseline plugin errors.

...then repeat the above steps with subsequent branches and trunk.

Also, check with the "dev" mailing list to confirm that this change is ok.


Appendix F: Version Numbers
---------------------------

**Jackrabbit**

Classic Jackrabbit uses even minor version numbers for stable releases, and uneven
numbers for unstable releases. For instance, as of September 2019, the latest
stable release was "2.18.3", and the latest unstable release was "2.19.4".

Stable releases are cut from a branch, where the branch name is based on
major and minor version number (here: "2.18"). Unstable releases are built from
trunk.

Creating a new major release implies creating a new branch (next would be "2.20"), see
[Appendix D](#Appendix_D:_Branching).

For creating releases, the default version numbers proposed by `mvn release:prepare`
work out of the box.

**Oak**

Oak historically used the same scheme, and moved away from that with "1.10.0" in 
Spring 2019.

Rather than creating unstable releases from trunk, we now create a stable release
every time. These keep the even minor numbers, so as of September 2019, the sequence
of releases since the change was: "1.12.0", "1.14.0", "1.16.0", and "1.18.0".

Creating releases from branches continues to work just like for classic Jackrabbit.
However, when cutting a new stable release from trunk, the default version numbers
suggested by `mvn release:prepare` need to be overridden.

For instance, when cutting "1.20.0", the next development release will be
"1.21-SNAPSHOT", not "1.22-SNAPSHOT". The following stable release would then
be "1.22.0".





