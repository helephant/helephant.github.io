# Tolerant reader

## Intent



## Motivation

Change is inevitable. Even the most well-designed contracts between a service and its consumer will need to evolve as the requirements for the system change. There is often a learning process when a service is created and with an original design based on imperfect knowledge. 

Most patterns focus on how the service can be designed to accommodate change. This is a pattern where the consumer can reduce the surface area of its dependency on a service.

Changing a contract between a service and its consumers becomes progressively more difficult as the number of consumers increases, particularly in systems where there is different ownership between service and consumers. The greater the cost of the change, the less able the service providers are able to respond to the requirements of the business. It is also more likely that change will happen as disruptive and risky large changes, rather than frequent small iterations. 

Forward and backwards comptaible.

## Pattern

The code that consumes the service in the consumer should only read the parts of the interface that the consumer is interested in. It should ignore everything else. 

If this pattern is successfully applied, the consumer should continue working if the service changes a part of the interface that the consumer doesn't use. The service should be able to add new fields, omit optional items, rename fields the consumer doesn't use, change their types or remove them. If the consumer doesn't use it, it shouldn't need to change to accomodate the new schema. 

Some techniques are not compatible with tolerant reader because they force the consumer to bind to the entire interface:
* Applying a schema to the entire message before reading it
* Some tools that create stub objects from service definitions in strongly typed languages

## Applicability


## Related patterns

* [Consumer-driven contract tests](consumer-driven-contract-tests.md)

## Useful resources

* [Martin Fowler](https://martinfowler.com/bliki/TolerantReader.html) - definitive description of the pattern
