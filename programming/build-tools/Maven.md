# move it

## Maven The Definitive Guide (quick check)

A build tool such as Ant is focused solely on preprocessing, compilation,
packaging, testing, and distribution. A project management tool such as
Maven provides a superset of features found in a build tool. In addition
to providing build capabilities, Maven can also run reports, etc.

... that encompasses a Project Object Model, a set of standards, a
project life, a dependency management system, and logic for executing
plugin goals at defined phases in a lifecycle.

### Convention over Configuration

Without customization, source code is assumed to be in _${basedir}/src/main/java_ and resources are assumed to be in _${basedir}/src/main/resources_. Tests are assumed to be in _${basedir}/src/test_, and a project is assumed to produce a JAR (Java ARchive) file. Maven assumes that you want to compile byte code to _${basedir}/target/classes_ and then create a distributable JAR file in _${basedir}/target_.

### Part II

Maven is more of a platform than a tool.

Running `mvn install` will process resources, compile source, execute unit
tests, create a JAR, and install the JAR in a local repository for reuse in other projects...

... `mvn test` ...

... **groupId**, **artifactId**, **packaging**, **version** - are
known as the Maven coordinates, which uniquely identify a project.
**name** and **url** are descriptive elements of the POM, providing a human-readable name and associating the project with a project web site.

Although your project might have a relatively minimal _pom.xml_, the contents of your project’s POM are interpolated with the contents of all parent POMs, user settings, and any active profiles. To see this “effective” POM, run

`mvn help:effective-pom`

then, you should see a much larger POM that exposes the default settings of Maven.

---

`mvn archetype:create -DgroupId=org.sonatype.mavenbook.ch03 -DartifactId=simple -DpackageName=org.sonatype.mavenbook` (**not found**)

the syntax to execute a single Maven plugin goal: _`mvn archetype:create`_

- **archetype**: identifier of a plugin
- **type**: identifier of a goal

A goal is a specific task that may be executed as a standalone goal or along with other goals as part of a larger build. (unit of work)

The core of Maven has little to do ... It delegates all of this work to Maven plugins like ...

`mvn install`

 This command didn’t specify a plugin goal; instead, it specified a Maven lifecycle phase ... The build lifecycle is an ordered sequence of phases involved in building a project.

Plugin goals can be attached to a lifecycle phase.

---

**groupId**, **artifactId**, **packaging** and **version**. These combined identifiers make up a project's coordinates. A Maven coordinate is an address for a specific point in "space": from general to specific. Maven pinpoints a project via its coordinates when one project relates to another, either as a dependency, a plugin, or a parent project reference. Maven coordinates are often written using a colon as a delimiter in the following format: **groupId:artifactId:packaging:version**.

- groupId: The group, company, team, organization, project, or other group. The convention for group identifiers is that they begin with the reverse domain name of the organization that creates the project.
- artifactId: A unique identifier under **groupId** that represents a single project.
- version: A specific release of a project. Projects undergoing active development can use a special identifier that marks a version as a **SNAPSHOT**.

A project’s **_groupId:artifactId:version_** make that project unique.

---

Maven ships with a [default remote repository location](https://repo.maven.apache.org/maven2)

```txt
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.12</version>
  <scope>test</scope>
</dependency>
```

Maven doesn’t just download the JUnit JAR file, it also downloads a POM file for the JUnit dependency. The fact that Maven downloads POM files in addition to artifacts is central to Maven’s support for transitive dependencies.

... transitive deps ... made possible by the fact that the Maven repository stores more than just bytecode; it stores metadata about artifacts.

 When a dependency has a scope of **test**, it will not be available to the **compile** goal of the Compiler plugin. It will be added to the classpath for only the **compiler:testCompile**

> ... page 40

---

`mvn dependency:resolve`, `mvn dependency:tree`, `mvn dependency:analyze`

`-X (--debug)` - maven debug flag

### Part III

Maven version format:

_`<major version>.<minor version>.<incremental version>-<qualifier>`_

- The qualifier exists to capture milestone builds such as alpha and beta releases

If a version contains the string "SNAPSHOT," then Maven will expand this token to a date and time value converted to UTC ... Snapshot versions are used for projects under active development. If your project depends on a software component that is under active development, you can depend on a snapshot release, and Maven will periodically attempt to download the latest snapshot from a repository when you run a build.

If project-a depends on project-b, which in turn depends on project-c, then project-c is considered a transitive dependency of project-a. If project-c depended on project-d, then project-d would also be considered a transitive dependency of project-a.

If a POM does not specify a direct parent using the **parent** element, that POM will inherit values from the Super POM.

Maven assumes that the parent POM is available from the local repository, or available in the parent directory (../pom.xml) of the current project. If neither location is valid, this default behavior may be overridden via the **relativePath** element. E.g., ... prefer a flat project structure ... child project were in a directory named _./project-a_ and the parent project were in a directory named _./a-parent_, you could specify the relative location of _./a-parent_'s POM with:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- ... -->
<project>
  <parent>
    <!-- ... -->
    <relativePath>../a-parent/pom.xml</relativePath>
  </parent>
</project>
```

---

Profiles allow for the ability to customize a particular build for a particular environment; profiles enable portability between different build environments.

- Since profiles override the default settings in a _pom.xml_, the **profiles** element is usually listed as the last element in a _pom.xml_.

- Each profile has to have an **id** element. This id element contains the name that is used to invoke this profile from the command line ... via **-P*profile_id***.

> ...

There are times when you’ll need to create an archive or directory with a custom layout. Such custom archives are called Maven Assemblies.

Using the period character (.) as a separator in property names is a standard practice throughout Maven POMs and profiles.

At the heart of Maven is an Inversion of Control (IoC) container called Plexus.

A Maven plugin is a Maven artifact that contains a Plugin descriptor and one or more Mojos. A Mojo can be thought of as a goal in Maven, and every goal corresponds to a Mojo. (Maven uses the term _Mojo_ bc it is a play on the word Pojo)

## real

The `mavenCentral()` alias means that dependencies are fetched from the [central Maven 2 repository](http://repo1.maven.org/maven2).

```groovy
repositories {
  mavenCentral()
}

// To get a Git project into your build ... request a project JitPack checks out the code,
// builds it and serves the build artifacts (jar, aar).
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}
```

[maven not resolve the source JARs? do it manually:](https://stackoverflow.com/questions/2059431/get-source-jars-from-maven-repository) `mvn dependency:sources` (for all artifacts)

[skip tests when packaging](https://stackoverflow.com/questions/7456006/maven-package-install-without-test-skip-tests) use option `-DskipTests`

[with this plugin, the `repackage` is done automatically after jar/war packaging](https://docs.spring.io/spring-boot/docs/2.1.12.RELEASE/reference/html/build-tool-plugins-maven-plugin.html)
  ```xml
  <build>
      <plugins>
        <plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
          <version>x.x.x</version>
          <executions>
            <execution>
              <goals>
                <goal>repackage</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
      </plugins>
    </build>
  ```

[how to include local lib directory?](https://stackoverflow.com/a/54146663/11844003), [see also](https://stackoverflow.com/a/22300875) and [this](https://stackoverflow.com/questions/10935135/maven-and-adding-jars-to-system-scope)
  ```xml
  <dependency>
      <groupId>anything</groupId>
      <artifactId>anything</artifactId>
      <version>anything</version>
      <scope>system</scope>
      <systemPath>${basedir}/lib/jar-name.jar</systemPath>
  </dependency>
  ```

[`dependencymanagement` and `dependencies`](https://stackoverflow.com/questions/2619598/differences-between-dependencymanagement-and-dependencies-in-maven)
