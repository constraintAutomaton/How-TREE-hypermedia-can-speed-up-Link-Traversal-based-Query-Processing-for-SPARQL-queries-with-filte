## Filter pushdown to discriminate link during LTQP
{:#guided_link_traversal}

LTQP in its most naive form has a pseudo-infinite domain [](cite:cites Hartig2016), as a result
it is not possible to evaluate the completeness and to have a stopping condition related to the finding of complete results [](cite:cites hartig2012). 
Also, given the vastness of the web, the overwhelming majority of data sources will not contribute to query completeness (in most realistic queries).
Hartig and Freytag [](cite:cites hartig2012) introduces the concept of reachability criterium, which consists of policies
of IRI to dereference, hence limiting the range of the web that has to be explored to consider to have obtained completeness.
Corrolary, those criteriums serve as a mechanism to prune links that are not relevant to the answer to the query.
This is particularly useful in the context of structured environments such as in the use case of Solid and fragmented datasets
where a priori we have metaknowledge of how to access data related to a query [](cite:cites taelman2023).
With this metaknowledge, the query engine can find triples that will describe the location of the information requested,
hence "guiding" the query engine towards the right data source [](cite:cites verborgh2020). 

Our pushdown filter is based in its use on the concept of reachability criterium.
In the definition by Hartig and Freytag [](cite:cites hartig2012) a reachability criterium is a function discriminating the dereferencing of 
an IRI based on the triple available in a current document a query.
In our approach, we interpret the hypermedia description of the constraint of the fragment as a boolean equation as
exemplify in [](#example-sparql).
In this example, the left hand of the expression, the variable, is contingent on a SPARQL query expression.
It is the variable pertaining to the property that the constraint is targeting.
The property targeted by the relation is defined by the object of the triple having the predicate `tree:path`.
In the example it was $$ ?t $$, because the example of [](#TREE-relation-turtle-example)
has the `tree:path` property `etsi:hasTimestamp`. 
The boolean operator such as; equal, greater than, is described by the [RDF type of the TREE relation](https://treecg.github.io/specification/#Relation), in Turtle serialization it is the object of the triple with the predicate "`a`".
Finally, the literal is simply represented by the object of the triple in the relation,
containing the predicate `tree:value`.
The SPARQL filter expression can naively be converted into a boolean expression.
Hence upon discovery of a document, the query engine gathers the relevant triples to form the boolean expression 
representing the constraint of the next fragment and pushdown the SPARQL filter expression.
After having those two boolean expressions close together they are evaluated to find the satisfiability and upon satisfaction
the IRI targeting the next fragment (`tree:node` in the TREE specification) is added to the link queue following the
concept of reachability criterium as illustrated in [](#running_example).


<figure id="running_example">
<img src="img/running_example.drawio.svg" alt="[Running example of our GLTQP approach]" class="figure-narrow" style="height: 20vh">
<figcaption markdown="block">
Running example of our GLTQP approach based on [](#example-sparql).
</figcaption>
</figure>

We made an open source implementation of this criterium available at [https://github.com/constraintAutomaton/comunica-feature-link-traversal/tree/feature/time-filtering-tree-sparqlee-implementation]() with an associated demo available at
[https://github.com/constraintAutomaton/TREE-Solver-LTQP-demo-engine](). In the rest of this section we will present our experimental result.