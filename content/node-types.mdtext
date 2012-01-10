Title: Node Types
Each node in a Jackrabbit workspace tree has a node type that defines the
child nodes and properties it may (or must) have. Developers can use node
types to define a custom content model for their application domain and
have Jackrabbit enforce the constraints of that model at the repository
level.

<a name="NodeTypes-PrimaryvsMixin"></a>
## Primary vs Mixin

There are two categories of node types, *primary* and *mixin*. Every node
has a primary node type assigned to it upon creation (see *Node.addNode*
in the JCR API). In addition, a mixin node type may be added to a node
later in its lifecycle (see *Node.addMixin*).

The primary node type of a node usually defines node structure (i.e.,
allowed and required child nodes and properties) related to the problem
domain being modeled. For example, a node used in storing content about
business contacts might have the primary type *myapp:Contact* which
defines properties such as *myapp:givenName*, *myapp:familyName* and so
forth.

Mixin node types usually specify additional properties or child nodes
related to a capability being added to the node. These capabilities may
include generic repository-level functions as in the case of the built-in
mixins *mix:versionable* and *mix:lockable*, for example, or
domain-level capabilities such as a (hypothetical) *myapp:Emailable*
mixin type that adds the property *myapp:emailAddress* to a node.

<a name="NodeTypes-Inheritance"></a>
## Inheritance

Primary node types are arranged in an inheritance hierarchy. Every primary
node type must be the subtype of at least one existing node type. The
built-in node type *nt:base* serves as the root of this hierarchy.
Jackrabbit supports multiple inheritance of node types so node types can
have more than one supertype.

Mixin node types do not have to have supertypes.

The JSR 170 specification and the current public review draft of the JSR
283 specification (section 4.7.7) leave it up to the implementation whether
e.g. the orderable child nodes setting is inherited from supertypes.
Inheritance semantics, especially with multiple inheritance, are
non-trivial at best and up to a certain degree arbitrary. Jackrabbit
therefore, in compliance with the spec, doesn't support inheritance of node
type attributes such as orderable.

<a name="NodeTypes-NodeTypeDefinition"></a>
## Node Type Definition

A node type definition has the following attributes:

* *Name* Every node type registered with the repository has a unique name.
The naming conventions for node 		    types are the same as
for items (i.e., they may have a colon delimited prefix).
* *Supertypes* A primary node type (with the exception of *nt:base*) must
extend another node type (and may extend more than one node type). A mixin
node type may extend another node type.
* *Mixin Status* A node type may be either primary or mixin.
* *Orderable Child Nodes Status* A primary node type may specify that child
nodes are client-orderable. If this status is set to true, then
*Node.orderBefore* can be used to set the order of child nodes. Only
primary node types control a node's status in this regard. This setting on
a mixin node type will not have 		    any effect on the node.
* *Property Definitions* A node type contains a set of definitions
specifying the properties that nodes of this node type are allowed (or
required) to have and the characteristics of those properties (see below).
* *Child Node Definitions* A node type contains a set of definitions
specifying the child nodes that nodes of this node type are allowed (or
required) to have and the characteristics of those child nodes (including,
in turn, their node types, see below).
* *Primary Item Name* A node type may specify one child item (property or
node) by name as the primary item. This indicator is used by the method
*Node.getPrimaryItem()*.

<a name="NodeTypes-PropertyDefinition"></a>
## Property Definition

A property definition (within a node type definition) contains the the
following information:

* *Name* The name of the property to which this definition applies, or
"***" if this definition is			      a "residual
definition', meaning that it applies to any additional properties with any
names apart from those otherwise defined in this node type.
* *Required Type* The required type of the property. One of
** *STRING*
** *BINARY*
** *LONG*
** *DOUBLE*
** *BOOLEAN*
** *DATE*
** *PATH*
** *NAME*
** *REFERENCE*
** *UNDEFINED* (the property can be of any type)
* *Value Constraints* The value constraints on the property define the
range of values that may be assigned			     to this
property.
* *Default Value* The value that the property will have if it is
auto-created.
* *Auto-create Status* Whether this property will be auto-created when its
parent node is created. Only properties with a default value can be
auto-created.
* *Mandatory Status* A mandatory property is one that must exist. If a node
of a type that specifies a			   mandatory property is
created then any attempt to save that node without adding the mandatory
property will fail. Since single-value properties either have a value or do
not exist (there being no concept of the null value) this implies that a
mandatory single-value property must have a value. A mandatory multi-value
property on the other hand may have zero or more values.
* *On-Parent-Version Status* The *onParentVersion* status of specifies
what happens to this property if a			   new version of
its parent node is created (i.e. a checked-in is done on it).
* *Protected Status* A protected property is one which cannot be modified
(i.e. have child nodes or properties added or removed) or removed from its
parent through the JCR API.
* *Multiple Values Status* Whether this property can have multiple values,
meaning that it stores an array of values, not just one. Note that this
"multiple values" flag is special in that a given node type may have two
property definitions that are identical in every respect except for the
their "multiple values" status. For example, a node type can specify two
string properties both called X, one of which is multi-valued and the other
that is not. An example of such a node type is *nt:unstructured*.

<a name="NodeTypes-ChildNodeDefinition"></a>
## Child Node Definition

A child node definition (within a node type definition) contains the the
following information:

* *Name* The name of the child node to which this definition applies or
"***" if this definition is			      a "residual
definition', meaning that it applies to any additional child nodes with any
			names apart from those otherwise defined in this
node type.
* *Required Primary Types* If it specifies only a single node type N then
the primary node type of this child node must be N or a subtype of N. If
this attribute specifies multiple node types N1, N2,..., Nm then the
primary node type of this child node must be a subtype of all the types N1,
N2, ... Nm. Note that this			   is possible because
Jackrabbit supports multiple inheritance among node types and that each
node still has one and only one primary node type.
* *Default Primary Type* This is the primary node type automatically
assigned if no node type information is specified when the node is created.
* *Auto-create Status* Governs whether this child node will be auto-created
when its parent node is created.
* *Mandatory Status* Governs whether the child node is mandatory. A
mandatory child node is one that must exist. If a mandatory child node is
missing from a parent node then save on the parent node will fail.
* *On-Parent-Version Status* This specifies what to do with the child node
if its parent node is versioned.
* *Protected Status* This governs whether the child node is protected. A
protected node is one which cannot be modified (have child node or
properties added to it or removed from it) or be removed from its	   
	      parent through the JCR API.
* *Same-Name Siblings Status* This governs whether this child node can have
same-name siblings, meaning that the parent node can have more than one
child node of this name.

<a name="NodeTypes-RegisteringNodeTypes"></a>
## Registering Node Types

Each Jackrabbit instance has a *NodeTypeRegistry* which is created on
start-up and populated with the set of built-in node types (these include
both those required by the JCR specification and others required by the
Jackrabbit implementation).

First you define your node types in a text file using the "Compact
Namespace and Node Type Definition" (CND) notation, then register them
using the  [*JackrabbitNodeTypeManager*](http://jackrabbit.apache.org/api/1.5/org/apache/jackrabbit/api/JackrabbitNodeTypeManager.html)
. The following code gives an example:


    import javax.jcr.Session;
    import org.apache.jackrabbit.api.JackrabbitNodeTypeManager;
    import java.io.FileInputStream;
    
    public class CustomNodeTypeExample {
        public static void RegisterCustomNodeTypes(Session session, String
cndFileName)
    	throws Exception {
    
    	// Get the JackrabbitNodeTypeManager from the Workspace.
    	// Note that it must be cast from the generic JCR NodeTypeManager
to the
    	// Jackrabbit-specific implementation.
    	JackrabbitNodeTypeManager manager = (JackrabbitNodeTypeManager)
    	       session.getWorkspace().getNodeTypeManager();
    	// Register the custom node types defined in the CND file
    	manager.registerNodeTypes(new FileInputStream(cndFileName),
    	       JackrabbitNodeTypeManager.TEXT_X_JCR_CND);
        }
    }


Continue to [Node Type Notation](node-type-notation.html)
 or [Node Type Visualization]
