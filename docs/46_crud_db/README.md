# CRUD interactions with a database

**CRUD** is the acronym for **CREATE, READ, UPDATE and DELETE**. These terms describe the four essential operations for creating and managing persistent data elements in relational databases.

## Create

The CREATE operation **adds a new record** to a database. In RDBMS, a database table row is referred to as a record, while columns are called attributes or fields. The CREATE operation adds one or more new records with distinct field values in a table.

Example SQL statement:
```sql
INSERT INTO <table name> VALUES (field value 1, field value, 2…)
```

## Read

READ returns records from a database table based on some search criteria. The READ operation can return all records and some or all fields.

Example SQL statement:
```sql
SELECT field 1, field 2, …FROM <table name> [WHERE <condition>]
```

## Update

UPDATE is used to modify existing records in the database. For example, this can be the change of address in a customer database or price change in a product database. Similar to READ, UPDATEs can be applied across all records or only a few, based on criteria.

An UPDATE operation can modify and persist changes to a single field or to multiple fields of the record. If multiple fields are to be updated, the database system ensures they are all updated or not at all. 

Example SQL statement:
```sql
UPDATE <table name> SET field1=value1, field2=value2,… [WHERE <condition>]
```

## Delete

DELETE operations allow the user to remove records from the database. A hard delete removes the record altogether, while a soft delete flags the record but leaves it in place. For example, this is important in payroll where employment records need to be maintained even after an employee has left the company.

Example SQL statement:
```sql
DELETE FROM <table name> [WHERE <condition>]
```
