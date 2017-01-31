# MEDIAFLUX

## Concepts

- assets are virtual containers for metadata and a content (eg. a data file, image, video, sound file, etc)
- in mediaflux, metadata are documents which are instances of document type. (so you need to define document types first before entering metadata)
- assets can be associated with multiple (metadata) documents, but can only be associated to one content 
- assets are stored in asset namespaces
- document types are stored in document type name spaces
- content are stored in "stores" (the underlying storage can be file system storage, aws s3, etc)
- content can also be stored outside of mediaflux using links
- namespaces are essentially "directories"
- you can create namespaces within name spaces
- everything (documents, document types, etc.) are defined and stored as using XML

## Talking to Mediaflux
1. Raw TCP/IP 
2. HTTP
3. HTTPS
4. SOAP   
Use Mediaflux client library to write Java and .Net applications that talk to mediaflux server

## Aterm 

- is essentially a command-line SOAP client to the mediaflux server with TCL scripting capabilities
- it can be used to execute server-side `mediaflux services`


## Useful Aterm commands

```sh

# ---
# Assets
# ---

# list asset namespaces
$ asset.namespace.list 

# create and get details of asset namespace
$ asset.namespace.create :namespace testNamespace
$ asset.namespace.describe :namespace testNamespace

# Another way to do this, is to treat aTerm like a file system to list assets in a namespace:
$ cd /testNamespace
$ ls


# ---
# Document types
# ---

# list document type namespaces
$ asset.doc.namespace.list

# create and get details of document type namespaces
$ asset.doc.namespace.create :namespace testNamespace
$ asset.doc.namespace.describe :namespace testNamespace

# list available doc types in global and specific namespace
$ asset.doc.type.list 
$ asset.doc.type.list :namespace testNamespace

# view documentation for doc type (eg. mf-note)
$ asset.doc.type.describe :type testDocTypeName
$ asset.doc.type.describe :type test-Namespace:testDocTypeName

# create document type in namespace ns with a string field called name
$ asset.doc.type.create 
                :type ns:test 
                :definition < :element -name x -type string >


# ---
# Data stores
# ---

# list stores available
$ asset.store.list

# describe stores (places to store files, images, videos, asset content)
$ asset.store.describe :name testStoreName

# ---
# Retrieve asset
# ---

# retrieve a data asset
$ asset.get :id 324234
$ asset.destroy :id 32423432



# ---
# Create asset
# ---

# the in-file could be a Java inputstream
# NOTE: there is a whitespace between the closing angle brackets "> >"

$ asset.create :namesapce testNS
                :meta < :mf-note
                        < :note "Hello World" > >
                :in file:/local/path/to/afile.dat


# ---
# Asset Query Language
# ---

# select items from namespace that match criteria in where clause
$ asset.query :namespace parentNs:subNs 
              :where xpath(doc-type/element\[@attributeName='value'\]) has value and
                     xpath(doc-type/element) = 'value'


# execute service on each item returned from query
$ asset.query :where namespace>=parentNs :action pipe :service -name asset.destroy

```

## MF Desktop (web client)
```sh
# use MF Desktop to add elements to doc types
$ asset.doc.type.list :namespace <ns>

# use MF Desktop to create dictionary items
$ dictionary.namespace.create : namesapce <ns>


```

## Export tcl script to install Doc type on another server (dev -> prod)
```sh
$ asset.doc.type.script.create :type <ns:doctype>
                                :out file:/path/to/file.tcl

#example                                
$ asset.doc.type.script.create :type myns:people
                                :out file:/home/user123/MakePeopleDocType.tcl
```


