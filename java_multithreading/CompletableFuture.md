# Introduction

CompletableFuture is a class by java, made for facilitating asynchronous processing. and multithreaded processes. This class implements the `Future` Interface and `CompletetionStage` interface.

## Using as a Simple Future Object

You can use the Compatable Futurea as a simple Future object to hold the return value of a thread which will return in Future.

```java
 public Future<String> calculateAsync() throws InterruptedException {
    CompletableFuture<String> completableFuture = new CompletableFuture<>();


    Executors.newCachedThreadPool().submit(() -> {
        Thread.sleep(500);
        completableFuture.complete("Hello");
        Thread.sleep(500);
        return null;
    });

    return completableFuture;
}
```

In the above example we declare a Completable Future object with a no-arg consturctor. the executor API is used to make a thread which will return in the future and the return value of it is stored in the `CompletableFuture` Object. We can call the function `calcculateAsync()` and use the `get()` method to block the current Thread till the get methos has returned.

```java
 String result = completableFuture.get();
    assertEquals("Hello", result);
```

In above case even though the thread sleeps for 1000ms in total, the get() method returns after 500ms because the complete method is called after 500ms.

## Running a method Asynchronously using a Supplier

You can use a Supplier instance like a lambda function with one return value and no inpur parameters to use it with supplyAsync function.

```java
CompletableFuture<String> future
  = CompletableFuture.supplyAsync(() -> {
        Thread.sleep(1000);
        return "hello"
      });
```

### Chaining computations

we can use the `thenApply()` method to chain calls on a `completableFuture` object.

```java
CompletableFuture<Response> future
  = CompletableFuture.supplyAsync(() -> {
        // get details from database
      });
future.thenApply( () -> {
    // send a email after getting details from the database
    });

```

using `get()` after this will execute both the functions and give the return get.

If we dont deen to return after a future chain, We can use the `thenAccept()` method which accepts a `Consumer` Object. and we can also the use `thenRun()` ,method to not return or accept arguments.

```java

//Supplier
CompletableFuture<String> completableFuture
  = CompletableFuture.supplyAsync(() -> "Hello");

//COnsumer
CompletableFuture<Void> future = completableFuture
  .thenAccept(s -> System.out.println("Computation returned: " + s));

future.get();

// Runnable
CompletableFuture<Void> future = completableFuture
  .thenRun(() -> System.out.println("Computation finished."));

```

## Combining Futures

This can be used to make two different calles to functions and combine those results.

```java

CompletableFuture<Response> future
  = CompletableFuture.supplyAsync(() -> {
        // call to an API which return the value into an object of tupe Resonse1
      }).thenCombine(() -> {
          // call to a second Api call with Response2 as return
      },
      Response(response1,response2));

```

## Running Multiple Futures in Parllel 

The CompletableFuture.allOf static method allows to wait for completion of all of the Futures provided as a var-arg

```java
CompletableFuture<String> future1  
  = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> future2  
  = CompletableFuture.supplyAsync(() -> "Beautiful");
CompletableFuture<String> future3  
  = CompletableFuture.supplyAsync(() -> "World");

CompletableFuture<Void> combinedFuture 
  = CompletableFuture.allOf(future1, future2, future3);

// ...

combinedFuture.get();

assertTrue(future1.isDone());
assertTrue(future2.isDone());
assertTrue(future3.isDone());
```
