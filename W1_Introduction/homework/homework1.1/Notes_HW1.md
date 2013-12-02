# Homework 1 - Notes

- Install MongoDB
- Restore command (m101)
- Connect with shell
- findOne command

---

	# Inflate the tar
	$ tar xvf hw1.tar
	$ mongorestore [dump_directory]

	# If mongod is not running as a service, start it:
	$ mongod

	# Connect to mongod through a mongo shell:
	$ mongo
	> use m101
	> show collections
	
	# http://docs.mongodb.org/manual/reference/method/db.collection.findOne/
	> db.hw1.findOne()

