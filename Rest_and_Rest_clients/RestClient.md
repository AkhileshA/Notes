# Rest Template

- [Rest Template](#rest-template)
  - [Introduction](#introduction)
  - [Setup](#setup)
    - [Used dependancies](#used-dependancies)
  - [Methods](#methods)
    - [.exchange()](#exchange)
      - [Examples](#examples)
    - [Most easy and most used](#most-easy-and-most-used)
  - [POST request](#post-request)

## Introduction

The RestTemplate is the central class within the Spring framework for executing synchronous HTTP requests on the client side.
By default uses the `java.net.HttpURLConnection` underneath but can be changed. We usually define a spring bean of the RestTemplate Class to configure it once and use it to make requests everytime in an App.

Also Get familiar with `WebClient` as RestTemplate is going to be depracated.

You can also use JXAB or SAX for xml and integrate wit hRestTemplate for automatioc deserialization with xml.

```java
@Bean
 RestTemplate restTemplate() {
    // example
    // you can also add convertors loke jackson and other http clients like okhttp or others here
    return new RestTemplate();
  }
```

## Setup

### Used dependancies

The Dependency spring-boot-starter-web is a starter for building web applications. This dependency contains the class RestTemplate.
We need `spring-core`, `spring-context` dependencies for spring framework. Then we need spring-web artefact that contains RestTemplate class. We also need jackson-mapper-asl for Spring JSON support through Jackson API.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
 <modelVersion>4.0.0</modelVersion>

 <groupId>com.journaldev.spring</groupId>
 <artifactId>SpringRestTemplate</artifactId>
 <version>1.0-SNAPSHOT</version>
 <properties>
  <spring.framework>4.3.0.RELEASE</spring.framework>
  <spring.web>3.0.2.RELEASE</spring.web>
  <serializer.version>2.8.1</serializer.version>
 </properties>
 <dependencies>
  <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-core</artifactId>
   <version>${spring.framework}</version>
  </dependency>
  <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-context</artifactId>
   <version>${spring.framework}</version>
  </dependency>
  <dependency>
   <groupId>org.codehaus.jackson</groupId>
   <artifactId>jackson-mapper-asl</artifactId>
   <version>1.9.4</version>
  </dependency>
  <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-web</artifactId>
   <version>${spring.web}</version>
  </dependency>
 </dependencies>
</project>
```

## Methods

### .exchange()

There are many oevrloaded versions of .exchange() method. this method gives more staraight and finer control over others.

#### Examples

```java
// Takes the Request from request entity and gives response in a response entity into a POJO of type `responseType`.
exchange(RequestEntity<?> entity, Class<T> responseType);
// sample usage
client.exchange(request, Employee.class);

```

```java
//Request Enitity Example
 RequestEntity<MyRequest> request = RequestEntity
     .post("https://example.com/{foo}", "bar")
     .accept(MediaType.APPLICATION_JSON)
     .body(body);
```

```java
 exchange(String url, HttpMethod method, HttpEntity<?> requestEntity, Class<T> responseType, Map<String,?> uriVariables);
```


### Most easy and most used 

```java
 .getForEntity(URI url, Class<T> responseType);
  getForEntity(String url, Class<T> responseType, Map<String,?> uriVariables);

  getForObject(String url, Class<T> responseType, Object... uriVariables);
  getForObject(URI url, Class<T> responseType);

```

- `responseType` is the type of the declared POJO we want the response body to be deserialized into.
  - We can use String.class to just get the response in form o fa a JSON in a string.

## POST request

RestTemplate has `postForEntity()`, `postForObject()` and `postForLocation()`.

```java
  postForEntity(String url, Object request, Class<T> responseType, Map<String,?> uriVariables);
  postForEntity(URI url, Object request, Class<T> responseType)p;

  postForLocation(String url, Object request, Object... uriVariables);
  postForLocation(URI url, Object request);

  postForObject(URI url, Object request, Class<T> responseType);
  postForObject(String url, Object request, Class<T> responseType, Object... uriVariables);

```

- The `postForLocation()` method gives the URI for the location of the allocated resource instead of the whole resource itself.
