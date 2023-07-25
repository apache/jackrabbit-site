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

Security Reports
--------------------------------------------------------------------------------

### Security Updates

Please note that binary patches are not produced for individual vulnerabilities. To obtain the fix for a particular 
vulnerability you should upgrade to the officially released version where that vulnerability has been fixed.

#### List of Vulnerabilities

Note: the vulnerability reports linked below will provide additional details including reference to the public 
announcement and a short description.

| CVE Number    | Type                                             | Fix Versions                                                    |
|---------------|--------------------------------------------------|-----------------------------------------------------------------|
| CVE-2009-0026 | Multiple cross-site scripting (XSS) vulnerabilities in Apache Jackrabbit before 1.5.2 allow remote attackers to inject arbitrary web script or HTML via the q parameter to (1) search.jsp or (2) swr.jsp.  | 1.5.2 |
| CVE-2015-1833 | XML external entity (XXE) vulnerability in Apache Jackrabbit before 2.0.6, 2.2.x before 2.2.14, 2.4.x before 2.4.6, 2.6.x before 2.6.6, 2.8.x before 2.8.1, and 2.10.x before 2.10.1 allows remote attackers to read arbitrary files and send requests to intranet servers via a crafted WebDAV request. | 2.2.14, 2.4.6, 2.6.6, 2.8.1, 2.10.1 |
| CVE-2016-6801 | Cross-site request forgery (CSRF) vulnerability in the CSRF content-type check in Jackrabbit-Webdav in Apache Jackrabbit 2.4.x before 2.4.6, 2.6.x before 2.6.6, 2.8.x before 2.8.3, 2.10.x before 2.10.4, 2.12.x before 2.12.4, and 2.13.x before 2.13.3 allows remote attackers to hijack the authentication of unspecified victims for requests that create a resource via an HTTP POST request with a (1) missing or (2) crafted Content-Type header. | 2.4.6, 2.6.6, 2.8.3, 2.10.4, 2.12.4, 2.13.3 |
| CVE-2023-37895 | Apache Jackrabbit RMI access can lead to RCE | 2.20.11, 2.21.18 |
| | |

### Reporting Vulnerabilities with Apache Jackrabbit

The Apache Software Foundation takes an active stance in eliminating security problems. We strongly encourage everyone 
to report vulnerabilities to the Apache security mailing list _security(at)apache.org_, before disclosing them in a public forum.

Please note that the security mailing list should only be used for reporting undisclosed vulnerabilities and 
managing the process of fixing them. We cannot accept regular bug reports or other queries at this address. If you wish 
to report a bug that isn't an undisclosed security vulnerability, please use [https://issues.apache.org/jira/projects/JCR/issues](https://issues.apache.org/jira/projects/JCR/issues).

### Errors and Omissions

Please report any errors or omissions to _security(at)apache.org_.
