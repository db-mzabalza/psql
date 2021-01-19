### Select values in the column from one table that are only available in another table
```sql
SELECT "Ncl Niv1", "Concurrent", AVG("Prix Num") AS avg_prix, '01-11-2020' date
FROM "STORE_PRICE_NOV_2"
WHERE "Code Produit" IN (SELECT distinct("Code Produit") FROM "STORE_PRICE_DEC")
GROUP BY "Ncl Niv1", "Concurrent"
```

### Concat 3 columns
```sql
SELECT concat_ws('_', "Concurrent", "Code Produit", "Id Magasin")
FROM "STORE_PRICE_NOV_2"
```
### Manually pivot table (columns to rows)
```sql
SELECT "Concurrent", "Id Magasin", "Code Produit", avg("Prix November") AS avg_prix, '01-11-2020' date, 'common' perimeter
FROM "store_price_nov_dec"
GROUP BY "Concurrent", "Id Magasin", "Code Produit"
UNION ALL
SELECT "Concurrent", "Id Magasin", "Code Produit", avg("Prix December") AS avg_prix, '01-12-2020' date, 'common' perimeter
FROM "store_price_nov_dec"
GROUP BY "Concurrent", "Id Magasin", "Code Produit"
```
