---
title: Java 8 Features
tags:
  - Java
  - Java 8
---

# Java 8 Features

Java 8 introduced several new features, some of the most significant ones are: Functional Interface and Lambda Expressions, Stream API, Default methods in interface, Optional class.

## Functional Interface

Functional interface is an interface that has only one abstract method. This means that it provides a single behavior or functionality, which can be implemented by any class that implements the interface.

In Java 8 and later versions, functional interfaces are annotated with the `@FunctionalInterface` annotation to indicate that they are intended to be used as functional interfaces. This annotation is optional, but it helps to ensure that the interface has only one abstract method and can be used in functional programming constructs such as lambda expressions and method references.

e.g. Consumer, Supplier, Function, and Predicate


### Default and static methods for interfaces

In Java 8, the concept of default and static methods for interfaces was introduced. These methods provide a way to add new functionality to existing interfaces without breaking backward compatibility. Prior to Java 8, an interface could only contain abstract methods and constants.


### Default vs Static methods

- Default methods are used to add new functionality to an existing interface, while static methods are used to provide utility methods that are not tied to any specific instance of the interface. 
- Default methods can be overridden by any implementing class, while static methods can only be accessed using the interface name.


### Widely Used Functional Interfaces

#### Consumer

The Consumer interface represents an operation that takes a single input and performs some action on it, without returning any result.

??? info "Methods"

    - abstract `accept(T t)`: takes an argument of type T and returns void.
    - `andThen(Consumer<? super T> after)`: allows chaining two Consumer operations together.


#### Supplier

The Supplier interface is used to represent any operation that generates a value without taking any input.

??? info "Methods"

    - abstract `get()`: takes no arguments and returns a result of a specified type.


#### Function

The Function interface represents a function that takes an argument of type `T` and produces a result of type `R`. The argument and result can be different types

??? info "Methods"

    - abstract `apply(T t)`, takes an argument of type T and returns a result of type R.
    - `andThen(Function<? super R, ? extends V> after)`: Returns a composed function that first applies the current function to the input, and then applies the after function to the result.
    - `compose(Function<? super V, ? extends T> before)`: Returns a composed function that first applies the before function to the input, and then applies the current function to the result.
    - `identity()`: Returns a function that always returns its input argument.


#### Predicate

The Predicate interface represents a boolean-valued function of one argument.

??? info "Methods"

    - abstract `test(T t)`: takes an argument of type T and returns a boolean value.
    - `and(Predicate<? super T> other)`: Returns a composed predicate that represents a logical AND of this predicate and another predicate.
    - `or(Predicate<? super T> other)`: Returns a composed predicate that represents a logical OR of this predicate and another predicate.
    - `negate()`: Returns a predicate that represents the negation of this predicate.


## Lambda Expressions

A lambda expression is a concise way to represent an anonymous function that can be passed around as a value. It is used to implement functional interfaces.

``` java
Runnable runnable = () -> System.out.println("Hello, world!");
```

### Method Reference

Java 8 that allows you to refer to an existing method by its name instead of writing a lambda expression. There are four types of method references:

1. Reference to a static method: using the class name followed by the method name.
``` java
// Using lambda expression
Arrays.sort(names, (a, b) -> MyUtils.compareByName(a, b));

// Using method reference
Arrays.sort(names, MyUtils::compareByName);
```

2. Reference to an instance method of an object: using the object reference followed by the method name.
```java
// Using lambda expression
Button button = new Button();
button.setOnAction((event) -> this.handleButtonClick(event));

// Using method reference
Button button = new Button();
button.setOnAction(this::handleButtonClick);
```

3. Reference to an instance method of an arbitrary object of a particular type: using the type name followed by the method name.
``` java
// Using lambda expression
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.sort((a, b) -> a.compareToIgnoreCase(b));

// Using method reference
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.sort(String::compareToIgnoreCase);
```

4. Reference to a constructor: using the new keyword followed by the class name.
``` java
// Using lambda expression
Supplier<List<String>> supplier = () -> new ArrayList<>();

// Using method reference
Supplier<List<String>> supplier = ArrayList::new;
```


## Stream API

The Stream API is used to process collections of objects.
> A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.

##### Main Features

- A stream is not a data structure instead it takes input from the Collections, Arrays or I/O channels.
- Streams don’t change the original data structure, they only provide the result as per the pipelined methods.
- Each intermediate operation is **lazily executed** and returns a stream as a result, hence various intermediate operations can be pipelined. Terminal operations mark the end of the stream and return the result.

### Intermediate Operations vs Terminal Operations

Intermediate operations return a stream as a result and terminal operations return non-stream values like primitive or object or collection or may not return anything. e.g. `filter()`, `map()`, `flatMap()`, `distinct()`, and `sorted()`.

Intermediate operations are ***lazily loaded***. When you call intermediate operations, they are actually not executed. They are just stored in the memory and executed when the terminal operation is called on the stream. e.g. `forEach()`, `reduce()`, `collect()`, and `count()`.

### Each intermediate operation is **lazily executed**

In the below example, the `filter()` method is an intermediate operation. If we run this code without any terminal operations, nothing will be printed to the console:
``` java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Stream<String> filteredNamesStream = names.stream()
    .filter(name -> {
        System.out.println("Filtering " + name);
        return name.startsWith("A");
    });
```


## Optional class

Optional is a ***container object*** used to contain not-null objects. Optional object is used to represent `null` with absent value.

This class has various utility methods to facilitate code to handle values as ‘available’ or ‘not available’ instead of checking null values.

Useful for circumventing handling of `NullPointerException`

---

:material-clock-edit-outline: Edit on Feb 24th, 2023

:material-clock-plus-outline: Created on Oct 13rd, 2022 