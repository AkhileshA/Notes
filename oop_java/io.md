- [I/O, Try-with-Resources](#io-try-with-resources)
  - [Streams](#streams)
  - [The Byte Stream Classes](#the-byte-stream-classes)
  - [The Character Stream Classes](#the-character-stream-classes)
  - [The Predefined Streams](#the-predefined-streams)
    - [Reading Console Input](#reading-console-input)
    - [Reading Character](#reading-character)
    - [Reading Strings](#reading-strings)
    - [Writing Console Output](#writing-console-output)
  - [The PrintWriter Class](#the-printwriter-class)
  - [Reading and Writing Files](#reading-and-writing-files)

# I/O, Try-with-Resources

## Streams

Java programs perform I/O through streams. A stream is an abstraction that
either produces or consumes information. 

## The Byte Stream Classes

Byte streams are defined by using two class hierarchies. At the top are two
abstract classes: InputStream and OutputStream. The abstract classes InputStream and OutputStream define several key
methods that the other stream classes implement. Two of the most important
are read( ) and write( ), which, respectively, read and write bytes of data. Each
has a form that is abstract and must be overridden by derived stream classes.

## The Character Stream Classes

Character streams are defined by using two class hierarchies. At the top are two
abstract classes: Reader and Writer. These abstract classes handle Unicode
character streams. The abstract classes Reader and Writer define several key methods that the
other stream classes implement. Two of the most important methods are read(
) and write( ), which read and write characters of data, respectively. Each has a
form that is abstract and must be overridden by derived stream classes.

## The Predefined Streams

System.out refers to the standard output stream. By default, this is the
console. System.in refers to standard input, which is the keyboard by default.
System.err refers to the standard error stream, which also is the console by
default. However, these streams may be redirected to any compatible I/O
device.  System.in is an object of type InputStream; System.out and System.err
are objects of type PrintStream. These are byte streams, even though they are
typically used to read and write characters from and to the console. As you will
see, you can wrap these within character-based streams, if desired.

### Reading Console Input

In Java, console input is accomplished by reading from System.in. To obtain
a character-based stream that is attached to the console, wrap System.in in a
BufferedReader object. BufferedReader supports a buffered input stream. A
commonly used constructor is shown here:

```java
BufferedReader(Reader inputReader)
```

Here, inputReader is the stream that is linked to the instance of
BufferedReader that is being created. Reader is an abstract class. One of its
concrete subclasses is InputStreamReader, which converts bytes to
characters. To obtain an InputStreamReader object that is linked to
System.in, use the following constructor:

```java
InputStreamReader(InputStream inputStream)
```

### Reading Character

To read a character from a BufferedReader, use read( ). The version of read( )
that we will be using is

```java
int read( ) throws IOException
```

Each time that read( ) is called, it reads a character from the input stream and
returns it as an integer value. It returns –1 when an attempt is made to read at
the end of the stream. As you can see, it can throw an IOException.

### Reading Strings

To read a string from the keyboard, use the version of readLine( ) that is a
member of the BufferedReader class. Its general form is shown here:

```java
String readLine( ) throws IOException
```

As you can see, it returns a String object.

### Writing Console Output

Console output is most easily accomplished with print( ) and println( ),
described earlier, which are used in most of the examples in this book. These
methods are defined by the class PrintStream (which is the type of object
referenced by System.out). Even though System .out is a byte stream, using it
for simple program output is still acceptable.

## The PrintWriter Class

For real-world programs, the recommended method of
writing to the console when using Java is through a PrintWriter stream.
PrintWriter is one of the character-based classes. Using a character-based
class for console output makes internationalizing your program easier.

PrintWriter defines several constructors. The one we will use is shown
here:

```java
PrintWriter(OutputStream outputStream, boolean flushingOn)
```

## Reading and Writing Files

Two of the most often-used stream classes are FileInputStream and
FileOutputStream, which create byte streams linked to files. To open a file,
you simply create an object of one of these classes, specifying the name of the
file as an argument to the constructor. Although both classes support additional
constructors, the following are the forms that we will be using:

```java
FileInputStream(String fileName) throws FileNotFoundException
FileOutputStream(String fileName) throws FileNotFoundException
```

