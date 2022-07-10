# *

## table of contents

- [why](#why)
- [primitives](#primitives)
- [classes](#classes)
- [date and time](#date-and-time)
- [generics](#generics)
- [collections](#collections)
- [lambdas](#lambdas)
- [files](#files)
- [threads](#threads)
- [db](#db)
- [api caller](#api-caller)
- [strange thoughts](#strange-thoughts)

## why

- why there are duplicated methods `empty()` and `isEmpty()` in the `Stack` class? [for the sake of backward compatibility](https://stackoverflow.com/a/24987559/11844003), in JDK 1.2, _Collection_ framework was added to JDK, and some methods were named in a different convention.

- why the code below does not compile:

  ```text
  Animal a = new Dog();
  if (a instanceof Dog){
      a.bark();
  }
  ```

  [this is a feature of statically-typed language](https://stackoverflow.com/questions/898909/is-it-possible-to-call-subclasses-methods-on-a-superclass-object/898937#898937), variables are assigned a type ahead of time, and checked at compile-time to see that the types match.

- why using `Objects.requireNonNull`? [Because you can make things explicit by doing so.](https://stackoverflow.com/a/45632962/11844003)
  Kirill Rakhman's comment added: You can make your code more compact by writing `this.bar = Objects.requireNonNull(bar, "bar must not be null");`

- Why are the Level.FINE logging messages not showing? [Loggers only log the message, i.e. they create the log records (or logging requests).](https://stackoverflow.com/questions/6315699/why-are-the-level-fine-logging-messages-not-showing/6315736#6315736) They do not publish the messages to the destinations, which is taken care of by the Handlers. Setting the level of a logger, only causes it to create log records matching that level or higher.

- Why am I getting a NoClassDefFoundError in Java? [While it's possible that this is due to a classpath mismatch between compile-time and run-time, it's not necessarily true.](https://stackoverflow.com/a/5756989/11844003)

- the code below does not compile

  ```text
  List<? extends Parent> list = ...
  Parent p = factory.get();   // returns concrete implementation
  list.set(0, p);
  ```

  TL;DR | PECS - "Producer - Extends, Consumer - Super". [Your List is a consumer of Parent objects.](https://stackoverflow.com/a/3716965/11844003)

  detailed | The meaning of `List<? extends Parent>` is "This is a list of some type which extends Parent. We don't know which type - it could be a `List<Parent>`, a `List<Child>`, or a `List<GrandChild>`." That makes it safe to fetch any items out of the `List<T>` API and convert from `T` to `Parent`, but it's not safe to call in to the `List<T>` API converting from `Parent` to `T`... because that conversion may be invalid. - [Jon Skeet's answer](https://stackoverflow.com/a/3716945/11844003)

  see also | [irreputable's answer](https://stackoverflow.com/a/3720780/11844003)

- java.lang.UnsupportedClassVersionError: unsupported major.minor version 52.0? [check you IDE settings](https://stackoverflow.com/a/35866015/11844003), by the way

  - java version: 8, classfile major version: 52
  - java version: 13, classfile major version: 55

- [Why are all methods in an `interface` definition implicitly `public`? Why does it not allow a `protected` method?](https://stackoverflow.com/questions/5376970/protected-in-interfaces)

- Access restriction: The type 'BASE64Decoder' is not API? All sun.* and com.sun.* packages are private to a Java implementation. Any future release of Java may alter them, possibly in ways which may break application code that relies on them. [source](https://stackoverflow.com/a/44271082/11844003)

- [why closing the resource](https://stackoverflow.com/questions/18002896/is-closing-the-resources-always-important) and [what if I'm not doing so](https://stackoverflow.com/questions/39619472/what-happens-if-i-dont-close-things-like-channels-streams-and-remote-connectio)

## primitives

- [safely casting long to int](https://stackoverflow.com/questions/1590831/safely-casting-long-to-int-in-java) `Math.toIntExact` with Java 8; or manually check `l < Integer.MIN_VALUE || l > Integer.MAX_VALUE`

- Cleanest way to toggle a boolean variable? use _bitwise XOR_ `theBoolean ^= true;` [Fewer keystrokes if your variable is longer than four letters](https://stackoverflow.com/a/224380/11844003)

## classes

- Is Java "pass-by-reference" or "pass-by-value"? [Java is always **pass-by-value**.](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value)

- [`System.getProperty("java.class.path")` 默认情况下可能会沿着这个顺序来找](https://www.zhihu.com/question/39523033/answer/81750667)

- how to use comparator? [source](https://stackoverflow.com/a/24227670/11844003)

  ```text
  Collections.sort(people,new Comparator<Person>(){
    @Override
    public int compare(final Person lhs,Person rhs) {
      //  return 1 if rhs should be before lhs 
      //  return -1 if lhs should be before rhs
      //  return 0 otherwise (meaning the order stays the same)
    }
  });
  ```

- [how to do comparing by two fields](https://stackoverflow.com/a/4805676/11844003)

- public, protected, package-private and private access modifiers explanation? [aioobe's answer](https://stackoverflow.com/a/33627846/11844003), by the way, see also the comments (the illustration table in the answer contains red and green colors, which are not well distinguishable by color-blind people)

- Static imports are used to reference static methods and fields directly. For types, regular imports are the way to go, also for static nested types. [from the answer to a (maybe) bad question](https://stackoverflow.com/a/37656958/11844003)

## date and time

### java 8 time

- [`java.time.LocalDate` and `java.util.Date` conversion](https://stackoverflow.com/questions/33066904/localdate-to-java-util-date-and-vice-versa-simplest-conversion)

- [get the current date time](https://stackoverflow.com/questions/5175728/how-to-get-the-current-date-time-in-java)

- [string to date conversion](https://stackoverflow.com/questions/4216745/java-string-to-date-conversion)

- [format date time](https://stackoverflow.com/questions/23069370/format-a-date-using-the-new-date-time-api)

- [sort date time](https://stackoverflow.com/questions/43679040/how-to-sort-date-in-java)

- [get first and last day of month](https://stackoverflow.com/questions/22223786/get-first-and-last-day-of-month-using-threeten-localdate) `LocalDate#withDayOfMonth` or `java.time.temporal.TemporalAdjusters.firstDayOfMonth`

## generics

- [is `List<Dog>` a subclass of `List<Animal>`?](https://stackoverflow.com/questions/2745265/is-listdog-a-subclass-of-listanimal-why-are-java-generics-not-implicitly-po) keyword: _covariant type_

- [capture conversion](https://stackoverflow.com/questions/4431702/what-is-a-capture-conversion-in-java-and-can-anyone-give-me-examples)

## collections

- [when to use `LinkedList` over `ArrayList`](https://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist-in-java#comment163960_323889)

- [differences between `List.of` and `Arrays.asList`](https://stackoverflow.com/questions/46579074/what-is-the-difference-between-list-of-and-arrays-aslist/46579348#46579348)

- [Immutable vs Unmodifiable collection](https://stackoverflow.com/questions/8892350/immutable-vs-unmodifiable-collection)

- [removing an element whiling iterating through a collection?](https://stackoverflow.com/questions/223918/iterating-through-a-collection-avoiding-concurrentmodificationexception-when-re) `Iterator.remove()` or java 8 `removeIf()`

- [remove elements while iterating - better approaches](https://stackoverflow.com/questions/10431981/remove-elements-from-collection-while-iterating) Shebla Tsama wrote an Old Timer Favorite

- [dynamically add items to an array?](https://stackoverflow.com/questions/5061721/how-can-i-dynamically-add-items-to-a-java-array) use list or some array copy func

- [convert a collection to an array?](https://stackoverflow.com/questions/9572795/convert-list-to-array-in-java)

- [copy list](https://stackoverflow.com/questions/689370/how-to-copy-java-collections-list)

## lambdas

- use lambda or method references? [choose the more readable one](https://stackoverflow.com/questions/24487805/lambda-expression-vs-method-reference)

- ["continue" within a foreach loop](https://stackoverflow.com/questions/32654929/move-to-next-item-using-java-8-foreach-loop-in-stream) using `return` would just work (it stops executing the current iteration)

## files

- how do I cause Word to open and edit a file? [source](https://stackoverflow.com/a/6871727/11844003)

  ```java
  import java.awt.Desktop;
  import java.io.File;
  import java.io.IOException;
  
  public class Test {
    public static void main(String[] a) {
      try {
        if (Desktop.isDesktopSupported()) {
          Desktop.getDesktop().open(new File("b:\\a.doc"));
        }
      } catch (IOException ioe) {
        ioe.printStackTrace();
      }
    }
  }
  ```

- delete the temporary file after closing that file? [source](https://stackoverflow.com/a/876876/11844003)

  ```text
  if (!temp.delete()) {
    // wasn't deleted for some reason, delete on exit instead
    temp.deleteOnExit();
  }
  ```

- `deleteOnExit` not deleting the created temporary file? [Make sure that whatever streams are writing to the file are closed.](https://stackoverflow.com/a/28751091/11844003)

- (using java api) how to find out the jdk version a class file is compiled for? [check](https://stackoverflow.com/a/1293372/11844003) by the way, you can use the `file` command to quickly get the version.

- Does `class.getResource("." /*dot*/)` have any special meaning? It will (in some cases) return a URL pointing to the directory that class file is in. It does not work with all JVMs. [source](https://stackoverflow.com/a/24307830/11844003)

- [get resource?](https://stackoverflow.com/questions/16570523/getresourceasstream-returns-null) `Your.class.getResourceAsStream("/dir/file.ass")`

- [if your resource is not in the same package as the class you are trying to access the resource from, then you have to give it relative path starting with `'/'`](https://stackoverflow.com/a/2103625/11844003)

## threads

- [where to create executorservices and when to close them?](https://stackoverflow.com/questions/43174685/where-to-create-executorservices-and-when-to-close-them)

- [when and how should i use a threadlocal variable](https://stackoverflow.com/questions/817856/when-and-how-should-i-use-a-threadlocal-variable/818364#818364)

- [final field freeze on object reachable from final fields???](https://stackoverflow.com/questions/4449252/java-final-field-freeze-on-object-reachable-from-final-fields)

- [Executors newCachedThreadPool vs newFixedThreadPool?](https://stackoverflow.com/questions/949355/executors-newcachedthreadpool-versus-executors-newfixedthreadpool)

- [what are the default settings of CompletableFuture's threadpool](https://stackoverflow.com/questions/62929715/java-completablefuture-threadpool-used)

- [FixedThreadPool vs CachedThreadPool: the lesser of two evils?](https://stackoverflow.com/questions/17957382/fixedthreadpool-vs-cachedthreadpool-the-lesser-of-two-evils)

## db

[how to write sql updating a blob](https://stackoverflow.com/questions/8348427/how-to-write-update-oracle-blob-in-a-reliable-way)

[stick with java time](https://stackoverflow.com/questions/22470150/how-to-get-a-java-time-object-from-a-java-sql-timestamp-without-a-jdbc-4-2-drive)

## api caller

- [make http post request using okhttp without a request body?](https://stackoverflow.com/questions/35743516/how-to-make-okhttp-post-request-without-a-request-body) `RequestBody.create(null, new byte[0])`

- [convert inputstream to bytearray](https://stackoverflow.com/questions/1264709/convert-inputstream-to-byte-array-in-java)

  1. java 9 `InputStream.readAllBytes()`
  2. Apache Commons IO `IOUtils.toByteArray(inputStream)`

- org.xml.sax.SAXParseException: Premature end of file? [the xml may be truncated to a zero length file](https://stackoverflow.com/a/14810069/11844003), the stream is read once the file offset position counter is moved to the end of file

- Can't find `@Nullable` inside `javax.annotation.*`? [include some dep](https://stackoverflow.com/a/19031259/11844003)

  ```text
  <dependency>
    <groupId>com.google.code.findbugs</groupId>
    <artifactId>jsr305</artifactId>
    <version>${g.findbugs.version}</version>
  </dependency>
  ```

- [upgrading to okhttp 4](https://square.github.io/okhttp/changelogs/upgrading_to_okhttp_4/)

## strange thoughts

- [intercept logback logging?](https://stackoverflow.com/questions/29076981/how-to-intercept-slf4j-with-logback-logging-via-a-junit-test)
- [dynamically generate a string used in an annotation?](https://stackoverflow.com/questions/10636201/java-annotations-values-provided-in-dynamic-manner)
- [switch over type java 8?](https://stackoverflow.com/questions/29570767/switch-over-type-in-java)
- [use `goto` properly?](https://stackoverflow.com/questions/26430630/how-to-use-goto-statement-correctly)
- [does use of final keyword improve the performance?](https://stackoverflow.com/questions/4279420/does-use-of-final-keyword-in-java-improve-the-performance)
- [specify character encoding of a string?](https://stackoverflow.com/questions/17907727/is-there-a-way-to-specify-the-character-encoding-to-the-java-lang-stringbuilder)
- [print the extended ASCII code?](https://stackoverflow.com/questions/22273046/how-to-print-the-extended-ascii-code-in-java-from-integer-value/22274879#22274879)
- [why initialize this byte array to 1024](https://stackoverflow.com/questions/6557799/why-initialize-this-byte-array-to-1024/6558174)

## end
