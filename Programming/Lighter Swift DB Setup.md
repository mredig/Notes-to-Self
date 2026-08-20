<!-- permalink: 7975e2b92fc72959872d63fce000943a DO NOT DELETE OR EDIT THIS LINE -->
# Lighter DB Setup

1. create sql file for db/table structure, eg 

	```sql
	CREATE TABLE person (
		id INTEGER PRIMARY KEY NOT NULL,
		name TEXT NOT NULL,
		age INTEGER NOT NULL,
		significant_other TEXT,
	);
	```

	- it should also work to just point to an existing db, i think

2. in a terminal, cd to the lighter checkout (you can drag it from the package dependencies in xcode) and run `swift run sqlite2swift <config-file> <target> <input-files> <output-file>`
3. if needed, add the newly created swift file to your project and use it!
