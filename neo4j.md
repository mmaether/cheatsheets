# Neo4j

- Graph: a collection of nodes, relationships.
- Relationships have only one direction. A person may own a home, but a home does not own a person.
  - Relationships have a type, i.e. owns, or is_the_owner_of.
- Properties: key-value pairs on a node or relationship.

George Clooney is a thing. :Person
His home is a thing. :Building
His corvette is a thing. :Vehicle, :Car

Person properties example:

```json
{
    name: 'George Clooney'
    birth_year: 1961
}
```

Building properties example:

```json
{
    location: 'Italy'
}
```

## Property Value Types

Type | Example
---- | -------
Boolean | true, false
Text | "aka string"
Numbers | 123, 56.70
Lists | ['must', 'be', 'same', 'type']

```
MATCH (node1)--(node2) RETURN node1, node2
```

## Read

```
[MATCH WHERE]
[OPTIONAL MATCH WHERE]
[WITH [ORDER BY] [SKIP] [LIMIT]]
RETURN [ORDER BY] [SKIP] [LIMIT]
```

## Cypher

Cypher is the Neo4j query language to manipulate graphs easily. It reuses syntax from SQL and mixes it with kind of ASCII-art to represent graphs. 

[Source](https://learnxinyminutes.com/docs/cypher/)

Match Relationships

```
MATCH (actor:Person)-[rel:ACTED_IN | DIRECTED]->(movie:Movie) 
RETURN actor, rel, movie
LIMIT 10
```

Optional Matches:

```
MATCH (movie:Movie)
MATCH (director:Person)-[:DIRECTED]->(movie)
MATCH (director)-[:ACTED_IN]->(movie)
RETURN movie.title, director.name
```

```
MATCH (movie:Movie)
OPTIONAL MATCH (director:Person)-[:DIRECTED]->(movie)<-[:ACTED_IN]-(director)
RETURN movie.title, director.name
```

```
MATCH (p1:Person)-[:HAS_CONTACT]->(p2:Person)-[:DIRECTED]->(movie:Movie)
RETURN p1.name, p2.name, movie.title
LIMIT 5
```

```
MATCH (p1:Person)-[:HAS_CONTACT]->(p2:Person)
OPTIONAL MATCH (p2)-[:DIRECTED]->(movie:Movie)
RETURN p1.name, p2.name, movie.title
```

```
MATCH (tom:Person{name: 'Tom Hanks', born: 1956})
RETURN tom
LIMIT 1
```

```
MATCH (tom:Person)
WHERE tom.name = 'Tom Hanks' AND tom.born = 1956
RETURN tom
LIMIT 1
```

### Regular Expression

You can match on regular expressions by using `=~ "regexp"` like this:

```cypher
MATCH (movie:Movie)
WHERE movie.title =~ '(?i)The.*'
RETURN movie.title
```

`(?i)` makes it case insensitive.

### Transform Results

ORDER BY, LIMIT, SKIP, AS

## Create

Create a Node

```
CREATE (cat:Cat:Animal{sound: 'Meow', eats: 'Birds'})
RETURN cat
```

Create relationships

```
CREATE (cat:Cat{name: 'Fluffy'})-[:GROOMS]->(cat)
CREATE (cat:Cat{name: 'Fluffy'})-[:GROOMS{period: 'Daily'}]->(cat)
```

Update relationships

```
MATCH (joe:Bunny{name: 'Joe Bunny'}),
(sarah:Bunny{name: 'Sarah Bunny'})
MERGE (joe)-[:LIKES]->(sarah)
MERGE (joe)<-[:LIKES]-(sarah)
RETURN joe, sarah
```

CREATE (tarantino:Person{name: 'Quentin Tarantino'})
CREATE (hatefulEight:Movie{title: 'The Hateful Eight'})
MERGE (tarantino)-[:DIRECTED]-(hatefulEight)
RETURN tarantino, hatefulEight

## Delete

```
MATCH (node)-[rel]-()
DELETE node, rel

MATCH (node)
DELETE node

// Or just have an Optional Match
MATCH (node)
OPTIONAL MATCH (node)-[rel]-()
DELETE node, rel

MATCH (node)
DETACH DELETE node

MATCH (tom:Person{name: 'Tom Hanks'}), 
(other)-[rel:HAS_CONTACT]->(tom)
DELETE rel
```
