# Compatible extensions pattern

__Also known as__: backward compatibility, non-breaking changes

## Intent
Compatible extensions is a pattern for extend APIs while preserving the behaviour of the existing contract by making only non-breaking changes. 

## Motivation

Change is inevitable 

You don't want to break clients or couple client and server release cycles

Maintaining multiple 


## Pattern

Breaking changes vs non-breaking changes

These types of changes can be backwards compatible:
* Adding completely new endpoint
* Adding optional input fields that have a default value that preserves existing functionality
* Adding additional output fields
* Relaxing validation rules
* Reducing enum ranges on output parameters

These types of changes are breaking changes:
* Adding mandatory input fields or make existing optional fields required
* Removing or renaming existing endpoints or fields
* Changing the semantic meaning of existing endpoints or fields
* Changing the type of fields
* Making validation rules more restrictive
* Reducing enum ranges for input parameters 
* Adding new enum values to output parameters

## Applicability

Making changes as compatible extensions is a great way to make small, ongoing changes to an API's contact. There are a lot of changes that can be made that shouldn't impact other consumers,  

This is more likely to be the case for endpoints that - read-only

It works well for completely new functionality, 

Sometimes avoiding breaking changes can mean compromising on the design of an API. Sometimes requirements change enough that an existing design is no longer an optimal and becomes a barrier to evolving the API in the future. Sometimes the original design was based on assumptions that turned out not to be correct. In these cases, other patterns like [maintaining multiple versions](maintaining-multiple-versions.md) with [planned obsolescence](planned-obsolescence.md) might be a better idea. 

## Challenges

Sometimes new features can interact with existing features in non-obvious ways. 





## Related patterns

* [Semantic versioning](semantic-versioning.md)
* [Expand-contract](expand-contract.md)
* [Tolerant reader](tolerant-reader.md)

## Useful resources
* [Zalando API guidelines](https://opensource.zalando.com/restful-api-guidelines/#107)
* [Preliminary Analysis of REST API Style Guidelines](https://pdfs.semanticscholar.org/adf6/e0d0a7223fc2c7a5829b224c4687e910caa4.pdf)
* [Designing for backwards compatibility](https://tedspence.com/api-design-backwards-compatibility-5899258fa5c3)