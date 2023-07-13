## Abstract
<!-- Context      -->
Linked data can be published online to describe all sort of concepts to form a 
pseudo infinite (knowledge) graph.
The data on the web are not organized in a way that at specific subgraph we have a guarenty to find complete information (following a contract) about a set of concepts.
Hence when making exploring the web of linked data 


the full information
about the data requested in a query


 Another important property of linked data is the ability
to get more context about the data by derefencing the IRI that compose a triple to obtain
a new data source with more triple describing the target. 
Also the links between the property of the object are semantic hence 


Linked Data can be published on the Web in a variety of APIs such as in subject pages or in a SPARQL endpoint.
Each API has its own set of trade-offs:
in the former, the client needs to perform a rather slow link traversal algorithm to find an answer to any query, but the 
API is cheap to host; while in the latter the server is able to provide a rather fast and concise answer to a 
well-defined query, but the API is more expensive to maintain. 
<!-- Need         -->
An in-between solution could work using guided link traversal and hypermedia, in which the server already exposes hints 
of an ordering of subjects in a search space.
<!-- Task         -->
The [TREE hypermedia specification](https://w3id.org/tree/specification) allows to define such relations between pages (fragments) containing zero or more members of the collection.
<!-- Object       -->
In this paper, we investigate a Guided Link Traversal-based Query Processing (GLTQP) approach to search through such 
interlinked fragments, and reduce the number of fragments that need to be visited by taking into account the described relations.
<!-- Findings     -->
Our findings show that we are able to use the hypermedia descriptions of the TREE specification to prune links to 
fragments that will certainly not contribute to the SPARQL query based on a reachability criteria that can be
the basis for a solver resolving a boolean equation combinaing the SPARQL FILTER expression and TREE Relation descriptions.
<!-- Conclusion   -->
This solver has been made available as open-source as part of the Comunica project to demonstrate how it can generate faster results on the client for 
SPARQL queries with FILTER clauses over TREE fragmented Linked Datasets.
