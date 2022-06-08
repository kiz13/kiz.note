# Mysql

partitioning

(linux) start mysql server `sudo service mysqld start` or [other ways](https://askubuntu.com/questions/82374/how-do-i-start-stop-mysql-server)

table of contents

- [dump](#dump)
- [meta information](#meta-info)
- [data type](#data-type)
- [misc sql in action](#sql)
- [old version (5.x) stuff](#elder)

## dump

### export

`mysqldump --no-tablespaces --column-statistics=0 -h x.x.x.x -u user_name -p database_name > dump.sql` [source, also check the comment that points out what's **-p**](https://stackoverflow.com/a/48810450/11844003)

- `-p` is for the password argument, not the database name. But it's insecure to store it in plain text so adding `-p` means you will be prompted for the password at login [source](https://stackoverflow.com/questions/2989724/how-to-mysqldump-remote-db-from-local-machine#comment91984954_48810450)
- the `column-statistics` option is enabled by default in mysqldump 8, disable it by setting to 0 [source](https://stackoverflow.com/questions/52423595/mysqldump-couldnt-execute-unknown-table-column-statistics-in-information-sc)
- Access denied you need (at least one of) the PROCESS privilege(s) ... [how to](https://dba.stackexchange.com/questions/271981/access-denied-you-need-at-least-one-of-the-process-privileges-for-this-ope) use `--no-tablespaces` option
- dump a set of table of one or more tables `mysqldump [options] db_name [tbl_1 tbl_2]` [source](https://stackoverflow.com/questions/18741287/mysqldump-exports-only-one-table)
- add `-d` option to dump only table structure

[(using powershell) why the dump sql file's encoding is utf16?](https://stackoverflow.com/questions/48465271/mysqldump-and-powershell-produces-utf-16) you need to add some options like `mysqldump blah blah | Out-File dump.sql -Encoding utf8`

[skip tables when dumping (with a script demonstrating how)](https://stackoverflow.com/a/425172/11844003) add one or multiple `--ignore-table=<database>.<table>` options

[export structure without `autoincrement`?](https://stackoverflow.com/questions/15656463/mysqldump-export-structure-only-without-autoincrement) I choose to delete that part manually

### import

`mysql -u user_name -p db_name < dump.sql` [source](https://stackoverflow.com/questions/17666249/how-do-i-import-an-sql-file-using-the-command-line-in-mysql)

## meta info

[show connections related info?](https://stackoverflow.com/questions/7432241/mysql-show-status-active-or-total-connections)

- `show status where variable_name = 'Threads_connected'`
- `show processlist`

[where does mysql store data?](https://stackoverflow.com/a/26403457) see also [this from mkyong](https://mkyong.com/mysql/where-does-mysql-stored-the-data-in-my-harddisk/)

- (for Windows 10) Locate the `my.ini` under the `${Mysql-installation}/MySQL Server ver.sion` and search the `datadir` key inside. That installation dir maybe `Program Files` or `ProgramData` (on my machine, version 8.0)
- or use `mysqld --verbose --help | grep datadir`

[show database sorted by creation date](https://stackoverflow.com/questions/34236157/mysql-show-database-sorted-by-creation-date)

  ```mysql
  select TABLE_SCHEMA,
        max(CREATE_TIME) create_time,
        max(UPDATE_TIME) update_time
  from information_schema.tables
  group by TABLE_SCHEMA
  order by create_time desc;
  ```

[show comment of fields ?](https://stackoverflow.com/questions/5404051/show-comment-of-fields-from-mysql-table)

- `show full columns from <tablename>`
- or query `information_schema.COLUMNS`

[list all the reserved words (5.x)?](https://stackoverflow.com/questions/14624292/is-there-a-way-to-list-all-the-reserved-words-in-mysql-using-the-mysql-command-l)

[allow remote access](https://stackoverflow.com/questions/50570592/mysql-8-remote-access)

create user with `create user 'xxx'@'localhost' identified by 'xxx'`

grant privilege with `grant all privileges on db.* to xxx@localhost with grant option`

[run sql script](https://stackoverflow.com/questions/8940230/how-to-run-sql-script-in-mysql)

[check InnoDB settings](https://stackoverflow.com/a/17977105/11844003) `show variables like 'innodb%'`

retrieve the current version of mysql: `select version()`

[what is `.log` suffix in the `version()` output](https://stackoverflow.com/questions/40331746/what-does-log-stand-for-in-mysql-version)

[How to estimate/predict data size and index size of a table](https://dba.stackexchange.com/questions/46069/how-to-estimate-predict-data-size-and-index-size-of-a-table-in-mysql)

## data type

[difference between utf8mb4 and utf8?](https://stackoverflow.com/questions/30074492/what-is-the-difference-between-utf8mb4-and-utf8-charsets-in-mysql)

[difference between bool and boolean?](https://stackoverflow.com/questions/4753963/whats-the-difference-between-mysql-bool-and-boolean-column-data-types) they are both synonyms for `tinyint(1)`

- `0` means `false`
- `1` means `true`

[base64 vs blob](https://stackoverflow.com/questions/29284266/mysql-base64-vs-blob)

[implicit conversion when compare string and number columns](https://stackoverflow.com/questions/64794779/is-it-a-problem-to-compare-a-string-to-an-int-column-in-mysql)

cast lob column: `cast (lob_field as char(length) character set utf8)`

blob size:

  ```text
  TINYBLOB    Up to 255 bytes  1 byte
  BLOB        Up to 64 Kb      2 bytes
  MEDIUMBLOB  Up to 16 Mb      3 bytes
  LONGBLOB    Up to 4 Gb       1 Bytes
  ```

[format date from millisecond](https://stackoverflow.com/questions/18176088/mysql-select-formatted-date-from-millisecond-field)

speed issues - select on tables containing blob? [Many people recommend using blob with only one primary key in a separate table and storing the blob metadata in another table with a foreign key to the blob table.](https://stackoverflow.com/a/13421726/11844003)

Operand should contain 1 column error? [In my case, the problem was that I surrounded my columns' selection with parenthesis by mistake](https://stackoverflow.com/a/63780290/11844003)

unique constraint - [`NULL` values can be repeated in a unique index.](https://stackoverflow.com/questions/18293543/can-i-conditionally-enforce-a-uniqueness-constraint)

both `2022/1/2` and `2022-01-02` is valid to be inserted to a date type column, because [MySQL permits a “relaxed” format for values specified as strings, in which any punctuation character may be used as the delimiter between date parts or time parts.](http://dev.mysql.com/doc/refman/5.0/en/datetime.html)

[what is the biggest id number that autoincrement can produce?](https://stackoverflow.com/questions/10707072/what-is-the-biggest-id-number-that-autoincrement-can-produce-in-mysql)

## sql

[change a `not null` column to a `null` column?](https://stackoverflow.com/questions/2607775/how-can-a-not-null-constraint-be-dropped) `alter table which_one modify column which_c int null;`

[mysql autocommit?](https://stackoverflow.com/a/11376698/11844003) By default, mysql runs with autocommit mode enabled. To disable autocommit mode implicitly for a single series of statements, use the `start transaction` statement, e.g., `start transaction; select @A:=sum(salary) from table1; update table2 set summary=@A; commit;`

[group rows with same column value into one row?](https://stackoverflow.com/questions/3664393/how-to-group-mysql-rows-with-same-column-value-into-one-row)

  ```sql
  select id, xx, group_concat(y)
  from tbl
    inner join tbl_2
      on tbl.id = tbl_2.id
  group by id
  ```

rename a column: `alter table tbl change old_name new_name datatype`

[function that equivalent to Oracle's `nvl`](https://stackoverflow.com/questions/7239498/is-there-a-function-equivalent-to-the-oracles-nvl-in-mysql) `coalesce(col, 'value if col is null')`

order by multiple column `order by column1 desc, column2 asc`

[hierarchical recursive query?](https://stackoverflow.com/a/33737203/11844003)

add a comment to the table `alter table tbl comment = 'wo'`

[case-sensitive search](https://stackoverflow.com/questions/2876789/how-can-i-search-case-insensitive-in-a-column-using-like-wildcard) `select xxx ... COLLATE utf8_general_ci`

[differences between different date time function](https://stackoverflow.com/questions/28315254/difference-between-sysdate-now-current-timestamp-current-timestamp-in-mysq)

[about varchar length, see also the comments](https://stackoverflow.com/a/1303484) The length of `VARCHAR` columns can be specified as a value from 0 to 255 before MySQL 5.0.3, and 0 to 65,535 in 5.0.3 and later versions. Bill Karwin commented that "FWIW, MySQL accepts `VARCHAR(65536)` too, but it **implicitly promotes** the column to `MEDIUMTEXT`"

`SUBSTRING_INDEX(str,delim,count)` returns the substring from string `str` before `count` occurrences of the delimiter `delim`. If count is negative, everything to the right of the final delimiter (counting from the right) is returned. [reference docs](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring-index)

- `SELECT SUBSTRING_INDEX('www.mysql.com', '.', -2);` gives `'mysql.com'`
- `SELECT SUBSTRING_INDEX('www.mysql.com', '.', 2);` gives `'www.mysql'`

[table comments length limit?](https://stackoverflow.com/questions/3571254/mysql-error-1628-comment-for-table-customer-is-too-long-max-60/14502814#14502814) 60? 255? or more? It depends on the version you are using.

[Ref](https://stackoverflow.com/a/48345961) Non-breaking space is often encoded as C2A0 (in hex), to find it, try

```sql
SELECT
  test.*
from
  (select
     og,
     replace(og, unhex('C2A0'), ' shit-marks ') temp
   from test) test
where
  test.temp like '%shit-marks%';
```

Unknown command `'\''` error when do imp? [You have binary blobs in your DB, try adding `--hex-blob` to your mysqldump statement.](https://stackoverflow.com/a/5915062/11844003)

UPDATE with SELECT query (update join) ? check [ref1](https://stackoverflow.com/a/1262848) and [ref2](https://www.cnblogs.com/duanxz/p/5099030.html)

[conditionally enforce a uniqueness constraint](https://stackoverflow.com/a/18293770/11844003)

> Add another column called something like `isactive`. Then create a unique constraint on `(username, isactive)`.
>
> Then you can have both an active and inactive user name at the same time. You will not be able to have two active user names.
>
> If you want multiple inactive names, use `NULL` for the value of `isactive`. `NULL` values can be repeated in a unique index.

## elder

[invalid default value for timestamp field?](https://stackoverflow.com/questions/9192027/invalid-default-value-for-create-date-timestamp-field)

[invalid value for datetime field?](https://stackoverflow.com/a/39668400/11844003) if you are using mysql 5.5.x, change type from `datetime` to `timestamp`

[invalid default value for timestamp field](https://stackoverflow.com/questions/40491518/create-table-with-null-timestamp-columns-in-mysql-5-7) I want this to be a nullable field, so `col timestamp null default null`

[timestamp and datetime diff](https://stackoverflow.com/questions/409286/should-i-use-the-datetime-or-timestamp-data-type-in-mysql)

[Strange MySQL warning 1264 for valid DateTime value](https://stackoverflow.com/questions/11731288/strange-mysql-warning-1264-for-valid-datetime-value)

[current date as default not working for 5.x](https://stackoverflow.com/a/20461045/11844003) the default value must be a constant; it cannot be a function or an expression. The exception is that you can specify `CURRENT_TIMESTAMP` as the default for a `TIMESTAMP` column.

[is there a clause like `drop column if exists`?](https://stackoverflow.com/questions/173814/using-alter-to-drop-a-column-if-it-exists-in-mysql) no? yes?
