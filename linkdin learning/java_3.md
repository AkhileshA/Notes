# Java Basics

## Java garbage collector

- Java has a garbage collector. when a variable is created, it is stored in the stack. and the objects are stored in the heap.

- you can explicitly dereference objects and variables by using `null`.

## Varaibles

- All the  primitive types have wrapper class in java.lang. they have a lot of useful static methods.

- Wrapper.MAX_VALUE has the max value of the primitive type. Ex: `Byte.MAX_VALUE`

- BigIntiger and BigDecimal are used to solve problems of floating point numbers.

## String

- it is an object.

- Use String builder to avoid intermediate temporary strings.

- compare strings using .eqalsTo() method instead of == because == checks if its the same object while the method checks for equality of hte contents.

- use `NumberFormat` or `DecimalFormat` to format primitive numerical types

