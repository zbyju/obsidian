Inspired by JavaScript and uses JavaScript-like objects and dot notation. MongoDB stores data in BSON (= Binary JSON), user sees JSON-like data.

# Main Features
## Collection interaction
MongoDB offers many methods to interact with collections, in which it stores data:
- find
- findOne
- insertOne
- insertMany
- updateOne
- updateMany
- replaceOne
- deleteOne
- deleteMany
- aggregate
- count
- mapReduce
- ...

## Find
`db.collection.find(selection, projection)`
`find` is the equivalent to `SELECT` in SQL. It first takes an argument - an object specifying how it should filter data and second argument specifying which fields to return.

## Aggregation pipelines
MongoDB of