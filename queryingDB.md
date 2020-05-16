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

### Show where x = 
db.states.find({state: “Alabama”})
- corresponds to Select * from states where state = “Alabama”

### Show where x in (a, b)
db.states.find({state: { $in: ["Connecticut", "New York"] }})

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()

show 1 row from a specified collection
db.states.findOne()
