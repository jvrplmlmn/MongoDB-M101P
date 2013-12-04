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