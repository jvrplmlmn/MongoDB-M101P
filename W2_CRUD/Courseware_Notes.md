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

## Queries with Dot Notation

The purpouse of dot notation is to allow you to reach inside nested documents looking for a specific embedded piece of information without any knowledge of any surrounding context.

    > db.users.insert({ name : "richard", email : { work : "richard@10gen.com", personal : "kreuter@example.com" } } );
    > db.users.findOne()
    {
    	"_id" : ObjectId("529f88a1865b4afb26b0ca96"),
    	"name" : "richard",
    	"email" : {
    		"work" : "richard@10gen.com",
    		"personal" : "kreuter@example.com"
    	}
    }
    > db.users.find( { email : { work : "richard@10gen.com", personal : "kreuter@example.com"  } } );
    { "_id" : ObjectId("529f88a1865b4afb26b0ca96"), "name" : "richard", "email" : { "work" : "richard@10gen.com", "personal" : "kreuter@example.com" } }
    > db.users.find( { email: { work : "richard@10gen.com" } } );
    > db.users.find( { "email.work" : "richard@10gen.com" } );
    { "_id" : ObjectId("529f88a1865b4afb26b0ca96"), "name" : "richard", "email" : { "work" : "richard@10gen.com", "personal" : "kreuter@example.com" } }
    >
        
### Quiz: Queries with Dot Notation

Suppose a simple e-commerce product *catalog* called catalog with documents that look like this:

    { product : "Super Duper-o-phonic", 
      price : 100000000000,
      reviews : [ { user : "fred", comment : "Great!" , rating : 5 },
                  { user : "tom" , comment : "I agree with Fred, somewhat!" , rating : 4 } ],
      ... }
  
Write a query that finds all products that cost more than 10,000 and that have a rating of 5 or better.

    db.catalog.find( { price : { $gt : 10000 }, "reviews.rating" : { $gte : 5} } )
    
## Querying, Cursors

**[cursor](http://docs.mongodb.org/manual/reference/glossary/#term-cursor)**

> A pointer to the result set of a query. Clients can iterate through a cursor to retrieve results. By default, cursors timeout after 10 minutes of inactivity.

In the `mongo` shell, the primary method for the read operation is the `db.collection.find()` method. This method queries a collection and returns a cursor to the returning documents.

To access the documents, you need to iterate the cursor. However, in the `mongo` shell, if the returned cursor is not assigned to a variable using the var keyword, then the cursor is automatically iterated up to 20 times to print up to the first 20 documents in the results.



#### Cursor methods

`cursor.sort()` Returns results ordered according to a sort specification.

`cursor.limit()` Constrains the size of a cursor’s result set.

`cursor.skip()` Returns a cursor that begins returning results only after passing or skipping a number of documents.

#### Examples:


    cur.sort ( { name : -1 } ); null;

    cur.sort ( { name : -1 } ).limit(3); null;
    
    while (cur.hasNext()) printjson(cur.next());
   
    cur.sort ( { name : -1 } ).limit(3).skip(2); null;
     
    
### Quiz: Querying, Cursors    

Recall the documents in the scores collection:

    {
    	"_id" : ObjectId("50844162cb4cf4564b4694f8"),
    	"student" : 0,
    	"type" : "exam",
    	"score" : 75
    }

Write a query that retrieves exam documents, sorted by score in descending order, skipping the first 50 and showing only the next 20.

    db.scores.find({type: "exam"}).sort({score: -1}).skip(50).limit(20)
    
## Counting Results

    db.scores.find({type: "exam"})

    db.scores.count({type: "exam"})

### Quiz: Counting Results

How would you count the documents in the scores collection where the type was "essay" and the score was greater than 90?

    db.scores.count({type: "essay", score: {$gt: 90}})
    
## Wholesale Updating of a Document    

#### Definition

`db.collection.update(query, update, options)`

Modifies an existing document or documents in a collection. By default, the `update()` method updates a **single** document. If the multi option is set to true, the method updates all documents that match the query criteria.



    db.collection.update(
                          <query>,
                          <update>,
                          {
                            upsert: <Boolean>,
                            multi: <Boolean>,
                          }
                        )
---

    db.people.update( { name: "Smith" }, { name: "Thompson", salary: 50000 } );

### Quiz: Wholesale Updating of a Document

Let's say you had a collection with the following document in it:

    { "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }

and you issued the query:

    db.foo.update({_id:"Texas"},{population:30000000})

What would be the state of the collection after the update?

- { "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }
- { "_id" : "Texas", "population" : 3000000, "land_locked" : 1 }
- **{ "_id" : "Texas", "population" : 30000000 }**
- { "_id" : ObjectId("507b7c601eb13126c9e3dcca"), "population" : 2500000 }

## Using the $set Command

**[$set operator](http://docs.mongodb.org/manual/reference/operator/update/set/#up._S_set)**

**Syntax:** `{ $set: { <field1>: <value1>, ... } }`

Use the `$set` operator to replace the value of a field to the specified value. If the field does not exist, the $set operator will add the field with the specified value.

**[$inc operator](http://docs.mongodb.org/manual/reference/operator/update/inc/)**

The `$inc` operator increments a value of a field by a specified amount. If the field does not exist, `$inc` adds the field and sets the field to the specified amount. `$inc` accepts positive and negative incremental amounts. Consider the following syntax:

    { $inc: { <field1>: <amount1>, ... } }

### Quiz: Using the $set Command

For the *users* collection, the documents are of the form

    {
    	"_id" : "myrnarackham",
    	"phone" : "301-512-7434",
    	"country" : "US"
    }

Please set myrnarackham's country code to "RU" but leave the rest of the document (and the rest of the collection) unchanged. 

Hint: You should not need to pass the "phone" field to the update query.

    
    db.users.update({_id: "myrnarackham"}, {$set: {country: "RU"}})
    
    
## Using the $unset Command

### Quiz: Using the $unset Command    

Write an update query that will remove the "interests" field in the following document in the *users* collection.

    { 
        "_id" : "jimmy" , 
        "favorite_color" : "blue" , 
        "interests" : [ "debating" , "politics" ] 
    }

Do not simply empty the array. Remove the key : value pair from the document.

    db.users.update({_id: "jimmy"}, {$unset: {interests: 1}})
    
## Using $push, $pop, $pull, $pushAll, $pullAll, $addToSet    

    > db.arrays.insert( { _id: 0, a : [ 1, 2, 3, 4 ] } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 1, 2, 3, 4 ] }
    > db.arrays.update( { _id : 0 }, { $set : { "a.2" : 5 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 1, 2, 5, 4 ] }
    > db.arrays.update( { _id : 0 }, { $push : { a : 6 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 1, 2, 5, 4, 6 ] }
    > db.arrays.update( { _id : 0 }, { $pop : { a : 1 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 1, 2, 5, 4 ] }
    > db.arrays.update( { _id : 0 }, { $pop : { a : -1 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 2, 5, 4 ] }
    > db.arrays.update( { _id : 0 }, { $pushAll : { a : [ 7, 8, 9 ] } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 2, 5, 4, 7, 8, 9 ] }
    > db.arrays.update( { _id : 0 }, { $pull: { a : 5 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 2, 4, 7, 8, 9 ] }
    > db.arrays.update( { _id : 0 }, { $pullAll: { a : [ 2, 4, 8 ] } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 7, 9 ] }
    > db.arrays.update( { _id : 0 }, { $addToSet : { a : 5 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 7, 9, 5 ] }
    > db.arrays.update( { _id : 0 }, { $addToSet : { a : 5 } } );
    > db.arrays.update( { _id : 0 }, { $addToSet : { a : 5 } } );
    > db.arrays.findOne()
    { "_id" : 0, "a" : [ 7, 9, 5 ] }
    >

### Quiz: Using $push, $pop, $pull, $pushAll, $pullAll, $addToSet

Suppose you have the following document in your friends collection:

    { _id : "Mike", interests : [ "chess", "botany" ] }

What will the result of the following updates be?

    db.friends.update( { _id : "Mike" }, { $push : { interests : "skydiving" } } );
    db.friends.update( { _id : "Mike" }, { $pop : { interests : -1 } } );
    db.friends.update( { _id : "Mike" }, { $addToSet : { interests : "skydiving" } } );
    db.friends.update( { _id : "Mike" }, { $pushAll: { interests : [ "skydiving" , "skiing" ] } } );
    
Answer:

    { _id : "Mike", "interests" : [ "botany", "skydiving", "skydiving", "skiing" ] }    
    
## Upserts

    db.people.update( { name : "George" }, { $set : {age : 40 } }, { upsert : true } )
    
### Quiz: Upserts    

After performing the following update on an empty collection

    db.foo.update({username:'bar'}, {'$set':{'interests':['cat', 'dog']}}, {upsert: true} );

What could be the state of the collection.

- { "_id" : ObjectId("507b78232e8dfde94c149949"), "interests" : [ "cat", "dog" ]}
- {"interests" : [ "cat", "dog" ], "username" : "bar" }
- {}
- **{ "_id" : ObjectId("507b78232e8dfde94c149949"), "interests" : [ "cat", "dog" ], "username" : "bar" }**

## Multi-update

    db.people.update( {}, { $set : { title : "Dr" } }, { multi : true } )

### Quiz: Multi-update

Recall the schema of the *scores* collection:

    {
    	"_id" : ObjectId("50844162cb4cf4564b4694f8"),
    	"student" : 0,
    	"type" : "exam",
    	"score" : 75
    }


Give every document with a *score* less than 70 an extra 20 points. 

If you input an incorrect query, don't forget to reset the problem state, as any wrong *update* will likely take you away from your initial state. 

    db.scores.update({score: {$lt: 70}}, { $inc : { score : 20 } }, {multi: true})
    
## Removing Data

    db.people.remove()
    db.people.remove({ name : { $gt : "M" }})
    db.people.drop()

### Quiz: Removing Data

Recall the schema of the *scores* collection:

    {
    	"_id" : ObjectId("50844162cb4cf4564b4694f8"),
    	"student" : 0,
    	"type" : "exam",
    	"score" : 75
    }

Delete every document with a score of less than 60.

    db.scores.remove({score : {$lt: 60}})
    
## getLastError

    > db.people.insert( { _id : "Smith", age : 30 } );
    > db.people.insert( { _id : "Smith", age : 30 } );
    E11000 duplicate key error index: test.people.$_id_  dup key: { : "Smith" }
    > db.runCommand( { getLastError : 1 } )
    {
    	"err" : "E11000 duplicate key error index: test.people.$_id_  dup key: { : \"Smith\" }",
    	"code" : 11000,
    	"n" : 0,
    	"connectionId" : 2,
    	"ok" : 1
    }
    > db.people.insert( { _id : "Jones", age : 30 } );
    > db.runCommand( { getLastError : 1 } )
    { "n" : 0, "connectionId" : 2, "err" : null, "ok" : 1 }
    >
    
    