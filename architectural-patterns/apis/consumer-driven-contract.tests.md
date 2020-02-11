# Consumer-driven contract tests

## Intent
Consumer-driven contract tests explicitly document consumer expectations of a service and allow the service to get fast feedback in understanding whether changes violate the expections of any consumer.

## Motivation

Consumer-driven contract tests express the expectations of each consumer explicitly as a test that is part of the service. The team that owns the service then can understand what expectations are for each client and get fast feedback if changes to the service will no longer meet those expectations. 

Consumer-driven contracts allow the service to be tested in isolation to the consumer. In theory, you should not have to run a real version of the consumer against the real version of the service to understand whether the change you have made is compatible. 

## Pattern

A consumer-driven contract is .... 

It can optionally be expressed as a set of tests that belong to the service which ensure that the service will continue to meet its commitment to that client as the service evolves, or could be expressed in other ways such as documentation. 


## Applicability

Multiple consumers, but not too many

Work better internally to an organisation - requires close collaboration between consumer and service

## Challenges

Up to date

Tests may be incomplete

Does not test for expectations around non-functional requirements

## Related patterns

* Integration tests

## Significant tools

* Pact tests

## Useful resources
* A description of the pattern on [Martin Fowler's website](https://martinfowler.com/articles/consumerDrivenContracts.html)
* Consumer-driven contracts on the [thoughtworks tech radar](https://www.thoughtworks.com/radar/techniques/consumer-driven-contract-testing)
* [Pact](https://docs.pact.io/#consumer-driven-contracts) - a tool for automating consumer-driven contracts
* [Pact nirvana](https://docs.google.com/document/d/e/2PACX-1vRf1kSDccImNipOOm1G-bjcSs-ifbZjf1v54K-dIcq8BLKeFPAAm_bf_p71UKqkRMIx30QWWL-kN8TI/pub)