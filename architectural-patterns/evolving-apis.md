
You have a problem that forces you to evolve your API, now you have two problems. 

What sort of change break the interface?

How your audience change how you will evolve
* inside a project
* inside a company
* from consumer devices
* public API

What pattern is graphql?

* Semantic versioning
* How to ask for a version
* How to specify a version

Getting design right
* Messages not objects
* Share vocabularies not models

https://stripe.com/gb/blog/api-versioning

## Evolving APIs
* Non-breaking changes
* Supporting multiple versions
* Deprecating things - sunset period
* Aggressive obsolescence
* [Expand contract](api-expand-contract.md)
* consumer-driven contracts (https://martinfowler.com/articles/consumerDrivenContracts.html)
* 

## Ways to 
* Version in uri - url or resource
* Version in header
* Content negotiation

## API tests
* Contract tests (https://martinfowler.com/bliki/ContractTest.html)


## Client patterns
* Tolerant reader/Must ignore
* Must forward (http://www.amundsen.com/talks/2017-03-sxsw/2017-03-sxsw-patterns.pdf)

## Anti-patterns


https://www.amazon.co.uk/Service-Design-Patterns-Fundamental-Addison-Wesley/dp/032154420X/ref=sr_1_1?crid=NWQANE2YN385&keywords=service+design+patterns&qid=1570786007&sprefix=service+design+pattern%2Caps%2C151&sr=8-1