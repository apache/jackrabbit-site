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

Issue Tracker
=============
Apache Jackrabbit uses Jira for tracking bug reports and requests for
improvements, new features, and other changes.

The issue tracker is available at https://issues.apache.org/jira/browse/JCR
and is readable by everyone. A Jira account is needed to create new issues
and to comment on existing issues. Use the [registration form](https://issues.apache.org/jira/secure/Signup!default.jspa)
to request an account if you do not already have one.

Issue workflow
--------------
When an issue is created, it's in the *Open* state. This is the time for
describing the issue and discussing possible ways of solving it. If a
proposed patch is attached, then the issue can optionally be moved to the
*Patch available* state to give it more visibility. If the patch is
cancelled because more work is needed, the issue moves back to the *Open*
state.

Once the issue is solved, the committer who committed the changes marks the
issue as *Resolved* with resolution type _Fixed_. Other resolution types
like _Duplicate_, _Invalid_ or _Won't Fix_ are used when resolving issues
that for one reason or another require no changes in the codebase. An issue
can be *Reopened* if the committed fix is found to be not good enough.

When an issue is resolved as fixed, the committer should set the "Fix
Version(s)" field to the next trunk version to mark that the change will be
included in that release. If the fix is also backported to one or more of
the maintenance branches (for backporting, use `svn merge -c _revision_
^/jackrabbit/trunk` in the root of the branch) the version numbers of the
relevant next maintenance releases should also be included in the "Fix
Version(s)" field.

Finally, once a release containing the change has been made, the release
manager will mark the issue *Closed*, after which the issue can no longer
be reopened (since the release can obviously no longer be changed).
Potential regressions or other related problems should be tracked in
separate followup issues.


Issue contents
--------------
See below for guidelines on how to use the various fields in an issue.

### Issue type
When creating a new issue, select the issue type based as follows:

| Issue type    | Description  |
|---------------|--------------|
| *Bug*         | Bug reports are used for cases where Jackrabbit fails not function as it should (as defined by the JCR specification or some other documentation). If you are not certain whether the issue you've found is actually a bug, please ask the Jackrabbit [mailing lists](mailing-lists.html) first for help.
| *New Feature* | Use a feature request when Jackrabbit does not have some functionality you need.
| *Improvement* | Use an improvement request to suggest improvements to existing features. Typical improvement requests are about updating documentation, increasing stability and performance, simplifying the implementation, or other such changes that make Jackrabbit better without introducing new features or fixing existing bugs. 
| *Test*        | Use this type when contributing test cases for existing features. Normally test cases should be contributed as a part of the original feature request or as regression tests associated with bug reports, but sometimes you just want to extend test coverage by introducing new test cases. This issue type is for such cases. 
| *Task*        | Used only for issues related to project infrastructure. 

### Issue summary, environment and description
The issue summary should be a short and clear statement that indicates the
scope of the issue. You are probably being too verbose if you exceed the
length of the text field. Use the Environment and Description fields to
provide more detailed information.

### Issue priority
Issue priority should be set according to the following:

| Issue priority  | Description
|-----------------|------------------------
| *Blocker*	  | Legal or other fundamental issue that makes it impossible to release Jackrabbit code
| *Critical*	  | Major loss of functionality that affects many Jackrabbit users
| *Major*	  | Important issue that should be resolved soon
| *Minor*	  | Nice to have issues
| *Trivial*	  | Trivial changes that can be applied whenever someone has extra time
