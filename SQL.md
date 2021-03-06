
## 1. USING

The USING clause specifies which columns to test for equality when two tables are joined. 
It can be used instead of an ON clause in the JOIN operations that have an explicit join clause.

**Example**:
<br><br>
The following query performs an inner join between the COUNTRIES table and the CITIES table on the condition that COUNTRIES.COUNTRY is equal to CITIES.COUNTRY:

```SELECT * FROM COUNTRIES JOIN CITIES USING (COUNTRY)```

The next query is similar to the one above, but it has the additional join condition that COUNTRIES.COUNTRY_ISO_CODE is equal to CITIES.COUNTRY_ISO_CODE:
<br><br>
```SELECT * FROM COUNTRIES JOIN CITIES USING (COUNTRY, COUNTRY_ISO_CODE)```


### Run migration through psql
```psql -h localhost -p 5432 db_name -U user_name -f ./dump.sql```

### Run dump through psql
```pg_restore -U postgres -h localhost -p 5432 -d db_name -1 dump-2021101315```
