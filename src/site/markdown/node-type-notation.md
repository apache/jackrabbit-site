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

Node Type Notation
==================
The Compact Namespace and Node Type Definition (CND) notation provides a
compact standardized syntax for defining node types and making namespace
declarations. The notation is intended both for documentation and for
programmatically registering node types (if you are unfamiliar with JCR
node types, you may want to read the general Node Types section first).

Here is a "worst-case scenario" example that demonstrates all the features of the notation:


    /*  An example node type definition */
    
    // The namespace declaration
    <ns = 'http://namespace.com/ns'>
    
    // Node type name
    [ns:NodeType]
    
    // Supertypes
    > ns:ParentType1, ns:ParentType2
    
    // This node type supports orderable child nodes
    orderable
    
    // This is a mixin node type
    mixin
    
    // Nodes of this node type have a property called 'ex:property' of type STRING
    - ex:property (string)
    
    // The default values for this
    // (multi-value) property are...
    = 'default1', 'default2'
    
    // This property is the primary item
    primary
    
    // and it is...
    mandatory autocreated protected
    
    // and multi-valued
    multiple
    
    // It has an on-parent-version setting of ...
    version
    
    // The constraint settings are...
    < 'constraint1', 'constraint2'
    
    // Nodes of this node type have a child node called ns:node which must be of
    // at least the node types ns:reqType1 and ns:reqType2
    + ns:node (ns:reqType1, ns:reqType2)
    
    // and the default primary node type of the child node is...
    = ns:defaultType
    
    // This child node is...
    mandatory autocreated protected
    
    // and supports same name siblings
    multiple
    
    // and has an on-parent-version setting of ...
    version


This definition can be written more compactly and with indentation:


    /*  An example node type definition */
    <ns = 'http://namespace.com/ns'>
    [ns:NodeType] > ns:ParentType1, ns:ParentType2
      orderable mixin
      - ex:property (string)
      = 'default1', 'default2'
        primary mandatory autocreated protected multiple
        version
        < 'constraint1', 'constraint2'
      + ns:node (ns:reqType1, ns:reqType2)
        = ns:defaultType
        mandatory autocreated protected multiple version


or, using short forms for the attributes, even like this:


    <ns='http://namespace.com/ns'>
    [ns:NodeType] >ns:ParentType1, ns:ParentType2 o m
      - ex:property='default1','default2' ! m a p * version <'constraint1', 'constraint2'
      + ns:node(ns:reqType1,ns:reqType2)=ns:defaultType m a p *  version



Grammar
-------
The following grammar defines the CND notation. Terminal symbols are in double quotes.


    cnd ::= {ns_mapping | node_type_def}
    ns_mapping ::= "<" prefix "=" uri ">"
    prefix ::= string
    uri ::= string
    node_type_def ::= node_type_name [supertypes] [options] {property_def | child_node_def}
    node_type_name ::= "[" string "]"
    supertypes ::= ">" string_list
    options ::= orderable_opt | mixin_opt | orderable_opt
    	    mixin_opt | mixin_opt orderable_opt
    orderable_opt ::= "orderable" | "ord" | "o"
    mixin_opt ::= "mixin" | "mix" | "m"
    property_def ::= "-" property_name [property_type_decl] [default_values] [attributes] [value_constraints]
    property_name ::= string
    property_type_decl ::= "(" property_type ")"
    property_type ::= "STRING" | "String" |"string" |
    		  "BINARY" | "Binary" | "binary" |
    		  "LONG" | "Long" | "long" |
    		  "DOUBLE" | "Double" | "double" |
    		  "BOOLEAN" | "Boolean" | "boolean" |
    		  "DATE" | "Date" | "date" |
    		  "NAME | "Name | "name" |
    		  "PATH" | "Path" | "path" |
    		  "REFERENCE" | "Reference" | "reference" |
    		  "UNDEFINED" | "Undefined" | "undefined" | "*"
    
    default_values ::= "=" string_list
    value_constraints ::= "<" string_list
    node_def ::= "+" node_name [required_types] [default_type] [attributes]
    node_name ::= string
    required_types ::= "(" string_list ")"
    default_type ::= "=" string
    attributes ::= "primary" | "pri" | "!" |
    	       "autocreated" | "aut" | "a" |
    	       "mandatory" | "man" | "m" |
    	       "protected" | "pro" | "p" |
    	       "multiple" | "mul" | "*" |
    	       "COPY" | "Copy" | "copy" |
    	       "VERSION" | "Version" | "version" |
    	       "INITIALIZE" | "Initialize" | "initialize" |
    	       "COMPUTE" | "Compute" | "compute" |
    	       "IGNORE" | "Ignore" | "ignore" |
    	       "ABORT" | "Abort" | "abort"
    string_list ::= string {"," string}
    string ::= quoted_string | unquoted_string
    quoted_string :: = "'" unquoted_string "'"
    unquoted_string ::= [A-Za-z0-9:_]+


CND Notation in Detail
----------------------

    cnd ::= {ns_mapping | node_type_def}

A CND consists of zero or more blocks, each of which is either namespace
declaration or a node type definition. Namespace prefixes referenced in a
node type definition block must be declared in a preceding namespace
declaration block.


### Namespace Declaration

    ns_mapping ::= "<" prefix "=" uri ">"
    prefix ::= string
    uri ::= string

A namespace declaration consists of prefix/URI pair. The prefix must be a
valid JCR namespace prefix, which is the same as a valid XML namespace
prefix. The URI can in fact be any string. Just as in XML, it need not
actually be a URI, though adhering to that convention is recommended.


### Node Type Definition

    node_type_def ::= node_type_name [super_types] [options] {property_def | child_node_def}

A node type definition consists of a node type name followed by an optional
supertypes block, an optional options block and zero or more blocks, each
either a property or node definition.


### Node Type Name

    node_type_name ::= "[" string "]" 

The node type name is delimited by square brackets and must be a valid JCR
name. It may be single-quoted (see Quoting, below). This element is the
only strictly required element within a node type definition, though a
definition consisting only of a node type name would simply define a new
node type identical to nt:base.


### Supertypes

    supertypes ::= ">" string_list

After the node type name comes the optional list of supertypes. If this
element is not present and the node type is not a mixin (see ?1.3.5
Options), then a supertype of nt:base is assumed. If present, the element
consists of a greater-than sign followed by a comma delimited list of node
type names, each of which may optionally be single-quoted (see Quoting
below). In Jackrabbit, multiple inheritance of node types is supported, so
this list can be greater than one item in length.


### Options

    options ::= orderable_opt | mixin_opt | orderable_opt mixin_opt | mixin_opt orderable_opt
    orderable_opt ::= "orderable" | "ord" | "o"
    mixin_opt ::= "mixin" | "mix" | "m"

The option indicators follow the node type name and optional supertype list.

If the keyword orderable (or a short form) is present, then the orderable
child node setting of the node type is true. If the keyword is missing,
then the setting is false.

If the keyword mixin (or a short form) is present, then this is a mixin
node type. If the keyword is missing, then this is a primary node type.


### Property Definition

    property_def ::= "-" property_name [property_type_decl] [default_values] [attributes] [value_constraints]

A property definition consists of a minus sign followed by a property name,
followed in turn by optional elements defining the property type, the
default values, the property attributes and the value constraints.


### Property Name

    property_name ::= string

The property name must be a valid JCR name or *, to indicate a residual
property definition. It may be single-quoted.


### Property Type

    property_type_decl ::= "(" property_type ")"
    property_type ::= "STRING" | "String |"string" |
    		  "BINARY" | "Binary" | "binary" |
    		  "LONG" | "Long" | "long" |
    		  "DOUBLE" | "Double" | "double" |
    		  "BOOLEAN" | "Boolean" | "boolean" |
    		  "DATE" | "Date" | "date" |
    		  "NAME | "Name | "name" |
    		  "PATH" | "Path" | "path" |
    		  "REFERENCE" | "Reference" | "reference" |
    		  "UNDEFINED" | "Undefined" | "undefined" | "*"

The property type is indicated by a keyword delimited by parentheses. If
the property type declaration is missing a type of STRING is assumed.


### Default Values

    default_values ::= "=" string_list

The default value or values, in the case of a multi-value property, are
indicated by an equal sign followed by either a single value in string form
or a comma-delimited list of values. The values may be single-quoted. If
the default value definition is missing then no default value is set.


### Attributes

    attributes ::= "primary" | "pri" | "!" |
    	       "autocreated" | "aut" | "a" |
    	       "mandatory" | "man" | "m" |
    	       "protected" | "pro" | "p" |
    	       "multiple" | "mul" | "*" |
    	       "COPY" | "Copy" | "copy" |
    	       "VERSION" | "Version" | "version" |
    	       "INITIALIZE" | "Initialize" | "initialize" |
    	       "COMPUTE" | "Compute" | "compute" |
    	       "IGNORE" | "Ignore" | "ignore" |
    	       "ABORT" | "Abort" | "abort"

The attribute indicators describe the characteristics of the property. The
presence of an attribute keyword indicates that the corresponding
characteristic applies to this property. It's absence indicates that the
corresponding characteristic does not apply.

The primary keyword indicates that this property is the primary item. It
may appear on a maximum of one property or child node definition within a
node type definition.

The multiple keyword indicates that this property is multi-valued.

A maximum of one on-version indicator may be present. If none is present
then an on-version setting of COPY is assumed.


### Value Constraints

    value_constraints ::= "<" string_list

Value constraint are specified by a less-than sign followed by a
comma-delimited list of constraint strings, each optionally single-quoted.


### Child Node Definition

    child_node_def ::= "+" node_name [required_types] [default_type] [attributes] 

A child node definition consists of a plus sign followed by a property
name, followed in turn by optional elements defining the required primary
node types, the default node type, and the node attributes.


### Node Name

    node_name ::= string

The node name must be a valid JCR name or `*`, to indicate a residual child
node definition. It may be single-quoted.


### Required Primary Node Types

    required_types ::= "(" string_list ")"

The required node types of the child node are indicated by a
comma-delimited list of node types, within parentheses. If this element is
missing then a required primary node type of nt:base is assumed. This is
the least restrictive setting possible.


### Default Primary Node Type

    default_type ::= "=" string

The default primary node type is indicated by an equals-sign followed by a
node type name, which may be single-quoted. If this element is missing then
no default primary node type is set.


### Attributes

    attributes ::= "primary" | "pri" | "!" |
    	       "autocreated" | "aut" | "a" |
    	       "mandatory" | "man" | "m" |
    	       "protected" | "pro" | "p" |
    	       "multiple" | "mul" | "*" |
    	       "COPY" | "Copy" | "copy" |
    	       "VERSION" | "Version" | "version" |
    	       "INITIALIZE" | "Initialize" | "initialize" |
    	       "COMPUTE" | "Compute" | "compute" |
    	       "IGNORE" | "Ignore" | "ignore" |
    	       "ABORT" | "Abort" | "abort"

The attribute indicators describe the characteristics of the child node.
The presence of an attribute keyword indicates that the corresponding
characteristic applies to this child node. It's absence indicates that the
corresponding characteristic does not apply.

The primary keyword indicates that this child node is the primary item. It
may appear on a maximum of one property or child node definition within a
node type definition.

The multiple keyword indicates that this child node may have same-name
siblings.

A maximum of one on-version indicator may be present. If none is present
then an on-version setting of COPY is assumed.


### Quoting

    string_list ::= string {"," string}
    string ::= quoted_string | unquoted_string
    quoted_string :: = "'" unquoted_string "'"
    unquoted_string ::= /* a string */

Single quotes (\') are used to allow for strings (i.e., names, prefixes,
URIs, values or constraint strings) with characters that would otherwise be
interpreted as delimiters.


### Escaping
The standard Java escape sequences are also supported:

    \n newline
    \t tab
    \b backspace
    \f form feed
    \r return
    \" double quote
    \' single quote
    \\ back slash
    \uHHHH Unicode character in hexadecimal


### Comments
Comment can also be included in the notation using either of the standard
Java forms:

    // A comment
    /* Another comment */

### Whitespace and Short Forms
The notation can be compacted by taking advantage of the following the fact that spacing around keychars 
(`[ ] > , - ( ) = <`), newlines and indentation are not required. So, the
following is also well-formed:

    [x] >y,z orderable mixin -p(date)=a,b primary mandatory autocreated protected multiple version <c,d

Additionally, though spaces are required around the keywords (orderable,
mixin, date, mandatory, etc.), short forms for keywords can be used. So,
this:

    [x] >y,z o m-p(date)=a,b ! m a p * version <c,d

is well-formed (but perhaps not recommended!).


### Why this Weird Notation?
Here's why:

Old Documentation Notation

Here is the definition of the built-in node type nt:resource using the old
documentation notation (used in v1.0 of the JCR specification, for example):


    NodeTypeName
      nt:resource
    Supertypes
      nt:base
      mix:referenceable
    IsMixin
      false
    HasOrderableChildNodes
      false
    PrimaryItemName
      jcr:data
    PropertyDefinition
      Name jcr:encoding
      RequiredType STRING
      ValueConstraints []
      DefaultValues null
      AutoCreated false
      Mandatory false
      OnParentVersion COPY
      Protected false
      Multiple false
    PropertyDefinition
      Name jcr:mimeType
      RequiredType STRING
      ValueConstraints []
      DefaultValues null
      AutoCreated false
      Mandatory true
      OnParentVersion COPY
      Protected false
      Multiple false
    PropertyDefinition
      Name jcr:data
      RequiredType BINARY
      ValueConstraints []
      DefaultValues null
      AutoCreated false
      Mandatory true
      OnParentVersion COPY
      Protected false
      Multiple false
    PropertyDefinition
      Name jcr:lastModified
      RequiredType DATE
      ValueConstraints []
      DefaultValues null
      AutoCreated false
      Mandatory true
      OnParentVersion IGNORE
      Protected false
      Multiple false


Old Configuration Notation

Here is the same node type in the standard XML notation (used in
configuration files in the Jackrabbit project, for example):


    <nodeType name="nt:resource"
    	  isMixin="false"
    	  hasOrderableChildNodes="false"
    	  primaryItemName="jcr:data">
        <supertypes>
    	<supertype>nt:base</supertype>
    	<supertype>mix:referenceable</supertype>
        </supertypes>
        <propertyDefinition name="jcr:encoding"
    			requiredType="String"
    			autoCreated="false"
    			mandatory="false"
    			onParentVersion="COPY"
    			protected="false"
    			multiple="false"/>
        <propertyDefinition name="jcr:mimeType"
    			requiredType="String"
    			autoCreated="false"
    			mandatory="true"
    			onParentVersion="COPY"
    			protected="false"
    			multiple="false"/>
        <propertyDefinition name="jcr:data"
    			requiredType="Binary"
    			autoCreated="false"
    			mandatory="true"
    			onParentVersion="COPY"
    			protected="false"
    			multiple="false"/>
        <propertyDefinition name="jcr:lastModified"
    			requiredType="Date"
    			autoCreated="false"
    			mandatory="true"
    			onParentVersion="IGNORE"
    			protected="false"
    			multiple="false"/>
    </nodeType>


New Format

And, here it is in the new CND notation:

    [nt:resource] > mix:referenceable
    - jcr:encoding
    - jcr:mimeType mandatory
    - jcr:data (binary) mandatory
    - jcr:lastModified (date) mandatory ignore


Case closed.

Syntax highlighting for text editors
------------------------------------
Here is a TextMate bundle for CND syntax highlighting: [CND.zip](CND.zip)
