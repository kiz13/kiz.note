# *

[](https://stackoverflow.com/questions/30074492/what-is-the-difference-between-utf8mb4-and-utf8-charsets-in-mysql)

[where does mysql store data?](https://stackoverflow.com/questions/26402884/where-does-mysql-store-data)

[what's the difference between mysql bool and boolean?](https://stackoverflow.com/questions/4753963/whats-the-difference-between-mysql-bool-and-boolean-column-data-types) they are both synonyms for `tinyint(1)`; 0 means false, 1 means true; check also this: [set default value for boolean column](https://stackoverflow.com/a/2221080/11844003)

[mysql autocommit stuff?](https://stackoverflow.com/a/11376698/11844003) By default, mysql runs with autocommit mode enabled. To disable autocommit mode implicitly for a single series of statements, use the `start transaction` statement, e.g., `start transaction; select @A:=sum(salary) from table1; update table2 set summary=@A; commit;`

[change a `not null` column to a `null` column?](https://stackoverflow.com/questions/2607775/how-can-a-not-null-constraint-be-dropped) `alter table which_one modify column which_c int null;`

[operand should contain 1 column](https://stackoverflow.com/a/63780290/11844003), invalid parentheses

[show database sorted by creation date](https://stackoverflow.com/questions/34236157/mysql-show-database-sorted-by-creation-date)

  ```sql
  select TABLE_SCHEMA,
        max(CREATE_TIME) create_time,
        max(UPDATE_TIME) update_time
  from information_schema.tables
  group by TABLE_SCHEMA
  order by create_time desc;
  ```

[allow remote access mysql 8](https://stackoverflow.com/questions/50570592/mysql-8-remote-access)

[group rows with same column value into one row?](https://stackoverflow.com/questions/3664393/how-to-group-mysql-rows-with-same-column-value-into-one-row)

  ```sql
  select id, xx, group_concat(y)
  from tbl
    inner join tbl_2
      on tbl.id = tbl_2.id
  group by id
  ```

add a comment to the table `alter table tbl comment = 'shit'`

[hierarchical recursive query?](https://stackoverflow.com/a/33737203/11844003)

rename a column: `alter table tbl change old_name new_name datatype`

cast lob column: `cast (lob_field as char(length) character set utf8)`

dump: `mysqldump --no-tablespaces --column-statistics=0 -h x.x.x.x -u user_name -p database_name > dump.sql` [source, also check the comment that points out what's **-p**](https://stackoverflow.com/a/48810450/11844003)
- `-p` is for the password argument - not the database name. But it's insecure to store it in plain text so adding `-p` means you will be prompted for the password at login [source](https://stackoverflow.com/questions/2989724/how-to-mysqldump-remote-db-from-local-machine#comment91984954_48810450)
- the `column-statistics` option is enabled by default in mysqldump 8, disable it by setting to 0 [source](https://stackoverflow.com/questions/52423595/mysqldump-couldnt-execute-unknown-table-column-statistics-in-information-sc)
- Access denied you need (at least one of) the PROCESS privilege(s) ... [how to](https://dba.stackexchange.com/questions/271981/access-denied-you-need-at-least-one-of-the-process-privileges-for-this-ope) use `--no-tablespaces` option
- dump a set of table of one or more tables `mysqldump [options] db_name [tbl_1 tbl_2]` [source](https://stackoverflow.com/questions/18741287/mysqldump-exports-only-one-table)
- add `-d` option to dump only table structure
- `mysql -u user_name -p db_name < dump.sql` [source](https://stackoverflow.com/questions/17666249/how-do-i-import-an-sql-file-using-the-command-line-in-mysql)
- [show connections related info?](https://stackoverflow.com/questions/7432241/mysql-show-status-active-or-total-connections)
  - `show status where variable_name = 'Threads_connected'`
  - `show processlist`

[skip tables when dumping (with a script demonstrating how)](https://stackoverflow.com/a/425172/11844003)

[(using powershell) why the dump sql file's encoding is utf16?](https://stackoverflow.com/questions/48465271/mysqldump-and-powershell-produces-utf-16) you need to add some options like `mysqldump blah blah | Out-File dump.sql -Encoding utf8`

Access denied for user xxx - check if there exists typo when you do grant shit

retrieve the current version of mysql: `select version()`

[function that equivalent to Oracle's `nvl`](https://stackoverflow.com/questions/7239498/is-there-a-function-equivalent-to-the-oracles-nvl-in-mysql) `coalesce(col, 'value if col is null')`

[format date from millisecond](https://stackoverflow.com/questions/18176088/mysql-select-formatted-date-from-millisecond-field)

[](https://stackoverflow.com/questions/9511476/speed-of-mysql-query-on-tables-containing-blob-depends-on-filesystem-cache)
[](https://stackoverflow.com/questions/29284266/mysql-base64-vs-blob)

[like brainstorm?](https://stackoverflow.com/questions/18293543/can-i-conditionally-enforce-a-uniqueness-constraint)

[mysql converts string to number when compare string and number columns](https://stackoverflow.com/questions/64794779/is-it-a-problem-to-compare-a-string-to-an-int-column-in-mysql)

order by multiple column `order by column1 desc, column2 asc`

## official docs

- `NO_AUTO_VALUE_ON_ZERO` [source](https://dev.mysql.com/doc/refman/8.0/en/sql-mode.html#sqlmode_no_auto_value_on_zero)

  > NO_AUTO_VALUE_ON_ZERO affects handling of AUTO_INCREMENT columns. Normally, you generate the next sequence number for the column by inserting either NULL or 0 into it. NO_AUTO_VALUE_ON_ZERO suppresses this behavior for 0 so that only NULL generates the next sequence number. This mode can be useful if 0 has been stored in a table's AUTO_INCREMENT column. (Storing 0 is not a recommended practice, by the way.) For example, if you dump the table with mysqldump and then reload it, MySQL normally generates new sequence numbers when it encounters the 0 values, resulting in a table with contents different from the one that was dumped. Enabling NO_AUTO_VALUE_ON_ZERO before reloading the dump file solves this problem. For this reason, mysqldump automatically includes in its output a statement that enables NO_AUTO_VALUE_ON_ZERO.

- [check](https://dev.mysql.com/doc/mysql-security-excerpt/5.7/en/connection-access.html)

## fun op

- log in `mysql -u root -p`
- create user `create user 'xxx'@'localhost' identified by 'xxx'`
- grant privilege `grant all privileges on db.* to xxx@localhost with grant option`
- export database `mysqldump -u user_name -p database_name > xxx.sql`
- import database `mysql -u user_name -p database_name < xxx.sql`
- [run sql script](https://stackoverflow.com/questions/8940230/how-to-run-sql-script-in-mysql)
- [check InnoDB settings](https://stackoverflow.com/a/17977105/11844003) `show variables like 'innodb%'`
- start mysql server `sudo service mysqld start` or [others](https://askubuntu.com/questions/82374/how-do-i-start-stop-mysql-server)
- [export structure without `autoincrement`?](https://stackoverflow.com/questions/15656463/mysqldump-export-structure-only-without-autoincrement) I choose to delete that shit manually
- [list all the reserved words](https://stackoverflow.com/questions/14624292/is-there-a-way-to-list-all-the-reserved-words-in-mysql-using-the-mysql-command-l)

## elder

[invalid default value for timestamp field?](https://stackoverflow.com/questions/9192027/invalid-default-value-for-create-date-timestamp-field)

[invalid value for datetime field?](https://stackoverflow.com/a/39668400/11844003) if you are using mysql 5.5.x, change type from `datetime` to `timestamp`

[invalid default value for timestamp field](https://stackoverflow.com/questions/40491518/create-table-with-null-timestamp-columns-in-mysql-5-7) I want this to be a nullable field, so `col timestamp null default null`

[timestamp and datetime diff](https://stackoverflow.com/questions/409286/should-i-use-the-datetime-or-timestamp-data-type-in-mysql)

[Strange MySQL warning 1264 for valid DateTime value](https://stackoverflow.com/questions/11731288/strange-mysql-warning-1264-for-valid-datetime-value)

[still date and time](https://stackoverflow.com/questions/20461030/current-date-curdate-not-working-as-default-date-value)

[what is `.log` suffix in the `version()` output](https://stackoverflow.com/questions/40331746/what-does-log-stand-for-in-mysql-version)

[is there a clause like `drop column if exists`?](https://stackoverflow.com/questions/173814/using-alter-to-drop-a-column-if-it-exists-in-mysql) no? yes?
