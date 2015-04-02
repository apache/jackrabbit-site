Title: Repository lifecycle
The lifecycle of any Jackrabbit Content Repository starts with a call to
one of the RepositoryFactory.create() methods passing optionally the source
of a repository configuration file (which by convention is called
config.xml) and the RepositoryFactoryHome, which points to a directory from
which the Repository will continue reading further information for start-up
and in many cases will store the actual data that is persisted in the
repository and its workspaces.

Not supplying the RepositoryFactoryHome will default to the users home dir
from the System property user.dir.

Not supplying the configuration file parameter will default to the value of
Repository.factory.config System Property and if that is not set it will
default to the config.xml in the RepositoryFactoryHome.

Calling the create() method will instantiate the RepositoryFactory
singleton that will then, through the getRepository(String name) method,
serve as the factory for Repository instances.

As per the config.xml a repository are started up with the respectively
configured RepositoryStore, the RepositoryStore defines where the
repository stores information that is visible for the entire Repository
which includes things like the uuid of the root node, repository
properties, the namespace registry, node type definitions or the version
backing store in a file structure as follows.


    ./meta:
    rep.properties
    rootUUID
    
    ./namespaces:
    ns_reg.properties
    
    ./nodetypes:
    custom_nodetypes.xml
    
    ./versions:


The RepositoryStore normally points to a regular (i.e. local) file system
but is abstracted through an abstract FileSystem that can be configured to
point to a different FileSystem implementation, in case the above
information should be stored in a different data container.

... to be continued ... 
