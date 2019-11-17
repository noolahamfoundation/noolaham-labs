# NF - Labs - Exploring Linked Data and Ontologies
## Purpose
The purpose of this exercise is to better understand linked data and ontologies.  Specifially, we will make use of 
Fedora [http://fedorarepository.org](http://fedorarepository.org) Linked Data Platform and Apache Jena Fuseki [https://jena.apache.org/documentation/fuseki2/index.html](https://jena.apache.org/documentation/fuseki2/index.html) SPARQL server.  
We will make use of dublin core ontology to describe creative works and link them to other resources such as people and places.

### See Also:
[NF Core Concepts Ontology - Prototype](https://docs.google.com/document/d/13jLu-OnyDwhw4LLOay6JBzhLxSioXJRjD2PjePTtRUA/edit)

### Audience
Anyone interested in applying Linked Data to problems in the Tamil context is welcome.  Though the exercises are geared towards the technically inclined, the discussion will be cross-disciplinary  

### Required Materials and Preparation
* Some background reading about Linked Data and Ontologies is helpful.
* A VM or server to install applications (optional, we will consider providing VMs if requested


### Learning Objectives
1. Creating RDF resources in Fedora
2. Creating RDF resources with non literal property values in Fedora
3. Exporting resource into serialized formats such as RDF/XML or JSON-LD using CURL
4. Linked Data Platform - CRUD
5. Importing the Triplestore and querying the triplestore using Apache Jena Fuseki  and SPARQL queries
6. Creating RDF resources with binary files
7. Querying and displaying RDF and binary files stored in Fedora 
8. Explore possibilities of building an Ontology for Noolaham content

### How To
Individual can undertake the exercises on their own or in discussion with peers.  If there is sufficient interest, we will have a skype or irc/conference meeting to discuss the concepts, technologies and applications.

### Exercise Milestones
- Setup fedora vagrant or docker
- Create resources using a simple ontology
- Query resources using SPARQL
- How to interact with Non RDF Resources (binary files)

### Documentation/References
- [https://wiki.duraspace.org/display/FEDORA46/Feature+Tour](https://wiki.duraspace.org/display/FEDORA46/Feature+Tour)
- [https://wiki.duraspace.org/display/FEDORA4x/LDP-PCDM-F4+In+Action#LDP-PCDM-F4InAction-Book-CreateDirectContainer](https://wiki.duraspace.org/display/FEDORA4x/LDP-PCDM-F4+In+Action#LDP-PCDM-F4InAction-Book-CreateDirectContainer)
- [https://github.com/projecthydra/hydra/wiki/LDP-Containers-for-the-perplexed#indirect-container](https://github.com/projecthydra/hydra/wiki/LDP-Containers-for-the-perplexed#indirect-container)
- [http://islandora.ca/sites/default/files/islandora_fedora4.pdf](http://islandora.ca/sites/default/files/islandora_fedora4.pdf)
 -[http://islandora.ca/sites/default/files/islandora_fedora4.pdf](Triplestore - http://www.krisalexander.com/innovation/2013/07/16/the-difference-between-a-triplestore-and-a-relational-database/)
- [LDP Primer - https://dvcs.w3.org/hg/ldpwg/raw-file/tip/ldp-primer/ldp-primer.html](LDP Primer - https://dvcs.w3.org/hg/ldpwg/raw-file/tip/ldp-primer/ldp-primer.html)
- [http://islandora.ca/sites/default/files/Introduction%20and%20Hands-on%20with%20Fedora%204.pdf](http://islandora.ca/sites/default/files/Introduction%20and%20Hands-on%20with%20Fedora%204.pdf)

### Installation and Tools
- [https://hub.docker.com/r/yinlinchen/fcrepo4-docker/](https://hub.docker.com/r/yinlinchen/fcrepo4-docker/) (Recommended)
- [https://github.com/fcrepo4-exts/fcrepo4-vagrant](https://github.com/fcrepo4-exts/fcrepo4-vagrant)
- [https://github.com/fcrepo4-labs/fcrepo-import-export](https://github.com/fcrepo4-labs/fcrepo-import-export)

### Concepts
- Linked Data
- RDF (subject predicate object)
- RDF properties
- RDF Resource vs Non RDF Resource
- Linked Data Platform
- LDP Containers
- Ontology
- Triplestore
- SPARQL Query

### Contact
- vakeeswaran@gmail.com
- natkeeran@gmail.com

### Technical Notes
 1. Fedora Insert Properties
  - insert Literal Value

INSERT {<> dc:title "image1" .}
WHERE { }

  - Insert Non Literal Value
  
INSERT {<> dc:creator <http://serverip:8080/fcrepo/rest/writer1> .}
WHERE { }

#### SPARQL
 - Get all triples
 
PREFIX ldp: <http://www.w3.org/ns/ldp#>

prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

prefix owl: <http://www.w3.org/2002/07/owl#>

SELECT ?subject ?predicate ?object

WHERE {

  ?subject ?predicate ?object
  
}

LIMIT 100

####Get all the works written by writer1

 PREFIX ldp: <http://www.w3.org/ns/ldp#>
 
PREFIX dc: <http://purl.org/dc/elements/1.1/>

prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#>

prefix owl: <http://www.w3.org/2002/07/owl#>

SELECT ?subject ?predicate ?object

WHERE {

  ?subject dc:creator <http://serverip:8080/fcrepo/rest/writer1>
  
}

LIMIT 25

#### Importing/Exporting Resources from Fedora
java -jar target/fcrepo-import-export-0.0.1-SNAPSHOT.jar --mode export --resource http://serverip:8080/fcrepo/rest/ --descDir data --binDir data --rdfExt .jsonld --rdfLang application/ld+json


### Sample RDF

```
<?xml version="1.0" encoding="UTF-8"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:ebucore="http://www.ebu.ch/metadata/ontologies/ebucore/ebucore#" xmlns:fedora="http://fedora.info/definitions/v4/repository#" xmlns:fedoraconfig="http://fedora.info/definitions/v4/config#" xmlns:foaf="http://xmlns.com/foaf/0.1/" xmlns:image="http://www.modeshape.org/images/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:ldp="http://www.w3.org/ns/ldp#" xmlns:mix="http://www.jcp.org/jcr/mix/1.0" xmlns:mode="http://www.modeshape.org/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:premis="http://www.loc.gov/premis/rdf/v1#" xmlns:rdfs="http://www.w3.org/2000/01/rdf-schema#" xmlns:sv="http://www.jcp.org/jcr/sv/1.0" xmlns:test="info:fedora/test/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <rdf:Description rdf:about="http://serverip:8080/fcrepo/rest/">
      <fedora:lastModified rdf:datatype="http://www.w3.org/2001/XMLSchema#dateTime">2016-09-23T15:05:16.836Z</fedora:lastModified>
      <rdf:type rdf:resource="http://www.w3.org/ns/ldp#RDFSource" />
      <rdf:type rdf:resource="http://www.w3.org/ns/ldp#Container" />
      <rdf:type rdf:resource="http://www.w3.org/ns/ldp#BasicContainer" />
      <fedora:writable rdf:datatype="http://www.w3.org/2001/XMLSchema#boolean">true</fedora:writable>
      <rdf:type rdf:resource="http://fedora.info/definitions/v4/repository#RepositoryRoot" />
      <rdf:type rdf:resource="http://fedora.info/definitions/v4/repository#Resource" />
      <rdf:type rdf:resource="http://fedora.info/definitions/v4/repository#Container" />
      <ldp:contains rdf:resource="http://serverip:8080/fcrepo/rest/book1" />
      <ldp:contains rdf:resource="http://serverip:8080/fcrepo/rest/writer1" />
      <ldp:contains rdf:resource="http://serverip:8080/fcrepo/rest/place1" />
      <ldp:contains rdf:resource="http://serverip:8080/fcrepo/rest/book2" />
      <fedora:hasTransactionProvider rdf:resource="http://serverip:8080/fcrepo/rest/fcr:tx" />
   </rdf:Description>
</rdf:RDF>
```

