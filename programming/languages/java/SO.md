# *

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

## generics

- [is `List<Dog>` a subclass of `List<Animal>`?](https://stackoverflow.com/questions/2745265/is-listdog-a-subclass-of-listanimal-why-are-java-generics-not-implicitly-po) keyword: _covariant type_
- [capture conversion](https://stackoverflow.com/questions/4431702/what-is-a-capture-conversion-in-java-and-can-anyone-give-me-examples)

## collections

- [when to use `LinkedList` over `ArrayList`](https://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist-in-java#comment163960_323889)
- [differences between `List.of` and `Arrays.asList`](https://stackoverflow.com/questions/46579074/what-is-the-difference-between-list-of-and-arrays-aslist/46579348#46579348)
- [Immutable vs Unmodifiable collection](https://stackoverflow.com/questions/8892350/immutable-vs-unmodifiable-collection)
- [removing an item whiling iterating through a collection?](https://stackoverflow.com/questions/223918/iterating-through-a-collection-avoiding-concurrentmodificationexception-when-re) `Iterator.remove()` or java 8 `removeIf()`
- [dynamically add items to an array?](https://stackoverflow.com/questions/5061721/how-can-i-dynamically-add-items-to-a-java-array) use list or some array copy func

## end
