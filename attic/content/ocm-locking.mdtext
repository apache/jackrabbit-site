Title: OCM Locking
Following the Jcr specification, it is possible to lock nodes and their
children (see section 8.4). You can see on this page the OCM API used to
lock on the object level. In order to lock an object, its matching node has
to implement the jcr mixin type "mix:lockable". It is possible to specify
this node type in the class descriptor:

<a name="OCMLocking-Abasicexample"></a>
## A basic example


    //
--------------------------------------------------------------------------------
    // Create and store an object graph in the repository
    //
--------------------------------------------------------------------------------
    A a = new A();
    a.setPath("/test");
    a.setA1("a1");
    a.setA2("a2");
    B b = new B();
    b.setB1("b1");
    b.setB2("b2");
    a.setB(b);
    
    C c1 = new C();
    c1.setId("first");
    c1.setName("First Element");
    C c2 = new C();
    c2.setId("second");
    c2.setName("Second Element");
    
    C c3 = new C();
    c3.setId("third");
    c3.setName("Third Element");
    
    Collection collection = new ArrayList();
    collection.add(c1);
    collection.add(c2);
    collection.add(c3);
    
    a.setCollection(collection);
    
    ocm.insert(a);
    ocm.save();
    
    
    //
--------------------------------------------------------------------------------
    // Check if the object is not locked
    //
--------------------------------------------------------------------------------
    if (ocm.isLocked("/test"))
    {
       System.out.println("Error : The object is locked- humm ??");
    }
    
    //
--------------------------------------------------------------------------------
    // Lock the object
    //
--------------------------------------------------------------------------------
    String lockToken = ocm.lock("/test", true, false);
    
    //
--------------------------------------------------------------------------------
    // Check if the object is not locked
    //
--------------------------------------------------------------------------------
    if (! ocm.isLocked("/test"))
    {
       System.out.println("Error : The object is not locked- humm ??");
    }
    
    //
--------------------------------------------------------------------------------
    // Unlock the object
    //
--------------------------------------------------------------------------------
    ocm.unlock("/test", lockToken);

