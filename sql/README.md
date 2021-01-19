### Select values in the column from one table that are only available in another table
```sql
SELECT "Ncl Niv1", "Concurrent", AVG("Prix Num") AS avg_prix, '01-11-2020' date
FROM "STORE_PRICE_NOV_2"
WHERE "Code Produit" IN (SELECT distinct("Code Produit") FROM "STORE_PRICE_DEC")
GROUP BY "Ncl Niv1", "Concurrent"
```
