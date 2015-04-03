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

Jackrabbit Text Extractors
==========================
This is the Text Extractors component of the Apache Jackrabbit project.
This component contains extractor classes that allow Jackrabbit to extract
text content from binary properties for full text indexing.


Supported document formats
--------------------------
The following document formats and MIME types are currently supported:

* Microsoft Word (org.apache.jackrabbit.extractor.MsWordTextExtractor)
    * application/vnd.ms-word
    * application/msword
* Microsoft Excel (org.apache.jackrabbit.extractor.MsExcelTextExtractor)
    * application/vnd.ms-excel
* Microsoft PowerPoint (org.apache.jackrabbit.extractor.MsPowerPointTextExtractor)
    * application/vnd.ms-powerpoint
    * application/mspowerpoint
* Portable Document Format (PDF) (org.apache.jackrabbit.extractor.PdfTextExtractor)
    * application/pdf
* OpenOffice.org (org.apache.jackrabbit.extractor.OpenOfficeTextExtractor)
    * application/vnd.oasis.opendocument.database
    * application/vnd.oasis.opendocument.formula
    * application/vnd.oasis.opendocument.graphics
    * application/vnd.oasis.opendocument.presentation
    * application/vnd.oasis.opendocument.spreadsheet
    * application/vnd.oasis.opendocument.text
* Rich Text Format (RTF) (org.apache.jackrabbit.extractor.RTFTextExtractor)
    * application/rtf
* HyperText Markup Language (HTML) (org.apache.jackrabbit.extractor.HTMLTextExtractor)
    * text/html
* Extensible Markup Language (XML) (org.apache.jackrabbit.extractor.XMLTextExtractor)
    * text/xml


Using the text extractors
-------------------------
To use these text extractors with the Jackrabbit Core:

1. add the jackrabbit-text-extractors jar file and the dependencies defined
in the Maven POM in the Jackrabbit classpath, and
1. add the fully qualified class names listed above in the
"textFilterClasses" parameter of the "SearchIndex" configuration element of
a Jackrabbit workspace configuration file (workspace.xml).
