# Tap postgres to CSV


1. Do schema discovery automatically
```
    tap-postgres -c ta-pg.json -d > catalog.json
```

2. update catalog.sjon

    add `selected`, `replication-method` into catalog.json
    
    ```
    "selected": true,
    "replication-method": "FULL_TABLE",
    ```

3. create `csv.json` for target

4. run command, postgres to CSV

Be careful `tap-postgres --catalog` not work, use `tap-postgres --properties` instead
```
    tap-postgres -c conf.json --properties catalog.json |target-csv -c csv.json > state.json 
```

5. run command, postgres to postgress
```
tap-postgres -c conf.json --properties catalog.json | target-postgres -c target-pg.json 
```