# *

context: **11g** Windows 10

[jdbc data source and url](https://docs.oracle.com/database/121/JJDBC/urls.htm#BEIDHCBA)

[no suitable driver found?](https://stackoverflow.com/questions/12103369/sqlexception-no-suitable-driver-found-for-jdbcoraclethin-localhost1521-or) The "ojdbc.jar" is not in the CLASSPATH of your application

## table of contents

- [安装前后需要注意的点](#安装前后需要注意的点)
- [小介绍](#小介绍)
  - [ADR](#adr)
- [导入导出数据相关](#导入导出数据相关)
- [写点 sql](#sql-stuff)
- [data type](#data-type)
- [database-link](#database-link)

## 安装前后需要注意的点

- choose you character set (gbk/utf8)
- log retention policy (with `adrci`)
- [彻底的卸载 oracle 11g](https://blog.csdn.net/Devin_LiuYM/article/details/59539020)
  1. **关服务**
  2. 删

      - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ 标识Oracle在windows下注册的各种服务
      - HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE 软件安装信息
      - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application 所有项目

  3. **重启**
  4. 删除 $Oracle_Home 下的所有数据
- [卸载2](https://zhuanlan.zhihu.com/p/34256436) **记得创建系统还原点哦**
  1. **关服务**
  2. 删

      - HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\【下】所有Oracle删除
      - HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\【下】所有Oracle删除
      - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\【下】所有Oracle删除
      - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\【下】所有Oracle删除
      - 删除所有Oracle入口
      - 删除环境变量CLASSPATH和PATH中有关Oracle的设定
      - 从桌面上、STARTUP（启动）组、程序菜单中，删除所有有关Oracle的组和图标

  3. **重启**
  4. 删除与Oracle有关的文件，选择Oracle所在的缺省目录C:\Oracle，删除这个入 口目录及所有子目录，并从Windows目录（一般为C:\WINDOWS）下删除oralce文件等等
- 监听问题，看看ip是否正确
  - [check](https://blog.csdn.net/idomyway/article/details/81211810)
  - [check](https://blog.csdn.net/qq_39313596/article/details/80472352)
- ORA-2800 创建用户时默认的密码过期限制是180天（11g 后引入的功能）[相关修改操作](https://www.cnblogs.com/luckly-hf/p/3828573.html)

## 小介绍

Whether Oracle talks about the connection ("Internet"), the combination of servers ("Grid"), or both ("Cloud"), they always mean: Place your data on our big, central boxes, and you’ll be cool and happy. [source](https://qr.ae/pGHMbh)

In short: SID = the unique name of your DB, ServiceName = the alias used when connecting. [check og](https://stackoverflow.com/questions/43866/how-sid-is-different-from-service-name-in-oracle-tnsnames-ora)

The _OCI_ driver is a _type 2_ JDBC driver and uses native code to connect to the database. The _Thin_ driver is a _type 4_ JDBC Driver that uses Java sockets to connect directly to Oracle. It implements Oracle's SQL*Net TCP/IP protocol directly. [check](https://stackoverflow.com/questions/21711085/what-is-the-difference-between-oci-and-thin-driver-connection-with-data-source-c)

You should consider a schema to be the user account and collection of all objects therein as a schema for all intents and purposes. e.g., SCOTT is a schema that includes the EMP, DEPT and BONUS tables with various grants, and other stuff. [check](https://stackoverflow.com/questions/880230/difference-between-a-user-and-a-schema-in-oracle)

---

### ADR

自從 Oracle 11g 開始，推出了 Automatic Diagnostic Repository (ADR) 這個功能，目的是用來集中化管理資料庫所有的 log 與 trace file (在 $ADR_BASE 下，預設為 $ORACLE_BASE)。

ADR 底下的檔案維護分為 SHORTP_POLICY 與 LONGP_POLICY ，SHORTP_POLICY 預設為 720 (單位:小時，30天) 自動清理 trace files 、Core dump files 與 Packaging information ; LONGP_POLICY 預設為 8760 (單位:小時，365天) 自動清理 Incident information 、 Incident dumps 與 alert logs。

修改 retention policy (there's also a shell script to do this, check the blog by Johannes Ahrends):

```shell
adrci> show homes
....(homes are listed)...
adrci> set home diag\....\the location
adrci> show control
.... (current settings are listed) ....
adrci> set control (SHORTP_POLICY = 168)
adrci> set control (LONGP_POLICY = 720)
```

直接通过命令清理 60 **分钟**前的 alert.xml (try `help purge`)

```shell
adrci> purge -age 60 -type ALERT
```

上述文字的出处

- [blog: easily drop logs with _ADR Command Interpreter_](https://streetkiter.wordpress.com/2011/04/06/do-you-really-need-one-year-old-logs-and-traces-for-your-oracle-database/)
- [clean the logs (dba.stackexchange.com)](https://dba.stackexchange.com/questions/15715/how-to-free-up-disk-space-which-logs-directories-to-clean)
- [clean the logs (dba.stackexchange.com)](https://dba.stackexchange.com/questions/119824/adrci-not-purge-trace-files-and-alert-logs)
- [blog: Automatic Diagnostic Repository 介绍 (需爬墙)](https://oraksumi.blogspot.com/2020/09/49-automatic-diagnostic-repository-adr.html)
- [detailed introduction of ADR Command Interpreter (oracle-base.com)](https://oracle-base.com/articles/11g/automatic-diagnostics-repository-11gr1)

## 导入导出数据相关

- `sqlplus /nolog;` | `sqlplus name/pwd` | `CONTENT=METADATA_ONLY` | `xxx as sysdba`

- [replace all existing objects?](https://dba.stackexchange.com/questions/204968/how-to-replace-and-overwrite-all-existing-objects-in-oracle-with-impdp-for-full) Not possible, there is no "Replace" option for non-table objects like procedures, packages etc. The best option would be to drop the schema entirely before the datapump import. This way, datapump will re-create the schema and all the contained objects.

- [replace all existing objects?](https://community.oracle.com/tech/apps-infra/discussion/3782157/replace-all-already-exist-object-when-doing-full-import-impdp) Not possible, `TABLE_EXISTS_ACTION=REPLACE` will only replace tables, there is no feature to replace all objects. You may have to drop all objects before importing or get DDL of user, drop user cascade and recreate the user and import again.

- [check what schema is in the dmp file](https://stackoverflow.com/questions/95578/how-to-determine-the-schemas-inside-an-oracle-data-pump-export-file)

  ```shell
  impdp '/ as sysdba' dumpfile=<your .dmp file> logfile=import_log.txt sqlfile=ddl_dump.txt
  ```

- [导入时出现 ora-01653: unable to extend table 的错误](https://www.cnblogs.com/xiaowangba/p/6314152.html) 有两种可能性（详说请见原博）[check also](https://blog.csdn.net/u010741112/article/details/105861678)
  1. 表空间不足
  2. 磁盘空间不足

- [Kill, cancel, resume or restart datapump expdp and impdp jobs (ORA-31626, ORA-31633, ORA-06512, ORA-00955)](https://blog.oracle48.nl/killing-and-resuming-datapump-expdp-and-impdp-jobs/)

- [How to kill, cancel, restart, stop data pump jobs](http://amit7oracledba.blogspot.com/2013/06/how-to-kill-cancel-restart-stop-data.html)

- [deep into `table_exists_action`](https://blog.csdn.net/huang_xw/article/details/7182577)

## sql stuff

implicit number and character conversion

---

- [overview by others](https://blog.csdn.net/qq_42994789/article/details/105944322)

- [update a blob column containing xml data](https://stackoverflow.com/questions/62590949/how-to-update-a-blob-column-containing-xml-data-in-oracle)

- [calc the table size](https://stackoverflow.com/a/10109416)

  ```sql
  -- Tables + Size KB
  select owner, table_name, round((num_rows * avg_row_len) / 1024) KB
  from all_tables
  where owner = 'xxx' and not owner like 'SYS%'  -- Exclude system tables
  and num_rows > 0  -- Ignore empty Tables
  order by KB desc  -- Biggest first
  ;
  ```

- [insert lots of dummy data into table](https://stackoverflow.com/questions/11738342/how-to-insert-1-million-random-row-into-table-database-oracle)

  ```sql
  create table dummy
  (
  row1 varchar2(200),
  row2 varchar2(200)
  );
  
  insert into dummy
  select rownum, 'Name' || rownum
  from dual
  connect by rownum <= 13000;
  ```

- [insert string which includes quotes?](https://stackoverflow.com/questions/21813786/insert-string-which-includes-quotes-in-oracle) use the alternative quoting like `q'['shit']'` [see also the official doc.](https://docs.oracle.com/cd/E11882_01/server.112/e41084/sql_elements003.htm#SQLRF00220) 这种数据以后可能得注意了？

- [wanna use alias in the `sum` function?](https://stackoverflow.com/questions/12354014/oracle-possible-to-use-alias-in-sum-function) The scoping rules of most databases do not allow you to use the aliased names in the same SELECT statement. You can do so using a subquery.

- [column alias is not allowed in a where clause?](https://stackoverflow.com/questions/28802134/sql-not-recognizing-column-alias-in-where-clause) Standard SQL disallows references to column aliases in a WHERE clause. This restriction is imposed because when the WHERE clause is evaluated, the column value may not yet have been determined.

- [if statement in SELECT?](https://stackoverflow.com/questions/15614751/if-statement-in-select-oracle) use `case` statement, `CASE WHEN ... THEN 1 ELSE 0 END`, see also [all controls statements on official doc.](https://docs.oracle.com/cd/E11882_01/appdev.112/e25519/controlstatements.htm#LNPLS004)

- [use rowid to delete records](https://stackoverflow.com/questions/9735988/deleting-a-table-in-oracle-with-where-condition-in-other-tables)

  ```sql
  delete from A
  where ROWID in
    (select A.ROWID
     from A,B
     where A.A1 = B.B1
       and A.A2 = concat(B.B2, B.B3, B.B4))
  ```

- [count number of occurrences of a character in a varchar2 string?](https://stackoverflow.com/questions/8169471/how-to-count-the-number-of-occurrences-of-a-character-in-an-oracle-varchar-value) try using`select REGEXP_COUNT('123-345-566', '-') from dual;` (works only in 11g)

- **use `savepoint`!**

  ```sql
  create table test_tb
  (
    col number
  );
  
  insert into test_tb (col) values (2);
  savepoint before_do_shit;
  
  insert into test_tb (col)
  select level
  from dual
  connect by level <= 2;
  savepoint insert_stuff;
  
  update test_tb
  set col = 3
  where col = 1;
  savepoint update_stuff;
  
  -- all records
  select col from test_tb;
  
  delete
  from test_tb
  where col is not null;
  savepoint delete_stuff;
  
  -- rollback;
  -- rollback to savepoint before_do_shit;
  -- rollback to savepoint insert_stuff;
  -- rollback to savepoint update_stuff;
  -- commit
  ```

- [sql developer execute a simple sql wont stop?](https://stackoverflow.com/questions/59147267/oracle-sql-developer-execute-script-wont-stop-running#comment104520683_59147267) try disconnecting from the server and setting it up again; [update query stuck forever](https://stackoverflow.com/questions/61554907/update-query-stuck-forever) it can be you have another open uncommitted transaction for the same set of records, so they are locked for that transaction.

- [what is a dual table](https://stackoverflow.com/questions/73751/what-is-the-dual-table-in-oracle)

- [fast way to check if some records in a table?](https://stackoverflow.com/questions/2131168/the-fastest-way-to-check-if-some-records-in-a-database-table) This will return 'Y' if a record exists and **nothing** otherwise.

  ```sql
  select 'Y' from dual where exists (select 1 from dummy where row1 = q'['fuck', he said]')

- [comparing dates](https://stackoverflow.com/questions/10178292/comparing-dates-in-oracle-sql) Note also that you can use either `> <` or `BETWEEN '' AND ''`. [see also `to_date` doc](https://docs.oracle.com/database/121/SQLRF/functions219.htm#SQLRF06132)

- [model a auto_increment column using trigger and sequence.](https://stackoverflow.com/a/11296469/11844003)

- [there's no boolean type, just use a check constraint.](https://stackoverflow.com/questions/3726758/is-there-any-boolean-type-in-oracle-databases)

- [DML commands need to be committed/rolled back](https://stackoverflow.com/questions/9541013/oracle-what-statements-need-to-be-committed). Those command includes `insert`, `update`, `delete`, `merge`, `call`, `lock table`, etc.

- [DDL statements (CREATE, ALTER, DROP, etc.) implicitly COMMIT before and after executing.](https://stackoverflow.com/questions/3908533/howto-use-rollback-commit-in-oracle-sql)

- [semicolon vs slash?](https://stackoverflow.com/questions/1079949/when-do-i-need-to-use-a-semicolon-vs-a-slash-in-oracle-sql/10207695) The `;` ends a SQL statement, whereas the `/` executes whatever is in the current "buffer". So when you use a `;` **and** a `/` the statement is actually executed twice. The `/` is mainly required in order to run statements that have embedded `;` like a `CREATE PROCEDURE` statement.

- `group by` stuff
  - [quick intro](https://docs.oracle.com/javadb/10.8.3.0/ref/rrefsqlj32654.html)
  - [when encountering date](https://stackoverflow.com/questions/11556382/group-by-not-working-in-oracle-11g)
  - still dunno how to group? [check this](https://stackoverflow.com/questions/43919957/oracle-group-by-only-one-column/43920159#43920159)
  - still not ok? [check this](https://stackoverflow.com/questions/1520608/ora-00979-not-a-group-by-expression)

- Use the `rowid` pseudo-column [to removing duplicate rows from table](https://stackoverflow.com/a/529119/11844003)

- [about ROWNUM](https://stackoverflow.com/questions/9240192/selecting-the-second-row-of-a-table-using-rownum/9240230#9240230)

- [`row_number` is quite inefficient](https://stackoverflow.com/a/830005/11844003) also note that you cannot use `ROWNUM BETWEEN :start and :end` without a subquery. `ROWNUM` is always assigned last and checked last, that's way ROWNUM's always come in order without gaps.

- [select non dup records only](https://stackoverflow.com/questions/45594336/select-non-duplicate-records-only-in-oracle)

- `partition by`
  - [detailed explanation](https://stackoverflow.com/a/561884/11844003)
  - [can also be used to discard duplicates](https://stackoverflow.com/a/32637419/11844003)
  - [use alias name](https://stackoverflow.com/questions/54073534/how-to-use-alias-name-with-partition-by-in-sql)

- `DUMP` returns a VARCHAR2 value containing the datatype code, length in bytes, and internal representation of expr. [check](https://docs.oracle.com/cd/B28359_01/server.111/b28286/functions048.htm#SQLRF00635)

  ```sql
  select dump('中', 1016)
  from dual;
  select dump(n'中', 1016)
  from dual;
  select dump('®', 1016)
  from dual;
  select dump(n'®', 1016)
  from dual;
  ```

- [setting a default value for a column wont affect the existing data in the table.](https://stackoverflow.com/a/21057944/11844003) note that the datatype isn't needed when only adding a default. `alter table foo modify (col2 default 'bar')`

- [join what?](https://stackoverflow.com/questions/18390588/how-to-use-oracle-outer-join-with-a-filter-where-clause)

- [How do I get a list of all the last modified tables in an Oracle database?](https://stackoverflow.com/a/46817496), [check also](http://facedba.blogspot.com/2018/10/flushdatabasemonitoringinfo-procedure.html)

- [query database name?](https://stackoverflow.com/questions/8978047/how-to-query-database-name-in-oracle-sql-developer) `select * from v$database` or `select ora_database_name from dual`

- [多对多映射](https://www.cnblogs.com/lgxlsm/archive/2013/05/15/3080994.html)

---

**PL/SQL** stands for procedural language extension to the _structured query language_

- [stored procedure name has length limit](https://stackoverflow.com/questions/11191299/why-is-there-a-maximum-length-for-stored-procedure-names)

- [how to use `savepoint` in pl/sql](https://docs.oracle.com/cd/B19306_01/appdev.102/b14261/sqloperations.htm#BABGAAIG)

- [execute an oracle stored procedure?](https://stackoverflow.com/questions/1854427/how-to-execute-an-oracle-stored-procedure) `begin proc end;`

- [multiple updates in execute immediate](https://stackoverflow.com/questions/32757446/multiple-updates-in-execute-immediate) You cannot simply concatenate multiple statements within an `EXECUTE IMMEDIATE` call - you'll either have to use several calls or ...

- [ORA-01006 ?](https://stackoverflow.com/questions/26491682/oracle-11g-bind-variable-does-not-exist) Bind variable should not be included within single quotes, as it would be treated as a String literal instead. [see also](https://stackoverflow.com/questions/55551386/how-to-solve-ora-01006-in-procedure)

- [check if a column exists before adding it to an existing table.](https://stackoverflow.com/a/6352261/11844003)

  ```sql
  /*
  user_tab_cols; -- For all tables owned by the user
  all_tab_cols ; -- For all tables accessible to the user
  dba_tab_cols; -- For all tables in the Database.
  */
  
  DECLARE
    v_column_exists number := 0;  
  BEGIN
    Select count(*) into v_column_exists
      from user_tab_cols
      where upper(column_name) = 'ADD_TMS'
        and upper(table_name) = 'EMP';
        -- and owner = 'SCOTT' --*might be required if you are using all/dba views
  
    if (v_column_exists = 0) then
      execute immediate 'alter table emp add (ADD_TMS date)';
    end if;
  end;
  ```

- [drop table constraints without dropping tables?](https://stackoverflow.com/a/3701647/11844003)

  ```sql
  begin
    for r in ( select table_name, constraint_name
               from user_constraints
               where constraint_type = 'R'
                 and OWNER = 'xxx')
      loop
        execute immediate 'alter table ' || r.table_name
          || ' drop constraint ' || r.constraint_name;
      end loop;
  end;
  ```

- [drop all objects on schema?](https://stackoverflow.com/a/53506575/11844003)

  ```sql
  begin
    for i in (select 'drop ' || OBJECT_TYPE || ' ' || OBJECT_NAME as stmt
              from ALL_OBJECTS
              where lower(OWNER) = 'cdmdm'
                and object_type in
                    ('VIEW', 'PACKAGE', 'SEQUENCE', 'PROCEDURE', 'FUNCTION', 'TABLE')
      )
      loop
        execute immediate i.stmt;
      end loop;
  end;
  ```

- [search what?](https://stackoverflow.com/questions/208493/search-all-fields-in-all-tables-for-a-specific-value-oracle)

- [is commit required after every `execute immediate`?](https://stackoverflow.com/questions/20433082/is-commit-required-after-every-execute-immediate) you should only commit once when the transaction is finished.

- [escape single quote in a string?](https://stackoverflow.com/questions/11315340/pl-sql-how-to-escape-single-quote-in-a-string) use literal quoting: `q'[insert into tbl (col) values ('burp')]'`

- [if-else conditions ?](https://stackoverflow.com/questions/19833642/if-else-condition-in-sql-stored-procedure)

- too many declarations of xxx? specify the parameter names when using the function, e.g., `dbms_scheduler.create_job(xxx => '', xxx => '', ...)`

---

- [where's my invalid character (ORA-00911)?](https://stackoverflow.com/a/10728434/11844003) **u may not include semicolon in the query string in the JDBC calls.**
- [construct readable sql query string](https://softwareengineering.stackexchange.com/questions/326135/how-to-create-multiline-strings-for-sql-queries-that-are-readable-maintainable)
- [maximum length of a table name?](https://stackoverflow.com/questions/756558/what-is-the-maximum-length-of-a-table-name-in-oracle)
- [order by multiple column?](https://stackoverflow.com/questions/13897024/sql-order-by-on-multiple-column)
- [use union?](https://stackoverflow.com/questions/49257562/union-and-union-all-in-oracle-database)
- [storing json in blob columns?](https://blogs.oracle.com/database/post/storing-json-in-blob-columns)
- [windows path and `BFILENAME` function](https://stackoverflow.com/questions/58982625/how-to-declare-windows-path-in-oracle-plsql)
- [I don't think you can tell Oracle to store trailing zeros, but you should be able to configure your SQL client (or your application) to format the output with the desired number of decimals](https://stackoverflow.com/questions/42199210/does-oracle-store-trailing-zeroes-for-number-data-type#comment71560056_42199210)
- add trailing zeros: [this](https://stackoverflow.com/questions/30323013/oracle-sql-how-to-add-00), [this](https://stackoverflow.com/questions/26583179/how-to-add-zeros-after-decimal-in-oracle), and [this](https://stackoverflow.com/questions/48305531/how-to-do-roundup-in-oracle-with-2-decimals-as-in)
  - `to_char(number, 999990D00)`
  - `to_char(number, 999990.00)`
  - `to_char(number, fm999999.00)`
  - `https://docs.oracle.com/cd/E11882_01/server.112/e41084/sql_elements004.htm#SQLRF00212`

## data type

[official ref](https://docs.oracle.com/cd/B28359_01/server.111/b28318/datatype.htm#CNCPT113)

> PL/SQL has additional datatypes for constants and variables, which include BOOLEAN, reference types, composite types (collections and records), and user-defined subtypes.

### VARCHAR

The `VARCHAR` datatype is synonymous with the `VARCHAR2` datatype. To avoid possible changes in behavior, **always** use the `VARCHAR2` datatype to store variable-length character strings.

### NUMBER

Optionally, you can also specify a precision (total number of digits) and scale (number of digits to the right of the decimal point):

    column_name NUMBER (precision, scale)

If a precision is not specified, the column stores values as given. If no scale is specified, the scale is zero.

Oracle guarantees portability of numbers with a precision equal to or less than 38 digits. You can specify a scale and no precision:

    column_name NUMBER (*, scale)

In this case, the precision is 38.

This table shows how scale factors affect numeric data storage:

| input data   | specified as  | stored as  |
| ------------ | ------------- | ---------- |
| 7,456,123.89 | number        | 7456123.89 |
| 7,456,123.89 | number (*,1)  | 7456123.9  |
| 7,456,123.89 | number (9)    | 7456124    |
| 7,456,123.89 | number (9,2)  | 7456123.89 |
| 7,456,123.89 | number (9,1)  | 7456123.9  |
| 7,456,123.89 | number (6)    | (not accepted, exceeds precision) |
| 7,456,123.89 | number (7,-2) | 7456100    |

If you specify a negative scale, Oracle Database rounds the actual data to the specified number of places to the left of the decimal point. E.g., specifying (7,-2) means "rounds to the nearest hundredths."

### LOB

The LOB datatypes `BLOB`, `CLOB`, `NCLOB`, and `BFILE` enable you to store and manipulate large blocks of unstructured data (such as text, graphic images, video clips, and sound waveforms) in binary or character format.

## database link

- [dblink 简单使用](https://www.cnblogs.com/wangyong/p/6354528.html)
  1. 权限赋予 使用 sysdba 用户操作 `grant create public database link to xxx;`
  2. 创建 dblink
  3. 使用 e.g. `select * from tblName@dblinkName`
- [use easy connect syntax rather than using TNS aliases](https://stackoverflow.com/a/51772303/11844003)
  ```sql
  create public database link remote_connect
  connect to system identified by ***
  using '//localhost:1521/orcl';
  ```
- dblink between 11g and 12c (access 12c from 11g)
  - [I encounter the ORA-12514 error](https://asktom.oracle.com/pls/apex/f?p=100:11:0::::P11_QUESTION_ID:9540068000346977405)
  - [I faced the ORA-28040 No Matching Authentication Protocol error?](https://community.oracle.com/tech/developers/discussion/4341584/dblinks-from-11g-to-12c) add the `SQLNET.ALLOWED_LOGON_VERSION_CLIENT=11` and `SQLNET.ALLOWED_LOGON_VERSION_SERVER=11` to the `$ORACLE_HOME/network/admin/sqlnet.ora` file. [check also](https://docs.oracle.com/database/121/NETRF/sqlnet.htm#NETRF182)
- [取决于](https://dba.stackexchange.com/questions/27523/sqlnet-ora-or-tnsnames-ora-changes-require-reboot)
