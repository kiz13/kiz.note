# [roadmap.sh](https://roadmap.sh/backend)

- [web server](#web-server)
  - [nginx](#nginx)
  - [tomcat](#tomcat)
- [testing](#testing)
- [web security](#web-security)
  - [ssl certificate](#ssl-certificate)
- [caching](#caching)
  - [Redis](#redis)
- [containerization](#containerization)
  - [Docker](#docker)
- [version control](#version-control)
  - [svn](#svn)

## web server

[内网某一网段访问速度很慢 1](https://bbs.csdn.net/topics/360001683) | [内网某一网段访问速度很慢 2](https://ask.csdn.net/questions/356448) | [netbios?](https://security.stackexchange.com/questions/63945/when-does-one-require-netbios)

[hardware time and system time](https://unix.stackexchange.com/questions/189880/difference-between-hardware-time-and-system-time)

[check what programming language a website is built in?](https://security.stackexchange.com/questions/117131/how-to-find-out-what-programming-language-a-website-is-built-in)

### nginx

[beginner's guide](https://nginx.org/en/docs/beginners_guide.html)

start nginx: `start nginx.exe`

By default, the configuration file is named `nginx.conf`

once nginx is started, it can be controlled by invoking the executable with the `-s` parameter:

```shell
nginx -s some_signal
```

that signal may be one of the following:

- `stop` fast shutdown
- `quit` graceful shutdown
- `reload` reloading the configuration file
- `reopen` reopening the log files

for getting the list of all running nginx processes

```shell
tasklist /fi "imagename eq nginx.exe"
```

---

知乎 - [8分钟深入浅出](https://zhuanlan.zhihu.com/p/34943332)

[nginx multiple location issues](https://serverfault.com/questions/361159/nginx-multiple-location-issues)

[what is the `location`](https://serverfault.com/questions/674425/what-does-location-mean-in-an-nginx-location-block)

[meaning of the tilde sign \(`~`\) in the location block](https://serverfault.com/questions/581474/nginx-meaning-of-the-tilde-in-the-location-block-of-the-nginx-conf)

[location directive not working?](https://serverfault.com/questions/596618/location-directive-not-working)

[configure nginx response mime-type?](http://www.nginxer.com/records/how-to-configure-nginx-to-return-text-or-json)

[what does `^` and `$` stand for](https://stackoverflow.com/questions/26016677/what-does-the-two-symbols-and-stand-for-in-nginx-configuration)

[using regex in the location settings block section](https://stackoverflow.com/questions/59846238/guide-on-how-to-use-regex-in-nginx-location-block-section)

### tomcat

[config tomcat user to allow access to manager app](https://stackoverflow.com/questions/16671858/im-not-able-to-log-in-tomcat-manager-app) `$tomcat_home/conf/tomcat-users`

[manager gui access denied?](https://stackoverflow.com/questions/43232878/apache-tomcat-9-unable-to-access-manager-webapp) do this: in the `CATALINA_HOME/webapps/manager/META-INF/context.xml` file, comment out this Valve tag

  ```xml
  <Context antiResourceLocking="false" privileged="true" >
  <!--
  <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
  -->
  </Context>
  ```

or more properly, [add you machine's ip](https://stackoverflow.com/questions/38551166/403-access-denied-on-tomcat-8-manager-app-without-prompting-for-user-password) like `allow="xxx|xxx|your.freaking.ip.address"`


## testing

[staging env and production env](https://softwareengineering.stackexchange.com/questions/117945/staging-environment-vs-production-environment)

[staging vs uat env](https://softwareengineering.stackexchange.com/questions/355103/whats-the-difference-between-staging-and-uat-environments)

[travis ci?](https://stackoverflow.com/questions/22587148/trying-to-understand-what-travis-ci-does-and-when-it-should-be-used)

## web security

[is https required for local network server to server communication?](https://security.stackexchange.com/questions/227020/is-https-required-for-local-network-server-to-server-communication)

[internet access whitelist?](https://superuser.com/questions/1182658/how-to-block-everything-all-incoming-and-outgoing-internet-access-except-those)

### ssl certificate

[Wikipedia - chain of trust](https://en.wikipedia.org/wiki/Chain_of_trust)

[servers certificate chain is incomplete?](https://stackoverflow.com/questions/47290165/ssl-servers-certificate-chain-is-incomplete)

[fix an incomplete ssl chain?](https://superuser.com/questions/644343/how-do-you-fix-an-incomplete-ssl-chain) see also [this](https://superuser.com/questions/644343/how-do-you-fix-an-incomplete-ssl-chain)

[import what](https://stackoverflow.com/a/22406950/11844003) `keytool -import -keystore ../jre/lib/security/cacerts -trustcacerts -alias "VeriSign Class 3 International Server CA - G3" -file /pathto/SVRIntlG3.cer`

[unable to find valid certification path to requested target?](https://stackoverflow.com/questions/65721938/unable-to-find-valid-certification-path-to-requested-target-when-loading-rdf-fr). Set `-Dcom.sun.security.enableAIAcaIssuers=true` would enable automatic intermediate certificate download

[ssl test](https://www.ssllabs.com/ssltest/analyze.html?d=ahwa.viegroup.cc)

[when import certificate using `java`, the default password is `changeit`](https://superuser.com/questions/1506440/import-certificates-using-command-line-on-windows)

## caching

### redis

https//redis.io

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

## containerization

### docker

- _Images_: The file system and configuration of the app which r used to create contains. To find out more about a Docker image, run `docker inspect IMAGE`.
- _Containers_: Running instances of the images -- containers run the actual app. A container includes an app and all of its dependencies... u create a container using `docker run`...
- _Docker daemon_: The background service running on the host that manages building, running and distributing the containers.
- _Docker client_: The CL tool that allows the user to interact with the daemon.
- _Docker store_: A registry of images, where u can find trusted and enterprise ready containers, plugins, and Docker editors.

---

- `docker images` show a list of all images on ur system (TAG in results refers a particular snapshot of the image)
- `docker ps -a(--all)` shows all containers
- `docker stop container_id`
- `docker rm CONTAINER`
- `docker pull ubuntu 12.04` When not providing a specific version number, the client defaults to the latest.
- `docker search`
- `docker run [options] image [command] [arg...]`

`docker run alpine ls -l` what happened?

1. The Docker client contacts the Docker daemon
2. The Docker daemon checks local store if the image is available
   locally, and if not, download it from the Docker Store.
3. The Docker daemon creates the container and then runs a command in that container
4. The Docker daemon streams the output of the command to the Docker client

`docker run -it alpine /bin/sh`, with `-i -t` option, it attaches an interactive tty in the container. Then u can run as many commands in the container as u want.

> On my pc the above command gives _the input device is not a TTY_, then prepend the command with `winpty` giving `runtime create failed ... no such file ...`. just use powershell. [check this](https://stackoverflow.com/a/56922783/11844003) and [this](https://stackoverflow.com/a/48623403/11844003)

---

A Dockerfile is a text file that contains a list of commands
that the Docker daemon calls while creating an image. It contains all the info that Docker needs to know to run the app:

- a base Docker image to run from
- location of the project code
- any dependencies it has
- and what commands to run at start-up

`docker build -t <username>/myfirstapp .` create a docker image from a Dockerfile.

- It takes an optional tag name with `-t` flag, and the location of the directory containing the `Dockerfile`
- the `.` indicates the current directory

`docker build -t ass/hole .` (build using `Dockerfile` under the current directory)

`docker run -p ip:container_ip ass/hole` run in a new container (publish [`--expose`] container's port to the host)

#### quick links

[should each image contain a jdk?](https://stackoverflow.com/questions/52849139/should-each-docker-image-contain-a-jdk)

[reddit - run multi containers using the same base image](https://www.reddit.com/r/docker/comments/kqd1ef/if_you_run_multiple_containers_of_the_same_image/)

## version control

### svn

- where is `svn`? By default, the "command line client tools" option is unchecked (i.e., it won't be installed)

- `svn list url`

- `svn info`

- `svn rm --keep-local dirname` [the directory is already "in" svn](https://stackoverflow.com/questions/116074/how-do-i-ignore-a-directory-with-svn#comment13441727_116075), then the status of it is _D_

- `svn update` Bring changes from the repository into the working copy. [see also](https://stackoverflow.com/questions/30055174/svn-status-files-d-while-files-does-not-exist-anymore-from-local-directory-nor)

- [ignoring files](https://stackoverflow.com/a/19593719/11844003)

- `svn ci` commit (ci): Send changes from your working copy to the repository.

- `svn add --force <directory>` (recursively) add un-versioned files [check](https://stackoverflow.com/a/1218274)

- [do this right](https://stackoverflow.com/questions/2152454/how-to-start-an-svn-project-from-the-command-line)

- `svn checkout` results in **504 gateway timeout**, try the conf below
  ```txt
  [http]
  proxy = http://127.0.0.1:7890
  sslVerify = false
  ```

## end
