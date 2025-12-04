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
This is a "how to" document for creating Apache Jackrabbit (Oak) releases. It
documents the current release process and needs to be updated as we move
forward.

This applies to both Jackrabbit 2.x and Jackrabbit Oak releases. For Jackrabbit FileVault please use the specific documentation at <https://jackrabbit.apache.org/filevault/howto_release.html> and <https://jackrabbit.apache.org/filevault-package-maven-plugin/howto_release.html> respectively.


Release planning
----------------
Jackrabbit releases are created based on user demand and the availability
of fixes and other requested changes. Any committer can declare their plan
to cut a release by sending an "Apache Jackrabbit (Oak) x.y.z Release Plan"
message to the Jackrabbit Developers Mailing List - [dev@jackrabbit.apache.org](mailto:dev@jackrabbit.apache.org) or
Oak Developers Mailing List - [oak-dev@jackrabbit.apache.org](mailto:dev@jackrabbit.apache.org).

The plan should refer to the project version for the list of
fixes to be included in the release and give a rough estimate of the
release schedule. It's OK to revise the plan if needed. Optimally, link to
the candidate release notes.

If you're not a committer, you can send a message to the mailing list
asking for a new release to be made. Including the list of specific fixes
you need and a short rationale of why you need the release.


Prerequisites for release managers
----------------------------------
You need to be a Jackrabbit (Oak) committer to prepare and perform a release, but
anyone is welcome to help test the release candidates and comment on the
release plans.

You should have a code signing key that is included in the Jackrabbit KEYS
file. See [Appendix A](#Appendix_A:_Create_and_add_your_key_to_the_Jackrabbit_KEYS_file) at the end of this page for more details.

You also need to tell Maven your Apache LDAP credentials needed for
deploying artifacts to the Nexus server at https://repository.apache.org/.
See [Appendix B](#Appendix_B:_Maven_settings) for the required settings.

You need write access to the following repositories:

 1. Git: source code - either https://gitbox.apache.org/repos/asf/jackrabbit.git or https://gitbox.apache.org/repos/asf/jackrabbit-oak.git
 2. Git: site - https://gitbox.apache.org/repos/asf/jackrabbit-site.git)
 3. Subversion: test / release: https://dist.apache.org/repos/dist/dev/jackrabbit and https://dist.apache.org/repos/dist/release/jackrabbit

The release announcement needs to be sent from your ASF mail account. It is recommended but not necessary to use that mail account
for all other communication as well.


Release management tasks
------------------------

It is useful but not required to keep track of all release tasks in a Jira ticket.
See https://issues.apache.org/jira/browse/OAK-11840 for an example.

### Part I: up to the release vote

1. Check the CI status of the project ([Jackrabbit Jenkins](https://ci-builds.apache.org/job/Jackrabbit/))
2. Consider checking the CVE database for vulnerabilities in dependencies,
   using `mvn org.owasp:dependency-check-maven:aggregate` (first run will be slow because CVE
   databases are downloaded and parsed). If dependencies need action, open tickets and make sure they
   are marked as candidate backports where applicable.
3. Make sure that an appropriate version for the release is entered in Jira 
   ([Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page),
   [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page))
   and that all the related issues have been resolved.
4. Create a new version in JIRA for the next release (if not present yet).
5. Check for issues that have been resolved but do not have "fixVersion" set - these may need to be updated before creating the release notes ([Jackrabbit Jira](https://issues.apache.org/jira/issues/?jql=project%20%3D%20JCR%20AND%20status%20%3D%20resolved%20AND%20fixVersion%20IS%20EMPTY%20ORDER%20BY%20issuekey%20DESC%20), [Oak Jira](https://issues.apache.org/jira/issues/?jql=project%20%3D%20OAK%20AND%20status%20%3D%20resolved%20AND%20fixVersion%20IS%20EMPTY%20ORDER%20BY%20issuekey%20DESC%20)).
6. If there are issues with a fixVersion but without a positive resolution (such as "abandoned", "won't do", "superceded"), remove all fixVersion entries.
8. Create a `RELEASE-NOTES.txt` file in the root folder of the project to be released. 
    If such a file already exists, update it for the release. See a previous 
    release notes for examples of what to include. The release note report in Jira is a 
    useful source of required information: Open the [Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page)
    or [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page) page,
    click on the release, then on the "Release Notes" link on the top.
    Double-check that all version numbers in the updated Release Notes are accurate. Commit with the Jira tracking issue for the release (if there is one).
8.  Make sure that the API docs can be built, using both `mvn javadoc:javadoc` and `mvn javadoc:aggregate` from the reactor pom.
9.  Make sure that the build succeeds with all Java versions it is supposed to support (trying with the earliest and latest is ok).
10. (Jackrabbit) Make sure that the release does not break Oak.
     * Check by building the applicable Oak version locally using `mvn clean install -PintegrationTesting -Djackrabbit.version=2.x.y-SNAPSHOT`
     * If the update does require changes in Oak, open JIRA tickets and link them to the JIRA tickets tracking the release activity.
11. If this is a stable branch, review changes to export versions which should be avoided (see [OAK-6346](https://issues.apache.org/jira/browse/OAK-6346) for context). If there are indeed changes (as in the example below), see [Appendix E](#Appendix_E:_Version_Changes).

        # Oak 1.8 as of November 2018
        git diff jackrabbit-oak-1.8.0 | grep -i "@Version" -B 6
        -@Version("1.5.0")
        +@Version("1.6.0")
12. On the other hand, if this is a release from trunk, carefully review all
    export versions and check that no change introduces new dependencies on
    Guava (see [OAK-7182](https://issues.apache.org/jira/browse/OAK-7182)).
13. When creating a "stable" release (even-numbered), check that we do not have
    dependencies to unstable releases. In particular, stable releases of Oak
    should not reference unstable Jackrabbit releases (if this is the case,
    a new stable Jackrabbit release might be required in order to proceed).
16. Build and deploy the release artifacts with Maven. See [below](#Steps_to_build_the_release_artifacts) for the exact steps.
17. Mark the version as released in Jira: [Jackrabbit Jira](https://issues.apache.org/jira/plugins/servlet/project-config/JCR/versions),
   [Oak Jira](https://issues.apache.org/jira/plugins/servlet/project-config/OAK/versions). You'll see all the defined project versions. From the settings menu, choose 'Release' on the version.
18. Do a sanity check that the [staged repository](https://repository.apache.org/index.html#stagingRepositories) on repository.apache.org contains all artifacts (~19 projects for Jackrabbit).
19. Close the staged repository, giving it a meaningful name, such as "Apache Jackrabbit 2.x.y RC"
20. Upload the artifacts to https://dist.apache.org/repos/dist/dev/jackrabbit/ as follows:

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

20. Note the URL of the staging repository.
21. Find the "vote" template (`./target/checkout/target/vote.txt`) generated by the Maven build and follow the instructions to verify the build yourself
22. Optional: update the "vote" template to mention the concrete staging repository URL. 
23. Start the vote thread by emailing the applicable mailing list ([Jackrabbit](mailto:dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20x.y.z), [Oak](mailto:oak-dev@jackrabbit.apache.org?subject=%5BVOTE%5D%20Release%20Apache%20Jackrabbit%20Oak%20x.y.z))
24. Wait 72 hours (we usually allow three business days, so be careful when a weekend is ahead)
25. Keep the "announcement" template (`./target/checkout/target/announcement.txt`) for later.

### Part II: after the release vote
   
If the vote fails (easy case first):

- remove the tag from source control,
- drop the staged repository,
- revert the version release in Jira,
- check for JIRA issues that in the meantime have been resolved for the "next" version, and set that version to "this" version,
- and announce that the vote has failed by replying to the vote email.

Otherwise:

1. Close the vote by publishing the results, replying to the original vote mail with a subject line of "[RESULT] [VOTE] Release Apache Jackrabbit ...".
2. Copy the release candidate from dev/jackrabbit to release/jackrabbit in https://dist.apache.org/repos/dist/ (for Jackrabbit, `version` is just the version number, for Oak it is prefixed with `oak/`, reflecting the directory structure) -- **be careful to properly set the version variable!!!**

        [ "x$version" = "x" ] || svn move -m "Apache Jackrabbit $version" \
        https://dist.apache.org/repos/dist/dev/jackrabbit/$version \
        https://dist.apache.org/repos/dist/release/jackrabbit/$version

3. Delete any older releases from the same branch (they're automatically archived)
4. Release the [staged repository](https://repository.apache.org/index.html#stagingRepositories) for synchronization to Maven central.
    * make sure this step actually succeeded (we have seen a case where it failed and a retry was needed)
5. Close all the issues included in the release: [Jackrabbit Jira](https://issues.apache.org/jira/projects/JCR?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) or [Oak Jira](https://issues.apache.org/jira/projects/OAK?selectedItem=com.atlassian.jira.jira-projects-plugin:release-page&amp;status=released) -> Choose the released version -> select "View in Issue Navigator". From the issue list you have the option to bulk update all the included issues. Just 'Transition Issues' from 'Resolved' to 'Closed' and you are done!
6. Update the Jackrabbit website to point to the new release ([GIT](https://github.com/apache/jackrabbit-site)) (the date should be the day when the release was finished).
    * add an entry to `index.md`
    * update `downloads.md` (see [below](#Creating_Markdown_for_Downloads_Page)) - while doing so please a) remove obsoleted entries, and b) move new entries for Jackrabbit and/or Oak to the top)
    * site will be updated by GitHub actions (previously: by deploying the site (`mvn site-deploy`))
    * [example](https://github.com/apache/jackrabbit-site/commit/b13aef04ac89e9f447d5366670545261b5eee4dd)
7. Jackrabbit: If the release was a Jackrabbit release used in Oak, make sure to also update the dependency (and potentially the Javadoc link) in oak-parent/pom.xml (example: [OAK-4743](https://issues.apache.org/jira/browse/OAK-4743) - the current mapping is Jackrabbit 2.22 -> Oak trunk, Jackrabbit 2.10 -> Oak 1.22)
8. Oak: If the previous release was a release used in Jackrabbit (for jackrabbit-api), make sure to also update the dependency in jackrabbit-parent/pom.xml (example: [JCR-4492](https://issues.apache.org/jira/browse/JCR-4492) - the current mapping is Oak latest stable -> Jackrabbit trunk and 2.22
9. Jackrabbit: consider updating the live site (https://svn.apache.org/repos/asf/jackrabbit/site/live/ - when producing the API docs, use a checkout of the actual release, specify an English locale (-Dlocale=en) and try to pick the right JDK version to minimize changes over the previously checked in docs).
10. Jackrabbit: If the release was a stable release that is used for the baseline check in trunk (right now: Jackrabbit 2.22), update trunk accordingly (example: [JCR-4312](https://issues.apache.org/jira/browse/JCR-4312))
11. Oak: oak-doc and oak-doc-railroad-macro are not in the reactor pom, thus need a manual update of version numbers
12. Send a release announcement to the
    [applicable mailing lists](mailto:announce@apache.org,announce@jackrabbit.apache.org,users@jackrabbit.apache.org,dev@jackrabbit.apache.org,oak-dev@jackrabbit.apache.org?subject=%5BANNOUNCE%5D%20Apache%20Jackrabbit%20...%20released)
    once the website and download mirrors have been synced (template generated in `./target/checkout/target/announcement.txt` -- note that mirrors may need up to 12 hours!).
    Please note the announcement mails needs to be sent from an @apache.org address.
    In case you are using a mailbox other than apache mailbox (such as gmail) to send mails for your apache address, make sure to send them in plain text format.
    (Warning: the announcement mailing lists are moderated. That means that mails could be rejected for various reasons, such as actual errors in the announcement or simply for the fact that the list moderators missed the requests. So check your inbox.)

Steps to build the release artifacts
------------------------------------
The release is built using the Maven release plugin (if your platform is Windows with Cygwin, see [Appendix C](#Appendix_C:_Cygwin)). See the [Performing a Maven Project Release](https://maven.apache.org/developers/release/maven-project-release-procedure.html) guide for more details. Make sure you have added the pgp key information in you maven settings file, especially if you have more than one key installed locally. See [Appendix B](#b) for the details.

In case you don't feel comfortable to keep the passwords in the file `~/.m2/settings.xml` forever, you need to set it now temporarily.

Note that preparing the release requires a tagging operation in the source
repository. Make sure upfront that non-interactive commits work 
(like `svn commit -m 'commit message'` or `git push`) without prompting for credentials, otherwise
the tagging step will fail.

1. Execute mvn `release:prepare`. This will update the POM files and tag the release in Git (see [Appendix F](#Appendix_F:_Version_Numbers) for how version numbers change).
2. Execute mvn `release:perform`. This will build the tagged release and deploy the artifacts to a staging repository on repository.apache.org. The non-Maven release artifacts are automatically deployed to your home directory on people.apache.org. You only need to add the key name if you have multiple keys and the code signing keys is not your default key.
3. Capture the URL of the staging repository; it can be added to the Vote email.

After this is done, you can remove the passwords from the file `~/.m2/settings.xml` if you don't want to keep it there.

#### Version Numbers

`release:prepare` will prompt for version numbers and SCM information. The defaults are correct for Jackrabbit, but not for Oak. Below is an example used in the release of 1.76.0:

       ...
       [INFO] 5/17 prepare:map-release-versions
       What is the release version for "Jackrabbit Oak"? (jackrabbit-oak) 1.75: : 1.76.0
       [INFO] 6/17 prepare:input-variables
       What is the SCM release tag or label for "Jackrabbit Oak"? (jackrabbit-oak) jackrabbit-oak-1.76.0: :
       [INFO] 7/17 prepare:map-development-versions
       What is the new development version for "Jackrabbit Oak"? (jackrabbit-oak) 1.76.1-SNAPSHOT: : 1.77-SNAPSHOT
       ...

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
You need to change the `~/.m2/settings.xml` file as follows. PGP key id: this is the second part of your key in the KEYS file. For example, this is "F07CA77B" if the first line of your key in the KEYS file is "pub 4096R/F07CA77B 2014-07-31". In case you are not comfortable to keep passwords and key passphrases in human-readable files, you can add them just before doing the release, and remove them just after the release. Instead of using the "gpg.passphrase" tag, you can try using `<gpg.executable>gpg2</gpg.executable>` (this should prompt you for the passphrase). For the ASF Maven repository passwords, you could use the [Maven password encryption](http://maven.apache.org/guides/mini/guide-encryption.html).

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
          <username><!-- Apache LDAP user name --></username>
          <password><!-- Apache LDAP password --></password>
        </server>
        <!-- To stage a Jackrabbit release -->
        <server>
          <id>apache.releases.https</id>
          <username><!-- Apache LDAP user name --></username>
          <password><!-- Apache LDAP password --></password>
        </server>
        <!-- To tag/checkout/checkin -->
        <server>
          <id>svn.apache.org</id>
          <username><!-- Apache LDAP user name --></username>
          <password><!-- Apache LDAP password --></password>
        </server>
        ...
      </servers>
    </settings>

Appendix C: Cygwin
------------------

The Subversion and Git support in the release plugin assumes platform-specific path delimiters, and thus does not work properly if the "git" or "svn" executable is the Cygwin version. The easiest workaround for this problem is to install a Windows-native GIT or SVN version as well, and to modify the PATH variable for the git/mvn invocation so that it's found instead of the Cygwin variant.

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

Create release notes to include all the changes accumulated - for a future 2.24.0 this means including
all changes labeled with `fixVersion` set to `2.24`.
Note that any change labeled with `fixVersion` set to any 2.23.* release should have `fixVersion: 2.24` as
well, unless the change is irrelevant for the release notes.


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

Creating a new major release implies creating a new branch (next would be "2.24"), see
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

Appendix G: fixVersion and backports
------------------------------------

For backports to maintenance branches, usually;

- wait for the change to be in a released version (this may be impossible for emergency changes)
- for simple issues, just re-use the (now closed) ticket, and cherry-pick the changes (that gets harder when branches diverge)
- when done, add to "fixVersion"

**Jackrabbit**

In Jackrabbit - where we have beta releases - once released, we backport *everything* into the newest stable branch
(right now from trunk to 2.22 branch). As these do not diverge (mostly), we can just cherry-pick all changes (and
update the fixVersion information). An exception would be SNAPSHOT dependencies.

Also, every ticket resolved in a beta release also should have the next stable branch as "fixVersion" (such as
2.23.n and 2.24). This ensures that 2.24.0, once it is released, will have complete release notes.
