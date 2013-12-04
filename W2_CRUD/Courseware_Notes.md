# Week 2: CRUD

## CRUD an the Mongo Shell

- **Create** ***Insert*** Insert
- **Read** ***Find*** Selecet
- **Update** ***Update*** Update
- **Delete** ***Remove*** Delete

MongoDB's CRUD operations exist as methods/functions in programming language APIs, not as a separate language.

This week we'll learn the CRUD APIs in the *mongo* shell, and their analogs in *pymongo*.

### Quiz: CRUD and the Mongo Shell

> By the end of this week, you'll know which of the following?

- **MongoDB's basic document creation, retrieval, modification, and removal operations**
- **Some features of the MongoDB shell, mongo**
- How to measure performance of MongoDB operations
- **How to manipulate MongoDB documents from Python**
- How to analyze data in MongoDB collections

## Secrets of the Mongo Shell

When you connect with the mongo shell to a mongoDB, you get a banner showing the MongoDB shell version and information about the database you're connnected to:

    $ mongo
    MongoDB shell version: 2.2.0
    Connecting to: test
    > 

The mongo shell is a JavaScript interpreter.

Online help:

    > help

Autocompletion:

    pri[tab]
    |
    |
    v
    print
    

JavaScript notes:

    > x = 1
    1
    > x
    1
    > y = "abc"
    abc
    > z = { a : 1 }
    { "a" : 1 }
    > z.a
    1
    > z["a"]
    1
    > z.a
    1
    > w="a"
    a
    > z[w]
    1
    

### Quiz: Secrets of the Mongo Shell

What does the following fragment of JavaScript output?

    x = { "a" : 1 };
    y = "a";
    x[y]++;
    print(x.a);
    
Answer:

**2**

## BSON Introduced

    > obj = { "a" : 1 , "b" : "hello" , "c" = [ "apples" , "tomatoes" ] }
    { "a" : 1 , "b" : "hello" , "c" = [ "apples" , "tomatoes" ] }
    > 
    
### Specification of BSON

Read more at [bsonspec.org](bsonspec.org).

BSON [bee · sahn], short for Bin­ary JSON, is a bin­ary-en­coded seri­al­iz­a­tion of JSON-like doc­u­ments. Like JSON, BSON sup­ports the em­bed­ding of doc­u­ments and ar­rays with­in oth­er doc­u­ments and ar­rays. BSON also con­tains ex­ten­sions that al­low rep­res­ent­a­tion of data types that are not part of the JSON spec. For ex­ample, BSON has a Date type and a BinData type.

BSON can be com­pared to bin­ary inter­change for­mats, like Proto­col Buf­fers. BSON is more "schema-less" than Proto­col Buf­fers, which can give it an ad­vant­age in flex­ib­il­ity but also a slight dis­ad­vant­age in space ef­fi­ciency (BSON has over­head for field names with­in the seri­al­ized data).

BSON was de­signed to have the fol­low­ing three char­ac­ter­ist­ics:

1. **Lightweight**: Keep­ing spa­tial over­head to a min­im­um is im­port­ant for any data rep­res­ent­a­tion format, es­pe­cially when used over the net­work.
2. **Traversable**:
BSON is de­signed to be tra­versed eas­ily. This is a vi­tal prop­erty in its role as the primary data rep­res­ent­a­tion for Mon­goDB.
3. **Efficient**: En­cod­ing data to BSON and de­cod­ing from BSON can be per­formed very quickly in most lan­guages due to the use of C data types.

---

    > new Date()
    ISODate("2013-12-04T19:05

### Quiz: BSON Introduced

Which of the following are types available in BSON?

- **Strings**
- **Floating-point numbers**
- Complex numbers
- **Arrays**
- **Objects**
- **Timestamps**

## Inserting Docs

    $ mongo
    MongoDB shell version: 2.4.8
    connecting to: test
    > doc = { "name" : "Smith", "age" : 30, "profession" : "hacker" }
    { "name" : "Smith", "age" : 30, "profession" : "hacker" }
    > db
    test
    > db.people.insert(doc)
    > db.people.find()
    { "_id" : ObjectId("529f6fe10562bbaa3a82da00"), "name" : "Smith", "age" : 30, "profession" : "hacker" }
    > db.people.insert ( { "name" : "Jones", "age" : 35, "profession" : "baker" } )
    > db.people.find()
    { "_id" : ObjectId("529f6fe10562bbaa3a82da00"), "name" : "Smith", "age" : 30, "profession" : "hacker" }
    { "_id" : ObjectId("529f70732213bcdc3f293aac"), "name" : "Jones", "age" : 35, "profession" : "baker" }
    >
      
**ObjectID** is an unique identifier.
 
i.e.: `db.people.insert` *insert* is a method in the **people** *collection* of the current *db*. 

**db** handler of the connection to the db
 
### Quiz: Inserting Docs

> Insert a document into the fruit collection with the attributes of "name" being "apple", "color" being "red", and "shape" being "round". Use the "insert" method.

    > db.fruit.insert({"name" : "apple", "color" : "red", "shape" : "round"})
    > db.fruit.find()
    {
        "_id" : ObjectId("529f7151132c1f614deafd3c"),
        "color" : "red",
        "shape" : "round",
        "name" : "apple"
    }
    
## Introduction to findOne

**[db.collection.findOne(\<criteria>, \<projection>)](http://docs.mongodb.org/manual/reference/method/db.collection.findOne/)**

- criteria ~ where in sql
- projection ~ select in sql

    > db.people.findOne()
    {
    	"_id" : ObjectId("529f6fe10562bbaa3a82da00"),
    	"name" : "Smith",
    	"age" : 30,
    	"profession" : "hacker"
    }
    > db.people.findOne({ "name" : "Jones" })
    {
    	"_id" : ObjectId("529f70732213bcdc3f293aac"),
    	"name" : "Jones",
    	"age" : 35,
    	"profession" : "baker"
    }
    > db.people.findOne({ "name" : "Jones" }, { "name" : true, "_id" : false })
    { "name" : "Jones" }
    > db.people.findOne({ "name" : "Jones" }, { "name" : true })
    { "_id" : ObjectId("529f70732213bcdc3f293aac"), "name" : "Jones" }
    >


### Quiz: Introduction to findOne

Use findOne on the collection users to find one document where the key username is "dwight", and retrieve only the key named email.

     > db.users.findOne({ "username": "dwight" }, { "email": true, "_id": false })
     
## Introduction to find

**[db.colleection.find(\<criteria>, \<projection>)](http://docs.mongodb.org/manual/reference/method/db.collection.find/)**

## Querying Using field selection

### Quiz: Querying Using field selection

Supposing a scores collection similar to the one presented, how would you find all documents with an essay score equal to 50 and only retrieve the *student* field?

    > db.scores.find({"type": "essay", "score": 50}, { "student": true, "_id": false})
    
## Querying Using $gt and $lt

- **$gt**
- **$gte**
- **$lt**
- **$lte**

### Quiz: Querying Using $gt and $lt

Which of these finds documents with a score between 50 and 60, inclusive?

- db.scores.find({ score : { $gt : 50 , $lt : 60 } } );
- **db.scores.find({ score : { $gte : 50 , $lte : 60 } } );**
- db.scores.find({ score : { $gt : 50 , $lte : 60 } } );
- db.scores.find({ score : { $gte : 50 , $lt : 60 } } );
- db.scores.find({ score : { $gt : 50 } } );

## Inequalities on Strings

### Quiz: Inequalities on Strings

Which of the following will find all users with name between "F" and "Q"?

- **db.users.find( { name : { $gte : "F" , $lte : "Q" } } );**
- **db.users.find( { name : { $lte : "Q" , $gte : "F" } } );**
- db.users.find( { name : { $gte : "f" , $lte : "Q" } } );
- db.users.find( { name : { $lte : "Q" } });

## Using regexes, $exists, $type

`$exists`

    db.people.find({ profession: { $exists: false } } );
    db.people.find({ profession: { $exists: false}});

`$type`

    db.people.find({ name: { $type: 2 }});

`$regex`

Names that contains "a"
    
    db.people.find({name: { $regex: "a" }});

Names that ends with an "e" (ends with a `$`):

    db.people.find({name: { $regex: "e$" }});

Names that start with an "A" (use the carrot: `^`)
db.people.find({name: { $regex: "^A" }});


### Quiz: Using regexes, $exists, $type

Write a query that retrieves documents from a *users* collection where the name has a "q" in it, and the document has an *email* field.

    db.users.find({ "name": { $regex: "q" }, "email": { $exists: true }})
    
## Using $or

The `$or` operator is a prefix operator.

### Quiz: Using $or

How would you find all documents in the scores collection where the score is less than 50 or greater than 90?

    db.scores.find( { $or : [ { score: { $lt: 50 } }, { score: { $gt: 90 } } ] })
    
## Using $and

    db.people.find( { $and : [ { name : { $gt : "C" } }, { name : { $regex : "a" } } ] } )

is equivalent to

    db.people.find( { name : { $gt : "C", $regex : "a" } } )
    
### Quiz: Using $and

What will the following query do?

    db.scores.find( { score : { $gt : 50 }, score : { $lt : 60 } } );


- Find all documents with score between 50 and 60
- Find all documents with score greater than 50
- **Find all documents with score less than 60**
- Explode like the Death Star
- None of the above

> Note: The second ocurrence of score replaces the first one.

## Querying Inside Arrays

### Quiz: Querying Inside Arrays

Which of the following documents would be returned by this query?

    db.products.find( { tags : "shiny" } );

- **{ _id : 42 , name : "Whizzy Wiz-o-matic", tags : [ "awesome", "shiny" , "green" ] }**
- { _id : 704 , name : "Fooey Foo-o-tron", tags : [ "blue", "mediocre" ] }
- **{ _id : 1040 , name : "Snappy Snap-o-lux", tags : "shiny" }**
- { _id : 12345 , name : "Quuxinator", tags : [ ] }

## Using $in and $all

`$all` example:

    db.accounts.find ( { favorites : { $all : [ "pretzels", "beer" ] } } )

`$in` example:

    db.accounts.find ( { name : { $in : [ "Howard", "John" ] } } )
    
### Quiz: Using $in and $all

Which of the following documents matches this query?

    db.users.find( { friends : { $all : [ "Joe" , "Bob" ] }, favorites : { $in : [ "running" , "pickles" ] } } )

- { name : "William" , friends : [ "Bob" , "Fred" ] , favorites : [ "hamburgers", "running" ] }
- { name : "Stephen" , friends : [ "Joe" , "Pete" ] , favorites : [ "pickles", "swimming" ] }
- **{ name : "Cliff" , friends : [ "Pete" , "Joe" , "Tom" , "Bob" ] , favorites : [ "pickles", "cycling" ] }**
- { name : "Harry" , friends : [ "Joe" , "Bob" ] , favorites : [ "hot dogs", "swimming" ] }

