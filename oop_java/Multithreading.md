- [Multithreading](#multithreading)
  - [The Thread Class and the Runnable Interface](#the-thread-class-and-the-runnable-interface)
  - [The Main Thread](#the-main-thread)
  - [Creating a Thread](#creating-a-thread)
    - [Implementing Runnable](#implementing-runnable)
    - [Extending Thread](#extending-thread)
  - [Using isAlive( ) and join( )](#using-isalive--and-join-)
  - [Thread Priorities](#thread-priorities)
  - [Synchronization](#synchronization)
    - [Using Synchronized Methods](#using-synchronized-methods)
  - [Interthread Communication](#interthread-communication)

# Multithreading

## The Thread Class and the Runnable Interface

Java’s multithreading system is built upon the Thread class, its methods, and
its companion interface, Runnable. Thread encapsulates a thread of execution.
Since you can’t directly refer to the ethereal state of a running thread, you will
deal with it through its proxy, the Thread instance that spawned it. To create a
new thread, your program will either extend Thread or implement the
Runnable interface.

## The Main Thread

1. It is the thread from which other “child” threads will be spawned.

1. Often, it must be the last thread to finish execution because it performs
various shutdown actions.

Although the main thread is created automatically when your program is
started, it can be controlled through a Thread object. To do so, you must obtain
a reference to it by calling the method currentThread( ), which is a public
static member of Thread. Its general form is shown here:

```java
static Thread currentThread( )
```

The sleep( ) method causes the thread from which it is called to
suspend execution for the specified period of milliseconds. Its general form is
shown here:

```java
static void sleep(long milliseconds) throws InterruptedException
```

The `sleep( )` method in Thread might throw an InterruptedException.

## Creating a Thread

Java defines two ways in which this can be accomplished:

* You can implement the Runnable interface.
* You can extend the Thread class, itself.

### Implementing Runnable

To implement
Runnable, a class need only implement a single method called run( ), which is
declared like this:

```java
public void run( )
```

`run( )` establishes the entry point for another, concurrent thread of execution
within your program. This thread will end when `run( )` returns.

After you create a class that implements Runnable, you will instantiate an
object of type Thread from within that class. Thread defines several
constructors. The one that we will use is shown here:

```java
Thread(Runnable threadOb, String threadName)
```

After the new thread is created, it will not start running until you call its
start( ) method, which is declared within Thread.

```java
void start()
```

### Extending Thread

The extending class must override
the run( ) method, which is the entry point for the new thread. As before, a call
to start( ) begins execution of the new thread.

## Using isAlive( ) and join( )

Two ways exist to determine whether a thread has finished. First, you can
call isAlive( ) on the thread. This method is defined by Thread, and its general
form is shown here:

```java
final boolean isAlive( )
```

While isAlive( ) is occasionally useful, the method that you will more
commonly use to wait for a thread to finish is called join( ), shown here:

```java
final void join( ) throws InterruptedException
```

## Thread Priorities

To set a thread’s priority, use the setPriority( ) method, which is a member
of Thread. This is its general form:

```java
final void setPriority(int level)
```

Here, level specifies the new priority setting for the calling thread. The value of
level must be within the range **MIN_PRIORITY** and **MAX_PRIORITY**.
Currently, these values are 1 and 10, respectively. To return a thread to default
priority, specify NORM_PRIORITY, which is currently 5. These priorities are
defined as static final variables within Thread.
You can obtain the current priority setting by calling the `getPriority( )`
method of Thread, shown here:

```java
final int getPriority( )
```

## Synchronization

Key to synchronization is the concept of the monitor. A monitor is an object
that is used as a mutually exclusive lock. Only one thread can own a monitor at
a given time.

You can synchronize your code in either of two ways. Both involve the use
of the synchronized keyword, and both are examined here.

### Using Synchronized Methods

Any time that you have a method, or group of methods, that manipulates the
internal state of an object in a multithreaded situation, you should use the
synchronized keyword to guard the state from race conditions.

## Interthread Communication

* `wait( )` tells the calling thread to give up the monitor and go to sleep until
some other thread enters the same monitor and calls notify( ) or
notifyAll( ).
* `notify( )` wakes up a thread that called wait( ) on the same object.
* `notifyAll( )` wakes up all the threads that called wait( ) on the same
object. One of the threads will be granted access.