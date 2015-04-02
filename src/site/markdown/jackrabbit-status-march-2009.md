Title: Jackrabbit Status March 2009
Apache Jackrabbit is a fully conforming implementation of the Content
Repository for Java Technology API (JCR, specified in JSR 170).

The Apache Jackrabbit project is in good shape. We have no board-level
issues at this time.

<a name="JackrabbitStatusMarch2009-Releases"></a>
## Releases

We made the following two releases from the 1.5 branch:

* Apache Jackrabbit 1.5.2 on January 20th
* Apache Jackrabbit 1.5.3 on February 27th

The 1.5.2 release contained a fix to the security issue CVE-2009-0026
(Cross site scripting issues in webapp). This was the first security issue
we had received through security@, and we had some initial confusion on how
we should react to such issues. The security team was very helpful in
guiding us.

We also made the following component releases from the older 1.4 branch:

* jackrabbit-core 1.4.7 on January 20th
* jackrabbit-core 1.4.8 on January 29th
* jackrabbit-core 1.4.9 on March 3rd

To get the JCR Commons subproject started we created and released a
standalone Jackrabbit parent POM:

* org.apache.jackrabbit:parent:2 on February 6th

<a name="JackrabbitStatusMarch2009-Legal"></a>
## Legal

No issues at the moment.

<a name="JackrabbitStatusMarch2009-Community/Development"></a>
## Community / Development

Michael Duerig joined the Jackrabbit team as a committer and PMC member.

The JCR Commons subproject was started after related discussion and a vote.
We are still in the process of setting up this new subproject. To respond
to earlier feedback from the board: we decided *not* to move these
components to Apache Commons to avoid splitting the development community.

There is continuous interest in the JCR-based CMIS implementation we are
developing in our sandbox. Florent Guillaume, who is not (yet) an Apache
committer, is working on a related codebase in an external Mercurial
repository under the working name "Chemistry". There are concerns over the
development being split over different source repositories. For now we hope
to bring all development into Apache svn and plan to manage the effort as
organic growth within the Jackrabbit project, possibly targetting a
subproject once the effort matures. Another option is to push the effort to
the Incubator as a new podling.

Starting with the 1.5.3 release our release notes include a section that
acknowledges everyone who has contributed to that release. The contents of
this section is based on the contribution report in Jira.

Work in Jackrabbit trunk continues and I expect us to release Jackrabbit
1.6.0 in a few months. After the 1.6 release we'll most likely start
targeting Jackrabbit 2.0 for release later this year. Jackrabbit 2.0 will
require Java 5 as the base platform.
