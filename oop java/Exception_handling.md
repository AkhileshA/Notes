# Exception Handling

An exception is
an abnormal condition that arises in a code sequence at run time. In other
words, an exception is a run-time error. In computer languages that do not
support exception handling, errors must be checked and handled manually—
typically through the use of error codes, and so on. This approach is as
cumbersome as it is troublesome. Java’s exception handling avoids these
problems.

## Exception-Handling Fundamentals

A Java exception is an object that describes an exceptional (that is, error)
condition that has occurred in a piece of code. When an exceptional condition
arises, an object representing that exception is created and thrown in the
method that caused the error.

- Exceptions thrown by Java relate to
fundamental errors that violate the rules of the Java language or the constraints
of the Java execution environment.
- Manually generated exceptions are
typically used to report some error condition to the caller of a method.

Java exception handling is managed via five keywords: `try`, `catch`, `throw`,
`throws`, and `finally`.

Program statements that
you want to monitor for exceptions are contained within a try block. If an
exception occurs within the try block, it is thrown. Your code can catch this
exception (using catch) and handle it in some rational manner. Systemgenerated
exceptions are automatically thrown by the Java run-time system. To
manually throw an exception, use the keyword throw. Any exception that is
thrown out of a method must be specified as such by a throws clause. Any code
that absolutely must be executed after a try block completes is put in a finally
block.

### General form

```Java
try{
    // body of code to monitor
}

catch( ExceptionType1 ExOb)
{
    //exception handler for ExceptionType1
}

catch( ExceptionType2 ExOb)
{
    //exception handler for ExceptionType2
}

// .....

finally
{
    // block of code to beexecuted after the try block
}

```

## Exception Types

All exception types are subclasses of the built-in class Throwable.
Thus, Throwable is at the top of the exception class hierarchy. 

Immediately below
Throwable are two subclasses that partition exceptions into two distinct
branches. One branch is headed by Exception. 

- This class is used for exceptional conditions that user programs should catch.
- This is also the class
that you will subclass to create your own custom exception types.
- There is an
important subclass of Exception, called RuntimeException. Exceptions of this
type are automatically defined for the programs that you write

The other branch is topped by `Error`, which defines exceptions that are not
expected to be caught under normal circumstances by your program.
Examples include Stack overflow.

![exception_table](/images/exception_chart.png)

## Uncaught Exceptions

Any exception that is not caught by your program will ultimately be
processed by the default handler. The default handler displays a string
describing the exception, prints a stack trace from the point at which the
exception occurred, and terminates the program.

## Using try and catch

To guard against and handle a run-time error, simply enclose the code that
you want to monitor inside a try block. Immediately following the try block,
include a catch clause that specifies the exception type that you wish to catch.
To illustrate how easily this can be done, the following program includes a try. 

Once
an exception is thrown, program control transfers out of the try block into the
catch block. Put differently, catch is not “called,” so execution never “returns”
to the try block from a catch.

When you use multiple catch statements, it is important to remember that
exception subclasses must come before any of their superclasses. This is
because a catch statement that uses a superclass will catch exceptions of that
type plus any of its subclasses. Thus, a subclass would never be reached if it
came after its superclass.

Nesting of try statements can occur in less obvious ways when method calls
are involved. For example, you can enclose a call to a method within a try
block. Inside that method is another try statement. In this case, the try within
the method is still nested inside the outer try block, which calls the method.

## Using Throw

it is possible for your program to throw an exception
explicitly, using the throw statement. The general form of throw is shown
here:

```java
throw ThrowableInstance;
```

### Example

```java
throw new NullPointerException("demo");
```

## Using throws

If a method is capable of causing an exception that it does not handle, it must
specify this behavior so that callers of the method can guard themselves against
that exception. You do this by including a throws clause in the method’s
declaration.

A throws clause lists the types of exceptions that a method might
throw. This is necessary for all exceptions, except those of type Error or
RuntimeException, or any of their subclasses.

## Using finally

When exceptions are thrown, execution in a method takes a rather abrupt,
nonlinear path that alters the normal flow through the method. Depending upon
how the method is coded, it is even possible for an exception to cause the
method to return prematurely. This could be a problem in some methods.

finally creates a block of code that will be executed after a try /catch block
has completed and before the code following the try/catch block. The finally
block will execute whether or not an exception is thrown. If an exception is
thrown, the finally block will execute even if no catch statement matches the
exception. Any time a method is about to return to the caller from inside a
try/catch block, via an uncaught exception or an explicit return statement, the
finally clause is also executed just before the method returns.

## Java’s Built-in Exceptions

The most general of these
exceptions are subclasses of the standard type `RuntimeException`. As
previously explained, these exceptions need not be included in any method’s
`throws` list.

## Creating Your Own Exception Subclasses

define a subclass of
Exception (which is, of course, a subclass of Throwable). Your subclasses
don’t need to actually implement anything—it is their existence in the type
system that allows you to use them as exceptions.

Exception defines four public constructors. Two support chained
exceptions, described in the next section. The other two are shown here:

```java
Exception( )

Exception(String msg)
```

## Chained Exceptions

To allow chained exceptions, two constructors and two methods were added
to Throwable. The constructors are shown here:

```java
Throwable(Throwable causeExc)
Throwable(String msg, Throwable causeExc)
```

In the first form, causeExc is the exception that causes the current exception.
That is, causeExc is the underlying reason that an exception occurred. The
second form allows you to specify a description at the same time that you
specify a cause exception. These two constructors have also been added to the
`Error`, `Exception`, and `RuntimeException` classes.

The chained exception methods supported by Throwable are getCause( )
and initCause( ). These methods are shown in Table 10-3 and are repeated here
for the sake of discussion.

```java
Throwable getCause( )
Throwable initCause(Throwable causeExc)
```

The getCause( ) method returns the exception that underlies the current
exception. If there is no underlying exception, null is returned. The initCause(
) method associates causeExc with the invoking exception and returns a
reference to the exception.

 