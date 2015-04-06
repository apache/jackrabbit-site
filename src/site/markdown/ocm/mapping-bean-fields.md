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

Mapping Bean Fields
===================
 The bean-descriptor maps a bean attribute into one JCR node	       (or
a set of properties). Generally, this attribute is an		object
based on a custom class.

 Based on our model defined here,	    the following bean-descriptor
is used to map the bean field		"pageInfo" (PageInfo class) into
the JCR node called "pageInfo".

 The PageInfo class has a corresponding class-descriptor in the 	 
mapping file. By this way, the Persistence Manager can map each 	 
PageInfo attributes. It is not necessary to specify the type in 	 
the bean-descriptor. The Persistence Manager uses the Java	    
introspection to get information on the each bean fields.


The JCR Structure
-----------------
Following our example, the resulting JCR structure is:


    /mysite/page1
      /mysite/page1/pageInfo
           my:title = "This is my page title"
           my:description = "This is my page description"
      ... other subnodes for page1 ...


By default, the persistence manager will create a subnode	   
(/mysite/page1/pageInfo) for the bean-descriptor pageInfo.


Using Another Bean Converter
----------------------------
The OCM framework gives you the freedom to choose another kind		 
of mapping for bean fields. For example, you can use a custom		
bean converter to access to the parent node (see the next	    
section below).

This can be done by writing your own bean converter class and		
reference this class in the bean-descriptor.


### Predefined Bean Converters

 Here is the list of existing custom  bean converters:
 
<table>
<tr><th> Custom Bean Converter Class </th><th> Description </th></tr>
<tr><td>
org.apache.jackrabbit.ocm.persistence.beanconverter.impl.ParentBeanConverterImpl
</td><td> Map a bean field to the parent node. it is used to access to the	   
     parent object in read-only mode. See below the example based on	   
       a Folder object. </td></tr>
<tr><td>
org.apache.jackrabbit.ocm.persistence.beanconverter.impl.InlineBeanConverterImpl
</td><td> Bean converter used to map some node properties into one nested	   
    bean field. The corresponding bean field is not associated to a	   
      subnode. </td></tr>
</table>

If you want to use one of this bean converter, you have to	    
reference it into a bean-field descriptor.

The following descriptor bean-descriptor contains a reference to	  
its parent folder (parentFolder attribute). Now the CmsObjectImpl	   
object has an attribute (parentFolder) that contains a reference	  
to the parent node.


    <class-descriptor 
        className="org.apache.jackrabbit.ocm.testmodel.inheritance.impl.CmsObjectImpl" 
        jcrType="my:cmsobjectimpl" >
      <field-descriptor fieldName="path" path="true" />
      <field-descriptor fieldName="name" jcrName="my:name" id="true" />
      <bean-descriptor 
        fieldName="parentFolder" 
        converter="org.apache.jackrabbit.ocm.persistence.beanconverter.impl.ParentBeanConverterImpl" 
      />
    </class-descriptor>


### Building your own Bean Converters

Here is the different steps used to create a new bean converter :

First, specify the converter class in the bean descriptor:


    <class-descriptor 
        className="org.apache.jackrabbit.ocm.testmodel.inheritance.impl.CmsObjectImpl" 
        jcrType="my:cmsobjectimpl" >
      <bean-descriptor 
        fieldName="parentFolder" 
        converter="org.apache.jackrabbit.ocm.persistence.beanconverter.impl.ParentBeanConverterImpl" 
      />
    </class-descriptor>


Then, implement the converter class (based on the interface	     
org.apache.jackrabbit.ocm.persistence.beanconverter.BeanConverter).

Your bean converter class can also extends the class	      
AbstractBeanConverterImpl to have a default implementation for		
some methods.

    import javax.jcr.Node;
    import javax.jcr.Session;
    
    import org.apache.commons.logging.Log;
    import org.apache.commons.logging.LogFactory;
    import org.apache.jackrabbit.ocm.exception.JcrMappingException;
    import org.apache.jackrabbit.ocm.exception.PersistenceException;
    import org.apache.jackrabbit.ocm.exception.RepositoryException;
    import org.apache.jackrabbit.ocm.mapper.Mapper;
    import org.apache.jackrabbit.ocm.mapper.model.BeanDescriptor;
    import org.apache.jackrabbit.ocm.mapper.model.ClassDescriptor;
    import org.apache.jackrabbit.ocm.persistence.atomictypeconverter.AtomicTypeConverterProvider;
    import org.apache.jackrabbit.ocm.persistence.beanconverter.BeanConverter;
    import org.apache.jackrabbit.ocm.persistence.objectconverter.ObjectConverter;
    /**
     *
     * Bean converter used to access to the parent object.
     *
     *
     * @author <a href="mailto:christophe.lombart@gmail.com">Lombart Christophe </a>
     *
     */
    public class ParentBeanConverterImpl extends AbstractBeanConverterImpl implements BeanConverter {
    
      private final static Log log = LogFactory.getLog(ParentBeanConverterImpl.class);
    
      public ParentBeanConverterImpl(Mapper mapper, ObjectConverter objectConverter, AtomicTypeConverterProvider atomicTypeConverterProvider)
      {
        super(mapper, objectConverter, atomicTypeConverterProvider);
      }
    
      public void insert(Session session, Node parentNode, BeanDescriptor beanDescriptor, ClassDescriptor beanClassDescriptor, Object object, ClassDescriptor parentClassDescriptor, Object parent)
          throws PersistenceException, RepositoryException, JcrMappingException {
    
          // Add code to insert the object
      }
    
      public void update(Session session, Node parentNode, BeanDescriptor beanDescriptor, ClassDescriptor beanClassDescriptor, Object object, ClassDescriptor parentClassDescriptor, Object parent)
          throws PersistenceException, RepositoryException, JcrMappingException {
    
          // Add code to update the object
      }
    
      public Object getObject(Session session, Node parentNode, BeanDescriptor beanDescriptor, ClassDescriptor beanClassDescriptor, Class beanClass, Object parent)
          throws PersistenceException, RepositoryException,JcrMappingException {
    
          // Add code to retrieve the object
      }
    
      public void remove(Session session, Node parentNode, BeanDescriptor beanDescriptor, ClassDescriptor beanClassDescriptor, Object object, ClassDescriptor parentClassDescriptor, Object parent)
    	    throws PersistenceException,  RepositoryException, JcrMappingException {
    
          // Add the code to remove the object
      }
    
    }

