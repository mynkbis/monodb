# monodb

MongoDB is a source-available cross-platform document-oriented database which stores data (BSON) in JSON-like documents with dynamic schema. It means you can store your records without worrying about the data structure such as the number of fields or types of fields to store values. Companies and development teams of all sizes use MongoDB because: The document data model is a powerful way to store and retrieve data that allows developers to move fast.

In MongoDB, we cannot establish such a relationship between the unstructured data of the collections. Hence it is considered as a non-relational database. MongoDB works on concept of collection and document. A group of document is refered as collection.
A document is a set of key-value pairs. Documents have dynamic schema means that documents in the same collection do not need to have the same set of fields or structure, and common fields in a collection's documents may hold different types of data.
 
# In UBUNTO 
# Start MongoDB
sudo service mongodb start
# Stop MongoDB
sudo service mongodb stop
# Restart MongoDB
sudo service mongodb restart
# To use MongoDB run the following command.
mongo

# DATA MODElLING

Data in MongoDB has a flexible schema. Documents in the same collection. They do not need to have the same set of fields or structure Common fields in a collection’s documents may hold different types of data.     

# Basic commands 

1. db.help(),  To get a list of commands
2. db.stats(),  This will show the database name, number of collection and documents in the database.
3. show databases, Will show the list of database.
4. use <database_name>, will create database with the given name.
5. db, will show the current database name. Note: Newly created database will not show in the list unless it have least one document into it.
6. Show collections, will show the list of collections.
7. db.dropDatabase(),  use to delete the selected or current database.

# creating collection and Insert sample data

1. db.createCollection("movie"),     This will create the collection named movie.
2. db.<COLLECTION_NAME>.drop(),   This will drop the selected collection.
3. db.movie.insertone({name : "I am number four"}),  This will insert one record to the collection name "movie".
    db.movie.insertmany([
        {name : "I am number four", year: 1995, rating: 18+, genre: "sci-fi", language: "American English"},
        {name : "Teens", year: 2001, rating: 18+, genre: "sci-fi", language: ["American English","Dubbed"]},
        {name : "Stree", year: 2017, rating: 18+, genre: "horror", language: "Hindi"},
        {name : "Chakrachal", year: 2000, rating: 18+, genre: "Documentry", language: "Regional"},
        {name : "Shairat", year: 2017, rating: 18+, genre: "romantic", language: "Hindi"},
        {name : "Pawn Star", year: 1992, rating: 18+, genre: "Fictional", language: ["American English","Dubbed"]}
        ]);
       Here we are entering many records.