# [Redis](https://redis.io)

If redis installation is ok, entering `ping` command should give "pong".

start redis: `redis-server redis.window.conf`

shutdown redis: `redis-cli -a password shutdown`

[redis.windows.conf vs redis.windows-service.conf?](https://stackoverflow.com/questions/56920798/redis-windows-conf-vs-redis-windows-service-conf) the former is meant to be run from the command line, the latter is meant to be run as a service.

[how to connect to a redis database?](https://www.digitalocean.com/community/cheatsheets/how-to-connect-to-a-redis-database)

- for a **local** Redis datastore, if you have `redis-server` installed, you can connect to the Redis instance with the `redis-cli` command, this will take you into redis-cli's _interactive mode_ which presents you with a _read-eval-print loop_ (REPL)
- for a **remote** Redis datastore, use `redis-cli -h host -p port_number -a password`

back up a key before deleting it: `dump your_key` this command will output a hexadecimal string that can be used to restore the key later using `restore your_key 0 hex-string`

[how to show all keys through redis-cli?](https://stackoverflow.com/a/17554440/11844003) There is a database concept in Redis. By default, you have 16 distinct databases, and the current default database is 0. The `SELECT` command can be used to switch a session to another database. There is one keyspace per database. The `info keyspace` command can be used to check whether some keys are defined in several databases.

- switch session to the database 1: `select 1`
- show all keys `keys *`

[use regex to filter keys](https://www.bennadel.com/blog/3708-using-regex-to-filter-keys-with-redis-key-scanner-in-lucee-cfml-5-2-8-50-and-jedis.htm) `SCAN cursor [MATCH pattern] [COUNT count]`

- The MATCH parameter can be used to include keys based on a **glob** style pattern.
- The COUNT is the number of keys to scan in one operation.

[get all keys with their values?](https://stackoverflow.com/questions/19354826/how-to-get-all-keys-with-their-values-in-redis) no native way of doing this, but you can try using some bash scripts

[you can use `flushdb` to remove all keys from the **current** database](https://stackoverflow.com/questions/6851909/how-do-i-delete-everything-in-redis)

[could not get a resource from the pool?](https://stackoverflow.com/a/17710645/11844003) this exception can be thrown if Redis is not running.

[Redis GUI](https://redis.com/redis-enterprise/redis-insight/) seems stop maintaining from 2020.6
