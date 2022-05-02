# *

[Never code for performance, always code for readability.](https://stackoverflow.com/a/1923866)

## java web

- [eclipse 根据 `.wsdl` 文件自动生成 webservice 的调用客户端](https://www.cnblogs.com/wqsbk/p/5297223.html)
- [jax-rs multiple paths?](https://stackoverflow.com/questions/4784028/jax-rs-multiple-paths/34921732) using _RESTEasy_ go with `@Path("/{a:path1|path2}")` if you want two paths to go to the same method.

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

---

The default class path is the current directory. Setting the `CLASSPATH` variable or using the `-cp (-classpath)` command-line option overrides that default, so if you want to include the current directory in the search path, you must include "." in the new settings.

Classpath entries that are neither directories nor archives (.zip or .jar files) nor * are ignored[.](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)

```shell script
javac Sun.java
# to run the program, specify a class name without extension
java Sun
```

The `java` launches the Java virtual machine. It executes the bytecodes that the compiler placed in the class file.

VM option: `-Duser.language=en` ; command-line option: `-J-Duser.language=en`
[](https://stackoverflow.com/questions/23749714/how-to-change-the-display-language-of-javac-to-english)

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

command argument? `-J-Duser.language=en`

- [the dollar sign has special meaning to most shells](https://stackoverflow.com/a/18442432/11844003)

the `-server` option: Select the Java HotSpot Server VM. On a 64-bit capable jdk only the Java HotSpot Server VM is supported so this option is implicit. This is subject to change in a future release. see also [hollow](https://stackoverflow.com/questions/17608639/use-of-java-server-option)

console outputs garbled characters? try go with `-Dfile.encoding=UTF-8`

[Configuring the JVM, Java Options, and Database Cache](https://docs.oracle.com/cd/E37116_01/install.111210/e23737/configuring_jvm.htm#OUDIG00007)

## groovy

[optional parentheses and dots](https://stackoverflow.com/questions/34711081/groovy-optional-parentheses-and-dots)

[features of groovy for gradle beginner](http://cloudchen.logdown.com/posts/248361/features-of-groovy-for-gradle-beginner)

[spock specification in gradle test not workings](https://stackoverflow.com/questions/57907876/trying-to-run-spock-specification-using-gradle-test-events-were-not-received)

[closure coercion](https://docs.groovy-lang.org/latest/html/documentation/core-semantics.html#closure-coercion)
