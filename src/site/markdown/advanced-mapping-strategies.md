Title: Advanced Mapping Strategies
<a name="AdvancedMappingStrategies-Inheritance"></a>
## Inheritance

TODO

<a name="AdvancedMappingStrategies-Interface"></a>
## Interface

TODO

<a name="AdvancedMappingStrategies-Components"></a>
## Components

A component is an entity that cannot live by its own, but has a logical
meaning. Take for example an Address. It may live alone, but doesn't make
much sense in some systems. Once associated with an User it starts making
sense. Now, as in RDBMS you can choose the persist this as a record in a
separate table with a 1-1 relation, or you may choose to persist Address
field along with the User.

Now, returning to JCR, the component is fitting perfectly the mixin notion.
A mixin cannot live by its own in the repository. It is associated with
some node. It's properties are added to the set of original node.

<a name="AdvancedMappingStrategies-Groupsomebeanattributesintoasubnode"></a>
## Group some bean attributes into a subnode

TODO

<a name="AdvancedMappingStrategies-Maptoanothernodestructure"></a>
## Map to another node structure

Sometime, it should be interesting to map to a different jcr node
structure. Here is an example, for a class "File", we can have:


    public class File
    {
      private String mimeType;
      private String encoding;
      private InputStream data;
      private Calendar lastModified;
      // Add getters/setters
    }


and in terms of JCR structure, we can have:


    nt:file
      jcr:content
        jcr:mimeType
        jcr:encoding
        jcr:data
        jcr:lastModified


So, the jcr:content node is an extra node to specify in the mapping file.
