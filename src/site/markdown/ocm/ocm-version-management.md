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

OCM Version Management
======================
Right now, the OCM tools provides basic versioning features:

* Check in, check out.
* Retrieve version history (first version, last version, the complete history, ...).
* Apply labels.

Later, we would like to add more advanced versioning support like version
compare, replace, revert, ... Each versioned object has to be mapped to a
mix:versionable JCR node. It is possible to specify this node type in the
xml class descriptor or with an annotation :


Check in - Check out
--------------------

    // Create a new page - first version
    Page page = new Page();
    page.setPath("/page");
    page.setTitle("Page Title");
    page.addParagraph(new Paragraph("para1"));
    page.addParagraph(new Paragraph("para2"));
    ocm.insert(page);
    ocm.save();
    
    // Update the page object and create a new version
    page.addParagraph(new Paragraph("para3"));
    ocm.checkout("/page");
    ocm.update(page);
    ocm.save();
    ocm.checkin("/page");
    
    // Update the page object and create a new version
    page.addParagraph(new Paragraph("para4"));
    ocm.checkout("/page");
    ocm.update(page);
    ocm.save();
    ocm.checkin("/page");



Retrieve the version history
----------------------------

    VersionIterator versionIterator = ocm.getAllVersions("/page");
    while (versionIterator.hasNext())
    {
        Version version = (Version) versionIterator.next();
        System.out.println("version found : "+ version.getName() + " - " +
    			  version.getPath() + " - " + version.getCreated().getTime());
    }


Retrieve version description
----------------------------

    // Retrieve the first version description
    Version baseVersion = ocm.getBaseVersion("/page");
    System.out.println("Base version : " + baseVersion.getName());
    
    // Retrieve the latest version description
    Version rootVersion = ocm.getRootVersion("/page");
    System.out.println("Root version : " + rootVersion.getName());


Retrieve the object state matching to a specific version
--------------------------------------------------------

    //Get the object matching to the first version
    Page  page = (Page) ocm.getObject( "/page", "1.0");


Using version labels
--------------------

    Page page = new Page();
    page.setPath("/page");
    page.setTitle("Page Title");
    page.addParagraph(new Paragraph("para1"));
    page.addParagraph(new Paragraph("para2"));
    ocm.insert(page);
    ocm.save();
    
    // Checkin with some labels
    page.addParagraph(new Paragraph("para3"));
    ocm.checkout("/page");
    ocm.update(page);
    ocm.save();
    ocm.checkin("/page", new String[]{"A", "B"});
    
    // Checkin with some labels
    page.addParagraph(new Paragraph("para4"));
    ocm.checkout("/page");
    ocm.update(page);
    ocm.save();
    ocm.checkin("/page", new String[]{"C", "D"});
    
    // Retrieve all labels
    String[] allLabels = ocm.getAllVersionLabels("/page");
    assertTrue("Incorrect number of labels", allLabels.length == 4);
    
    // Retrieve labels assigned to the version 1.1
    String[] versionLabels = ocm.getVersionLabels("/page", "1.1");
    assertTrue("Incorrect number of labels", versionLabels.length == 2);
    assertTrue("Incorrect label", versionLabels[0].equals("C") || versionLabels[0].equals("D"));
    assertTrue("Incorrect label", versionLabels[1].equals("C") || versionLabels[0].equals("D"));

