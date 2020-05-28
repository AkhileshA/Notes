# Java’s Selection Statements

## If

```java
if (condition1) statement1;
else if(condition2) statement2;
.
.
.
else if(conditionN-1) statementN-1;
else statementN;
```

## switch

```java
switch (expression) {
case value1:
// statement sequence
break;
case value2:
// statement sequence
break;
...
case valueN :
// statement sequence
break;
default:
// default statement sequence
}
```

The expression can be anything among the primitive types or String.
The break statement is used inside the switch to terminate a statement
sequence. When a break statement is encountered, execution branches to the
first line of code that follows the entire switch statement.

## Iteration Statements

Java’s iteration statements are for, while, and do-while

### while

```java
while(condition) {
// body of loop
}
```

### do while

```java
do{
// body of loop
}while(condition);
```

### for loop 

```java
for(initializations; condition; iteration)
{
    // body of the loop
}

```

each expression in the loop declaration is optional.

### The For-Each Version of the for Loop

The general form of the for-each version of the for is shown here:

```java
for(type itr-var : collection) statement-block
```
