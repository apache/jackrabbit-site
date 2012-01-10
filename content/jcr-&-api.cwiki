Jackrabbit is a complete, and fully compliant implementation of  the Content Repository API for Java Technology (JCR) and therefore its primary API is defined by JCR. For a developer this means that most operations required are defined by the JCR API. The classes and interfaces within Apache Jackrabbit are only needed when accessing functionality that is not specified in JCR.

Beyond the JCR API Jackrabbit features numerous extensions and administrational features that are needed to run a repository  but are not (yet) specified by JCR. (see [Jackrabbit Architecture])

See the javadoc documentation of the JCR API and Apache Jackrabbit releases:

* [JCR 2.0|http://www.day.com/maven/javax.jcr/javadocs/jcr-2.0/]
* [Apache Jackrabbit 2.2|http://jackrabbit.apache.org/api/2.2/]
* [Apache Jackrabbit 2.1|http://jackrabbit.apache.org/api/2.1/]
* [Apache Jackrabbit 2.0|http://jackrabbit.apache.org/api/2.0/]

* [JCR 1.0|http://www.day.com/maven/jsr170/javadocs/jcr-1.0/]
* [Apache Jackrabbit 1.6|http://jackrabbit.apache.org/api/1.6/]
* [Apache Jackrabbit 1.5|http://jackrabbit.apache.org/api/1.5/]
* [Apache Jackrabbit 1.4|http://jackrabbit.apache.org/api/1.4/]
* [Apache Jackrabbit 1.3|http://jackrabbit.apache.org/api/1.3/]
* [Apache Jackrabbit 1.2|http://jackrabbit.apache.org/api/1.2.3/]
* [Apache Jackrabbit 1.0|http://jackrabbit.apache.org/api-1/]

h2. JSR-170 Levels

The Content Repository API for Java Technology (JSR-170) is split into different Levels of compliancy, to allow Repository Vendors to gradually adopt JSR-170 and to avoid that the overhead is unnecessarily high for repository vendors that only want to expose portions of their repository functionality through a JSR-170 compliant Interface.   JSR-170 specifies a Level 1, a Level 2 and a set of advanced repository  feature blocks. Jackrabbit is fully JSR-170 compliant and therefore supports Level 1, Level 2 and all the optional blocks.

h3. Level 1 : Ease of Adoption, Covering many usecases

The Scope of Level 1 of JSR-170 to cover a large number of simple  Applications, that need to search repositories and need to read  from repositories. Level 1 specifies a read-only API that allows to  introspect Node and Property-types and offers hierarchical read access to content stored in a repository. 

{center}!level-1.jpg!{center}

Level 1 of JSR-170 is geared to allow people to write  applications such as search and display Portlets,  CMS-Templates, Reports, Exports or other applications  that harvest, search, present or display information  from one or multiple repositories.

h3. Level 2 : Writeable Repository

Level 2 of JSR-170 specifies all the writing  capabilities need to bi-directionally interact with a content repository in a fine and coarse grained  fashion.

{center}!level-2.jpg!{center}

Applications written against Level 2 of JSR-170 include management applications or generally speaking any  application that generates data, information or content for both structured and unstructured information.

h3. Advanced Options

On top of Level 1 or Level 2 a number of functional  block serve for more advanced repository functionality. This includes functions like: Versioning,  (JTA) Transactions, Query using SQL, Explicit  Locking and Content Observation.

{center}!level-adv.jpg!{center}

A fully JSR-170 compliant repository like Jackrabbit encompasses all the functionalities and therefore lends itself as general purpose, off-the-shelf  infrastructure for Content-, Document- and Source Code Management or for just about any  other application that persists content.