# Introduction to gRPC

`Modern software system` is a collection of distributed msoftware applications that are running at different network locations and communicate with each other with message passing using different communication protocols.

`Microservices architecture` is about building a software application as a collection of independent, autonomous (developed, deployed, and scaled independently), business capability-oriented, and lossely coupled services.

`Inter-process communications` are usually implemented using message passing with a synchronous request-response style or asynchronous event-driven styles.

In the `synchronous communication style`, the client process sends a request message to the server process over the network and waits for a response message.

In `asynchronous event-driven messaging`, processes communicate with asynchronous message passing by using an intermediary known as an `event broker`.

It's common to build synchronous communication as `RESTful services`, where you model your application or services as a collection of resources that can be accessed and have their state changed via network calls that take place over HTTP protocol. However, they are quite bulky, inefficient, and error-prone. This is where gRPC comes into picture.

## What is gRPC?

`gRPC` is an inter-process communication technology that allows you to connect, invoke, operate, and debug distributed heterogeneous applications as easily as making a local function call.

`The service interface definition` contains information on how your service can be consumed by consumers, what methods you allow them to call, what method parameters and message formats to use when invoking those methods, etc. It is specified using `Interface Definition Language (IDL)`.

Using service definition, you can generate server-side code known as `server skeleton`, which simplifies the server-side logic by providing low-level communication abstractions. You can also generate client-side code, known as `client stub`, which simplifies the client-side communication with abstractions to hide low-level communication for different programming languages.

The underlying gRPC framework handles all the complexities that are normally associated with enforcing strict service contracts, data serialization, network communication,authentication, access control, observability, and so on.

## Service Definition

gRPC uses `protocol buffers` as the IDL to define the service interface. Protocol buffers are a language-agnostic, platform-neutral, extensible mechanism to serializing structured data.

Since the service definition is an extension to the protocol buffer specification, a special gRPC plug0in is used to generate code from the proto file.

A service is thus a collection of methods that can be remotely invoked. Each method has input parameters and return types that we define as either part of the service or that can be imported into the protocol buffer definition.

## gRPC Server

To make the service do its job, you need to do the following:

- Implement the service logic of the generated service skeleton by overriding the service base class.
- Run a gRPC server to listen for requests from clients and return the service responses.

## gRPC Client

The client stub provides the same methods as the server, which your client code can invoke; the client stub translates them to remote function invocation network calls that go to the server side.

## Client-server Message Flow

When a gRPC client invokes a gRPC service, the client-side gRPC library uses the protocol buffer and marshals the remote procedure call, which is then sent over HTTP/2. On the server side, the request is unmarshaled and the respective procedure invocation is executed using protocol buffers.

## Evolution of Inter-Process Communication

### Conventional RPC

RPC was a popular inter-process communication technique for building client-service applications. With RPC a client can remotely invoke a function of a method just like calling a local method.However, most such conventional RPC implementations are overwhelmingly complex, as they are built on top of communication protocols such as TCP, which hinders interoperability and are based on bloated specifications.

### SOAP

`Simple Object Access Protocol` is the standard communication technique in a service-oriented architecture to exchange XML-based structured data between services and communicates over any underlying communication protocol such as HTTP.

With SOAP you can define the service interface, operations of that service and an associated XML message format to be used to invoke those operations. However, the complexity of message format and complexities of specifications built around SOAP, hinders the agility of building distributed applications.

### REST

`Representational State Transfer` is the foundation of the resource-oriented architecture, where you model distributed applications as a collection of resources and the clients that access those resources can change the state of those resources.

In HTTP you can model a RESTful web application as a collection of resources accessible using a unique identifier (URL). The state-changing operations are applied on top of those resources in the form of HTTP verbs (GET, POST, etc.). The resource state is represented in text formats such as JSON, XML, HTML, YAML.

However, with the proliferation of number of microservices and their network interactions RESTful services have not been able to meet the expected requirements, such as:

- Inefficient text-based message protocols
- Lacks strongly typed interfaces between apps
- REST architectural style is hard to enforce
