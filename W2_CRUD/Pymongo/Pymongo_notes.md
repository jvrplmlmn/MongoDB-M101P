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