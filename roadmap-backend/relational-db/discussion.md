# *

A [JDBC driver](https://en.wikipedia.org/wiki/JDBC_driver) is a software component enabling a Java application to interact with a database.

## misc

- It is widely considered good style to qualify all column names in a join query, so that the query won't fail if a duplicate column name is later added to one of the tables.

- [reasons why select star is bad](https://tanelpoder.com/posts/reasons-why-select-star-is-bad-for-sql-performance/)

- why is the `alias_name` not resolved in `group by alias_name`? [not all databases allows column aliases for the `GROUP BY`](https://stackoverflow.com/a/53735514/11844003)

- table prefixes [use a short name of the application or solution](https://stackoverflow.com/a/324183/11844003)

- [how does a prepared statement prevent sql injection?](https://stackoverflow.com/questions/1582161/how-does-a-preparedstatement-avoid-or-prevent-sql-injection)

- [group by and distinct differences](https://stackoverflow.com/questions/164319/is-there-any-difference-between-group-by-and-distinct)

- [log some application info to file or database?](https://stackoverflow.com/a/3458899/11844003) log to both file system (first, immediately) and then to a database (even if delayed)

- [using or not using foreign key](https://dba.stackexchange.com/questions/168590/not-using-foreign-key-constraints-in-real-practice-is-it-ok), see also [this one](https://stackoverflow.com/questions/57507444/what-are-the-advantages-disadvantages-of-having-all-foreign-keys-in-the-fact-tab)

- [user-role-schema design](https://stackoverflow.com/questions/10879143/how-to-design-a-user-role-schema-in-a-sql-server-database)

- [performance of `in`](https://stackoverflow.com/questions/1013797/is-sql-in-bad-for-performance) first, `in` clause are generally internally rewritten by most databases to use the `or` logical connective...

- question asked in 2016 [about index use of a log table](https://dba.stackexchange.com/questions/159432/what-index-type-to-use-for-a-log)

- [use junction table for dealing many-to-many relationship](https://dba.stackexchange.com/questions/106001/are-junction-tables-a-good-practice)

- [how does indexing work?](https://stackoverflow.com/questions/1108/how-does-database-indexing-work)

- [physical | logical / hard | soft delete of record](https://stackoverflow.com/questions/378331/physical-vs-logical-hard-vs-soft-delete-of-database-record)

- [differences between `truncate` and `delete`](https://stackoverflow.com/questions/139630/whats-the-difference-between-truncate-and-delete-in-sql)

## relation?

[Entity-attribute-value model](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model)

[I want to create model at runtime?](https://softwareengineering.stackexchange.com/questions/238511/mvc4-how-to-create-model-at-run-time) dont -> EAV table -> NoSQL -> ...

[is EAV bad?](https://softwareengineering.stackexchange.com/questions/93124/eav-is-it-really-bad-in-all-scenarios)

[is EAV really an anti-pattern](https://stackoverflow.com/questions/31347290/eav-in-an-ecommerce-case-is-it-really-an-anti-pattern)

[How to design a database for User Defined Fields?](https://stackoverflow.com/questions/5106335/how-to-design-a-database-for-user-defined-fields)
