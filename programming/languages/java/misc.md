# *

## java web

- [eclipse 根据 `.wsdl` 文件自动生成 webservice 的调用客户端](https://www.cnblogs.com/wqsbk/p/5297223.html)
- [jax-rs multiple paths?](https://stackoverflow.com/questions/4784028/jax-rs-multiple-paths/34921732) using _RESTEasy_ go with `@Path("/{a:path1|path2}")` if you want two paths to go to the same method.
- [why with the `@Consumes(MediaType.APPLICATION_JSON)` annotation, my method gets request body as string](https://stackoverflow.com/questions/24588822/consumesmediatype-application-json-annotation-but-getting-request-body-as-str)
- [javax-servlet api vs servlet api](https://stackoverflow.com/questions/34349047/difference-between-javax-servlet-api-jar-vs-servlet-api-jar)

## remote debug

- [what are java command line options to set to allow JVM to be remotely debugged](https://stackoverflow.com/a/138518/11844003)
  - before Java 5 `-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=1044`
  - Java 5 and above `-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=1044`
- [Tomcat 开启远程调试](https://huangyijie.com/2013/10/29/tomcat-remote-debug/)
  - windows 下将 `SET CATALINA_OPTS=-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=xxxx` 作为 `startup.bat` 或者 `catalina.bat` 文件的第一行命令
  - linux 下在 `bin/startup.sh` 或者 `bin/catalina.sh` 开头添加 `declare -x CATALINA_OPTS="-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=xxxx"`
- [remote debugging Tomcat with eclipse?](https://stackoverflow.com/questions/3835612/remote-debugging-tomcat-with-eclipse)

## command line tools

- [decompile a jar into java files](https://stackoverflow.com/questions/35564270/how-to-decompile-a-jar-into-java-files-from-command-prompt/49906852)
  - `java -jar jd-cli.jar [options] [Files to decompile]`
  - with log trace `jd-cli ur-target.jar -od folder_result -g ALL`
- convert wsdl to java classes `wsimport -keep -s dest-folder the-wsdl-url`
- [change compiled class file without decompile?](https://stackoverflow.com/questions/14069082/how-to-change-already-compiled-class-file-without-decompile) try using Recaf
- [why is `java -version` returning a different version to the one defined in JAVA_HOME?](https://superuser.com/questions/237737/why-is-java-version-returning-a-different-version-to-the-one-defined-in-java-ho) Run `where java` to see if it prints something quite unexpected.
- compiling multiple jar using javac, you need to [stop the shell from `globbing` the wild-card in `lib/*.jar` by escaping it](https://stackoverflow.com/questions/30313812/compiling-multiple-jar-and-java-files-using-javac)
- [the dollar sign has special meaning to most shells](https://stackoverflow.com/a/18442432/11844003)
- console outputs garbled characters? try go with `-Dfile.encoding=UTF-8`
- [change the display language of javac?](https://stackoverflow.com/questions/23749714/how-to-change-the-display-language-of-javac-to-english) add this option: `-J-Duser.language=en`
- [a generic reference Q&A for new Java users about ](https://stackoverflow.com/questions/18093928/what-does-could-not-find-or-load-main-class-mean) couldn't find or load main class
- [use of java server option](https://stackoverflow.com/questions/17608639/use-of-java-server-option)
- [modify a file inside a jar](https://stackoverflow.com/questions/1224817/modifying-a-file-inside-a-jar) use `jar uf jar-file new-files`
- [Can't execute jar: "no main manifest attribute"](https://stackoverflow.com/questions/9689793/cant-execute-jar-file-no-main-manifest-attribute) to make a jar executable, you need to jar a file called META-INF/MANIFEST.MF
- [why do jvm arguments start with `-D`](https://stackoverflow.com/questions/44745261/why-do-jvm-arguments-start-with-d)

---

The default class path is the current directory. Setting the `CLASSPATH` variable or using the `-cp (-classpath)` command-line option overrides that default, so if you want to include the current directory in the search path, you must include "." in the new settings.

Classpath entries that are neither directories nor archives (.zip or .jar files) nor * are ignored.

```shell script
javac Sun.java
# to run the program, specify a class name without extension
java Sun
```

The `java` launches the Java virtual machine. It executes the bytecodes that the compiler placed in the class file.

`jar [-]cvf JAR_FILE_NAME FILE1 FILE2`

- `c` create a new archive
- `v` generate verbose output on standard output
- `f` specify archive file name

If any file is a directory then it is processed recursively.

In addition to class files and other resources, each JAR file contains a _manifest_ file that describes special features of the archive. This file is called `MANIFEST.MF` and is located in a special `META-INF` subdirectory of the JAR file. The minimum legal manifest is just: (notes the newline)

```text
Manifest-Version: 1.0

```

`jar cfm JAR_FILE_NAME ManifestFileName FILE1 ...`

- `m` include manifest information from specified manifest file

To update the manifest of an existing JAR file, place the additions into a text file and: `jar ufm xx.jar manifest-addtions.mf`

- `u` update existing archive

`jar cvfe xx.jar MainClass MainClass.class FILE2 ...`

- `e` specify application entry point for stand-alone application bundled into an executable jar file

the `-server` option: Select the Java HotSpot Server VM. On a 64-bit capable jdk only the Java HotSpot Server VM is supported so this option is implicit. This is subject to change in a future release.

[Configuring the JVM, Java Options, and Database Cache](https://docs.oracle.com/cd/E37116_01/install.111210/e23737/configuring_jvm.htm#OUDIG00007)

find `$JAVA_HOME` on *nix system, check [ref1](https://unix.stackexchange.com/questions/154955/how-to-find-where-is-java-home-set) and [ref2](https://unix.stackexchange.com/questions/21689/how-to-find-path-where-jdk-installed)

### ssl

[import what](https://stackoverflow.com/a/22406950/11844003) `keytool -import -keystore ../jre/lib/security/cacerts -trustcacerts -alias "VeriSign Class 3 International Server CA - G3" -file /pathto/SVRIntlG3.cer`

[when import certificate using `java`, the default password is `changeit`](https://superuser.com/questions/1506440/import-certificates-using-command-line-on-windows)

[unable to find valid certification path to requested target?](https://stackoverflow.com/questions/65721938/unable-to-find-valid-certification-path-to-requested-target-when-loading-rdf-fr). Set `-Dcom.sun.security.enableAIAcaIssuers=true` would enable automatic intermediate certificate download

## groovy

[optional parentheses and dots](https://stackoverflow.com/questions/34711081/groovy-optional-parentheses-and-dots)

[features of groovy for gradle beginner](http://cloudchen.logdown.com/posts/248361/features-of-groovy-for-gradle-beginner)

[spock specification in gradle test not workings](https://stackoverflow.com/questions/57907876/trying-to-run-spock-specification-using-gradle-test-events-were-not-received)

[closure coercion](https://docs.groovy-lang.org/latest/html/documentation/core-semantics.html#closure-coercion)
