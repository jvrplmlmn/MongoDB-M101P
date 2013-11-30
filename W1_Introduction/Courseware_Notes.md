# Week 1: Introduction

## Welcome to M101P

- 7 week class
- Python code

### Logistics & Scoring
- Video Lectures (available on Youtube) ~ 2hs / week = 0%
- Quizzes after each video = 0%
- Homeworks = 50% (Drop Lowest)
- Final Exam = 50%

With a score greater than 65%, you get a 10gen completion certificate.

### Quiz: Welcome to M101P

What counts towards your final grade in the class?
- Quizzes
- **Homeworks**
- **Final Exam**
- Class Participation

## What is MongoDB?

- Non Relational datastore for **JSON** documents.
- **JSON** stands for JavaScript Object Notation
- Key-value storage

Examples:

	{"name": "Andrew"}

	{"a": 4,
	 "b": 5,
	 "c": 7}

JSON documents can have some kind of hierarchy:

	{a: 6,
	 b: 7,
	 fruit: ["apple", "pear", "banana"]}

Relational data is usually a series of tables (columns and rows).

**MongoDB is Schemaless**

Different documents can have different schemas.

### Quiz: What is MongoDB?

Which of the following statements are true about MongoDB?

- **MongoDB is document oriented.**
- MongoDB supports Joins.
- **MongoDB has dynamic schema.**
- MongoDB supports SQL.

## MongoDB Relative to Relational

Scalability & Performance vs Depths of Functionality

- Scalability & Performance = memcached, key-value store
- Depth of Functionality = RDBms (ie. Oracle)

MongoDB doesn't support:
- **Joins**: joins scale poorly.
- **Transactions**.

### Quiz: MongoDB Relative to Relational

Which features did MongoDB omit in order to retain scalability?

- **Joins**
- Indexes
- Secondary Indexes
- **Transactions across multiple collections**

Joins are not particulary horizontally scalable.
Indexes are supported within MongoDB, they're neccesary for good performance, and they allow horizontal scalable.

## Overview of Building an App with MongoDB

- **mongod** process
- **mongo shell**, connects to mongod and allows you to interact with it
- Python: bottle, pymongo

## Quick introduction to the Mongo Shell

	# mongo
	Connecting to: test
	> use test
	switched to db test
	> db.things.save({a:1, b:2, c:3}
	> db.things.find()
	{ "_id": ObjectID("..."), "a": 1, "b": 2, "c": 3 }

### Quiz: Quick introduction to the Mongo Shell

Which of the following expressions are valid JSON documents?

- **{a:1, b:2, c:3}**
- {a,1; b,4, c,6}
- {a:1; b:1; c:4}
- (A,1; b:2; c,4}

## Introduction to JSON

### Quiz: Introduction to JSON

Which of the following are valid JSON documents?

- **{a:1, b:2, c: 3}**
- **{a:1, b:2, c:[1,2,3,4,5]}** The third key has a value within an array.
- **{a:1, b:{}, c: [ { a:1, b:2}, 5, 6]}** The value for the b key is an empty JSON document. The value for the c key is an array with 1 JSON document and 2 values.
- **{ }** Empty JSON document.

## Installing MongoDB (mac)

Download the latest stable version:

	tar xvf mongodb-osx-x86_64-2.4.8.tgz

For development environment:

	sudo $SHELL 
	mkdir -p /data/db
	chmod 777 /data/db
	ls -ld /data/db

Run the `mongod` process and check it's up and running:

	# bin $ ./mongod

Open another terminal and do some testing:

	# bin $
	MongoDB shell version: 2.4.8
	connecting to: test
	Welcome to the MongoDB shell.
	For interactive help, type "help".
	For more comprehensive documentation, see
		http://docs.mongodb.org/
	Questions? Try the support group
		http://groups.google.com/group/mongodb-user
	> db.names.save({'name':'javier'})
	> db.names.find()
	{ "_id" : ObjectId("5299c864071a97a435a8a277"), "name" : "javier" }
	>
## Installing Bottle and Python

`Bottle` is a Python web framework.

Installing:

	pip install bottle

Example code:

	from bottle import route, run, template

	@route('/hello/<name>')
	def index(name='World'):
    	return template('<b>Hello {{name}}</b>!', name=name)

	run(host='localhost', port=8080)

Run it:

	python hello_world.py

Test it:

- Open a browser
- Type: `localhost:8080/hello/foo`

## Installing PyMongo (mac)

- MondoDB installed, running as `mondod` process.
- Application, writted in Python using the bottle framework. Allows to get HTTP requests.

PyMongo is the driver that connects the application and the DB.

Install:

	# Download:
	api.mongodb.org/python/current

	# Pip: 	
	pip install pymongo

## Hello World on a Web Server

![](./BringingItAllTogether.png)

Run:

	# bin $ ./mongod

Open browser:

	localhost:8082

Modify the content in the mongodb:
	
	$ ./mongo
	MongoDB shell version: 2.4.8
	connecting to: test
	> db.names.find()
	{ "_id" : ObjectId("5299c864071a97a435a8a277"), "name" : "javier" }
	> var j = db.names.findOne()
	> j.name = "Dwight"
	Dwight
	> db.names.save(j)
	> var j = db.names.findOne()
	> j
	{ "_id" : ObjectId("5299c864071a97a435a8a277"), "name" : "Dwight" }
	> var j = db.names.findOne()
	> j.name = "Andrew"
	Andrew
	> db.names.save(j)
	> j
	{ "_id" : ObjectId("5299c864071a97a435a8a277"), "name" : "Andrew" }
	>

Refresh the URL and check the changes.

## JSON Revisited

Data structures:

- **Arrays**: lists of things `[...]`
- **Dictionaries**: associated maps `{ keyword:value,}`

### Quiz: JSON Revisited

Write the JSON for a simple document containing a single "fruit" that has as its value an array containing three strings: "apple", "pear", and "peach":

	{"fruit": ["apple", "pear", "peach"]}	

## JSON Subdocuments

### Quiz: JSON Subdocuments

Write a JSON document with a single key, "address" that has as it value another document with the keys “street_address”, “city”, “state”, “zipcode”, with the following values: “street_address” is "23 Elm Drive", “city” is "Palo Alto", “state” is "California", “zipcode” is "94305":

	{"address": {"street_address": "23 Elm Drive",
    	         "city": "Palo Alto",
        	     "state": "California",
            	 "zipcode": "94305"}
	}
