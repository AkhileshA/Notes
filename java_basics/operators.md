# Introduction

Most of its operators can be divided
into the following four groups: arithmetic, bitwise, relational, and logical. Java
also defines some additional operators that handle certain special situations.

Since the bitwise operators manipulate the bits within an integer: it is
important to understand what effects such manipulations may have on a value.
Specifically, it is useful to know how Java stores integer values and how it
represents negative numbers.Java uses an
encoding known as two’s complement, which means that negative numbers are
represented by inverting (changing 1’s to 0’s and vice versa) all of the bits in a
value, then adding 1 to the result.

## The Left Shift

The left shift operator, <<, shifts all of the bits in a value to the left a specified
number of times. It has this general form:
>value << num

For each shift left, the high-order bit
is shifted out (and lost), and a zero is brought in on the right.

- As you know, byte and short values are
promoted to int when an expression is evaluated.Java’s automatic type promotions produce unexpected results when you are
shifting byte and short values.

## The Right Shift

### Signed right shift

The right shift operator, >>, shifts all of the bits in a value to the right a
specified number of times. Its general form is shown here:
> value >> num

- When you are shifting right, the top (leftmost) bits exposed by the right shift
are filled in with the previous contents of the top bit.

### Unsigned right shift

Java’s unsigned,
shift-right operator, >>>, which always shifts zeros into the high-order bit.

## Logical Operators

Logical - &, | , ^
Short Circuit - &&, ||

- In short Circuit statements, the execution of expression is stopped once its evaluation is decided by a part of it already.
