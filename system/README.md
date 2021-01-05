
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
