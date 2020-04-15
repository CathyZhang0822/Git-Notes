### MySQL ‘show status’ and open database connections
You can show MySQL open database connections (and other MySQL database parameters) using the MySQL show status command, like this:
```
mysql> show status like 'Conn%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| Connections   | 8     | 
+---------------+-------+
1 row in set (0.00 sec)


mysql> show status like '%onn%';
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| Aborted_connects         | 0     | 
| Connections              | 8     | 
| Max_used_connections     | 4     | 
| Ssl_client_connects      | 0     | 
| Ssl_connect_renegotiates | 0     | 
| Ssl_finished_connects    | 0     | 
| Threads_connected        | 4     | 
+--------------------------+-------+
7 rows in set (0.00 sec)
```
All those rows and values that are printed out correspond to MySQL variables that you can look at. Notice that I use like 'Conn%'in the first example to show variables that look like "Connection", then got a little wiser in my second MySQL show status query.

### MySQL show processlist
Here's what my MySQL processlist looks like when I had my Java application actively running under Tomcat:
```
mysql> show processlist;
+----+------+-----------------+--------+---------+------+-------+------------------+
| Id | User | Host            | db     | Command | Time | State | Info             |
+----+------+-----------------+--------+---------+------+-------+------------------+
|  3 | root | localhost       | webapp | Query   |    0 | NULL  | show processlist | 
|  5 | root | localhost:61704 | webapp | Sleep   |  208 |       | NULL             | 
|  6 | root | localhost:61705 | webapp | Sleep   |  208 |       | NULL             | 
|  7 | root | localhost:61706 | webapp | Sleep   |  208 |       | NULL             | 
+----+------+-----------------+--------+---------+------+-------+------------------+
4 rows in set (0.00 sec)
And here's what it looked like after I shut Tomcat down:

mysql> show processlist;
+----+------+-----------+--------+---------+------+-------+------------------+
| Id | User | Host      | db     | Command | Time | State | Info             |
+----+------+-----------+--------+---------+------+-------+------------------+
|  3 | root | localhost | webapp | Query   |    0 | NULL  | show processlist | 
+----+------+-----------+--------+---------+------+-------+------------------+
1 row in set (0.00 sec)
```
As a final note, you can also look at some MySQL variables using the mysqladmin command at the Unix/Linux command line, like this:
```
$ mysqladmin status

Uptime: 4661  Threads: 1  Questions: 200  Slow queries: 0  Opens: 16  Flush
tables: 1  Open tables: 6  Queries per second avg: 0.043
```
