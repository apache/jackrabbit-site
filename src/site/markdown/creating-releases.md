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
release schedule. It's OK to revise the plan if needed.

If you're not a committer, you can send a message to the mailing list
asking for a new release to be made. Including the list of specific fixes
you need and a short rationale of why you need the release.


Prerequisites for release managers
----------------------------------
You need to be a Jackrabbit committer to prepare and perform a release, but
anyone is welcome to help test the release candidates and comment on the
release plans.

You should have a code signing key that is included in the Jackrabbit KEYS
file. See Appendix A at the end of this page for more details.

You also need to tell Maven your Subversion credentials needed for
deploying artifacts to the Nexus server at https://repository.apache.org/.
See Appendix B for the required settings.


Release management tasks
------------------------
1. Make sure that an appropriate version for the release is entered in Jira and that 
    all the related issues have been resolved. This is also a good time to create a 
    new version in JIRA for the next release.
2. Create a `RELEASE-NOTES.txt` file in the root folder of the project to be released. 
    If such a file already exists, update it for the release. See a previous 
    release notes for examples of what to include. The release note report in Jira is a 
    useful source of required information: Open the [Jira Oak](https://issues.apache.org/jira/browse/OAK) page, 
    click on the release, then on the "Release Notes" button on the top right. When done, commit the file.
3. Build and deploy the release artifacts with Maven. See below for the exact steps.
4. Close the [staged repository](https://repository.apache.org/index.html#stagingRepositories) on repository.apache.org.
5. Upload the artifacts to https://dist.apache.org/repos/dist/dev/jackrabbit/ (instructions at the end of the build)

        cd /path/to/jackrabbit-dev
        scp -r /path/to/jackrabbit/target/checkout/target/$version $version
        svn add $version
        svn commit -m "Apache Jackrabbit $version release candidate" $version

6. Start the vote thread, wait 72 hours. See the vote template generated by the Maven build.
7. If the vote fails (easy case first) remove the tag from svn and drop the staged repository - done
8. If the vote is successful
    1. close the vote by publishing the results
    2. copy the release candidate from dev/jackrabbit to release/jackrabbit in https://dist.apache.org/repos/dist/, and delete any older releases from the same branch (they're automatically archived),

        svn move -m "Apache Jackrabbit $version" \
        https://dist.apache.org/repos/dist/dev/jackrabbit/$version \
        https://dist.apache.org/repos/dist/release/jackrabbit/$version

    3. release the [staged repository](https://repository.apache.org/index.html#stagingRepositories) for synchronization to Maven central.
    4. mark the version as released in Jira: [Jira Project Home](https://issues.apache.org/jira/browse/JCR) -> Project Summary -> Administer Project. Under Versions, click &lt;More>. You'll see all the defined project versions. From the settings menu, choose 'Release' on the version.
    5. close all the issues included in the release: Jira Project Home -> Change Log -> Choose the released version. From the issue list you have the option to bulk update all of the included issues. Just 'Transition Issues' from 'Resolved' to 'Closed' and you are done!

9. Update the Jackrabbit web site to point to the new release.
10. Send the release announcement once the web site and download mirrors have been synced. Please note the announce mails needs to be sent from an @apache.org address.


Steps to build the release artifacts
------------------------------------
The release is built using the Maven release plugin. See the [Releasing a Maven project](http://maven.apache.org/developers/release/releasing.html) guide for more details. Make sure you have added the pgp key information in you maven settings file, especially if you have more than one key installed locally. See [Appendix B](#b) for the details.

In case you don't feel comfortable to keep the passwords in the file `~/.m2/settings.xml` forever, you need to set it now temporarily.

There have been some problems with certain combinations of Java and Maven versions. A known combinations where releasing was successful is Java 7 with Maven 3.2.2. In case you get an exception "Proxy Error" in the `release:perform`, see the [Apache Services Status Page](http://status.apache.org/), however it has been reported that the status page is not always accurate.

1. Execute mvn `release:prepare`. This will update the POM files and tag the release in svn.
2. Execute mvn `release:perform`. This will build the tagged release and deploy the artifacts to a staging repository on repository.apache.org. The non-Maven release artifacts are automatically deployed to your home directory on people.apache.org. You only need to add the keyname if you have multiple keys and the code signing keys is not your default key.

After this is done, you can remove the passwords from the file `~/.m2/settings.xml` if you don't want to keep it there.


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
    using your @apache.org address as the email and "CODE SIGNING KEY" as the comment.
2. The Jackrabbit KEYS file is managed in https://svn.apache.org/repos/asf/jackrabbit/dist/KEYS. To modify the file, first checkout the dist directory:
    
        svn checkout https://svn.apache.org/repos/asf/jackrabbit/dist

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