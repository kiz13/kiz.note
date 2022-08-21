# 🍃

A [preamble](https://www.vocabulary.com/dictionary/preamble) is a brief introduction to a speech

- 使用 `@Bean` 定義 Bean 的時候, 預設會使用方法的名稱作為 Bean 的名稱
- `@Autowired` If a class only declares a single constructor to begin with, it will always be used, even if not annotated. An annotated constructor does not have to be public.
- `PropertySourcesPlaceholderConfigurer`

  ```text
    // 該實例是 Spring 本身需要的 Bean
    // @Configuration 標註的類別在載入之後，生成實例之前，就
    // 必須能取得 PropertySourcesPlaceholderConfigurer 實例
    // 因而 Spring 在這部份是透過 static 方法來解決
    @Bean
    public static PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
      return new PropertySourcesPlaceholderConfigurer();
    }
  ```

- `MappingJackson2HttpMessageConverter`
- `@ResponseBody` automatically handles the serialization of data passed into the service as JSON(default)

## discussions

@Autowired HttpServletRequest vs passing as parameter?

> [Both are ok](https://stackoverflow.com/a/48575275/11844003) Spring stores the `HttpServletRequest` into a `ThreadLocal` type variable, which is a thread-safe map that keeps `HttpServletRequest` in the current thread context.

validation in controller or service?

> [In the service.](https://stackoverflow.com/a/46480007/11844003) Controllers should be light-weight and pass on requests.

return `ResponseEntity` vs return pojo

> [Returning just a bean is fine but doesn't give you much flexibility.](https://stackoverflow.com/a/49673748/11844003) `ResponseEntity<T>` represents the **entire HTTP response**.

Where does the `@Transactional` annotation belong?

> [I think transactions belong on the service layer. It's the one that knows about units of work and use cases.](https://stackoverflow.com/a/1079125/11844003)

[am I supports to use a service layer?](https://stackoverflow.com/questions/9633498/do-i-really-need-a-service-layer)

> ya outa ur goddamn mind?

about dependency injection, [he said](https://stackoverflow.com/questions/39890849/what-exactly-is-field-injection-and-how-to-avoid-it#comment67070350_39891473)

> Very ugly constructor with 8 dependencies is actually awesome as it is a red flag that something is wrong, class has too many dependencies and is probably violating single responsibility principle and should be refactored.

[best practice to handle duplicate entry](https://softwareengineering.stackexchange.com/questions/350996/what-will-be-the-best-practice-to-handle-duplicate-entry-in-db-in-spring-mvc-th)

[performance impact of using aop](https://stackoverflow.com/questions/433475/performance-impact-of-using-aop)

[profile via spring and profile via build tool](https://stackoverflow.com/questions/66103584/what-is-the-difference-between-profiles-via-spring-or-via-a-build-tool-like-mave)

[create bean with abstract class](https://stackoverflow.com/a/48440850/11844003)

## application configuration

[use spring profiles in SpringBoot (mkyong)](https://mkyong.com/spring-boot/spring-boot-profile-based-properties-and-yaml-example/)

[spring doc (swagger)](https://springdoc.org/properties.html)

[configure hikaricp with jtds](https://stackoverflow.com/questions/42247864/configure-hikaricp-in-spring-boot-with-jtds)

[multiple datasource with `jdbc-url`](https://stackoverflow.com/questions/49088847/after-spring-boot-2-0-migration-jdbcurl-is-required-with-driverclassname)

[setting custom properties in a spring-boot way](https://stackoverflow.com/a/32066380)

SpringBoot uses [relaxed rules](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config.typesafe-configuration-properties.relaxed-binding) for binding `Environment` properties to `@ConfigurationProperties` beans

After Spring Boot 2.0 migration: jdbcUrl is required with driverClassName? [credits](https://stackoverflow.com/a/49141541) Spring Boot 2.x changed default JDBC connection pool from Tomcat to HikariCP. Here comes incompatibility, because Hikari has no url property (but does have a jdbcUrl property), so you must change the property key from `xxx.url` to `xxx.jdbc-url`

[springboot and prometheus_grafana](https://refactorfirst.com/spring-boot-prometheus-grafana)

### logging

[configure logger](https://stackoverflow.com/questions/30571319/spring-boot-logging-pattern)

default log location? [loggers are pre-configured to use console output](https://stackoverflow.com/a/31939886/11844003)

[configure logging file](https://stackoverflow.com/questions/39158191/default-logging-file-for-spring-boot-application)

## rest controller

- [annotations that receive form data](https://stackoverflow.com/questions/24551915/how-to-get-form-data-as-a-map-in-spring-mvc-controller)

- [receive form data and file](https://stackoverflow.com/questions/51938056/spring-boot-upload-form-data-and-file)

- [receive multipart form data?](https://stackoverflow.com/questions/57802148/how-can-i-receive-multipart-form-data-in-spring-mvc-controller)

  ```java
  class Ass {
    @RequestMapping(path = "/putRequest",
        produces = { "application/json" },
        consumes = { "multipart/form-data" },
        method = RequestMethod.PUT)
    public ResponseEntity<SuccessDto> requestPut(@Valid @RequestParam(value = "commit", required = false, defaultValue="false") Boolean commit, @Valid @RequestPart("file") MultipartFile file) {
      return new ResponseEntity<>(HttpStatus.OK);
    }
  }
  ```

- [request with two forward slashes failed?](https://stackoverflow.com/questions/48453980/spring-5-0-3-requestrejectedexception-the-request-was-rejected-because-the-url)

- [return file having outputstream?](https://stackoverflow.com/questions/27741283/return-file-from-spring-controller-having-outputstream) Just note, with the Byte-streams, you keep everything in-memory.
  - get the `OutputStream` from the `HttpServletResponse` and write something to it
  - return `ResponseEntity` with `InputStreamResource` (totally Spring)

- to map the date formatted value (received from form) to the `java.time.LocalDate` entity field, you should add `@DateTimeFormat(pattern = "what")` to it. [source](https://stackoverflow.com/questions/43079923/localdate-in-form)

- [use `LocalDateTime` as `RequestParam`?](https://stackoverflow.com/questions/40274353/how-to-use-localdatetime-requestparam-in-spring-i-get-failed-to-convert-string) add `@DateTimeFormat` to it

### jackson

- [jackson ignore null field during serialization](https://stackoverflow.com/questions/11757487/how-to-tell-jackson-to-ignore-a-field-during-serialization-if-its-value-is-null) `mapper.setSerializationInclusion(Include.NON_NULL);`

- [configure jackson `objectmapper`](https://stackoverflow.com/a/32842962/11844003)

- [ignore unmapped fields](https://stackoverflow.com/questions/5455014/ignoring-new-fields-on-json-objects-using-jackson)
  - `@JsonIgnoreProperties(ignoreUnknown = true)`
  - `ObjectMapper#configure(Deserializationxxx.yyy)`

## dao

- The default constructor exists only for the sake of JPA

- [use beanpropertyrowmapper without matching column names?](https://stackoverflow.com/questions/9469586/spring-how-to-use-beanpropertyrowmapper-without-matching-column-names)

- [insert "null primitive" in jdbc?](https://stackoverflow.com/a/17657152/11844003) use `setObject` instead

- [jpa not support java time instant](https://stackoverflow.com/questions/49309076/why-jpa-does-not-support-java-time-instant)

- [using `like` in prepared statement](https://stackoverflow.com/questions/8247970/using-like-wildcard-in-prepared-statement) `ps.setString(1, "%" + sb + "%")`

- [org.hibernate.QueryException: Space is not allowed after parameter prefix ':' ?](https://stackoverflow.com/a/54117834/11844003) escape the assignment operator in the native query like `"xxx \\:="` (p.s. but this leads to a problem, check the `idea.log`) see [also](https://stackoverflow.com/questions/9460018/how-can-i-use-mysql-assign-operator-in-hibernate-native-query)

- com.mysql.cj.jdbc.exceptions.CommunicationsException [check this](https://stackoverflow.com/questions/69394504/connection-com-mysql-cj-jdbc-connectionimplee48bb3-marked-as-broken-because-of) and [this](https://stackoverflow.com/questions/11301707/attempt-to-reconnect-jdbc-pool-datasource-after-database-restarts)

- [(v2ex) Hikari 连接池，连接超时被关闭](https://www.v2ex.com/t/688926#r_9231887)

- [can I do validation using Spring Data JDBC?](https://stackoverflow.com/a/62403357/11844003) Spring Data JDBC does no validation. (p.s. Validation should happen in the constructor so that it is not possible to create an invalid object in the first place.)

- [hikari, `Thread starvation or clock leap detected`](https://stackoverflow.com/questions/38703876/log-warning-thread-starvation-or-clock-leap-detected-housekeeper-delta-springh) If you run the app locally and the computer went to sleep it happens.

- [`ChainedTransactionManager`](https://stackoverflow.com/questions/48954763/spring-transactional-with-a-transaction-across-multiple-data-sources)

- `keyHolder.getKey()` returns `null`? set the second parameter to `Statement.RETURN_GENERATED_KEYS` in `connection.prepareStatement()` [credit](https://stackoverflow.com/a/53656226/11844003)

### comparison

- difference between hibernate and spring data jpa? [Hibernate is a JPA implementation, while Spring Data JPA is a JPA data access abstraction. Spring Data JPA cannot work without a JPA provider](https://stackoverflow.com/a/23863416)

- [namedparameterjdbctemplate vs jdbctemplate](https://stackoverflow.com/questions/16359316/namedparameterjdbctemplate-vs-jdbctemplate)

- [spring data jdbc jpa etc](https://stackoverflow.com/questions/42470060/spring-data-jdbc-spring-data-jpa-vs-hibernate)

- [jpa / jdbc](https://stackoverflow.com/questions/4406310/why-use-jpa-instead-of-writing-the-sql-query-using-jdbc)

## old world

- [war file: could not find or load main class?](https://stackoverflow.com/a/51841838/11844003) try packaging the WAR with maven plugin

  ```shell
  mvn clean package spring-boot:repackage
  ```

- to use the tags in the `xxx` schema, you need to have the xx preamble at the top of the Spring XML configuration file

- In most cases, however, application-level beans should not need to interact with the [Environment](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/core/env/Environment.html) directly but instead may have to have ${} property values replaced by a property placeholder configurer such as `PropertySourcesPlaceholderConfigurer`, which itself is EnvironmentAware and as of Spring 3.1 is registered by default when using `<context:property-placeholder/>`

- [change order the bean def in xml file to override the dup bean](https://stackoverflow.com/questions/5849192/springs-overriding-bean)

- [spring with java config (no xml)](https://stackoverflow.com/questions/28293400/spring-root-and-servlet-context-with-java-config)

- In general your root configuration should scan for everything but `@Controllers` and your web configuration should only detect `@Controllers`

- [url pattern for servlet filters](https://stackoverflow.com/questions/35434978/how-to-specify-url-pattern-for-servlet-filters-in-webapplicationinitializer)

- [configure context programmatically without web xml?](https://stackoverflow.com/questions/38348608/how-to-configure-context-param-programmatically-without-web-xml)

- [servlet url mapping](https://stackoverflow.com/a/14225540)

- `/` and `/*` url pattern differences, [check](https://stackoverflow.com/questions/4140448/difference-between-and-in-servlet-mapping-url-pattern)

## helping links

- [開源框架：Spring](https://openhome.cc/Gossip/Spring/index.html)
- [programmatic transaction management](https://docs.spring.io/spring-framework/docs/3.0.0.M3/reference/html/ch11s06.html)
- [spring boot with docker](https://spring.io/guides/gs/spring-boot-docker/)
