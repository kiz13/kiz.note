# *

- [idea 连接 sqlserver](https://www.jetbrains.com/help/datagrip/db-tutorial-connecting-to-ms-sql-server.html#connect-by-using-sql-server-authentication)
- [connect to sqlserver using jdbc (java application)](https://stackoverflow.com/questions/2451892/how-do-i-connect-to-a-sql-server-2008-database-using-jdbc)
- [配置 sqlserver auth 后重启](https://blog.csdn.net/qq_39217004/article/details/105164041)
- [18456 error when login to MSSQL?](https://stackoverflow.com/questions/20923015/login-to-microsoft-sql-server-error-18456) in the SSMS, go Properties > Security > Server authentication, choose _SQL Server and Windows Authentication mode_. Then restart the SQL Service. [check also](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/change-server-authentication-mode?view=sql-server-ver15)

## run query

[pagination](https://stackoverflow.com/questions/2135418/equivalent-of-limit-and-offset-for-sql-server)

```tsql
SELECT email FROM emailTbl
WHERE user_id=3
ORDER BY Id
OFFSET 0 ROWS
FETCH NEXT 10 ROWS ONLY;
```

[use transactions](https://stackoverflow.com/questions/10153648/correct-use-of-transactions-in-sql-server)

## jdbc

[mssql and jtds](https://stackoverflow.com/questions/4393766/differences-between-ms-sql-microsofts-jdbc-drivers-and-jtdss-driver)

SSL Error: "The server selected protocol version TLS10 is not accepted by client preferences [TLS12]"

- use jTDS
- use mssql-jdbc
  - [repo issues 1803](https://github.com/microsoft/mssql-jdbc/issues/1803)
  - check compatibility [ref1](https://docs.microsoft.com/en-us/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix?view=sql-server-ver15#sql-version-compatibility) and [ref2](https://support.microsoft.com/en-us/topic/kb3135244-tls-1-2-support-for-microsoft-sql-server-e4472ef8-90a9-13c1-e4d8-44aad198cdbe) then configure sqlserver [ref1](https://stackoverflow.com/questions/67261458/com-microsoft-sqlserver-jdbc-sqlserverexception-the-driver-could-not-establish), [ref2](https://stackoverflow.com/questions/68126780/how-to-fix-the-server-selected-protocol-version-tls10-is-not-accepted-by-client)

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
