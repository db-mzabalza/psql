
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
