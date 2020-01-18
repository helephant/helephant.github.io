#REST - the architecture of the web

REST, Representational State Transfer, formally describes the architecture and constraints that define the World Wide Web. 

It's hard to think of a computer system in the world that has been more successful than the web or had such an impact on the way we live. I think that makes its design quite interesting to anyone who designs distributed systems. 

The REST architectural style was documented by (Roy Fielding)[https://roy.gbiv.com/untangled/] who was an author of the HTTP protocol and co-founder of the Apache HTTP server project. It is documented in his (surprisingly readable dissertation))[https://www.ics.uci.edu/~fielding/pubs/dissertation/software_arch.htm] which was published in 2000. His goal was to capture the current architectural characteristics of the web so they could be used to evaulate future proposals and understand whether they would change the characteristics of the system. 


## The requirements of the web

What makes the web different from other systems?

- The scale of the web
- Crossing organisational boundaries
- Gradual, fragmented change
- Enables machine to human, machine to machine communication
- Needed to be easy to get started with

When the web was first created, the goal was for people to share information across organisational boundaries. It is structured as a distributed hypermedia system, which was general enough to support many different types of information and enabled complex interlinking of resources.

Sharing information across systems from different organisation throws up challenges because groups that provide a service have limited influence over the groups that consume it. This cause many of the challanges around providing internet scale services including:
- limited control over the load or validity of messages
- multiple trust boundaries can be present in a single transaction
- possible malicious actors

To build a cross-organisational distributed system, the web needed to be tolerate resources changing independently and availability. It is important to continually evolve the standards and technologies that underpin the web and that can be rolled out gradually. Newer resources and older resources need to be able to coexist. 

It is also important that differenet resources operate very independently so that it is possible to consume content, even if the other resources that the service link to are unavailable.  

# The building block stanards of the web


URI, HTTP and HTML


#REST architectural constraints

To achieve these goals, 

The REST architecture is defined by a set of architectural constraints that restrict the design and implementation choices of the system in order to achieve what? 

##Client-server
The user interface concerns are separated from data storage so both can evolve independently, even across organisational boundaries. 

##Stateless 
Each request must contain all of the information needed by the server to supply the response and does not take advantage of stored context on the server. Session state is maintained by the client. 

This constraint improves:
* visibility - the request is atomic and it is possible to understand the interaction by seeing just a single request
* scalability - it allows horizontal scaling across multiple servers to respond to requests 
* reliability - makes it easier to recover from partial failures

It also makes it possible to introduce components between the client and the server like caches, proxies and loggers that can view, modify or respond to the requests.

##Cacheable
To improve network efficiency, data within a response must be identified as cacheable or non-cacheable. If the data is cacheable, the client may re-use the response for subsequent requests. This can improve performance for the end user. 

##Uniform interface
A REST architecture must provide a uniform interface for communicating between client and server. 

This simplifies the communication between components. The components are decoupled from the services they provide, which makes them easier to evolve. It means it's possible to create generalised components that can provide aspects of the system, without being coupled to the details of each service or client. 

## Layered system

A REST architecture must be extensible by allowing multiple layers of components that can not see past the immediate layer they are interacting with. Restricting this promotes service independent. Layers can encapsulate systems built on a different architecture, break down complex components into smaller pieces, distribute owership, load balance requests across multiple servers. 

# The elements of a REST architecture

## Resource 

A resource is the core REST abstraction. It is what we call a piece of information that can be the target of a hypertext rerference. 

* The semantic concept that the resource targets should not change. 
* The data that a resource targets can change. For example a resource that represents tomorrow's weather would return different temperatures depending on when it was called.
* A resource may contain both data and references to other resources. 
* Resources may be an empty set. This allows clients to target resoources that do not currently exist. 
* A resource can be any information that can be named. It could return text, a HTML document, JSON data, an image, a binary stream.. 

Resources are identified by resource identifiers, which are URIs. 

## Representation 

A representation is used to transfer information about a resource between components. It can be used to retrieve the current state of a resource or be provided by a client to request an update to the resource's state.

* A representation is a series of bytes that represent the resource, plus meta data to describe it. 
* The meta-data is representated as key-value pairs.
* The meta-data can contain information about the representation, the resource and sometimes about the message (such as data to verify integrity).
* The REST architecture does not put any restrictions on how to represent resources. This has been deliberately left generic.  

A resource may support multiple representations, which can be selected using content negotiation based on the request's meta-data. 

* The data format of a representation is returned in a meta-data field called a media-type. 
* The client can send a media-type to specify what type of representation it would like to receive.
* Composite media-types can be used to return multiple representations within the same message.

## Components

There are basically three different types of components in a REST architecture:

* User agents - a client that requests access to a resource. The most common example is a web browser, but it may also be something like a web-scraper or another service that consumes a resource. 
* Origin servers - the definitive source for a set of resources. It provides representations to user agents and may offer functionality to allow resource state changes. 
* Intermediary components - sit between user agents and orgin servers. They forward and sometimes translates requets and responses. For example proxies and gateway proxies may do things like encapsulate interfaces for other services, translate data, enforce security or improve performance. 

## Connectors

Connectors manage network connectivity for components. They encapsulate the activities required to access resources and transfer representations between components and hide the communication mechanisms from the components. 

Connectors provide an abstract interface for requesting resources, so it is possible to substitute access to the origin server with a call to a different connector that may provide additional functionality like access to cached requests. 

This works well because all REST interactions must be stateless. Each request contains all of the information needed to understand and fulfil the request. Any connector between the client and the server can also use this information to enhance or fulfil the request.

The REST architecture describes the following types of connectors:

* Client - initiates communication by sending a request.
* Server - listens for connections and provides access to resources by fulfilling requests with responses. 
* Cache - reduces latency by storing reponses that can be returned for future requests. Caches may live directly on the client, on the server or in between. There are standard request and response meta-data fields that can determine whether or not a response is cacheable. 
* Resolver - translate resource identifiers into network address information. The most common example is a DNS resolver. 
* Tunnel - relays information across network boundaries. For example a HTTP proxy.

# What does this mean for people designing other systems?