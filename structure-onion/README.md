# Structure of Code

The high-level packages consists of the following layers:
- joint: 
- app: includes service etc. 
- domain: DDD etc. 
- infra: it is short for infrastructure.

There are several principles about which classes should or not be used in the specific layers: 
- joint and infra: Any classes can be used, because these layers are responsible for docking with external services, referred frameworks would be various. 
- app and domain: Only should built-in JDK classes be used(include java.** and javax.* etc). These layers include the core business logic, where it is better to not refer to other frameworks in case of replacing technical frameworks in the future. 

## Package: Joint
This layer can be used to place joint from upstream services. 
Usually, joint layer places the invokee side, including but not limiting mainly request from upstream system, such as mq, http endpoint etc.

Usually, there are the following styles to organise joints:
- By the type of interface
- By service name

### By the type of interface
For example, upstream services have varieties of invocations, such as restful API, kafka, gRPC etc. 
We can create the structure of package in joint layer
```
restful
kafka
grpc
```

### By service name
For example, upstream services have varieties of invocations, such as restful API, kafka, gRPC etc. 

### Naming convention

Different types of input endpoints can have different naming postfix to make it clear to identify the usage of classes. 

For example, as follows: 
- HTTP RESTFUL: *Resource - used for http endpoints implemented by jaxrs(javax.ws.rs:javax.ws.rs-api or jakarta.ws.rs:jakarta.ws.rs-api)
- HTTP RESTFUL: *Controller - used for http endpoints implemented by spring-mvc or spring-web. 
- Websocket: *Websocket
- TCP: to be decided. *Endpoint, *TCP etc as alternatives. 
- GPRC: to be decided. *Endpoint, *GrpcEndpoint, *GrpcService(easy to confound with Service in app layer) etc as alternatives.
- KAFKA: should be placed in infra layer for both producer and consumer. 

## Layer: Application
Business logic implementation. 
as follow: 
- service: places Service classes, used to organise business logic. 

As per principle, there should not be non-java built-in classes in application layer.
But if we use some necessary dependencies(such as ioc/di, spring etc), it is unavoidable to use relevant external dependencies. 
In this case, we can put relevant config about dependency injections into a config package, which will be the only package referring to external dependencies in this layer. 

## Layer: Infra
Generally, it is just fine to initialize downstream services just once and provide logic layer invocation with them. 
Usually, infra layer places the invoker side, including but not limiting such as database, mq(kafka etc), restful api etc.
So it makes sense to put these invocation services into the same place uniformly.

### By service name
For example, there are many other downstream services which we need to invoke, called as customer-service, user-service, account-service etc. 

// should be the structure of tree. 
```
customer
user
account
```
