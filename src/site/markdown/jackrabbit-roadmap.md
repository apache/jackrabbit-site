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

Jackrabbit Roadmap
==================
This is a roadmap of future Apache Jackrabbit releases and features. See [the dev@ list](mailing-lists.html)
for the latest status.


Unstable/stable release model
-----------------------------
Starting with Jackrabbit 2.3 we are adopting a "Linux-style"
unstable/stable release model with odd/even minor version numbers used to
mark the status of a release.

* [Jackrabbit 2.3 (trunk)](https://svn.apache.org/repos/asf/jackrabbit/trunk/) ([download](downloads.html#v23))

Unstable 2.3.x releases will be cut fairly frequently directly from
Jackrabbit trunk, and a stable 2.4 release branch will be created later on.
At current rate it looks like the 2.4 branch can be created before the end
of 2011.

Once the 2.4 branch has been created, trunk will switch to 2.5.x and
continue progressing towards 2.6, etc.


Maintenance branches
--------------------
We currently support the following maintenance branches:

* [Jackrabbit 2.2](https://svn.apache.org/repos/asf/jackrabbit/branches/2.2/) ([download](downloads.html#v22))
* [Jackrabbit 2.1](https://svn.apache.org/repos/asf/jackrabbit/branches/2.1/) ([download](downloads.html#v21))
* [Jackrabbit 2.0](https://svn.apache.org/repos/asf/jackrabbit/branches/2.0/) ([download](downloads.html#v20))


End of life
-----------
The Jackrabbit 1.6 maintenance branch has reached its end of life status.
No more patch releases will be cut from the 1.6 branch, and the latest
1.6.5 release will be archived in December 2011.

* [Jackrabbit 1.6](https://svn.apache.org/repos/asf/jackrabbit/branches/1.6/) ([download](downloads.html#v16))

There is currently no schedule for declaring the end of life of any of the
stable 2.x maintenance branches.


Prototyping the future
----------------------
The ongoing microkernel work in the Jackrabbit sandbox is being used to
prototype a possible next generation architecture for a future major new
Jackrabbit release.
