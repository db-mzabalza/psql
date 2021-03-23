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
```ALTER USER ttsering with CREATEDB CREATEROLE SUPERUSER;```

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
```sql
SELECT column_name, data_type from information_schema.columns WHERE table_name = 'table_name'
```

### Save query in .csv table
```sql
copy (SELECT * FROM "STORE_PRICE_AUGUST" where "Code Produit" = '1267413') To '/home/mzabalza/test.csv' CSV DELIMITER ',' HEADER
```
# psql system
basic psql commands

### Restart postgres service
```
sudo systemctl restart postgresql.service
```

### Conf file path
```
/etc/postgresql/11/main/postgresql.conf
```

### Disk space used by database
```
SELECT pg_database_size('dbname')
```

### save database
```
pg_dump <db_name> > <output_file>
```
```
sudo su - postgres
pg_dump db_name > db_name.bak
```
and find backup in /var/lib/postgresql

## Save dump table
```
pg_dump  --table="public.\"STORE_PRICE_JUNE\"" kf_pricing > store_price_june.dump
```

## Load dumped table
```
psql -U mzabalza -p 5432 -h localhost -d test < my_dump_2.sql
```

### SHOW ACTIVE CONNECTIONS AND CURRENT ACTIVITY ON DATABASE
```
select *
from pg_stat_activity
where datname = 'mydatabasename';
```
