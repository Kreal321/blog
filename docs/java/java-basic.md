---
title: Java SE Basic
tags:
  - Java
  - Java SE
  - OCA
---

# Java Building Blocks

Topics: Scopes of variables, structure of a Java class, main method, import java packages, platform independence, object orientation, encapsulation

Topics: objects, classes, fields, methods, and comments


## Objects and Classes

In Java programs, classes are the basic building blocks. 

==When you define a class, you are creating a blueprint or a template for an object.== A class contains all the properties (attributes or fields) and behaviors (methods) that an object of that class will have.

To actually use the class, you need to create an instance of that class, which is also called an object. ==An object is a runtime instance of a class in memory.== All the various objects of all the different classes represent the state of your program.

### Class vs Object

{==

A class defines the properties and behaviors that objects of that class will have, while an object is an instance of a class that has its own unique state.

==}

- Classes are the basic building blocks.
- An object is a runtime instance of a class in memory.


### Class vs File

##### Requirements

- You can even put two classes in the same file. When you do so, at most one of the classes in the file is allowed to be public.
- If you do have a public class, it needs to match the filename, including case.

``` java title="Animal.java" linenums="1"
public class Animal {
  private String name;
}
class Animal2 {
}
```


### Fields and Methods

Two primary elements: methods (functions or procedures), and fields (variables). Together these are called the members of the class. Variables hold the state of the program, and methods operate on that
state.

!!! info "What is a method signature?"

    A method signature refers to the part of the method declaration that specifies the method's name, return type, and parameters. In other words, the method signature defines the inputs and outputs of the method.

## Comment

There are three types of comments in Java.

1. single-line comment:
``` java
// comment until end of line
```

2. multiple-line comment / multiline comment
``` java
/* Multiple
* line comment
*/
```

3. Javadoc comment:
``` java
/**
* Javadoc multiple-line comment
* @author Kason
*/
```

??? example "Example: Is it a single-line or a multiline comment?"

    ``` java linenums="1"
    /*
    * // anteater
    */
    // bear
    // // cat
    // /* dog */
    /* elephant */
    /*
    * /* ferret */
    */
    ```

    - The 2nd line `anteater` is in a multiline comment. Everything between /* and */ is part of a multiline comment—even if it includes a single-line comment within it! 

    - The 3rd line `bear` is the basic single-line comment. `cat` and `dog` are also single-line comments. Everything from // to the end of the line is part of the comment, even if it is another type of comment. 

    - The 8th line `elephant` is the basic multiline comment.

    - The 10th line `ferret` doesn’t compile. Everything from the first `/*` to the first `*/` is part of the comment, which means the compiler sees something like this: `/* */ */` And there is an extra */. 


## Java `Main()` Method

Java doesn’t need to create an object to call the main() method. The JVM does this, more or less, when loading the class name given to it.

??? info "What is JVM, JRE or JDK"

    - Java Virtual Machine (JVM)
      It is a software component that executes Java bytecode. When you write Java code and compile it, the resulting `.class` file contains bytecode that can be executed by any JVM, regardless of the underlying hardware or operating system, so ==Java is known as a portable language==.

    - Java Runtime Environment (JRE)
      It is a package that includes the JVM, along with a set of libraries and other components needed to run Java applications. The JRE is used to run Java applications on ==end-user machines==.

    - Java Development Kit (JDK)
      It is a package that includes the JRE, along with additional tools and utilities needed to ==develop Java applications==. These include a compiler, debugger, and various development libraries. 

Here is an example of main() method to print the first two arguments passed in:

``` java title="Example.java" linenums="1"
public class Example {
  public static void main(String[] args) {
    System.out.println(args[0]);
    System.out.println(args[1]);
  } 
}
```

To compile and execute this code

```
$ javac Example.java
$ java Example Hello World
```

### Access Modifier

`public`: declares this method’s level of exposure to potential callers in the program

### `static` keyword

The keyword `static` binds a method to its class so it can be called by just the class name without creating an object.

### return type

The keyword `void` represents the return type. A method that returns no data returns control to the caller silently. In general, it’s good practice to use void for methods that change an object’s state.

### parameter list


### Package Declarations and Imports

- When using wildcards `*`, Every class in the package is available to the program when Java complies it, but it does not import child packages, fields or methods. It only imports classes.
- You might think that including so many classes slows down your program, but it doesn’t. The
compiler figures out what’s actually needed.
- Naming Conflicts: When the class is found in multiple packages, Java gives you the compiler error
    
``` java
import java.util.*;
import java.sql.*; // DOES NOT COMPILE: The type Date is ambiguous
```
    


### Constructors

- the name of the constructor matches the name of the class, and there’s not return type
- you don’t have to code a constructor—the compiler will supply a “do nothing” default constructor for you

### Order of Initialization

- Fields and instance initializer blocks are run in the order in which they appear in the file.
- The constructor runs after all fields and instance initializer blocks have run.

### Numeric Literal

a feature added in Java 7. You can have underscores in numbers to make them easier to read:

``` java
int million2 = 1_000_000;
```

- You can add underscores anywhere except at the beginning of a literal, the end of a literal, right before a decimal point, or right after a decimal point

### Difference between primitive types and reference

- reference types can be assigned null,  but primitive types will give you a compiler error
- primitives do not have methods.
- primitive types have lowercase type names

### Declaring Multiple Variables

- If you want to declare multiple variables in the same statement, they must share the same type declaration and not repeat it.
    
``` java
double d1, double d2; // not legal
double d1, d2; // legal
```
    

### Identifiers

- The name must begin with a letter or the symbol `$` or `_`.
- Subsequent characters may also be numbers.
- You cannot use the same name as a Java reserved word.

### Default Initialization of Variables

- A local variable is a variable defined within a method. Local variables must be initialized before use.
- Variables that are not local variables are known as instance variables or class variables. (or fields). Instance and class variables do not require you to initialize them. As soon as you declare these variables, they are given a default value

---

:material-clock-edit-outline: Edit on Feb 24th, 2023

:material-clock-plus-outline: Created on Oct 13rd, 2022 
