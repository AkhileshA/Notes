# Introduction

It is important to state at the outset that Java is a strongly typed language.

## The Primitive Types

Java defines eight primitive types of data: byte, short, int, long, char, float,
double, and boolean.

### Integers

Java defines four integer types: byte, short, int, and long. Java does not support unsigned, positiveonly
integers.

1. **byte:** range of 8 bits.
1. **short:** range of 16 bits.
1. **int:**  range of 32 bits.
1. **long:** range of 64 bits.

- Octal values are denoted in Java by a leading zero.
Normal decimal numbers cannot have a leading zero.
- You signify a hexadecimal constant with a leading zero-x, (0x
or 0X).
- You can also specify integer literals using binary. To do so, prefix the value
with 0b or 0B.
- You can embed one or more underscores in an integer literal. Doing so
makes it easier to read large integer literals

### Floating point numbers

Java implements the standard (IEEE–754) set of floating-point types and operators.There are two kinds of floatingpoint
types, float and double, which represent single- and double-precision
numbers, respectively. 

1. **float:** : width - 32 bits.
1. **double:** : width - 64 bits.

- All transcendental math functions, such as sin( ), cos( ), and sqrt( ), return
double values.
- Floating-point literals in Java default to double precision. To specify a float
literal, you must append an F or f to the constant.


### Characters

In Java, the data type used to store characters is char. Its a Unicode representation. At
the time of Java’s creation, Unicode required 16 bits.ASCII character set
occupies the first 127 values in the Unicode character set.

### Booleans

Java has a primitive type, called boolean, for logical values. It can have only
one of two possible values, true or false. This is the type returned by all
relational operators.

### String

String literals in Java are specified like they are in most other languages—by
enclosing a sequence of characters between a pair of double quotes.

## Variable

The variable is the basic unit of storage in a Java program. A variable is
defined by the combination of an identifier, a type, and an optional initializer.

### Declaring a variable

In Java, all variables must be declared before they can be used. The basic form
of a variable declaration is shown here:

>type identifier [ = value ][, identifier [= value ] …];

### Dynamic Initialization

Java allows variables to be initialized dynamically, using any expression valid at the
allows variables to be initialized dynamically, using any expression valid at the
time the variable is declared.

### The Scope and Lifetime of Variables

A block ( {...} ) defines a scope .

## Type conversion and Casting

### Java’s automatics conversions

an automatic type conversion will take place if the following two conditions are met.

- The two types are compatible.
- The destination type is larger than the source type 
  - byte -> int possible but not int -> byte.
- There is no automatic conversions from *numeric types* to char or boolean.

### Casting Incompatible Types

To create a conversion between two incompatible types, you must use a cast.
A cast is simply an explicit type conversion. It has this general form:

```java
    (target-type) value;
```

### Automatic Type Promotion in Expressions

In an expression, the precision required of an intermediate value will sometimes
exceed the range of either operand.

- Java automatically
promotes each byte, short, or char operand to int when evaluating an
expression.

- As useful as the automatic promotions are, they can cause confusing
compile-time errors. For example, this seemingly correct code causes a
problem.because the operands were automatically promoted
to int when the expression was evaluated, the result has also been promoted to
int. Thus, the result of the expression is now of type int, which cannot be
assigned to a byte without the use of a cast.


```java
    byte b = 50;
    b = b * 2; // Error! Cannot assign an int to a byte!
```

## Arrays

### One-Dimensional Arrays

The general
form of a one-dimensional array declaration is

```java 
type variable-name[ ];
```

To link an array variablewith an actual, physical
array of integers, you must allocate one using new and assign it to
the variable.The general form of new as it applies to
one-dimensional arrays appears as

```java
array-variable = new type [size];

// OR


int month_days[] = new int[12];
```
The elements in the array allocated by new will
automatically be initialized to zero (for numeric types), false.

- Java strictly checks to make sure you do not accidentally try to store or
reference values outside of the range of the array. The Java run-time system
will check that all array indexes are in the correct range.

### Multidimensional Arrays

he following declares a twodimensional
array variable called twoD

```java
int twoD[][] = new int[4][5];
```

When you allocate memory for a multidimensional array, you need only
specify the memory for the first (leftmost) dimension. You can allocate the
remaining dimensions separately.

```java
int twoD[][] = new int[4][];
twoD[0] = new int[5];
twoD[1] = new int[2];
twoD[2] = new int[5];
twoD[3] = new int[3];
```

#### Alternative Array Declaration Syntax

There is a second form that may be used to declare an array:
>type[ ] var-name;

## Introducing Type Inference with Local Variables

Beginning with JDK 10, it is now possible to let the compiler infer the type
of a local variable based on the type of its initializer, thus avoiding the need to
explicitly specify the type. To support local
variable type inference, the context-sensitive identifier ``var`` was added to Java
as a reserved type name. Remeber that the defaults of floating point numbers are double and int for numeric types.

-you cannot use brackets on the
left side of a var declaration. Thus, both of these declarations are invalid. java identifies the variable directly as a `type[]` object.

```java
var[] myArray = new int[10]; // Wrong

var myArray[] = new int[10]; // Wrong
```