# *

- Three kinds of variable are [implicitly declared `final`](https://docs.oracle.com/javase/specs/jls/se8/html/jls-4.html#jls-4.12.4): a field of an interface, a local variable which is a resource of a `try`-with-resources statement, and an exception parameter of a multi-`catch` clause.

- A _constant variable_ is a `final` variable of primitive type or type `String` that is initialized with a [constant expression](https://docs.oracle.com/javase/specs/jls/se8/html/jls-15.html#jls-15.28). A constant expression is typically a `String`, or an arithmetic expression that can be evaluated at compile time.

- method invocation conversion: widening, boxing, unboxing, [..check](http://docs.oracle.com/javase/specs/jls/se8/html/jls-5.html#jls-5.3)

- [illegal forward reference](https://docs.oracle.com/javase/specs/jls/se8/html/jls-8.html#jls-8.3.3)

- [Nested enum types are implicitly static.](http://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html#jls-8.9)

- [initialization order ?](https://docs.oracle.com/javase/specs/jls/se14/html/jls-12.html#jls-12.4.2)

- A Java compiler is encouraged (but not required) to provide a warning if a switch on an enum-valued expression lacks a default label and lacks case labels for one or more of the enum's constants. Also in more [details](https://docs.oracle.com/javase/specs/jls/se8/html/jls-14.html#jls-14.11)

- declared `final`, or be effectively final; be definitely assigned [rules apply to both lambda and inner class](https://docs.oracle.com/javase/specs/jls/se8/html/jls-15.html#jls-15.27.2)

- If only one operand expression is of type String, then string conversion is performed on the other operand to produce a string at run time. [Details](https://docs.oracle.com/javase/specs/jls/se8/html/jls-15.html#jls-15.18.1)

- [java underscore keyword?](https://stackoverflow.com/questions/23523946/underscore-is-a-reserved-keyword)

- [casting conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.5)

- [comparing two enums](https://stackoverflow.com/a/2937561/11844003) because there is only one instance of each `enum` constant, it is permissible to use `==` operator when comparing two object references if it is known that at least one of them refers to an `enum` constant