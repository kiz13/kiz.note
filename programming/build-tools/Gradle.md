# a build automation tool

## gradle in action (book quick check)

In `AbstractTask`'s `execute` method:

```groovy
closure.setDelegate(task);
closure.setResolveStrategy(Closure.DELEGATE_FIRST);
```

By default, Gradle executes the task in alphanumeric order.

One of the conventions the _Java plugin_ introduces is the location of the source code. By default, the plugin searches for production source code in the directory `src/main/java`.

The `setting.gradle` (the default name) file declares the configuration required to instantiate the project's hierarchy.

`gradle -q (quite)`

dependency report: `$ gradle dependencies`

---

### Migrating dependencies

Gradle distinguishing between the dependencies required to build a module and the dependencies required to build a module that depends on it. Maven makes no such distinction, so published POMs typically include dependencies that consumers of a library don't actually need.

the `api` configuration is only available to projects that specifically apply the _Java Library Plugin_

Dependencies required for test compilation should be declared against the `testImplementation` configuration. Those that r only required for running the tests should use `testRuntimeOnly`.

> War plugin adds `providedCompile` and `providedRuntime` dependency configurations. These behave slightly differently from `compileOnly` and simply ensure that those dependencies aren't packaged in the WAR file. However, the dependencies are included on runtime and test runtime classpaths ...

The import scope is mostly used within `<dependencyManagement>` blocks and applies solely to POM-only publications. See also [Using bills of material](https://docs.gradle.org/current/userguide/migrating_from_maven.html#migmvn:using_boms)

U can also specify a regular dependency on a POM-only publication. In this case, the dependencies declared in that POM r treated as normal transitive dependencies of the build.

Imagine u want to use the `groovy-all` POM for ur tests. Its a POM-only publication that has its own dependencies listed inside a `<dependencies>` block. The result of this will be that all `compile` and `runtime` scope dependencies in the `groovy-all` POM get added to the test runtime classpath, which only the `compile` scope dependencies get added to the test compilation classpath. Dependencies with other scopes will be ignored.

---

### Using bills of materials (BOMs)

Maven allows u to share dependency constraints by defining dependencies inside a `<dependenciesManagement>` section of a POM file that has a packaging type of `pom`. This special type of POM(a BOM) can then be imported into other POMs so that u have consistent library versions across ur projects.

Gradle can use such BOMs for the same purpose, using ... `platform()` ... it'll ignore any dependencies declared in the `<dependencies>` block.

---

### [Build Environment](https://docs.gradle.org/current/userguide/build_environment.html)

When configuring Gradle behavior u can use: (listed in order of highest to lowest precedence):

- **Command-line** flags such as `--build-cache`.
- **System properties** such as `systemProp.http.proxyHost=somehost.org` stored in a `gradle.properties` file.
- **Gradle properties** such as `org.gradle.caching=true` that r typically stored in a `gradle.properties` file in a project root dir or `GRADLE_USER_HOME` environment variable.
- **Environment variables** such as `GRADLE_OPTS` sourced by the environment that executes Gradle

[Compatibility matrix](https://docs.gradle.org/current/userguide/compatibility.html)

---

Gradle runs on the JVM and uses serveral supporting libraries that require a non-trivial initialization time.

To get a list of running Gradle Daemons and their statues use the `--status` command.

Initialization scripts(a.k.a _init scripts_) r similar to other scripts but r run before the build starts. Several possible uses:

- supply personal info about the user that is required by the build, such as repository or database authentication credentials.
- Define machine specific details, such as where JDKs r installed
- Register build listeners.
- Register build loggers. U might wish to customize how Gradle logs the events that it generates.

Several ways to use an init script: [hmm....](https://docs.gradle.org/current/userguide/init_scripts.html#sec:using_an_init_script)

## SO

[ways to add gradle support to intellij projects?](https://stackoverflow.com/questions/26745541/best-way-to-add-gradle-support-to-intellij-project?rq=1)

[method leftshift not found](https://stackoverflow.com/questions/55793095/could-not-find-method-leftshift-for-arguments-after-updating-studio-3-4)

[difference between `implementation` and `compile`?](https://stackoverflow.com/questions/44493378/whats-the-difference-between-implementation-and-compile-in-gradle)

[unknown property `mainclass`?](https://stackoverflow.com/questions/61976771/could-not-set-unknown-property-mainclass-for-extension-application)

[apply android gradle plugin using new syntax](https://stackoverflow.com/questions/43128340/apply-android-gradle-plugin-using-new-syntax)

[differences between `implementation`, `api` and `compile`](https://stackoverflow.com/questions/44493378/whats-the-difference-between-implementation-api-and-compile-in-gradle)
