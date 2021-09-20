---
attachments: [Clipboard_2021-09-16-10-18-06.png, Clipboard_2021-09-16-11-17-34.png, Clipboard_2021-09-16-11-21-33.png, Clipboard_2021-09-16-11-22-00.png]
tags: [Notebooks/DesignDataApp]
title: 02-2 - Data Models and Query Languages - Graph Moels
created: '2021-09-16T06:47:25.689Z'
modified: '2021-09-20T05:59:04.520Z'
---

# 02-2 - Data Models and Query Languages - Graph Moels

### Graph Model

The relational model can handle simple cases of many-to-many relationships, but as the connections within your data become more complex, it becomes more natural to start modeling your data as a graph. 

graph consists of two kinds of objects: 
* vertices - also known as nodes or entities
* edges - also known as relationships or arcs

graphs are not limited to homogeneous data, such as web graph (web pages and links) or road network, an equally powerful use of graphs is to provide a consistent way of storing completely different types of objects in a single datastore. For example Facebook maintains a single graph with many different types of vertices and edges: vertices represent people, locations, events, checkins, and comments made by users;
edges indicate which people are friends with each other, which checkin happened in which location, who commented on which post, who attended
which event, and so on.

![](@attachment/Clipboard_2021-09-16-10-18-06.png)

Graphs are good for evolvability. You could imagine extending the graph to also include many other facts about Lucy and Alain, or other people. For instance, you could use it to indicate any food allergies they have (by introducing a vertex for each allergen, and an edge between a person and an allergen to indicate an allergy), and link the allergens with a set of vertices that show which foods contain which substances.

As is typical for a declarative query language, you don’t need to specify such execution details when writing the query: the query optimizer automatically chooses the strategy that is predicted to be the most efficient.
One language is Cypher, which created for Noe4j database, but one can also query using SQL (the relationship itself can be stored in relational database). But in graph query you may not know the number of joins needed, you may need to traverse a variable number of edges before you find the vertex you’re looking for. The book have a good exmaple why not use SQL here in page 85.

#### Triple-Stores and SPARQL

The triple-store model is mostly equivalent to the property graph model, but it add various tools and languages. In a triple-store, all information is stored in the form of very simple three-part statements: subject, predicate, object (Jim, Like, Bananas). 

* Subject = vertex
* object:
  1. A value in a primitive datatype (string, number) ==>  predicate and object are key and value. for exmaple (lucy, age, 33) is like the vertex (lucy {"age": 33}).
  2. another vertex, then the predicate is the label of the edge that connect two values. for example (lucy, Married_to, alain).

  ![](@attachment/Clipboard_2021-09-16-11-17-34.png)


In this example: 
* vertices of the graph are written as _:someName. The name doesn’t mean anything outside of this file; it exists only because we otherwise wouldn’t know which triples refer to the same vertex. 
* When the predicate represents an edge, the object is a vertex, as in _:idaho :within _:usa. 
* When the predicate is a property, the object is a string literal, as in _:usa :name "United States".

You can use semicolons to say multiple things about the same subject, which will reduce the repetitiveness.

![](@attachment/Clipboard_2021-09-16-11-22-00.png)

