# 常见的Postgres commands

**注意**：PostgreSQL interprets `"` as being quotes for identifiers, `'` as being quotes for strings.

| description | command |
| ---- | --- |
| Show tables | `\dt` |
| Describe table | `\d <table name>` |
| Select a database | `\c <database name>` ie: `\c devdb`|
| Insert | `INSERT INTO TABLE_NAME (column1, column2, column3,...columnN) VALUES (value1, value2, value3,...valueN);` <br> `INSERT INTO "wish" ("id", "title", "description") VALUES (1, 'first wish', 'This is my first wish');`|
| Select | 1. `SELECT * FROM "wish";` (table name要加引号)|
| Delete | 1. `DELETE FROM "EMPLOYEES"  WHERE "ID" = 1;`|
