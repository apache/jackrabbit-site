Title: Jackrabbit Text Extractors
This is the Text Extractors component of the Apache Jackrabbit project.
This component contains extractor classes that allow Jackrabbit to extract
text content from binary properties for full text indexing.

<a name="JackrabbitTextExtractors-Supporteddocumentformats"></a>
### Supported document formats

The following document formats and MIME types are currently supported:

* Microsoft Word (org.apache.jackrabbit.extractor.MsWordTextExtractor)
 o application/vnd.ms-word
 o application/msword
* Microsoft Excel (org.apache.jackrabbit.extractor.MsExcelTextExtractor)
 o application/vnd.ms-excel
* Microsoft PowerPoint
(org.apache.jackrabbit.extractor.MsPowerPointTextExtractor)
 o application/vnd.ms-powerpoint
 o application/mspowerpoint
* Portable Document Format (PDF)
(org.apache.jackrabbit.extractor.PdfTextExtractor)
 o application/pdf
* OpenOffice.org (org.apache.jackrabbit.extractor.OpenOfficeTextExtractor)
 o application/vnd.oasis.opendocument.database
 o application/vnd.oasis.opendocument.formula
 o application/vnd.oasis.opendocument.graphics
 o application/vnd.oasis.opendocument.presentation
 o application/vnd.oasis.opendocument.spreadsheet
 o application/vnd.oasis.opendocument.text
* Rich Text Format (RTF) (org.apache.jackrabbit.extractor.RTFTextExtractor)
 o application/rtf
* HyperText Markup Language (HTML)
(org.apache.jackrabbit.extractor.HTMLTextExtractor)
 o text/html
* Extensible Markup Language (XML)
(org.apache.jackrabbit.extractor.XMLTextExtractor)
 o text/xml

<a name="JackrabbitTextExtractors-Usingthetextextractors"></a>
### Using the text extractors

To use these text extractors with the Jackrabbit Core:

1. add the jackrabbit-text-extractors jar file and the dependencies defined
in the Maven POM in the Jackrabbit classpath, and
1. add the fully qualified class names listed above in the
"textFilterClasses" parameter of the "SearchIndex" configuration element of
a Jackrabbit workspace configuration file (workspace.xml).
