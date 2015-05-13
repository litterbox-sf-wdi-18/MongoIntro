#The Wonderful World of Mongo

##Learning Objectives

|By the end of this lesson, you should be able to...|
| :--- |
| Compare and contrast a SQL to a noSQL database |
| Create a Schema and Model using mongoose |
| Perform CRUD operations on a single model | 

###Terminology

* RDBMS
* NoSQL
* Schema

##Install Party

### [Homebrew](http://brew.sh/)

One of the tools we're going to need today is called Homebrew. We can use it to quickly install other libraries that we'll need. It is a version control manager for 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

While you wait, indulge in some Homebrew [history](http://en.wikipedia.org/wiki/Homebrew_Computer_Club)

### [MongoDB](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/)

To get started today we are going to want to install a database to store all of our data. To save us time we are going use a database called MongoDB. 


* First take a deep breath and relax. Installing things is tricky, but you'll be fine.
* First we'll need to run brew update to update our brew packages.

  ```bash
  brew update
  ```
* Next we'll neet to run `brew install` for **MongoDB**

  ```bash
  brew install mongodb
  ```

* Next we'll need a directory for **MongoDB** to save data.

  ```bash
  sudo mkdir -p /data/db
  ```

  * Next we'll want to make sure we have permission to read and write to this directory.

  ```bash
  sudo chown -R $USER /data/db
  ```
  
### Concepts

A **RDBMS** is a relational database management system.

**NoSQL** relies on storage of key value pairs; similar to a JavaScript object.

![](http://smartdatacollective.com/sites/smartdatacollective.com/files/RDBMSvsNoSQL.jpeg)
####An analogy of RDBMS vs NoSQL

NoSQL databases store information like you would recipes in a book. When you want to know how to make a cake, you go to that recipe, and all of the information about how to make that cake (ingredients, preparation, mixing, baking, finishing, etc.) are all on that one page.

SQL is like shopping for the ingredients for the recipe. In order to get all of your ingredients into your cart, you have to go to many different aisles to get each ingredient. When you are done shopping, your grocery cart will be full of all the ingredients you had to run around and collect.

Wouldn’t it be nicer if there was a store was organized by recipe, so you could go to one place in the store and grab everything you need from that one spot? Granted you’ll find ingredients like eggs in 50 different places, so there’s a bit of overhead when stocking the shelves, but from a consumer standpoint it was much easier/faster to find what they were looking for.

[mgoffin/Stack Overflow](http://stackoverflow.com/questions/14428069/sql-and-nosql-analogy-for-the-non-technical/14428221#14428221)

###CRUD

We want to get started **creating**, **reading**, **updating**, and **deleting** our own data, CRUD.

### Setup

First let's install `mongoose` in a new project folder.

```javascript
npm init
npm install --save mongoose
```

### Connecting

First make sure mongo is running. In a separate terminal window run.

```bash
mongod
```

Go into you node repl, just type `node` into bash. Let's require `mongoose` and connect to our databse. Mongoose will handle the create on connection.


```javascript

> var mongoose = require("mongoose");

> mongoose.connect("mongodb://localhost/test");

```

### Modeling

Let's create Book model. A Book has a few different characteristics: `title`, `author`,  and `description`.


```javascript

var BookSchema = new mongoose.Schema({
    title: String,
    author: String,
    description: String
});
```

and 

```javascript
var Book = mongoose.model('Book', BookSchema);

```


## Building and Creating

* If you want to **build up** a new Book you can just do the following:

  ```javascript
  var book = new Book({title: "Alice's Adventures In Wonderland"});
  ```

  Then you can play with it.

  ```javascript
  book.author = "Lewis Carroll";
  ```
  
  
  This is called **building** as you're playing with an object that can be saved to the database, but don't exist there yet.

  Once you're done building you can `save` the book.

  ```javascript
  book.save()
  ```


* If you want to build & save in one step you can use `create`.

  ```javascript
  Book.create({title: "The Giver"}, function (err, book) {
    console.log(book);
  });
  ```


##Resources

* [Del](https://github.com/DelmerGA/advanced_js_talk/blob/master/intro_express_part_3.md)
* Download [MongoDB](https://www.mongodb.org/downloads)
* [Extensive Tutorial](http://www.tutorialspoint.com/mongodb/mongodb_overview.htm)
* [Mongo Intro](http://www.mongodb.org/about/introduction/)
* [CRUD Intro](http://docs.mongodb.org/manual/core/crud-introduction/)
* [Mongoose](http://mongoosejs.com/docs/)