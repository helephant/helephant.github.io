
You have a problem that forces you to evolve your API contract, so you create a new version. Now you have two problems. 

What sort of change break the interface?

Here is my toolbox of options in accomodating change in services. 

How your audience change how you will evolve
* inside a project
* inside a company
* from consumer devices
* public API

## Evolving APIs
The best choices will depend a lot on the context of the system, but here are some options available when circumstances for a change of an existing API that is consumed by an independent consumer: 

* [Compatible extensions](compatible-extensions.md) - make backwards compatible changes that won't break [tolerant readers](tolerant-reader.md)
* [Maintaining multiple versions](maintaining-multiple-versions.md) - maintain multiple versions of the API
* [Breaking changes](breaking-changes.md) - make breaking changes that force clients to upgrade

If the API is extended to support both new and old clients, it is important to be explicit about what the long term support is to set the expectations for the client and to allow the team evolving the service to plan. Having multiple ways to access the same functionality can quickly add complexity and make the API difficult to maintain and evolve in the future. 

* [Expand contract](expand-contract.md) - first support the new and old way to interact with the API simultaneously and then remove the old way
* Deprecating things - sunset period
* [Support all versions forever](https://stripe.com/gb/blog/api-versioning)
* Planned obsolescence

## Declaring versions
* [Semantic versioning](semantic-versioning.md)
* [W3C paper on versioning](https://www.w3.org/2001/tag/doc/versioning)

## Allowing a client to request a version
* Version in uri - url or resource
* Version in header
* Content negotiation

## Something Consumer-Service contracts
* Schemas
* [Specification by example](https://www.thoughtworks.com/insights/blog/specification-example)
* [Consumer-driven contract tests](consumer-driven-contract-tests.md)
* Integration tests
* Integration contract tests


## Client patterns
Generally the service provider makes most of the decisions around and bears much of the cost of evolving a contract. Changes can be disruptive for the client particularly if they happen often or if the client is not interested in the new functionality. Here are some patterns for minimizing the client's coupling to a service contract.

* [Tolerant reader](tolerant-reader.md)
* Must forward (http://www.amundsen.com/talks/2017-03-sxsw/2017-03-sxsw-patterns.pdf)

## Anti-patterns

* Coupling client and service release cycles

https://www.amazon.co.uk/Service-Design-Patterns-Fundamental-Addison-Wesley/dp/032154420X/ref=sr_1_1?crid=NWQANE2YN385&keywords=service+design+patterns&qid=1570786007&sprefix=service+design+pattern%2Caps%2C151&sr=8-1