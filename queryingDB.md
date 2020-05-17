

# Mongo Commands
https://docs.mongodb.com/manual/tutorial/query-documents/
- [Getting Up And Running](#getting-up-and-running)
- [Querying](#querying)
  - [Specify Equality Conditions](#specify-equality-conditions)
  - [Specify And Conditions](#specify-and-conditions)
  - [Specify Or Conditions](#specify-or-conditions)
  - [Specify And as well as Or Conditions](#specify-and-as-well-as-or-conditions)
  - [Specify Nested Equality](#specify-nested-equality)
  - [Projecting Fields to return from a query](#projecting-fields-to-return-from-a-query)
  - [Aliasing Fields](#aliasing-fields)
	  - [Nested field as a single key](#nested-field-as-a-single-key)

## Getting Up And Running
### Turn On
turn on mongo server, connect to local db
mongod --dbpath /Users/Jake/data/db/

### Open
open mong cli
mongo

### Show DBs
show databases
show dbs

### Select a DB
select a database to use for the duration of the querying
use <db>
use povertystates

### Show collections in db
show collections ins the selected database
show collections
in my example the collection returns ‘states’

### See All Docs in a collection 
select ALL docs in the collection
db.states.find({})
- Corresponds to Select * from states

## Connecting to DB Through CLI
### Local DB
- 
### Remote (Atlas) DB

## Querying
### Specify Equality Conditions
[Query Filters](https://docs.mongodb.com/manual/core/document/#document-query-filter)
[Query Selectors](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors) like $eq, $gt, $gte

#### Show where x = 
db.states.find({state: “Alabama”})
- corresponds to Select * from states where state = “Alabama”

#### Show where x in (a, b)
db.states.find({state: { $in: ["Connecticut", "New York"] }})
- corresponds to Select * from states where state in ("Connecticut", "New York")

#### Show where x in (a, b)
db.states.find({state: { $in: ["Connecticut", "New York"] }})

### Specify And Conditions
[Comparison Operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/#query-selectors-comparison)

#### Show where x = a AND y = b
db.inventory.find( { status: "A", qty: { $lt: 30 } } )
- corresponds to SELECT * FROM inventory WHERE status = "A" AND qty < 30

### Specify Or Conditions
#### Show where x = a AND y = b
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )
- corresponds to SELECT * FROM inventory WHERE status = "A" OR qty < 30

### Specify And as well as Or conditions
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )
- corresponds to SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")

### Specify nested equality
db.inventory.find( { "size.h": { $lt: 15 } } )
- corresponds to Select * from inventory where ... well.... size.h is less than 15


## Projecting Fields to return from a query
https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/
```
A projection can explicitly include several fields by setting the  
<field> to 1 in the projection document. The following operation 
returns all documents that match the query. In the result set, only
the item, status and, by default, the _id fields return in the 
matching documents.
```

### Naming fields
db.inventory.find( { status: "A" }, { item: 1, status: 1 } )
- corresponds to Select _id, item status from inventory where status = "A"
- **NOTE** the _id field returns in the result set by default

### Hiding the _id field
db.collection.find({whereClause: whereValue}, { item: 1, status: 1, _id: 0 })
**NOTE** the ```_id: 0``` is the command to "hide" the _id field from the result set


## Aliasing Fields
### nested field as a single key

db.states.aggregate([{$project: {_id: 0, state: 1, percentBelowPovertyMale: "$percentBelowPoverty.gender.male" }}])