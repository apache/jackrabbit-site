Title: OCM Search

<a name="OCMSearch-Searchingasingleobject"></a>
## Searching a single object


    QueryManager queryManager = ocm.getQueryManager();
    
    // Build the search filter
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.addEqualTo("text", "Para 1");   // Text is an attribute in the class
Paragraph
    
    // Build the query
    Query query = queryManager.createQuery(filter);
    Paragraph paragraph = (Paragraph) ocm.getObject(query);


<a name="OCMSearch-Searchingacollection"></a>
## Searching a collection


    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    Collection result = ocm.getObjects(query);


<a name="OCMSearch-Searchingwithaniterator"></a>
## Searching with an iterator


    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    Iterator iterator = ocm.getObjectIterator(query);


<a name="OCMSearch-Removeobjectsbasedonaquery"></a>
## Remove objects based on a query


    QueryManager queryManager = ocm.getQueryManager();
    Filter filter = queryManager.createFilter(Paragraph.class);
    filter.setScope("/test/node1//");
    Query query = queryManager.createQuery(filter);
    ocm.remove(query);

