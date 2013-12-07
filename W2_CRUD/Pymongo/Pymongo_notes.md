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