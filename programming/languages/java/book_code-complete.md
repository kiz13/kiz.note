# *

## prerequisite

Upstream activities ... The skills needed to plan a project, create a compelling business case, develop comprehensive and accurate requirements, and create high-quality architectures are ...

Programmers are at the end of the software food chain. The architect consumes the requirements; the designer consumes the architecture; and the coder consumes the design.

... find an error as close as possible to the time at which it was introduced.

## language description

- _C_ was developed at Bell Labs.
- _C++_ was developed at Bell Laboratories (_/ˈla-b(ə-)rə-ˌtȯr-ē/_).
- _Fortran_ stands for FORmula TRANslation.
- The acronym "Perl" stands for Practical Extraction and Report Language.
- The acronym "PHP" originally stood for Personal Home Page but now stands for PHP: Hypertext Processor.
- The acronym BASIC stands for Beginner’s All-purpose Symbolic Instruction Code.
- ...

## B

... paradox implies that you have to "solve" the problem once in order to clearly define it and then solve it again to create a solution that works.

## part 2

### ch5 design in construction

Some kinds of subsystems appear again and again in different systems, e.g., _Business rules_, _User interface_, _Database access_, _System dependencies_.

Coupling describes how tightly a class or routine is related to other classes or routines. The goal is to create classes and routines with small, direct, visible, and flexible relations to other classes and routines, which is known as "loose coupling."

Classes that contain strongly related functionality are described as having strong cohesion.

Design patterns provide the cores of ready-made solutions that can be used to solve many of software’s most common problems.

- Design for Test

...Wiki (that is, a collection of Web pages that can be edited easily by anyone on your project using a Web browser).

### ch6 working classes

- _Be critical of classes that contain more than about seven data members_ The number "7±2" has been found to be a number of discrete items a person can remember while performing other tasks (Miller 1956).
- _Don’t expose member data in public_
- You shouldn’t inherit from a base class unless the derived class truly "is a" more specific version of the base class (Liskov 1988)
- Be suspicious of base classes of which there is only one derived class
- Be suspicious of classes that override a routine and do nothing inside the derived routine
- _Make all data private, not protected_ As Joshua Bloch says, "Inheritance breaks encapsulation" (2001). When you inherit from an object, you obtain privileged access to that object’s protected routines and data. If the derived class really needs access to the base class’s attributes, provide protected accessor functions instead.
- _Initialize all member data in all constructors, if possible_

- Class interfaces should provide a consistent abstraction.
- Containment is usually preferable to inheritance unless you’re modeling an "is a" relationship.

### ch7 high-quality routines

A routine is an individual method or procedure invocable for a single purpose.

- _Don’t differentiate routine names solely by number_
- _Put parameters in input-modify-output order_ Instead of ordering parameters randomly or alphabetically, list the parameters that are input-only first, input-and-output second, and output-only third.
- _Don’t use routine parameters as working variables_
- _Limit the number of a routine’s parameters to about seven_ Seven is a magic number for people’s comprehension. Psychological research has found that people generally cannot keep track of more than about seven chunks of information at once (Miller 1956).
- ... combine the call and the test into one line of code increases the density of the statement and, correspondingly, its complexity.

## part3 variables

- Ideally, declare and define each variable close to where it’s first used

### floating-point numbers

The main consideration in using floating-point numbers is that many fractional decimal numbers can’t be represented accurately using the 1s and 0s available on a digital computer. Nonterminating decimals like 1/3 or 1/7 can usually be represented to only 7 or 15 digits of accuracy.

- Avoid additions and subtractions on numbers that have greatly different magnitudes

## part4 statements

Not a few people don't have not any trouble understanding a nonshort string of nonpositives.

- _In if statements, convert negatives to positives and flip-flop the code in the if and else clauses_

- _Apply DeMorgan’s Theorems to simplify boolean tests with negatives_

DeMorgan’s Theorems let you exploit the logical relationship between an expression and a version of the expression that means the same thing because it’s doubly negated. Then you can write `if ( !(displayOK && printerOK) )` instead of `if (!displayOK || !printerOK)`

- Writing Numeric Expressions in Number-Line Order

- In C-derived languages, put constants on the left side of comparisons? [check also](https://en.wikipedia.org/wiki/Yoda_conditions)

- _Simplify a nested if by retesting part of the condition_

## part5 code improvements

characteristic of software quality:

- ...
- **robustness** The degree to which a system continues to function in the presence of invalid inputs or stressful environmental conditions.
- **Maintainability** The ease with which you can modify a software system to change or add capabilities, improve performance, or correct defects.
- ...
- **Testability** The degree to which you can unit-test and system-test a system; the degree to which you can verify that the system meets its requirements.

## part *

### ch32 self-documenting code

Although useful in some circumstances, endline comments pose several problems. The comments have to be aligned to the right of the code so that they don’t interfere with the visual structure of the code...

- _Avoid endline comments on single lines_ Most endline comments just repeat the line of code, which hurts more than it helps
- _Avoid endline comments for multiple lines of code_
- _Use endline comments to annotate data declarations_
- _Avoid using endline comments for maintenance notes_
- _Use endline comments to mark ends of block_

Focus paragraph comments on the why rather than the how, e.g.,

```txt
// if establishing a new account
if ( accountFlag == 0 ) ...
```

Don’t document bad code—rewrite it

Comment the end of each control structure

Document the source of algorithms that are used

IEEE

## ch33.7 laziness

Writing a tool to do the unpleasant task so that you never have to do the task again
