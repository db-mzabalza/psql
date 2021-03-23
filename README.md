

# POSTGRES SQL QUERIES

### JOIN ON SUBQUERIES
```sql
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
```sql
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
```sql
CREATE TABLE article_comp ( like "STORE_PRICE_NOV" including all)
```


### Create table like other table (table, but no content)
```sql
CREATE TABLE mycopy AS
SELECT * FROM mytable;
```
### CREATE TABLE FROM SELECTION OF OTHER
```sql
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
```sql
UPDATE article_comp
SET "Code_Produit" = "Gencod"
WHERE concurrent = 'mrbricolage'
```

### REMOVE .0 FROM A COLUMN
```sql
UPDATE article_comp SET "Code_Produit"=trim(trailing '.0' FROM "Code_Produit"::text)
WHERE concurrent = 'mrbricolage'
```

### SELECT ORDER BY DATE
```sql
select * from  comments
order by created_at desc;
```

### DELETE ORDER BY DATE
```sql
DELETE FROM table_name
WHERE condition;
```

### INSERT VALUES INTO A TABLE FROM A SELECT QUERY
```sql
insert into <tableName1>
select * from <tableName2> where item_id=2;
```

## GROUP BY

### GROUP BY AND COUNT
```sql
SELECT count(sirene) as sirene_count, activiteprincipaleetablissement, trancheeffectifsetablissement  FROM sirene
group by activiteprincipaleetablissement, trancheeffectifsetablissement
```


### DROP DUPLICATES GENERAL
```sql
DELETE from matching_products a using matching_products b
WHERE a = b 
AND a.ctid < b.ctid
```

### DROP DUPLICATES BY COLUMNS
```sql
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
```sql
ALTER TABLE IF EXISTS article_comp
RENAME TO article_comp_old;
```

### CHECK INDEXES
```sql
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
```sql
CREATE INDEX index_id_august ON public."STORE_PRICE_AUGUST" USING btree ("Id Magasin", "Code Produit");
```

### DROP INDEX
```sql
DROP INDEX title_idx;
```

### CAST VARIABLES
```sql
SELECT *
FROM table_a a
LEFT JOIN table_b b
ON column_a::VARCHAR = column_b 
```




