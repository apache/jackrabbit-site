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

Jackrabbit JCR to SPI
=====================
This is the JCR to SPI component of the Apache Jackrabbit project. It
provides and exposes the JCR API to the application and is a consumer of an
implementation of the [SPI interfaces](jackrabbit-spi.html).

Jackrabbit JCR to SPI is intended to act as a generic implementation of the
transient component that is layered on top of the persistent state of the
JCR repository. The latter is is represented by the SPI implementation.

This means that JCR to SPI handles

* transient storage of pending changes.
* resolution of namespaces to prefixes.
* Session-local namespace mappings.
* Session-mediated XML import.
* XML export.
