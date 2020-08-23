What's REST?

## resoures

* [Zalando RESTful API guidelines](https://opensource.zalando.com/restful-api-guidelines/#api-design-principles)
* [Build APIs you won't hate](https://leanpub.com/build-apis-you-wont-hate)
* [Irresistable APIs](https://www.amazon.de/Irresistible-APIs-Designing-that-developers/dp/1617292559)
* [Thoughts on RESTful API Design](https://restful-api-design.readthedocs.io/en/latest/)

(Roy Fielding's dissertation)[https://www.ics.uci.edu/~fielding/pubs/dissertation/software_arch.htm]

Why build APIs using rest?

HTTP vs rest

HTTP is already well supported. 

The basics of how to do it. 

Using the built-in infrastructure: caching..

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

Components are.. 

* User agent - a client that requests access to a resource. The most common example is a web browser.
* Origin server - the definitive source for a set of resources. It provides representations to user agents and may offer functionality to allow resource state changes. 
* Intermediary components - sit between user agents and orgin servers. They forward and sometimes translates requets and responses. For example proxies and gateway proxies may do things like encapsulate interfaces for other services, translate data, enforce security or improve performance. 

## Connectors

Connectors manage network connectivity for components. They encapsulate the activities required to access resources and transfer representations between components and hide the communication mechanisms from the components. 

Connectors provide an abstract interface for requesting resources, so it is possible to substitute access to the origin server with a call to a different connector that may provide additional functionality like access to cached requests. 

This works well because all REST interactions must be stateless, so each request contains all of the information needed to understand and fulfil the request. Any connector between the client and the server can also use this information to enhance or fulfil the request.

The rest architecture describes the following types of connectors:

* Client - initiates communication by sending a request.
* Server - listens for connections and provides access to resources by fulfilling requests with responses. 
* Cache - reduces latency by storing reponses that can be returned for future requests. Caches may live directly on the client, on the server or in between. There are standard request and response meta-data fields that can determine whether or not a response is cacheable. 
* Resolver - translate resource identifiers into network address information. The most common example is a DNS resolver. 
* Tunnel - relays information across network boundaries. For example a HTTP proxy.


# Defining a contract

* Swagger

# Referencing other resources

* HATEOS 
* URIs as identifiers
* URI naming conventions

# Strategies for evolving APIs

You have a problem, so you version your API. Now you have two versions of the problem. 

What type of changes really hurt?

* Exapand and contract
* Semantic versioning
* Version in URI
* Version in accepts header
* Version using content negotiation
* Consumer-driven contracts

# Testing APIs

* Mocking services

# Anti-patterns

* One 'version' per client
* Entity services
* 

