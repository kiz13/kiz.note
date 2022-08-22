# move it

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

skip tests? check [official docs](https://maven.apache.org/surefire/maven-surefire-plugin/examples/skipping-tests.html)

the default _plugin:goal_ of lifecycle binding for the _test_ phase on packaging `jar` or `war` is `surefire:test` check [official docs](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#built-in-lifecycle-bindings)

[List of predefined Maven properties](https://github.com/cko/predefined_maven_properties/blob/master/README.md)
