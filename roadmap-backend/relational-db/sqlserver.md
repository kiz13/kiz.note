# *

- [idea 连接 sqlserver](https://www.jetbrains.com/help/datagrip/db-tutorial-connecting-to-ms-sql-server.html#connect-by-using-sql-server-authentication)
- [connect to sqlserver using jdbc (java application)](https://stackoverflow.com/questions/2451892/how-do-i-connect-to-a-sql-server-2008-database-using-jdbc)
- [配置 sqlserver auth 后重启](https://blog.csdn.net/qq_39217004/article/details/105164041)
- [18456 error when login to MSSQL?](https://stackoverflow.com/questions/20923015/login-to-microsoft-sql-server-error-18456) in the SSMS, go Properties > Security > Server authentication, choose _SQL Server and Windows Authentication mode_. Then restart the SQL Service. [check also](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/change-server-authentication-mode?view=sql-server-ver15)
- [table showing minimum requirements for the sql server version to be installed for the corresponding OS](https://docs.microsoft.com/en-us/troubleshoot/sql/general/use-sql-server-in-windows)

## data type

[meaning of the prefix N?](https://stackoverflow.com/questions/10025032/what-is-the-meaning-of-the-prefix-n-in-t-sql-statements-and-when-should-i-use-it) It denotes that the subsequent string is in Unicode \(the N actually stands for National language character set\). Which means that you are passing an `NCHAR`, `NVARCHAR` or `NTEXT` value, as opposed to `CHAR`, `VARCHAR` or `TEXT`.

[store images in the table?](https://stackoverflow.com/questions/5613898/storing-images-in-sql-server/5613926#5613926)

If an integer dividend is divided by an integer divisor, the result is an integer that has any fractional part of the result truncated. check [ms docs](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/divide-transact-sql?view=sql-server-ver16#result-types)

## run sql

[pagination](https://stackoverflow.com/questions/2135418/equivalent-of-limit-and-offset-for-sql-server)

```tsql
SELECT email FROM emailTbl
WHERE user_id=3
ORDER BY Id
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY;
```

[use transactions](https://stackoverflow.com/questions/10153648/correct-use-of-transactions-in-sql-server)

play with `varbinary`
- how to create column for storing large binary data? [`varbinary(max)`](https://stackoverflow.com/a/8240903/11844003)
- how to insert string into a varbinary column? [SQL Server requires an explicit conversion from varchar to varbinary](https://stackoverflow.com/a/3275585/11844003), then use `cast('text' as varbinary)` / `convert(varbinary, 'text')`
- [how to set limit of a varbinary column?](https://stackoverflow.com/questions/34741079/can-i-set-2-mb-for-maximum-size-of-varbinary) use `CONSTRAINT`: `alter ... add constraint xxx check (datalength(col) <= :limit)`

[do large varbinary data affect select queries?](https://dba.stackexchange.com/questions/232941/do-varcharmax-nvarcharmax-and-varbinarymax-columns-affect-select-queries)

[improve performance of table with image fields?](https://stackoverflow.com/questions/2253582/how-to-improve-performance-in-sql-server-table-with-image-fields)

escape single quote? use another single quote `select 'my name''s slim shady'` [ref](https://stackoverflow.com/questions/1586560/how-do-i-escape-a-single-quote-in-sql-server)

[convert `datetime` to `date`](https://docs.microsoft.com/en-us/sql/t-sql/functions/cast-and-convert-transact-sql?view=sql-server-ver16#date-and-time-styles), e.g.,
- `convert(varchar, getdate(), 23)` => `yyyy-mm-dd`
- `convert(varchar, getdate(), 101)` => `mm/dd/yyyy`

[add a column after/before a specific column with `alter` clause?](https://stackoverflow.com/a/4732461) Nope, you better go with some other stuff
- use SQL Server Management Studio
- drop and re-adding the table
- create a new table and moving the data over manually

## jdbc

[mssql and jtds](https://stackoverflow.com/questions/4393766/differences-between-ms-sql-microsofts-jdbc-drivers-and-jtdss-driver)

SSL Error: "The server selected protocol version TLS10 is not accepted by client preferences [TLS12]"

- use jTDS
- use mssql-jdbc
  - [repo issues 1803](https://github.com/microsoft/mssql-jdbc/issues/1803)
  - check compatibility [ref1](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix?view=sql-server-ver15#sql-version-compatibility) and [ref2](https://support.microsoft.com/en-us/topic/kb3135244-tls-1-2-support-for-microsoft-sql-server-e4472ef8-90a9-13c1-e4d8-44aad198cdbe) then configure sqlserver [ref1](https://stackoverflow.com/questions/67261458/com-microsoft-sqlserver-jdbc-sqlserverexception-the-driver-could-not-establish), [ref2](https://stackoverflow.com/questions/68126780/how-to-fix-the-server-selected-protocol-version-tls10-is-not-accepted-by-client)

insert string as `nvarchar`? [`PreparedStatement.setNString()`](https://stackoverflow.com/questions/38654672/sql-server-nvarchar-and-java-prepared-statement#comment64692422_38654672)

## linked server

[steps to create linked mysql server](https://www.mssqltips.com/sqlservertip/4570/access-mysql-data-from-sql-server-via-a-linked-server/)
1. install ODBC
2. in SSMS, click **New Linked Server**
3. enter the provider string (e.g., `Driver={MySQL ODBC 8.0 ANSI Driver};DATABASE=dbname;OPTION=134217728;password=p@sswo0d;UID=uname;SERVER=localhost`) and other necessary inputs

[create linked server using t-sql](https://database.guide/create-a-linked-server-in-sql-server-t-sql-example/)
1. install ODBC
2. ```tsql
     /* example */
     EXEC sp_addlinkedserver @server = N'link_name'
     ,@srvproduct=N'MySQL'
     ,@provider=N'MSOLEDBSQL'
     ,@provstr=N'Driver={MySQL ODBC 8.0 ANSI Driver};DATABASE=dbname;OPTION=134217728;password=p@sswo0d;UID=uname;SERVER=localhost'
     GO
     ```

[linked server, **Access denied**?](https://dba.stackexchange.com/a/269918) `password` or `pwd`, choose the one that works（不深入研究了

test it with: `exec sp_testlinkedserver link_name;`

query with: `select * from openquery(link_name, query_str);`

drop it with: `exec sp_dropserver link_name go`
