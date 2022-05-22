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
