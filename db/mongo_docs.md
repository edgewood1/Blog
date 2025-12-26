# A Guide to MongoDB and Mongoose

This document covers the basics of interacting with MongoDB through the `mongo` shell and using the Mongoose ODM (Object Data Modeling) library in a Node.js environment.

## 1. MongoDB Basics

### 1.1. Core Concepts

-   **Database**: A container for collections.
-   **Collection**: A group of MongoDB documents. Equivalent to a table in a relational database.
-   **Document**: A single record in a collection, stored in BSON format (a binary representation of JSON). Equivalent to a row.
-   **Field**: A key-value pair in a document. Equivalent to a column.

### 1.2. The `mongo` Shell

The `mongo` shell is an interactive JavaScript interface to MongoDB.

**Setup:**
1.  **Start the MongoDB Server**: Run the `mongod` command in your terminal. This starts the database process.
2.  **Open the Shell**: In a **new terminal window**, run the `mongo` command. This connects to the running server.

**Basic Shell Commands:**
-   `show dbs`: List all available databases.
-   `use <databaseName>`: Switch to a specific database. If it doesn't exist, it will be created upon the first data insertion.
-   `db`: Show the current database you are in.
-   `show collections`: List all collections in the current database.

### 1.3. CRUD Operations in the Shell

-   **Create**:
    -   `db.myCollection.insert({ name: "joe", city: "durham" })`: Inserts a new document into `myCollection`.
    -   `db.myCollection.save({ ... })`: Inserts a new document or updates an existing one if an `_id` is provided.

-   **Read**:
    -   `db.myCollection.find()`: Retrieves all documents in the collection.
    -   `db.myCollection.find({ "continent": "Africa" })`: Finds all documents matching the query filter.

-   **Update**:
    -   `db.myCollection.update({ "country": "Morocco" }, { $set: { "capital": "Rabat" } })`: Updates fields on a document matching the query.
    -   `db.myCollection.update({ "country": "Morocco" }, { $push: { "majorcities": "Agadir" } })`: Adds an element to an array field.

-   **Delete**:
    -   `db.myCollection.remove({ "country": "Morocco" })`: Deletes all documents matching the query.
    -   `db.myCollection.update({ "country": "Morocco" }, { $unset: { "capital": "Rabat" } })`: Removes a specific field from a document.
    -   `db.myCollection.update({ "country": "Morocco" }, { $pull: { "majorcities": "Agadir" } })`: Removes an element from an array field.

-   **Sorting**:
    -   Append `.sort({ field: 1 })` for ascending order or `.sort({ field: -1 })` for descending order.
    -   `db.myCollection.find().sort({ _id: 1 })`

## 2. Mongoose ODM for Node.js

Mongoose is a library for Node.js that provides a schema-based solution to model your application data. It includes built-in type casting, validation, query building, and business logic hooks.

### 2.1. Defining a Schema

A Schema maps to a MongoDB collection and defines the shape of the documents within that collection.

```javascript
const mongoose = require('mongoose');
const { Schema } = mongoose;

const userSchema = new Schema({
  username: {
    type: String,
    trim: true,
    required: "Username is Required"
  },
  password: {
    type: String,
    trim: true,
    required: "Password is Required",
    validate: [
      (input) => input.length >= 6,
      "Password should be at least 6 characters long."
    ]
  },
  email: {
    type: String,
    unique: true,
    match: [/.+@.+\..+/, "Please enter a valid e-mail address"]
  },
  notes: [
    {
      type: Schema.Types.ObjectId,
      ref: "Note" // This references the 'Note' model
    }
  ]
});
```

### 2.2. Creating Custom Methods

You can add custom instance methods to your schemas.

```javascript
userSchema.methods.makeCool = function() {
  this.username = `${this.username}...the Coolest!`;
  return this.username;
};
```

### 2.3. Creating a Model

To use your schema definition, you need to convert it into a Model you can work with.

```javascript
const User = mongoose.model("User", userSchema);

module.exports = User;
```

### 2.4. CRUD Operations with Mongoose

In your server file, you can now use the `User` model to perform CRUD operations.

```javascript
const User = require("./userModel.js");
const Note = require("./noteModel.js");

// Connect to MongoDB
mongoose.connect("mongodb://localhost/myAppDB", { useNewUrlParser: true });

// --- Create ---
app.post("/submit", function(req, res) {
  // `req.body` should match the schema structure
  User.create(req.body)
    .then(dbUser => {
      res.json(dbUser);
    })
    .catch(err => {
      res.status(400).json(err);
    });
});

// --- Read ---
app.get("/users", function(req, res) {
  User.find({})
    .then(dbUsers => {
      res.json(dbUsers);
    })
    .catch(err => {
      res.status(400).json(err);
    });
});

// --- Update ---
app.post("/update/:id", function(req, res) {
  User.findOneAndUpdate({ _id: req.params.id }, { $set: { username: req.body.username } }, { new: true })
    .then(dbUser => {
      res.json(dbUser);
    })
    .catch(err => {
      res.status(400).json(err);
    });
});

// --- Delete ---
app.get("/delete/:id", function(req, res) {
  User.remove({ _id: mongojs.ObjectID(req.params.id) }) // Assuming mongojs helper for ID
    .then(result => {
      res.json(result);
    })
    .catch(err => {
      res.status(400).json(err);
    });
});
```

### 2.5. Handling Relationships (`populate`)

Mongoose can populate references to documents in other collections. In our `userSchema`, the `notes` field references the `Note` model.

**Step 1: Create a Note and associate it with a User.**
```javascript
app.post("/articles/:id", function(req, res) {
  // First, create a new note
  Note.create(req.body)
    .then(function(dbNote) {
      // Then, find the User and push the new note's _id into the user's notes array
      // { new: true } returns the updated user
      return User.findOneAndUpdate({ _id: req.params.id }, { $push: { notes: dbNote._id } }, { new: true });
    })
    .then(function(dbUser) {
      res.json(dbUser);
    })
    .catch(function(err) {
      res.json(err);
    });
});
```

**Step 2: Retrieve a User and populate their notes.**
When you find a user, you can use `.populate()` to replace the stored note IDs with the full note documents.
```javascript
app.get("/user-with-notes/:id", function(req, res) {
  User.findOne({ _id: req.params.id })
    // Populate all of the notes associated with the User
    .populate("notes")
    .then(function(dbUser) {
      res.json(dbUser);
    })
    .catch(function(err) {
      res.json(err);
    });
});
```
The resulting `dbUser` object will now contain an array of full `Note` documents instead of just their `_id`s.
