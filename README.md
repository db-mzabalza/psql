# psql
basic psql commands

### List Users
```\du```

### List databases
```\l```

### List databases
```\c <databaseName>```

### Lists tables, views and sequences with their associated access privileges.
```\dp```

### Give all the permissions to a user on a DB
```GRANT ALL PRIVILEGES ON DATABASE <dbName> to <userName>;```

### Give all the permissions to a user on a DB
```GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;```


### Grant all privileges on all tables in the schema:
```GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;```