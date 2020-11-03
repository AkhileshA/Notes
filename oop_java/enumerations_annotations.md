- [Introduction](#introduction)
  - [Enumerations](#enumerations)
    - [Java Enumerations Are Class Types](#java-enumerations-are-class-types)
  - [Type Wrappers](#type-wrappers)
    - [Character](#character)
    - [Boolean](#boolean)
    - [The Numeric Type Wrappers](#the-numeric-type-wrappers)
  - [Annotations](#annotations)
    - [Annotation Basics](#annotation-basics)

# Introduction

## Enumerations

In its simplest form, an enumeration is a list of named constants that define a
new data type and its legal values. Thus, an enumeration object can hold only a
value that was declared in the list.

even though enumerations define a class type, you do not
instantiate an enum using new. You declare and use an enumeration
variable in much the same way as you do one of the primitive types.

### Java Enumerations Are Class Types

Although you don’t
instantiate an enum using new, it otherwise has much the same capabilities as
other classes.For example, you can give them constructors, add
instance variables and methods, and even implement interfaces. 

It is important to understand that each enumeration constant is an object of
its enumeration type. Thus, when you define a constructor for an enum, the
constructor is called when each enumeration constant is created. Also, each
enumeration constant has its own copy of any instance variables defined by the
enumeration.

You can obtain a value that indicates an enumeration constant’s position in
the list of constants. This is called its ordinal value, and it is retrieved by
calling the ordinal( ) method, shown here:

```java
final int ordinal( )
```

You can compare the ordinal value of two constants of the same
enumeration by using the compareTo( ) method.

```java
final int compareTo(enum-type e)
```

## Type Wrappers

The type wrappers are Double, Float, Long, Integer, Short, Byte,
Character, and Boolean. These classes offer a wide array of methods that
allow you to fully integrate the primitive types into Java’s object hierarchy.

### Character

it is recommended that you use the static method valueOf( ) to obtain a Character object. It is shown here:

```java
static Character valueOf(char ch)
```

To obtain the char value contained in a Character object, call charValue( ),
shown here:

```java
char charValue( )
```

### Boolean

it is recommended that you use the static method valueOf(
) to obtain a Boolean object. It has the two versions shown here:

```java
static Boolean valueOf(boolean boolValue)
static Boolean valueOf(String boolString)
```
To obtain a boolean value from a Boolean object, use booleanValue( ),
shown here:

```java
boolean booleanValue( )
```

It returns the boolean equivalent of the invoking object.

### The Numeric Type Wrappers

By far, the most commonly used type wrappers are those that represent
numeric values. These are `Byte`, `Short`, `Integer`, `Long`, `Float`, and `Double`. All
of the numeric type wrappers inherit the abstract class Number. Number
declares methods that return the value of an object in each of the different
number formats. These methods are shown here:

```java
byte byteValue( )
double doubleValue( )
float floatValue( )
int intValue( )
long longValue( )
short shortValue( 
```

it is recommended that you use one of the
valueOf( ) methods to obtain a wrapper object. The valueOf( ) method is a
static member of all of the numeric wrapper classes and all numeric classes
support forms that convert a numeric value or a string into an object. For
example, here are two of the forms supported by Integer:

```java
static Integer valueOf(int val)
static Integer valueOf(String valStr) throws NumberFormatException
```

## Annotations

Java provides a feature that enables you to embed supplemental information
into a source file. This information, called an annotation, does not change the
actions of a program. Thus, an annotation leaves the semantics of a program
unchanged. However, this information can be used by various tools during both
development and deployment.

### Annotation Basics

An annotation is created through a mechanism based on the interface. 