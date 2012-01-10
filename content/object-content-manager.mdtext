Title: Object Content Manager
The main component in the OCM framework is the ObjectContentManager. It
converts an object graph into JCR nodes and properties and vice versa. The
ObjectContentManager is always associated with a JCR Session. It is used to
retrieve, create, update and delete objects from a JCR content repository.
Usually there is one ObjectContentManager per user session.

This page describes how an ObjectContentManager is working and how it can
be initialised in your applications. 

<a name="ObjectContentManager-HowdoestheObjectContentManagerwork?"></a>
## How does the Object Content Manager work ?

Thanks to a Mapping Descriptor, the ObjectContentManager is able to use the
appropriate mapping strategy for each persistent object (pojo). The Mapping
Descriptor contains one Class Descriptor per persistent class. Each Class
Descriptor contains mapping information for the corresponding class
attributes.

In the point of view implementation, the Mappring Descriptor is a java
object injected into the ObjectContentManager (see the interface
org.apache.jackrabbit.ocm.mapper.Mapper). Right now, there are 2 different
Mapping Descriptor implementations:

    * Annotation : each persistent object is annoted in order to provide to
the ObjectContentManager all the required information on its mapping
strategy (see the class
org.apache.jackrabbit.ocm.mapper.impl.annotation.AnnotationMapperImpl).
    * XML configuration file : the class descriptors are defined in one or
more XML config files used by the ObjectContentManager when it is
instantiated (see the class
org.apache.jackrabbit.ocm.mapper.impl.digester.DigesterMapperImpl). 

For a business developer, it is not necessary to know how the
ObjectContentManager is using the Class Descriptors. He has to make only a
choice between annoted classes or XML files. Below, you can see how to
setup correctly an ObjectContentManager. 

<a name="ObjectContentManager-HowdoesanobjectispersistedintoaJCRrepository?"></a>
## How does an object is persisted into a JCR repository ?

In all cases, a persistent object (a pojo) is mapped into a JCR node and
its fields are mapped into subnodes or properties depending on their types.

There are 3 "field types":

* Atomic fields
    Primitive data types and simple objects (String, Long, Double, ...) .
Those fields are mapped into JCR properties. 

* Bean fields
    One class can contain an 1..1 association to another bean. In this
case, the field is a custom object. Those fields are mapped into JCR
subnodes or a referenced node. 

* Collection fields
    One class can contain an 1..n association to a collection of beans (or
Map). Those fields are mapped into a collection of JCR subnodes or a
collection of referenced nodes. It is also possible to map a java
collection into a multivalue property. 

The Mapping descriptor contains also information on inheritances, interface
mapping strategy, lazy loading, custom converter, cache strategy, etc. 
<a name="ObjectContentManager-Basicsetup(withannotedpersistentclasses)"></a>
## Basic setup (with annoted persistent classes)

When you start your application, you need the following code to initialize
correctly the Object Content Manager.


    import javax.jcr.Session;
    import javax.jcr.Repository;
    		      
    import org.apache.jackrabbit.ocm.manager.impl.ObjectContentManagerImpl;
    import org.apache.jackrabbit.ocm.mapper.Mapper;
    import
org.apache.jackrabbit.ocm.mapper.impl.annotation.AnnotationMapperImpl;
    
    		      
    // 1. Instantiate a JCR session
    Repository repository = ...;
    Session session = repository.login(...);
    		      
    // 2. Register the different persistent classes
    List classes = new ArrayList();
    classes.add(MyContent.class); // Call this method for each persistent class
    
    				      
    // 3. Instantiate the object content manager
    Mapper mapper = new AnnotationMapperImpl(classes);
    ObjectContentManager ocm = new ObjectContentManagerImpl(session, mapper);


<a name="ObjectContentManager-Basicsetup(withoneormoreXMLMappingDescriptorfiles)"></a>
## Basic setup (with one or more XML Mapping Descriptor files)

When you start your application, you need the following code to initialize
correctly the Object Content Manager.

    import javax.jcr.Session;
    import javax.jcr.Repository;
    
    import org.apache.jackrabbit.ocm.mapper.Mapper;
    import org.apache.jackrabbit.ocm.mapper.impl.digester.DigesterMapperImpl;
    import org.apache.jackrabbit.ocm.manager.ObjectContentManager;
    import org.apache.jackrabbit.ocm.manager.impl.ObjectContentManagerImpl;
    import
org.apache.jackrabbit.ocm.manager.atomictypeconverter.AtomicTypeConverterProvider;
    import
org.apache.jackrabbit.ocm.manager.atomictypeconverter.impl.DefaultAtomicTypeConverterProvider;
    import org.apache.jackrabbit.ocm.manager.objectconverter.ObjectConverter;
    import
org.apache.jackrabbit.ocm.manager.objectconverter.impl.ObjectConverterImpl;
    import org.apache.jackrabbit.ocm.query.QueryManager;
    import org.apache.jackrabbit.ocm.query.impl.QueryManagerImpl;
    
    // 1. Instantiate a JCR session
    Repository repository = ...;
    Session session = repository.login(...);
    
    // 2. Specify the different mapping files
    String[]
 files = {
          "./src/test-config/jcrmapping.xml",
          "./src/test-config/jcrmapping-atomic.xml",
          "./src/test-config/jcrmapping-beandescriptor.xml"
      };
    
    // 3. Instantiate the object content manager
    ObjectContentManager ocm = new ObjectContentManagerImpl(session, files);
    



<a name="ObjectContentManager-APIOverview"></a>
## API Overview

With the current Object Manager API, it is possible to:

* Manage the object life cycle (insert, update, delete, retrieve). See [Basic OCM operations](basic-ocm-operations.html)
.
* Search single object or collections with criteria. See [OCM Search](ocm-search.html)
.
* Lock objects. See [OCM Locking](ocm-locking.html)
.
* Manage versions (check int, check out, create a new version, show
history). See [OCM Version Management](ocm-version-management.html)
.

We plan to add other features in a future release. 
