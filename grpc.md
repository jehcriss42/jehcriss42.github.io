*gRPC - Overview and Testing Strategy*

Starting from the beginning:

**Remote Procedure Call (RPC):**

RPC is a protocol used in the operating system and intends to provide a logical client-to-server communication specifically for the support of network applications (IBM document about RPC concepts here). 

gRPC was initially created by Google but it is an open source RPC framework for a few years now (a curiosity about the g here).

**How gRPC works?**

Remember the client-to-server communication? Basically, the client connects to the server using the Proto request. The gRPC Server is defined with the methods, parameters, and return types that can be called remotely.

  <img align="central" src="https://grpc.io/img/landing-2.svg" />

It is important to know the request and response are based on a binary payload (so if we want to know the content of the requests and responses, we need to use some tool to decode). The reason of this is the Protocol Buffers.

Protocol Buffers provides a mechanism for serializing structured data. It is based on the definition language created in the proto files, proto compiler, run time libraries, and serialization. By using Protocol Buffers, we have advantages such as compact data storage, fast parsing, and availability in many programming languages.

An example of the content of a proto file is:



**What is the difference between gRPC and REST?**

They are models to design APIs. 

Representational State Transfer (REST) is not a protocol or standard; it can be implemented in different ways. When a request is made by a client, the information is delivered in a format like JSON, HTML, plain text, etc.  There are a few criterias to be considered RESTful, which is a set of architectural constraints, for example, a client-server architecture with requests managed through HTTP, and stateless client-server communication. To check it in more detail, click here.

By now you should have realized a few differences in the architecture and data exchange. 

There are pros and cons to each API design. It does not stop at REST and gRPC, there is  SOAP, Graphql, and so on.

I'll leave it to you to do this research if you are interested. :)

**How are we going to test gRPC implementation?**

Thinking about Testing/Quality Assurance in a project is the same as thinking about Software Engineering. From the Requirements, Design, Code Standards, and DevOps (CI/CD with continuous testing). To put it in perspective a CI/CD process can look like this:

Development/Code Analysis

Unit Test/Mutation test 

Code Review 

Deploy in an environment 

Health Check 

Smoke Test 

Sanity Test 

Integration Test 

Regression Test
Focusing on the tests after a version is deployed in an environment (such as dev, qa, production - or even local) for the gRPC implementation, there are several tools available. The selection of the tools depends on the way to connect to gRPC Server: unary RPC, server streaming RPC, client streaming RPC, bidirectional streaming RPC. For example:

Grpcurl (very similar to curl), BloomRPC, Postman, and Insomnia: they supports all kinds of RPC methods, including streaming methods;

But these tools do not provide the test section so different scenarios can be added and automatically tested. 

Another option is to customize this: 

It is possible to create a test automation architecture based on a programming language supported by gRPC so clients can be created and test scenarios can be added. For example:

Using .NET and xUnit the test architecture can look like this: 



And there is a lot more to explore, such as performance and security test.

A considerable difference between REST and gRPC is contract testing. While there are tools for REST APIs such as PACT and Spring Cloud Contract, the proto file serves as the contract for gRPC. It is the same file that clients will use. But we can have contract issues when we create services with dependencies (but this is a new subject!).
