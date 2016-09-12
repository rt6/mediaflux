# mediaflux

## Useful Aterm commands

```sh
$ asset.doc.namespace.list
$ asset.doc.namespace.create :namespace <ns>
$ asset.namespace.describe :namespace <ns>
$ asset.store.describe :name <storeName>
$ asset.get :id <id>
$ asset.destroy :id <id>

# view documentation for doc type (eg. mf-note)
$ asset.doc.type.describe :type <docTypeName>

# the in-file could be a Java inputstream
$ asset.create :namesapce <ns>
                :meta <: mf-note
                        <: note "Hello World" >>
                :in-file <local-path>

# view projects on the server
$ cd projects
$ ls

```

#Export tcl script to install Doc type on another server (dev -> prod)
```sh
$ asset.doc.type.script.create :type <ns:doctype>
                                :out file://path/to/file.tcl

#example                                
$ asset.doc.type.script.create :type myns:people
                                :out file://home/user123/MakePeopleDocType.tcl
```
