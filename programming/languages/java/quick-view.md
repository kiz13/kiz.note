# *

## fundamental

- _Autoboxing_ is the automatic conversion that the Java compiler makes between the primitive types and their corresponding object wrapper classes.

- For strings, the hash codes are derived from their contents.

- The default values are only what Java guarantees when the variable is used as a member of a class.

- A static final variable that is not initialized during declaration can only be initialized in static block.

- The `static` keyword means that a field, method or nested class is related to the _type_ rather than any particular _instance_ of the type.

Assigning a String literal to a String instance, the compiler creates a string object having the string literal that we have provided and assigns it to the provided string instance. (JVM creates a memory location especially for Strings called _String Constant Pool_) Thats why String can be initialized without `new` keyword. But if the object already exist in the memory it does not create a new Object rather it assigns the same old object to the new instance.

- In general, floating point is bad for precise values. It's particularly bad for decimal fractions, because common values (such as 0.1) do not have a binary representation.

- `b/B` If the argument arg is null, then the result is "false". If arg is a boolean or Boolean, then the result is the string returned by String.valueOf(arg). Otherwise, the result is "true", [more info](https://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#syntax)

- `%[arg_index$][flags][width][.precision]conversion` Except for %% and %n, all format specifiers must match an argument.

`'` and `"` aren't interchangeable in Java like they are in some other languages. `'` is for character literals and `"` is for string literals.

- Be **cautious** to the accessor methods that return references to mutable objects.

- downcast/RTTI

- `Class#isInstance` returns true if the specified Object argument is non-null and can be cast to the reference type represented by this Class object

- `getClass().getTypeParameters()` info lost

- `Matcher#group(0)` always return the entire match.

## features

The use of the underscore character in the numeric literals have been legal since Java 7, it have no effect on the values of numeric literals, but can make them much easier to read if used with discretion

Consider adding underscores to numeric literals, whether fixed of floating point, if they contain five or more consecutive digits.

For base ten literals, whether integral or floating point, you should use underscores to separate literals into groups of three digits indicating positive and negative powers of one thousand.

## class & interface

- Overridden methods may throw only the exceptions specified in their base-class versions, or exceptions derived from the base-class exceptions.

- An overriding method can also return a subtype of the type returned by the overridden method. This subtype is called a _covariant return type_.

If you override the `equals()` method, you change the way two objects are equated and Object's implementation of `hashCode()` is no longer valid. Therefore, if you override the `equals()` method, you must also override the `hashCode()` method as well.

- Methods called from constructors should generally be declared final.

- When you give `this` an argument list in a constructor, it makes an explicit call to the constructor that matches that argument list.

If a constructor does not explicitly invoke a superclass constructor, the Java compiler automatically inserts a call to the no-argument constructor of the superclass. If the super class does not have a no-argument constructor, you will get a compile-time error. Object does have such a constructor, so if Object is the only superclass, there is no problem.

The choice of which overloading to invoke is made at compile time; selection among overloaded methods is static.

With abstract classes, you can declare fields that are not static and final, and define public, protected, and private concrete methods. With interfaces, all **fields** are automatically _`public static final`_.

- Final methods are inherited but they are not eligible for overriding.

An empty interface is known as tag or marker interface. E.g., `Serializable`, `EventListener`, and `Remote(java.rmi.Remote)` are tag interfaces.

## I/O

- `InputStream in = null;` The initial null value makes sure that each stream variable contains an object reference before invoking close.

- Supporting all possible line terminators allows programs to read text files created on any of the widely used operating systems.

- By default, a scanner uses white space to separate tokens. White space characters include blanks, tabs, and line terminators.

- An `InputStreamReader` is a bridge from byte streams to character streams: It reads bytes and decodes them into characters.

- `FileWriter` is meant for writing streams of characters. For writing streams of raw bytes, consider using a `FileOutputStream`.

Many file systems use "." notation to denote the current directory and ".." to denote the parent directory. The following examples both include redundancies:

```txt
/home/./joe/foo
/home/sally/../joe/foo
```

The `normalize` method of `Path` removes any redundant elements, which includes any `.` or `directory/..` occurrences. Both of the preceding examples normalize to `/home/joe/foo`.

## collections

- Be aware that **List** behavior changes depending on **equals()** behavior.

- A generic type parameter __erases to its first bound__. type annotation such as `List<T>` are erased to `List`, and ordinary type variables are erased to `Object` unless a bound is specifed.

- using `Array.newInstance()` is the recommended approach for creating arrays in generics.

- `List` actually means "a raw List that holds any Object type", whereas `List<?>` means "a non-raw List of _some specific type_".

- `null` elements are prohibited in `ArrayDeque`

- There can only be one null key in `HashMap`

- The methods `asList` and `subList` return immutable Lists because they are "backed" by the underlying array and list, respectively. If u structurally modify the backing list, u get a concurrent modification exception.
