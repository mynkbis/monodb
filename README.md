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
3. db.movie.insertone({name : "I am number four"}),db.movie.insertone({name : "I am number four"}),  This will insert one record to the collection name "movie".
    db.movie.insertMany([
		{
            First_Name: "Radhika",
		    Last_Name: "Sharma",
		    Date_Of_Birth: "1995-09-26",
		    e_mail: "radhika_sharma.123@gmail.com",
		    phone: "9000012345"
		},
		{
			First_Name: "Rachel",
			Last_Name: "Christopher",
			Date_Of_Birth: "1990-02-16",
			e_mail: "Rachel_Christopher.123@gmail.com",
			phone: "9000054321"
		},
		{
			First_Name: "Fathima",
			Last_Name: "Sheik",
			Date_Of_Birth: "1990-02-16",
			e_mail: "Fathima_Sheik.123@gmail.com",
			phone: "9000054321"
		}
	{ item: "journal", qty: 25, status: "A", size: { h: 14, w: 21, uom: "cm" }, tags: [ "blank", "red" ] },
    { item: "notebook", qty: 50, status: "A", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank" ] },
    { item: "paper", qty: 10, status: "D", size: { h: 8.5, w: 11, uom: "in" }, tags: [ "red", "blank", "plain" ] },
    { item: "planner", qty: 3, status: "D", size: { h: 22.85, w: 30, uom: "cm" }, tags: [ "blank", "red" ] },
    { item: "postcard", qty: 45, status: "A", size: { h: 10, w: 15.25, uom: "cm" }, tags: [ "blue" ] }
]); Here we are entering many records.

4. Show only required fields in result
    -> db.movie.find(), will show all the records of the document.
         -> db.movie.find().pretty(),  will show the records in structured way.
            -> db.movie.find({First_Name: "Fathima"}).pretty(),  will show the records of Fathima in structured way.
                 -> db.movie.find({First_Name: "Fathima"},{_id:0, phone: 1}).pretty();  here _id: 0 represent this field not to show, and phone: 1 will show fathima's phone field only. Those field which are present in find method with 0 will not be shown and 1 will show.
    -> db.movie.find({ 'size.uom': "cm" }, { _id: 0, item: 1 }).pretty();   here we are searching inside nested object.
5. Searching inside array
    -> And query
        db.movie.find({ tags: { $all: ["blank", "plain"] } }).pretty();
    -> OR query
        db.movie.find({ tags: { $in: ["plain", "blue"] } }).pretty();
6. Operators
   -> Greater than // $gt
        > db.movie.find({ qty: { $gt: 25 }  }).pretty(),  will show the data which have quantity greater than 25.

   -> Greater than or equal to // $gte
        > db.movie.find({ qty: { $gte: 25 }  }).pretty(),  will show the data which have quantity greater than and equal to 25.

   -> Less than // $lt
        > db.movie.find({ qty: { $lt: 25 }  }).pretty(),  will show the data which have quantity less than 25

   -> Less than or equal to // $lte
       > db.movie.find({ qty: { $lte: 25 }  }).pretty(),  will show the data which have quantity less than and equal to 25

   -> Sort
        > db.movie.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 });   will show only qnty, and item and id is turned off. sort method will arrange the filtered items in acending or decending order as -1 represent the arrangement here - sign is for higher to lower.
        > db.movie.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: 1 });  will sort data from lower to higher order.

   -> Limit
        > db.movie.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 }).limit(3);  it will show the sorted data up to limit of 3 means only 3 records matching the criteria will be shown.
        > db.movie.find({}, { qty: 1, item: 1, _id: 0 }).limit(3);
        > db.movie.find({}, { qty: 1,first_Name: "Fathima", _id: 0 }).pretty().sort({qty:-1}).limit(3);  sorted data will be shown 
        but only 3 records will be displayed.

   -> Skip
        > db.movie.find({}, { qty: 1, item: 1, _id: 0 }).sort({ qty: -1 }).skip(1).limit(1);  this will show the filtered sorted data and skip 1 will leave the first field/record and will show from next record

7. Updating documents
    // update 
    > db.movie.updateOne({ item: "planner" }, { $set: { qty: 100 } });  we have updated the planner's quantity to 100;

    // add a field ( incase field is not the part of document )
    db.movie.updateOne({ item: "planner" }, { $set: { price: 1000 } });  we are inserting a new field i.e price to planner using set method.
        
    // remove a field
    db.movie.updateOne({ item: "planner" }, { $unset: { price: 1 } });  we are removing the price field using unset method. 

8. Updating arrays  

    > db.movie.updateOne({ item: "planner" }, { $push: { tags: "magenta" } });  adding magenta to the field
    > db.movie.updateOne({ item: "planner" }, { $pull: { tags: "blank" } });     removing blank from the field.

    >>>> findOneAndUpdate() method

    db.movie.findOneAndUpdate({First_Name: 'Radhika'},{
         $set: { Age: '30',e_mail: 'radhika_newemail@gmail.com'}}),   this will search the field first_name: "Radhika" and will update the that record which was encountered first while searching and will show the record how it looks now.   

    >>>>> updateMany() method
        db.movie.updateMany(
	{Age:{ $gt: "25" }},
	{ $set: { Age: '00'}}),   this will update all the field matching the search criteria.


9. Deleting documents

    > db.movie.deleteOne({ item: "diary" }); this will delete the entire record of item diary.

10. createIndex() Method

    Indexes support the efficient resolution of queries. Without indexes, MongoDB must scan every document of a collection to select those documents that match the query statement. This scan is highly inefficient and require MongoDB to process a large volume of data.
    
    Indexes are special data structures, that store a small portion of the data set in an easy-to-traverse form. The index stores the value of a specific field or set of fields, ordered by the value of the field as specified in the index.

    >>>>>db.movie.getIndexes();
    > db.movie.find({item: "planner"}).explain("executionStats");
    > db.movie.createIndex({ item: 1 });
    > db.movie.dropIndex({ item: 1});




# UBUNTO commands for mongoose and other.

$ mkdir nodejs-express-mongodb   (created a folder)
$ cd nodejs-express-mongodb  (switched to the folder)
$ npm init (we initialize the Node.js App with a package.json file:)
$ npm install express mongoose cors --save  (We need to install necessary modules: express, mongoose and cors.)

# Setup Express web server

In the root folder, create a new server.js file: and import the modules and parsers,
then run $ node server.js 

# Configure MongoDB database & Mongoose
In the app folder, we will create a separate config folder for configuration with db.config.js file and import the module 
module.exports = {
    url: "mongodb://localhost:27017/Suryad"
  };

  # Define Mongoose
  1. create app/models/index.js with the following code:

  const dbConfig = require("../config/db.config.js");

const mongoose = require("mongoose");
mongoose.Promise = global.Promise;

const db = {};
db.mongoose = mongoose;
db.url = dbConfig.url;
db.tutorials = require("./tutorial.model.js")(mongoose);

module.exports = db;
 
 2. In models folder, create tutorial.model.js file like this
 module.exports = mongoose => {
  const Tutorial = mongoose.model(
    "tutorial",
    mongoose.Schema(
      {
        title: String,
        description: String,
        published: Boolean
      },
      { timestamps: true }
    )
  );

  return Tutorial;
};

This Mongoose Model represents tutorials collection in MongoDB database. These fields will be generated automatically for each Tutorial document: _id, title, description, published, createdAt, updatedAt, __v.
# Create the Controller

Inside app/controllers folder, let’s create tutorial.controller.js with these CRUD functions:

    create
    findAll
    findOne
    update
    delete
    deleteAll
    findAllPublished

const db = require("../models");
const Tutorial = db.tutorials;

// Create and Save a new Tutorial
exports.create = (req, res) => {
  
};

// Retrieve all Tutorials from the database.
exports.findAll = (req, res) => {
  
};

# Define Routes

When a client sends request for an endpoint using HTTP request (GET, POST, PUT, DELETE), we need to determine how the server will reponse by setting up the routes.

These are our routes:

    /api/tutorials: GET, POST, DELETE
    /api/tutorials/:id: GET, PUT, DELETE
    /api/tutorials/published: GET

