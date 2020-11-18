- [Intorduction](#intorduction)
  - [What is Camel?](#what-is-camel)
    - [Camel core Architecture](#camel-core-architecture)
      - [Routing and mediation engine](#routing-and-mediation-engine)
      - [Extensive component library](#extensive-component-library)
      - [(EIP) Enterprise integration patterns](#eip-enterprise-integration-patterns)
      - [DSL](#dsl)
    - [Camel’s message model](#camels-message-model)
    - [Message](#message)
      - [Headers and Attachments](#headers-and-attachments)
      - [Body](#body)
    - [Exchange](#exchange)
  - [Architecture](#architecture)
  - [Camel Concepts](#camel-concepts)
    - [Camle Context](#camle-context)
    - [Routes](#routes)
      - [Route Format in Java DSL](#route-format-in-java-dsl)
  - [Importrant Camel Components](#importrant-camel-components)
    - [Direct Component](#direct-component)
    - [HTTP Component](#http-component)
  - [ProducerTemplate](#producertemplate)
    - [important methods](#important-methods)
    - [Example call](#example-call)
  - [Consumer Template](#consumer-template)
  - [important Methods](#important-methods-1)
  - [Sample Code](#sample-code)
    - [Route](#route)
    - [Producer and ConsumerTemplate Usage](#producer-and-consumertemplate-usage)

# Intorduction

Apache camle is an integration framework which can connect different services or platforms with ease and with the developer not needing to know the underlying specifics of each technology they are using. 

## What is Camel?

At the core of the Camel framework is a routing engine—or more precisely, a routing-engine builder. It allows you to define your own routing rules, decide from which sources to accept messages, and determine how to process and send those messages to other destinations. Camel uses an integration language that allows you to define complex routing rules, akin to business processes. the fundamental principles of Camel is that it makes no assumptions about the type of data you need to process.

### Camel core Architecture

#### Routing and mediation engine

The core feature of Camel is its routing and mediation engine. A routing engine selectively moves a message around, based on the route’s configuration.

#### Extensive component library

Camel provides an extensive library of more than 280 components. These components enable Camel to connect over transports, use APIs, and understand data formats.

#### (EIP) Enterprise integration patterns

Camel is heavily based on EIPs. Although EIPs describe integration problems and solutions and provide a common vocabulary, the vocabulary isn’t formalized. Camel tries to close this gap by providing a language to describe the integration solutions.

#### DSL

At its inception, Camel’s domain-specific language (DSL) was a major contribution to the integration space. Since then, several other integration frameworks have followed suit and now feature DSLs in Java, XML, or custom languages. The purpose of the DSL is to allow the developer to focus on the integration problem rather than on the tool—the programming language. Here are some examples of the DSL using different formats and staying functionally equivalent

### Camel’s message model

Camel uses two abstractions for modeling messages,

- `org.apache.camel.Message` —The fundamental entity containing the data being carried and routed in Camel.
- `org.apache.camel.Exchange`—The Camel abstraction for an exchange of messages. This exchange of messages has an in message, and as a reply, an out message.

### Message

Messages are the entities used by systems to communicate with each other when using messaging channels. Messages flow in one direction, from a sender to a receiver. Messages are uniquely identified with an identifier of type java.lang.String. The identifier’s uniqueness is enforced and guaranteed by the message creator, it’s protocol dependent, and it doesn’t have a guaranteed format.

![Camel Message](/images/camelMessage.PNG)

#### Headers and Attachments

Headers are values associated with the message, such as sender identifiers, hints about content encoding, authentication information, and so on. Headers are name-value pairs; the name is a unique, case-insensitive string, and the value is of type java.lang.Object. Camel imposes no constraints on the type of the headers.

#### Body

The body is of type java.lang.Object, so a message can store any kind of content and any size. It’s up to the application designer to make sure that the receiver can understand the content of the message. When the sender and receiver use different body formats, Camel provides mechanisms to transform the data into an acceptable format, and in those cases the conversion happens automatically with type converters, behind the scenes.

### Exchange 

An exchange in Camel is the message’s container during routing. An exchange also provides support for the various types of interactions between systems, also known as message exchange patterns (MEPs)

- `InOnly` — A one-way message (also known as an event message).
- `InOut` —A request-response message. For example, HTTP-based transports are often request-reply.

[](/images/camelExchange.PNG)

- `Exchange ID`: A unique ID that identifies the exchange. Camel automatically generates the unique ID.
- `MEP` : A pattern that denotes whether you’re using the InOnly or InOut messaging style. 

## Architecture

[](/images/camelArchitecture.PNG)

The routing engine uses routes as specifications indicating where messages are routed. Routes are defined using one of Camel’s DSLs. Processors are used to transform and manipulate messages during routing as well as to implement all the EIPs, which have corresponding names in the DSLs. Components are the extension points in Camel for adding connectivity to other systems. To expose these systems to the rest of Camel, components provide an endpoint interface.

## Camel Concepts

### Camle Context

it contains the following things:

- Components
  - camel core components like `http`, `file`, etc; each dealing with specific
- Endpoints
  - Markers is a route denoting the denoting the position in a route. it can be startm end or any component call.
- Routes
- Type Converters
- Data formats
- Registry
- Languages

### Routes

Routes are obviously a core abstraction for Camel. The simplest way to define a route is as a chain of processors. There are many reasons for using routers in messaging applications. By decoupling clients from servers, and producers from consumers, routes can do the following:

#### Route Format in Java DSL

> "<component_name:any_name>?query_parameters"

Example:

```java
from("direct:abcd")
			.setHeader(Exchange.HTTP_METHOD, simple("GET"))
			.to("ahc:http://localhost:8080").unmarshal(jsonDataFormat).to("direct:end");
```

## Importrant Camel Components

### Direct Component

The Direct component provides direct, synchronous invocation of any consumers when a producer sends a message exchange.
This endpoint can be used to connect existing routes in the same camel context.

### HTTP Component

It handles the http requests with configuration specified in its HEADERS and BODY or the exchange.

## ProducerTemplate

This can be used to produce a request and also consume the response in case on InOut exchanges.

### important methods

```java
  <T> CompletableFuture<T>	asyncRequestBody(Endpoint endpoint, Object body, Class<T> type)
  CompletableFuture<Exchange>	asyncCallback(Endpoint endpoint, Exchange exchange, Synchronization onCompletion)
  CompletableFuture<Exchange>	asyncSend(Endpoint endpoint, Exchange exchange)
```

### Example call  

```java
//InOut Requestr
Response resp = producerTemplate.requestBody("direct:route1",null,Response.class);

// InOnly
Response resp = producerTemplate.asyncSendBody("direct:route1",Request);
```

## Consumer Template 

can be used to consume and use the exchange at any endpoint which can be the end or any component call in the middle of the route

## important Methods

```java
Object receiveBody(Endpoint endpoint)
Object receiveBody(String endpointUri,
                   long timeout)
Object receiveBodyNoWait(String endpointUri)

<T> T receiveBody(String endpointUri,
                  Class<T> type)


```



```java
Exchange exchange = consumer.receive("direct:end",10000);
```

## Sample Code

### Route

```java
@Component
public class RequestRouter extends RouteBuilder {

	@Override
	public void configure() throws Exception {
		
		JacksonDataFormat jsonDataFormat = new JacksonDataFormat(Response.class);
		
		from("direct:abcd")
			.setHeader(Exchange.HTTP_METHOD, simple("GET"))
			.to("ahc:http://localhost:8080").unmarshal(jsonDataFormat).to("direct:end");
				
	}
}
```

### Producer and ConsumerTemplate Usage

```java
@RestController("/")
public class Controller {

	@Autowired
	ProducerTemplate template;
	
	@Autowired
	ConsumerTemplate consumer;
	
	@GetMapping
	public Response getReq() throws Exception
	{				
		template.asyncSendBody("direct:abcd",null);
		Exchange exchange = consumer.receive("direct:end",10000);
		Response resp = exchange.getIn().getBody(Response.class)
		System.out.println("message 1 " + resp);		
		return resp; 
	}
```

Here Spring takes care of injection of producer and consumer template and the producer calls the `direct:abcd` route and the consumer consumes the `direct:end` which is the end of the route. since the producer produces the request using a async command, the main thread can go with its flow instead of waiting for the route to be done and dealt with.
