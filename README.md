# psql
basic psql commands

### List Users
```\du```

### List databases
```\l```

### Go to database
```\c <databaseName>```

### Lists tables, views and sequences with their associated access privileges.
```\dp```

### Give all the permissions to a user on a DB
```GRANT ALL PRIVILEGES ON DATABASE <dbName> to <userName>;```

### Give all the permissions to a user on a DB
```GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;```


### Grant all privileges on all tables in the schema:
```GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;```

### Grant access to tables which will be created in future
```
alter default privileges in schema public grant all on tables to oleroy;
```

### Show columns in table:
```SELECT * from information_schema.columns WHERE table_name = '<table_name>'```

### Save query in .csv table
```copy (SELECT * FROM "STORE_PRICE_AUGUST" where "Code Produit" = '1267413') To '/home/mzabalza/test.csv' CSV DELIMITER ',' HEADER```

# POSTGRES SQL QUERIES

### JOIN ON SUBQUERIES
```
SELECT *
FROM (
	SELECT * FROM orange_ruralite
	WHERE "Zoning_Simple" = 'RIP'
	
) orange
RIGHT JOIN (
	SELECT siret, codecommuneetablissement FROM sirene
	WHERE sirene.codecommuneetablissement in (
		SELECT distinct(depcom) from city
		WHERE region_name = 'Bretagne'
	)
) sirene
	
ON orange."INSEE_COM" = sirene."codecommuneetablissement"
```
```
SELECT * FROM sirene
WHERE sirene.codecommuneetablissement in (
	SELECT distinct(depcom) from city
	WHERE region_name = 'Bretagne'
)
AND codecommuneetablissement in (
	SELECT distinct("INSEE_COM") from orange_ruralite
	WHERE "Zoning_Simple" = 'RIP'
)
```

### Create table like other table
```CREATE TABLE article_comp ( like "STORE_PRICE_NOV" including all)```

### Copy values from one column to another
```
UPDATE article_comp
SET "Code_Produit" = "Gencod"
WHERE concurrent = 'mrbricolage'
```
