# Mongo Commands
https://docs.mongodb.com/manual/tutorial/query-documents/

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

## Specify Equality Conditions
[Query Filters](https://docs.mongodb.com/manual/core/document/#document-query-filter)
[Query Selectors](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors) like $eq, $gt, $gte

### Show where x = 
db.states.find({state: “Alabama”})
- corresponds to Select * from states where state = “Alabama”

### Show where x in (a, b)
db.states.find({state: { $in: ["Connecticut", "New York"] }})
- corresponds to Select * from states where state in ("Connecticut", "New York")

### Show where x in (a, b)
db.states.find({state: { $in: ["Connecticut", "New York"] }})

## Specify And Conditions
[Comparison Operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/#query-selectors-comparison)

### Show where x = a AND y = b
db.inventory.find( { status: "A", qty: { $lt: 30 } } )
- corresponds to SELECT * FROM inventory WHERE status = "A" AND qty < 30

## Specify Or Conditions
### Show where x = a AND y = b
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )
- corresponds to SELECT * FROM inventory WHERE status = "A" OR qty < 30

## Specify And as well as Or conditions
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )
- corresponds to SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")

