# Creating a database with an application user

Because we don't want web applications using the root acces to logon to our database, we will create a new database with a dedicated user to acces only that database.

Now let's use our database admin tool (MySQL workbench) with root acces and create a new database called `VIVES` for school purposes with a specific user called `webuser`to acces this database.

## When using MySQL-server

```sql
CREATE DATABASE vives;
USE vives;
CREATE USER 'webuser'@'localhost' IDENTIFIED WITH mysql_native_password BY "secretpassword";
GRANT ALL PRIVILEGES ON vives.* TO 'webuser'@'localhost';
```

Push `CTRL`+`SHIFT`+`ENTER` to run this query step by step.

## When using MariaDB-server

```sql
CREATE DATABASE vives;
USE vives;
CREATE USER 'webuser'@'localhost' IDENTIFIED BY "secretpassword";
GRANT ALL PRIVILEGES ON vives.* TO 'webuser'@'localhost';
```

Push `CTRL`+`SHIFT`+`ENTER` to run this query step by step.

