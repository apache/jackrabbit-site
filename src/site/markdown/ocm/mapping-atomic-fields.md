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

Mapping Atomic Fields
=====================
The field-descriptor maps a bean attribute based on a Java primitive	   
type into a JCR property. By default, the persistence manager uses	   
the correct mapping in function of the attribute type (see below	   
the section "Supported Types").

Based on our model defined here,	   the following field-descriptor
maps the bean field "title"	      (String type) into the JCR property
"my:title".


Supported Types
---------------
 It is not necessary to specify the type in the field-descriptor.	   
The Persistence Manager uses the java introspection to get	    
information on each atomic field.

<table>
<tr><th> Java Type </th><th> Jcr Type </th></tr>
<tr><td> String </td><td> STRING </td></tr>
<tr><td> Boolean, boolean </td><td> BOOLEAN </td></tr>
<tr><td> Double, double </td><td> DOUBLE </td></tr>
<tr><td> Integer, int </td><td> DOUBLE </td></tr>
<tr><td> Long, long </td><td> LONG </td></tr>
<tr><td> byte\[\](\.html)
 </td><td> BINARY </td></tr>
<tr><td> java.io.InputStream </td><td> BINARY </td></tr>
<tr><td> java.util.Calendar </td><td> LONG (corresponding to Calendar.getTimeInMillis() </td></tr>
<tr><td> java.sql.Timestamp </td><td> LONG (corresponding to Timestamp.getTime() </td></tr>
<tr><td> java.util.Date </td><td> LONG (corresponding to java.util.Date.getTime() </td></tr>
</table>

 Due to some issues with Jackrabbit (mainly with xpath queries),	  
Calendar, Timestamp and date are converted into JCR LONG.	    We plan
to add other converters for those types in the next release.


Using Another Atomic Type Converter
-----------------------------------
The OCM framework gives you the freedom to choose another kind of	  
mapping for atomic fields. For example, you can convert 	
java.util.Date bean field into a JCR Date type instead of a	     JCR
Long type. This can be done by writing your own atomic type	    
converter class.

Let's start with a simple example. If you want to use a mapping 	 
strategy which convert a boolean bean field into a JCR Long type,	   
you have to make the following steps:


### Specify the converter class in the field descriptor


    <class-descriptor
        className="org.apache.jackrabbit.ocm.testmodel.Atomic"
        jcrType="nt:unstructured">
      <field-descriptor
          fieldName="int2boolean" 
          jcrName="int2boolean"
          converter="org.apache.jackrabbit.ocm.persistence.atomic.Int2BooleanTypeConverterImpl"
      />
    </class-descriptor>


### Implement the converter class

Use the interface org.apache.jackrabbit.ocm.persistence.atomic.AtomicTypeConverter

    package org.apache.jackrabbit.ocm.persistence.atomic;
    
    import javax.jcr.Value;
    import javax.jcr.ValueFactory;
    
    import org.apache.jackrabbit.ocm.exception.IncorrectAtomicTypeException;
    import org.apache.jackrabbit.ocm.persistence.atomictypeconverter.AtomicTypeConverter;
    
    /**
     * This is a simple converter which convert a boolean field value into a jcr long property.
     *
     * @author <a href="mailto:christophe.lombart@gmail.com">Christophe Lombart</a>
     */
    public class Int2BooleanTypeConverterImpl implements AtomicTypeConverter
    {
      /**
       *
       * @see org.apache.jackrabbit.ocm.persistence.atomictypeconverter.AtomicTypeConverter#getValue(java.lang.Object)
       */
      public Value getValue(ValueFactory valueFactory, Object propValue)
      {
        if (propValue == null)
        {
          return null;
        }
        boolean value = ((Boolean) propValue).booleanValue();
        int jcrValue = 0;
    
        if (value)
        {
          jcrValue = 1;
        }
        return valueFactory.createValue(jcrValue);
      }
    
    
        /**
         *
         * @see org.apache.jackrabbit.ocm.persistence.atomictypeconverter.AtomicTypeConverter#getObject(javax.jcr.Value)
         */
      public Object getObject(Value value)
        {
          try
          {
    	long jcrValue = value.getLong();
    	if (jcrValue == 1)
    	{
    	   return new Boolean(true);
    	}
    	else
    	{
    	   return new Boolean(false);
    	}
        }
        catch (Exception e)
        {
          throw new IncorrectAtomicTypeException("Impossible to convert the value : " + value.toString()  , e);
        }
        }
    
      /**
       *
       * @see org.apache.jackrabbit.ocm.persistence.atomictypeconverter.AtomicTypeConverter#getStringValue(java.lang.Object)
       */
      public String getStringValue(Object object)
      {
    
        return ((Boolean) object).booleanValue() ? "1" : "0";
      }
    
    }

