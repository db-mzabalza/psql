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

### Create User
```CREATE USER melkhalil with PASSWORD '<passwordName>';```

### Altering existing users permissions
```ALTER USER melkhalil with CREATEDB, CREATEROLE, CREATEUSER, SUPERUSER ;```

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

### Restart postgres
```
sudo systemctl restart postgresql.service
```

### Check logs
```
tail -f postgresql-11-main.log
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

### Create table like other table (table, but no content)
```CREATE TABLE article_comp ( like "STORE_PRICE_NOV" including all)```


### Create table like other table (table, but no content)
```
CREATE TABLE mycopy AS
SELECT * FROM mytable;
```
### CREATE TABLE FROM SELECTION OF OTHER
```
CREATE TABLE article_comp_jan AS
SELECT 
"Id Magasin" as "Id_Magasin",
"Enseigne",
"Code Produit" as "Code_Produit",
"Prix Num" as "Prix_Num",
"Remise",
"Gencod",
"Marque",
"Concurrent" as "concurrent"
from "STORE_PRICE_DEC"
```

### Copy values from one column to another
```
UPDATE article_comp
SET "Code_Produit" = "Gencod"
WHERE concurrent = 'mrbricolage'
```

### REMOVE .0 FROM A COLUMN
```
UPDATE article_comp SET "Code_Produit"=trim(trailing '.0' FROM "Code_Produit"::text)
WHERE concurrent = 'mrbricolage'
```

### SELECT ORDER BY DATE
```
select * from  comments
order by created_at desc;
```

### DELETE ORDER BY DATE
```
DELETE FROM table_name
WHERE condition;
```

### INSERT VALUES INTO A TABLE FROM A SELECT QUERY
```
insert into <tableName1>
select * from <tableName2> where item_id=2;
```

### GROUP BY AND COUNT
```
SELECT count(sirene) as sirene_count, activiteprincipaleetablissement, trancheeffectifsetablissement  FROM sirene
group by activiteprincipaleetablissement, trancheeffectifsetablissement
```


### DROP DUPLICATES GENERAL
```
DELETE from matching_products a using matching_products b
WHERE a = b 
AND a.ctid < b.ctid
```

### DROP DUPLICATES BY COLUMNS
```
DELETE from matching_products a using matching_products b
WHERE a.ctid < b.ctid
AND  a.material_code = b.material_code
AND  a.kff_article = b.kff_article
AND  a.concurrent = b.concurrent
AND  a.conc_product_label = b.conc_product_label
AND  a.conc_product_price = b.conc_product_price
AND  a.conc_product_url = b.conc_product_url
AND  a.conc_product_img = b.conc_product_img;
```
### ALTER TABLE NAME
```
ALTER TABLE IF EXISTS article_comp
RENAME TO article_comp_old;
```

### CHECK INDEXES
```
SELECT
    tablename,
    indexname,
    indexdef
FROM
    pg_indexes
WHERE
    schemaname = 'public'
ORDER BY
    tablename,
    indexname;
```

### CREATE INDEX
```
CREATE INDEX index_id_august ON public."STORE_PRICE_AUGUST" USING btree ("Id Magasin", "Code Produit");
```
