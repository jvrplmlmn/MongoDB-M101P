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

