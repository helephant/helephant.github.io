# Compatible extensions pattern

__Also known as__: backward compatibility, non-breaking changes

## Intent
Compatible extensions is a pattern for extend APIs while preserving the behaviour of the existing contract by making only non-breaking changes. 

## Motivation

This pattern allows certain types of changes to an API without breaking commpatibility for existing clients, provided they are [tolerant readers](tolerant-reader.md). It decouples client and server release cycles.

## Pattern

Only changes which allow existing consumers to continue consuming the API without being updated are allowed. This means avoiding changing parts of the API that existing clients are coupled to or making any contraints on the API more strict. 

These types of changes will only be backwards compatible provided they preserve the current behavior and semantics of the API:
* Adding optional input fields that have a default value that preserves existing functionality
* Adding additional output fields
* Relaxing validation rules
* Adding new enum ranges for input parameters
* Reducing enum ranges on output parameters

These types of changes will be breaking changes and are not compatible extensions: 
* Adding mandatory input fields or make existing optional fields required
* Removing or renaming existing endpoints or fields
* Changing the semantic meaning of existing endpoints or fields
* Changing the type of fields
* Making validation rules more restrictive
* Reducing enum ranges for input parameters 
* Adding new enum values to output parameters

## Applicability

Making changes as compatible extensions is a great way to make small, ongoing changes to an API's contact. There are a lot of changes that can be made that shouldn't impact other consumers, provided they are [tolerant readers](tolerant-reader.md).

This is a useful when it is difficult to change all existing clients at the same time as the service API, such as APIs with many or external consumers.

It is often easier to make compatible extensions to read-only endpoints than ones that accept data from a client. Clients can often safely ignore extra fields returned in a response, but many new input fields will be required or not possible to default. 

## Challenges

It is possible to accidentally change the behaviour or semantic meaning of an endpoint while preserving the API. While existing clients may continue to still be able to communicate with the service, the end result may not be the same as before. 

Sometimes new features can interact with existing features in non-obvious ways, which can introduce subtle bugs for either new or existing clients or for clients that use particular combinations of endpoints or parameters. 

Sometimes avoiding breaking changes can mean compromising on the design of an API. Sometimes requirements change enough that an existing design is no longer an optimal and becomes a barrier to evolving the API in the future. Sometimes the original design was based on assumptions that turned out not to be correct. In these cases, other patterns like [maintaining multiple versions](maintaining-multiple-versions.md) with [planned obsolescence](planned-obsolescence.md) might be a better idea. 

It is also possible that, extending an API in a compatible way will drive a signficant amount of complexity into either the API or the implementation of it.

## Related patterns

* [Tolerant reader](tolerant-reader.md)
* [Expand-contract](expand-contract.md)

## Useful resources
* [Zalando API guidelines](https://opensource.zalando.com/restful-api-guidelines/#107)
* [Preliminary Analysis of REST API Style Guidelines](https://pdfs.semanticscholar.org/adf6/e0d0a7223fc2c7a5829b224c4687e910caa4.pdf)
* [Designing for backwards compatibility](https://tedspence.com/api-design-backwards-compatibility-5899258fa5c3)