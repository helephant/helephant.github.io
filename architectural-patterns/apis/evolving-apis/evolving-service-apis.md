
You have a problem that forces you to evolve your API contract, so you create a new version. Now you have two problems. 

What sort of change break the interface?

How your audience change how you will evolve
* inside a project
* inside a company
* from consumer devices
* public API

What pattern is graphql?

Versioning:
* [Semantic versioning](semantic-versioning.md)
* [W3C paper on versioning](https://www.w3.org/2001/tag/doc/versioning)
* How to ask for a version
* How to specify a version

Getting design right
* Messages not objects
* Share vocabularies not models
* Share contracts, not types

https://stripe.com/gb/blog/api-versioning

## Evolving APIs
* Non-breaking changes - backward and forward compatibility
* Supporting multiple versions
* Deprecating things - sunset period
* Aggressive obsolescence
* [Expand contract](expand-contract.md)

## Ways to 
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


https://www.amazon.co.uk/Service-Design-Patterns-Fundamental-Addison-Wesley/dp/032154420X/ref=sr_1_1?crid=NWQANE2YN385&keywords=service+design+patterns&qid=1570786007&sprefix=service+design+pattern%2Caps%2C151&sr=8-1