# Feign CLient With Spring boot

- [Feign CLient With Spring boot](#feign-client-with-spring-boot)
  - [Intorduction](#intorduction)
  - [Using Feign](#using-feign)
  - [OpenFeign Integration with Spring Boot](#openfeign-integration-with-spring-boot)
    - [Dependancies for Spring  Boot](#dependancies-for-spring-boot)
  - [Steps to use Feign Client](#steps-to-use-feign-client)
    - [Simple CLient COnfiguration](#simple-client-configuration)
  - [Overriding Defaults](#overriding-defaults)
    - [Configuration with a configuration class](#configuration-with-a-configuration-class)
      - [Example](#example)
    - [Configuration using application.yml](#configuration-using-applicationyml)
    - [Hystrix Support](#hystrix-support)
      - [Example for Hystrix support](#example-for-hystrix-support)
    - [Logging](#logging)
    - [Error Handling](#error-handling)
    - [Configuring using OpenFeign](#configuring-using-openfeign)

## Intorduction

Feign is a Java to HTTP client binder inspired by Retrofit, JAXRS-2.0, and WebSocket.

## Using Feign

To include Feign in your project use the starter with **group** `org.springframework.cloud` and *artifact id* `spring-cloud-starter-openfeign`. 

Feign client is a easy way to consume web services. we declare a interface with the annotation `@FeignClient` and enable the clients with the annotation @EnableFeignClient on the main application. Provide appropriate Jackson or any pther parsing annotations which is appropriate for your needs and declare the client in the Controller or any part of your application where you want to make the calls to the client with the Spring `@Autowired` annotation. Spring will instantiate the client and now you can make the calls as per 

- `HttpMessageConverters ` used for marshelling and Demarshilling of messages are same as Spring WEB.

## OpenFeign Integration with Spring Boot

### Dependancies for Spring  Boot

To include Feign in your project use the starter with `group` `org.springframework.cloud` and `artifact id` `spring-cloud-starter-openfeign`

## Steps to use Feign Client

- Annotate the DTOs in acordance with the encoder and the decoder being used.
- use `@EnableFeignClients` t oenable the Feign clients on the main application calss.
Example Usage

```java
  @SpringBootApplication
  @EnableFeignClients
  public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }


  ```

  - Annotate the client interface defenition with `@FeignClient`


### Simple CLient COnfiguration

```java
@FeignClient(name = "test", url = "http://localhost:8080")
public interface Client {
	@RequestMapping(method = RequestMethod.GET )
	public Response req();
	
	@RequestMapping(method = RequestMethod.POST)
	public Response post(@RequestBody Request req);
}

```

## Overriding Defaults

- `FeignClientsConfiguration.class` provides the default configurations.

### Configuration with a configuration class

the decault beans provided and required for feign client are 

`Decoder`, `Encoder`, `Logger`,`Contract`,`Feign.Builder`,`Client`

- if Spring Cloud LoadBalancer is in the classpath, FeignBlockingLoadBalancerClient is used. If none of them is in the classpath, the default feign client is used.

Spring Cloud OpenFeign does not provide the following beans by default for feign, but still looks up beans of these types from the application context to create the feign client:

`Logger.Level`, `Retryer`, `ErrorDecoder`, `Request.Options`, `Collection<RequestInterceptor>`, `SetterFactory` ,`QueryMapEncoder`

#### Example

```java
@Configuration
public class FooConfiguration {
    @Bean
    public Contract feignContract() {
        return new feign.Contract.Default();
    }

    @Bean
    public BasicAuthRequestInterceptor basicAuthRequestInterceptor() {
        return new BasicAuthRequestInterceptor("user", "password");
    }

    @Bean
    public OkHttpClient client() {
        return new OkHttpClient();
    }
}
```

### Configuration using application.yml

```yml
feign:
  client:
    config:
      feignName:
        connectTimeout: 5000
        readTimeout: 5000
        loggerLevel: full
        errorDecoder: com.example.SimpleErrorDecoder
        retryer: com.example.SimpleRetryer
        requestInterceptors:
          - com.example.FooRequestInterceptor
          - com.example.BarRequestInterceptor
        decode404: false
        encoder: com.example.SimpleEncoder
        decoder: com.example.SimpleDecoder
        contract: com.example.SimpleContract
```

### Hystrix Support

- `feign.hystrix.enabled=true` to enable hystrix support. Hystrix has fallback support. This allows to implement fallback methods when a method fails. Fallback support is for handling errors when in a client call. we can choose to call the client again or even return a custom or null object in its place.

#### Example for Hystrix support

```java
@Component
public class JSONPlaceHolderFallback implements JSONPlaceHolderClient {

    @Override
    public List<Post> getPosts() {
        return Collections.emptyList();
    }

    @Override
    public Post getPostById(Long postId) {
        return null;
    }
}
```

to let the feign client know that there is a fall back support, use the `fallback` varaible in the `feignClient` Declaration.

```java
@FeignClient(value = "jplaceholder",
  url = "https://jsonplaceholder.typicode.com/",
  fallback = JSONPlaceHolderFallback.class)
  interface Client{
    ....
  }
```

### Logging

enable logging using the package name of the client interfaces in `application.properties`

```application.properties
to enable logging to all clients
logging.level.com.baeldung.cloud.openfeign.client: DEBUG

// to debug only for a perticular client
logging.level.com.baeldung.cloud.openfeign.client.JSONPlaceHolderClient: DEBUG

```

### Error Handling

By default a FeignException is thrown. `ErrorDecoder` interface can  help us handle errors ina  different way.

```java
public class CustomErrorDecoder implements ErrorDecoder {
    @Override
    public Exception decode(String methodKey, Response response) {

        switch (response.status()){
            case 400:
                return new BadRequestException();
            case 404:
                return new NotFoundException();
            default:
                return new Exception("Generic error");
        }
    }
}
```

```java
@Configuration
public class ClientConfiguration {

    @Bean
    public ErrorDecoder errorDecoder() {
        return new CustomErrorDecoder();
    }
}
```

### Configuring using OpenFeign

we can make the client using the Feign Builder API this way

```java
@Import(FeignClientsConfiguration.class)
class FooController {

 private FooClient fooClient;

 private FooClient adminClient;


    	@Autowired
 public FooController(Decoder decoder, Encoder encoder, Client client, Contract contract) {
  this.fooClient = Feign.builder().client(client)
    .encoder(encoder)
    .decoder(decoder)
    .contract(contract)
    .requestInterceptor(new BasicAuthRequestInterceptor("user", "user"))
    .target(FooClient.class, "http://PROD-SVC");

  this.adminClient = Feign.builder().client(client)
    .encoder(encoder)
    .decoder(decoder)
    .contract(contract)
    .requestInterceptor(new BasicAuthRequestInterceptor("admin", "admin"))
    .target(FooClient.class, "http://PROD-SVC");
    }
}
```

