# Introduction

The class is at the core of Java. It is the logical construct upon which the entire
Java language is built because it defines the shape and nature of an object.

A class is a template for an object, and an object is an
instance of a class.

```java
class classname{
    type var1;
    type var2;
    //....
    type varN;

    type method1(par-list){
        //body of the method
    }
    type method2(par-list){
        //body of the method
    }
    // ....

    type methodN(par-list){
        //body of the method
    }

}

```

you only specify main() method only if its the starting point of the program.

To actually create a object, you will use a statement like the following:

```java
Class myClass= new Class(); // create a object called mybox
```

After this statement executes, myClasswill refer to an instance of its object. Thus, it
will have “physical” reality.

## Declaring Objects

Obtaining
objects of a class is a two-step process. First, you must declare a variable of the
class type. This variable does not define an object. Instead, it is simply a
variable that can refer to an object. Second, you must acquire an actual,
physical copy of the object and assign it to that variable. You can do this using
the new operator. The new operator dynamically allocates (that is, allocates at
run time) memory for an object and returns a reference to it.
***In Java, all class objects must be
dynamically allocated .***

```java
// the two steps described above
Box mybox; // declare reference to object
mybox = new Box(); // allocate a Box object 
```

After the second line executes,
you can use mybox as if it were a Box object. But in reality, mybox simply
holds, in essence, the memory address of the actual Box object.

## A Closer Look at new

the new operator dynamically allocates memory for an
object. In the context of an assignment, it has this general form:

> class-var = new classname ( );

this calls the constructor of the classname being called.

## Assigning Object Reference Variables

Object reference variables act differently than you might expect when an
assignment takes place.

```java
Box b1 = new Box();
Box b2 = b1;
```

You might think that b2 is being assigned a reference to a copy of the object
referred to by b1. However, this would be wrong. Instead, after this fragment
executes, b1 and b2 will both refer to the same object.

## Methods

This is the general form of a method:

```java
type name(parameter-list) {
// body of method
}
```

Here, type specifies the type of data returned by the method. This can be any
valid type, including class types that you create. If the method does not return a
value, its return type must be void.

Methods that have a return type other than void return a value to the calling
routine using the following form of the return statement:

```java
return value;
```

It is important to keep the two terms parameter and argument straight. A
parameter is a variable defined by a method that receives a value when the
method is called.An argument is a
value that is passed to a method when it is invoked.

## Constructors

A constructor initializes an object immediately upon creation. It has the
same name as the class in which it resides and is syntactically similar to a
method.
Once defined, the constructor is automatically called when the object
is created, before the new operator completes.

### The `this` Keyword

Sometimes a method will need to refer to the object that invoked it. To allow
this, Java defines the this keyword. when a local variable has the
same name as an instance variable, the local variable hides the instance
variable. It is useful when the parameters of a class method overload the instance variables.

## A Closer look at methods and classes

### Overloading methods

In Java, it is possible to define two or more methods within the same class that
share the same name, as long as their parameter declarations are different.

- We need to be careful ehile declaring overloaded methods as java1s automatic type conversions can also interfere.
for example.

```java
class test{

 public int method(int i,int j)
 {
  System.out.println("in int");
  return i;
 }
 public double method(double i)
 {
  System.out.println("in double");
  return i;
 }
}
```

gives the output as "in double" when callet with ``testobj.method(12)``.

## Using Objects as Parameters

However, it is both correct and common to pass objects to methods.
When you pass a primitive type to a method, it is passed by value. Thus, a
copy of the argument is made, and what occurs to the parameter that receives
the argument has no effect outside the method.
objects are passed by what is effectively call-by-reference. Keep in
mind that when you create a variable of a class type, you are only creating a
reference to an object. Thus, when you pass this reference to a method, the
parameter that receives it will refer to the same object as that referred to by the
argument. This effectively means that objects act as if they are passed to
methods by use of call-by-reference.

### Recursion

When a method calls itself, new local variables and parameters are allocated
storage on the stack, and the method code is executed with these new variables
from the start. As each recursive call returns, the old local variables and
parameters are removed from the stack, and execution resumes at the point of
the call inside the method.

When writing recursive methods, you must have an if statement somewhere
to force the method to return without the recursive call being executed. If you
don’t do this, once you call the method, it will never return.

## Introducing Access Control

By controlling access, you can prevent misuse. How a member can be accessed is determined by the access modifier
attached to its declaration. Java supplies a rich set of access modifiers. Some
aspects of access control are related mostly to inheritance or packages.

Java’s access modifiers are public, private, and protected. Java also
defines a default access level. protected applies only when inheritance is
involved. The other access modifiers are described next.

- When a member of a class is
modified by public, then that member can be accessed by any other code.

- When a member of a class is specified as private, then that member can only
be accessed by other members of its class.

-When no access
modifier is used, then by default the member of a class is public within its own
package, but cannot be accessed outside of its package.

An access modifier precedes the rest of a member’s type specification. That
is, it must begin a member’s declaration statement. Here is an example:

```java
public int i;
private double j;
private int myMethod(int a, char b) { //...
```

## Understanding static

There will be times when you will want to define a class member that will be
used independently of any object of that class.To create such a member, precede its declaration with the
keyword static. When a member is declared static, it can be accessed before
any objects of its class are created, and without reference to any object. You
can declare both methods and variables to be static.

Methods declared as static have several restrictions:

- They can only directly call other static methods of their class.
- They can only directly access static variables of their class.
- They cannot refer to this or super in any way. 

If you need to do computation in order to initialize your static variables, you
can declare a static block that gets executed exactly once, when the class is
first loaded.

## Introducing final

A field can be declared as final. Doing so prevents its contents from being
modified, making it, essentially, a constant. This means that you must initialize
a final field when it is declared. You can do this in one of two ways: First, you
can give it a value when it is declared. Second, you can assign it a value within
a constructor.

## Introducing Nested and Inner Classes

It is possible to define a class within another class; such classes are known as
nested classes. The scope of a nested class is bounded by the scope of its
enclosing class. A nested class has access to the members, including
private members, of the class in which it is nested.A nested class
that is declared directly within its enclosing class scope is a member of its
enclosing class. It is also possible to declare a nested class that is local to a
block. There are two types of nested classes: static and non-static. A static nested
class is one that has the static modifier applied. Because it is static, it must
access the non-static members of its enclosing class through an object. That is,
it cannot refer to non-static members of its enclosing class directly. Because of
this restriction, static nested classes are seldom used

## String

String are immutable,once a String object is created, its contents cannot be altered.Java defines peer classes of String, called StringBuffer and
StringBuilder, which allow strings to be altered, so all of the normal
string manipulations are still available in Java.

few useful methods:

- `int ength()` - gives the lenth of the string
- `char charAt(int idx)` - gives the character at idx.
- `boolean equals(Strong str)` - checks for equality of contents of the strings.

Command line arguments are stored in a string.

## Varargs: Variable-Length Arguments

Situations that require that a variable number of arguments be passed to a
method are not unusual. the usual format to declare a method with variable Arguments is:

```java
    type_name method_name(type_name1 var1,
                            type_name2 var2,
                            .
                            .
                            type_nameN ... varN)
```

the arguments after N-1 are treated to be going into the varN. it can be accessed as array in the method.