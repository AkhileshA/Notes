# Inheritance

Inheritance is one of the cornerstones of object-oriented programming because
it allows the creation of hierarchical classifications. Using inheritance, you can
create a general class that defines traits common to a set of related items.

## Inheritance Basics

To inherit a class, you simply incorporate the definition of one class into
another by using the extends keyword.

```java
class SubClass extends SuperClass{
    .
    .
    .
}
```

You can only specify one superclass for any subclass that you create. Java
does not support the inheritance of multiple superclasses into a single subclass.

## Member Access and Inheritance

Although a subclass includes all of the members of its superclass, it cannot
access those members of the superclass that have been declared as private.

- ## A Superclass Variable Can Reference a Subclass Object

It is important to understand that it is the type of the reference variable—not
the type of the object that it refers to—that determines what members can be
accessed. That is, when a reference to a subclass object is assigned to a
superclass reference variable, you will have access only to those parts of the
object defined by the superclass

## Using super

### Using super to Call Superclass Constructors

A subclass can call a constructor defined by its superclass by use of the
following form of super:

```java
super(arg-list);
```

Here, arg-list specifies any arguments needed by the constructor in the
superclass. `super( )` must always be the first statement executed inside a
subclass’ constructor.

When a subclass calls super( ), it is calling the constructor of its immediate superclass. Thus, super( )
always refers to the superclass immediately above the calling class. This is true
even in a multileveled hierarchy. Also, super( ) must always be the first
statement executed inside a subclass constructor.

### A Second Use for super

This second form of super is most applicable to situations in which member
names of a subclass hide members by the same name in the superclass. The second form of super acts somewhat like this, except that it always refers
to the superclass of the subclass in which it is used. This usage has the
following general form:

```java
super.member;
```

## When Constructors Are Executed

In a class hierarchy, constructors complete their
execution in order of derivation, from superclass to subclass. Further, since
super( ) must be the first statement executed in a subclass’ constructor, this
order is the same whether or not super( ) is used.

## Method Overriding

In a class hierarchy, when a method in a subclass has the same name and type
signature as a method in its superclass, then the method in the subclass is said
to override the method in the superclass. When an overridden method is called
from within its subclass, it will always refer to the version of that method
defined by the subclass. The version of the method defined by the superclass
will be hidden.

### Dynamic Method Dispatch

Method overriding forms the basis for one of Java’s most powerful
concepts: dynamic method dispatch. Dynamic method dispatch is the
mechanism by which a call to an overridden method is resolved at run time,
rather than compile time. Dynamic method dispatch is important because this
is how Java implements run-time polymorphism.

Let’s begin by restating an important principle: a superclass reference
variable can refer to a subclass object. Java uses this fact to resolve calls to
overridden methods at run time. Here is how. When an overridden method is
called through a superclass reference, Java determines which version of that
method to execute based upon the type of the object being referred to at the
time the call occurs. Thus, this determination is made at run time. When
different types of objects are referred to, different versions of an overridden
method will be called. **In other words, it is the type of the object being referred to (not the type of the reference variable) that determines which version of an overridden method will be executed.** 
Therefore, if a superclass contains a
method that is overridden by a subclass, then when different types of objects
are referred to through a superclass reference variable, different versions of the
method are executed.

## Using Abstract Classes

There are situations in which you will want to define a superclass that declares
the structure of a given abstraction without providing a complete
implementation of every method. That is, sometimes you will want to create a
superclass that only defines a generalized form that will be shared by all of its
subclasses, leaving it to each subclass to fill in the details. In this case, you want some way to ensure
that a subclass does, indeed, override all necessary methods. Java’s solution to
this problem is the abstract method. You can require that certain methods be overridden by subclasses by
specifying the abstract type modifier. To declare an abstract method, use this
general form:

```java
abstract type name(parameter-list);
```

- Any class that contains one or more abstract methods must also be declared
abstract.
- To declare a class abstract, you simply use the abstract keyword in
front of the class keyword at the beginning of the class declaration.
- There can
be no objects of an abstract class. That is, an abstract class cannot be directly
instantiated with the new operator.

## Using final with Inheritance

The keyword final has three uses. First, it can be used to create the equivalent
of a named constant. This use was described in the preceding chapter. The other
two uses of final apply to inheritance. Both are examined here.

### Using final to Prevent Overriding

While method overriding is one of Java’s most powerful features, there will be
times when you will want to prevent it from occurring. To disallow a method
from being overridden, specify final as a modifier at the start of its declaration.
Methods declared as final cannot be overridden.

Methods declared as final can sometimes provide a performance
enhancement: The compiler is free to inline calls to them because it “knows”
they will not be overridden by a subclass. When a small final method is called,
often the Java compiler can copy the bytecode for the subroutine directly inline
with the compiled code of the calling method, thus eliminating the costly
overhead associated with a method call.

### Using final to Prevent Inheritance

Sometimes you will want to prevent a class from being inherited. To do this,
precede the class declaration with final. Declaring a class as final implicitly
declares all of its methods as final, too. As you might expect, it is illegal to
declare a class as both abstract and final since an abstract class is incomplete
by itself and relies upon its subclasses to provide complete implementations.

## The Object class

There is one special class, Object, defined by Java. All other classes are
subclasses of Object. That is, Object is a superclass of all other classes. This
means that a reference variable of type Object can refer to an object of any
other class. Also, since arrays are implemented as classes, a variable of type
Object can also refer to any array.

The methods getClass( ), notify( ), notifyAll( ), and wait( ) are declared as
final. You may override the others. These methods are described elsewhere in
this book. However, notice two methods now: equals( ) and toString( ). The
equals( ) method compares two objects. It returns true if the objects are equal,
and false otherwise. The

