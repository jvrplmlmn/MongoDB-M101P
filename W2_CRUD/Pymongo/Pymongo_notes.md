## Pymongo: find, find_one and Cursors

![](./images/find_findone_cursors.png)

    mongo < create_student_collection.js

### Quiz: Pymongo: find, find_one and Cursors

In the following code snippet:

    import pymongo
    import sys
    
    # establish a connection to the database 
    # note this uses the now deprecated Connection class, as we did in the lecture.
    # MongoClient is the preferred way of connecting.
    connection = pymongo.Connection("mongodb://localhost", safe=True)
    
    # get a handle to the school database
    db=connection.school
    scores = db.scores
         
    try:
            xxxx
            
    except:
            print "Unexpected error:", sys.exc_info()[0]
    
    
    print doc

please enter the one line of python code that would be needed in in place of xxxx to find one document in the collection.

    doc = scores.find_one()
    
## Pymongo: Using field Selection     

Code:

    python using_find_with_selector.py

### Quiz: Pymongo: Using field Selection 

Which of the following could work using Pymongo, depending on variable names, to select out just the student_id from the scores collection using a find command.

- cursor = students.find({'student_id':1, '_id':0})
- cursor = students.find({'student_id':1})
- **cursor = students.find({}, {'student_id':1, '_id':0})**
- cursor = students.find({}, {student_id:1, _id:0})

## Pymongo: Using $gt and $lt

Code:

    find_using_gt_lt.py

### Quiz: Pymongo: Using $gt and $lt

In the following code, what is the correct line of code, marked by xxxx, to search for all quiz scores that are greater than 20 and less than 90.

    import pymongo
    import sys
    
    # establish a connection to the database
    connection = pymongo.Connection("mongodb://localhost", safe=True)
    
    # get a handle to the school database
    db=connection.school
    scores = db.scores
    
    
    def find():
    
        print "find, reporting for duty"
    
        xxxx
    
        try:
            iter = scores.find(query)
    
        except:
            print "Unexpected error:", sys.exc_info()[0]
            
        return iter
    
    find()


- query = {'score':{'$gt':20, '$lt':90}}
- **query = {'type':'quiz', 'score':{'$gt':20, '$lt':90}}**
- query = {'type':'quiz', '$gt':{'score':20}, '$lt':{'score':90}}
- query = {'type':'quiz', 'score':{$gt:20, $lt:90}}

## Importing from Reddit

Code:
    
    python read_reddit.py
    
## Pymongo: Using a regex

Code:

    python using_regex.py

## Pymongo: Using Dot Notation

Code:

    python using_dot_notation.py

### Quiz: Pymongo: Using Dot Notation

In the following code, what do you think will happen if a document that matches the query doesn't have a key called *media.oembed.url*?

    import pymongo
    import sys
    
    # establish a connection to the database
    connection = pymongo.Connection("mongodb://localhost", safe=True)
    
    # get a handle to the reddit database
    db=connection.reddit
    scores = db.stories
    
    
    def find():
    
        print "find, reporting for duty"
    
        query = {'media.oembed.type':'video'}
        projection = {'media.oembed.url':1, '_id':0}
    
        try:
            iter = scores.find(query, projection)
    
        except:
            print "Unexpected error:", sys.exc_info()[0]
    
        sanity = 0
        for doc in iter:
            print doc
            sanity += 1
            if (sanity > 10):
                break
            
    
    find()



- Pymongo will throw an exception.
- **Pymongo will return an empty document.**
- Pymongo will return a document with the following structure {media:{oembed:{url:{}}}}
- Pymongo will return a document with the following structure {media:{oembed:{}}}

## Pymongo: Sort, Skip and Limit

skip(2), limit(3), sort(1)

Code:

    python using_limit_skip_sort.py

### Quiz: Pymongo: Sort, Skip and Limit

Supposed you had the following documents in a collection named things.

    { "_id" : 0, "value" : 10 }
    { "_id" : 2, "value" : 5 }
    { "_id" : 3, "value" : 7 }
    { "_id" : 4, "value" : 20 }

If you performed the following query in pymongo:

    cursor = things.find().skip(3).limit(1).sort('value',pymongo.DESCENDING)

which document would be returned?


- The document with _id=0
- **The document with _id=2**
- The document with _id=3
- The doucment with _id=4

## Pymongo: Inserting

Code:

    insert_quiz.py
    using_insert.py

### Quiz: Pymongo: Inserting

Do you expect the second insert below to succeed?

    # get a handle to the school database
    db=connection.school
    people = db.people
    
    doc = {"name":"Andrew Erlichson", "company":"10gen",
                  "interests":['running', 'cycling', 'photography']}
    
    try:
            people.insert(doc)   # first insert
            del(doc['_id'])
            people.insert(doc)   # second insert
    
    except:
            print "Unexpected error:", sys.exc_info()[0]

- No, because the _id will be a duplicate in the collection.
- No, because the del call will delete the entire record in Python.
- **Yes, because the del call will remove the _id key added by the pymongo driver in the first insert.**
- Yes, because the Pymongo driver always adds a unique _id field on insert.

## Pymongo: Updating

Code:

    using_update.py

### Quiz: Pymongo: Updating

In the following code fragment, what is the python expression in place of xxxx to set a new key "examiner" to be "Jones" Please use the $set operator

    def using_set():
    
        print "updating record using set"
        # get a handle to the school database
        db=connection.school
        scores = db.scores
    
    
        try:
            # get the doc
            score = scores.find_one({'student_id':1, 'type':'homework'})
            print "before: ", score
    
            # update using set
            scores.update({'student_id':1, 'type':'homework'},
                          xxxx)
    
            score = scores.find_one({'student_id':1, 'type':'homework'})
            print "after: ", score
    
        except:
            print "Unexpected error:", sys.exc_info()[0]
            raise
            
Answer:

    {'$set' : {'examiner': 'Jones'}}            
    
## Pymongo: Upserts

Code:

    using_upsert.py
    
### Quiz: Pymongo: Upserts    

Suppose we would like to upsert the following document into the collection *stuff*:

    {_id:"bat", friend:'ball', cousin:'glove'}

Which of the following python statements work. Check all that apply.


- stuff.update({'_id':'bat'}, {'friend':'ball', 'cousin':'glove'}, upsert=True)
- stuff.update({'_id':'bat'}, {'friend':'ball', 'cousin':'glove'}, upsert=False)
- **stuff.update({'_id':'bat'}, {'_id':'bat', 'friend':'ball', 'cousin':'glove'}, upsert=True)**
- **stuff.update({'_id':'bat'}, {'$set': {'friend':'ball', 'cousin':'glove'}}, upsert=True)**

## Pymongo: find_and_modify

Code:

    using_find_and_modify.py