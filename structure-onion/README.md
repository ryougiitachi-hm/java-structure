# Structure of Code

The high-level packages consists of the following layers:
- joint: 
- app: includes service etc. 
- domain: DDD etc. 
- infra: it is short for infrastructure.

## Package: Joint
This layer can be used to place joint from upstream services. 
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

## Layer: Infra
Generally, it is just fine to initialize downstream services just once and provide logic layer invocation with them. 
So it makes sense to put these invocation services into the same place uniformly.

### By service name
For example, there are many other downstream services which we need to invoke, called as customer-service, user-service, account-service etc. 
```
customer
user
account
```
