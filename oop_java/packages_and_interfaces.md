- [Packages and Interfaces](#packages-and-interfaces)
  - [Packages](#packages)
    - [Defining a Package](#defining-a-package)
    - [Finding Packages and CLASSPATH](#finding-packages-and-classpath)
    - [Importing packages](#importing-packages)
  - [Interfaces](#interfaces)
    - [Implementing Interfaces](#implementing-interfaces)
    - [Accessing Implementations Through Interface References](#accessing-implementations-through-interface-references)
    - [Default Interface Methods](#default-interface-methods)
    - [Use static Methods in an Interface](#use-static-methods-in-an-interface)
    - [Private Interface Methods](#private-interface-methods)
  - [Rules for dealing Multiple Inheritance Issues](#rules-for-dealing-multiple-inheritance-issues)

# Packages and Interfaces

Packages are containers for classes. They are used to keep the class
name space compartmentalized. For example, a package allows you to create a
class named List, which you can store in your own package without concern
that it will collide with some other class named List stored elsewhere.
Packages are stored in a hierarchical manner and are explicitly imported into
new class definitions.

Through the use of the interface keyword, Java allows you to
fully abstract an interface from its implementation. Using interface, you can
specify a set of methods that can be implemented by one or more classes. In its
traditional form, the interface, itself, does not actually define any
implementation. Although they are similar to abstract classes, interfaces have
an additional capability: A class can implement more than one interface. **By contrast, a class can only inherit a single superclass (abstract or otherwise).**

## Packages

The package is both a
naming and a visibility control mechanism. You can define classes inside a
package that are not accessible by code outside that package. You can also
define class members that are exposed only to other members of the same
package. This allows your classes to have intimate knowledge of each other,
but not expose that knowledge to the rest of the world.

### Defining a Package

To create a package is quite easy: simply include a package command as the
first statement in a Java source file. Any classes declared within that file will
belong to the specified package. The package statement defines a name space
in which classes are stored.This is the general form of the package statement:

```java
package pkg;
```

Typically, Java uses file system directories to store packages.
For example, the .class files
for any classes you declare to be part of mypackage must be stored in a
directory called mypackage. More than one file can include the same package statement. The package
statement simply specifies to which package the classes defined in a file
belong. It does not exclude other classes in other files from being part of that
same package. Most real-world packages are spread across many files.

You can create a hierarchy of packages. To do so, simply separate each
package name from the one above it by use of a period. The general form of a
multileveled package statement is shown here:

```java
package pkg1[.pkg2[.pkg3]];
```

A package hierarchy must be reflected in the file system of your Java
development system. For example, a package declared as
package a.b.c;
needs to be stored in a\b\c in a Windows environment. Be sure to choose your
package names carefully. You cannot rename a package without renaming the
directory in which the classes are stored.

### Finding Packages and CLASSPATH

- By default, the Java run-time system uses the
current working directory as its starting point. Thus, `if your package is in a subdirectory of the current directory, it will be found.`
- You can specify a directory path or paths by setting the `CLASSPATH` environmental variable.
- You can use the `-classpath` option with java and javac to specify the.

As explained, AccountBalance is now part of the package mypack. This
means that it cannot be executed by itself. That is, you cannot use this
command line:

>java AccountBalance

AccountBalance ***must*** be qualified with its package name.

### Importing packages

It could become tedious to type in the long dot-separated package
path name for every class you want to use. For this reason, Java includes the
import statement to bring certain classes, or entire packages, into visibility.
In a Java source file, import statements occur immediately following the
package statement (if it exists) and before any class definitions. This is the
general form of the import statement:

```java
import pkg1 [.pkg2].(classname | *);
```

All of the standard Java SE classes included with Java begin with the name
java. The basic language functions are stored in a package called java.lang.
Normally, you have to import every package or class that you want to use, but
since Java is useless without much of the functionality in java.lang, it is
implicitly imported by the compiler for all programs. This is equivalent to the
following line being at the top of all of your programs:

```java
import java.lang.*;
```

- If a class with the same name exists in two different packages that you
import using the star form, the compiler will remain silent, unless you try to
use one of the classes. In that case, you will get a compile-time error and have
to explicitly name the class specifying its package.

## Interfaces

Using the keyword interface, you can fully abstract a class’ interface from its
implementation. That is, using interface, you can specify what a class must do,
but not how it does it. Also, one class can
implement any number of interfaces.

- To implement an interface, a class must provide the complete set of methods
required by the interface.

-variables can be declared inside interface
declarations. They are implicitly final and static, meaning they cannot be
changed by the implementing class. They must also be initialized. All methods
and variables are implicitly public.

-If a class includes an interface but does not fully implement the methods
required by that interface, then that class must be declared as abstract

-One interface can inherit another by use of the keyword extends. The syntax is
the same as for inheriting classes. When a class implements an interface that
inherits another interface, it must provide implementations for all methods
required by the interface inheritance chain.

> By providing the interface keyword, Java allows you to fully utilize the “one interface, multiple methods” aspect of polymorphism.

### Implementing Interfaces

Once an interface has been defined, one or more classes can implement that
interface. To implement an interface, include the implements clause in a class
definition, and then create the methods required by the interface.

```java
class classname [extends superclass] [implements interface[,interface]] {
    //body
}
```

If a class implements more than one interface, the interfaces are separated with
a comma. If a class implements two interfaces that declare the same method,
then the same method will be used by clients of either interface. The methods
that **implement** an interface must be declared **public**.

### Accessing Implementations Through Interface References

You can declare variables as object references that use an interface rather than
a class type. Any instance of any class that implements the declared interface
can be referred to by such a variable. When you call a method through one of
these references, the correct version will be called based on the actual instance
of the interface being referred to. This is one of the key features of interfaces.
The method to be executed is looked up dynamically at run time, allowing
classes to be created later than the code which calls methods on them. The
calling code can dispatch through an interface without having to know anything
about the “callee.”

### Default Interface Methods

An interface default method is defined similar to the way a method is defined
by a class. The primary difference is that the declaration is preceded by the
keyword default.

>To define a default method, precede its declaration with default.

### Use static Methods in an Interface

Like static methods in a class, a static method defined by
an interface can be called independently of any object. Thus, no
implementation of the interface is necessary, and no instance of the interface is
required, in order to call a static method. Instead, a static method is called by
specifying the interface name, followed by a period, followed by the method
name. Here is the general form:

> static interface methods are not inherited by either an implementing class or a subinterface.

```java
InterfaceName.staticMethodName
```

### Private Interface Methods

A private interface method can be called only by a default method or another private
method defined by the same interface.

## Rules for dealing Multiple Inheritance Issues

- A class implementation takes priority over an interface
default implementation.

