# Consumer-driven contract tests

## Intent
Consumer-driven contract tests explicitly document consumer expectations of a service and allow the service to get fast feedback in understanding whether changes violate the expections of any consumer.

## Motivation

Consumer-driven contract tests express the expectations of each consumer explicitly as a test that is part of the service. The team that owns the service then can understand what expectations are for each client and get fast feedback if changes to the service will no longer meet those expectations. 

Both of these things help consumers as well as service providers. A reliable and stable service helps consumers because it means their system can deliver on its goals. The ability of service providers to move faster and more confidently means they can be more responsive to consumer needs. Being able to deliver both of these things builds trust between both groups. 

Consumer-driven contracts allow the service to be tested in isolation to the consumer. In theory, you should not have to run a real version of the consumer against the real version of the service to understand whether the change you have made to either system are compatible. This can mean not needing to deal with the complicated and slow integration environments that are expensive to maintain and can often be unreliable.

## Pattern

A consumer-driven contract testing is a set of automated tests that belong to the service which ensure that the service will continue to meet its commitment to each client as the service evolves. They express each client's expectations of the contract between client and service. 

## Applicability

This is most useful in scenarios where there are multiple consumers for a single service. If there is only a single consumer then hopefully the service's contract and the consumer's expectations are near to being the same. This would mean there shouldn't be significant differences between provider driven contract tests and consumer driven contract tests. 

I can see this being more practical when consumer and service are both internal to a company or when there are a small number of external consumers with a close relationship with the team. This would not be practical with many external consumers that did not have a relationship with the team and were able to collaborate on building and maintaining the tests. 

## Challenges

I think the biggest challenge would be keeping the tests up to date, since changes in expectations would generally come from the consumer and could happen at any time without the service provider being aware. This may be mitigated by frameworks like [Pact](https://docs.pact.io/#consumer-driven-contracts) that make it possible to automate the changes between consumers and service.

These tests have the same challenges as any other types off test in that they are only as good as the cases they test. It's always a challenge, but it doesn't mean there's not value in automation. You very quickly discover if the tests are no high enough quality when you start to make changes. Issues quickly give you a sense of what is missing. 

Another thing that is a wider issue than consumer driven contract tests is they probably won't give you an idea of non-functional requirements that consumers rely on such as scalability and latency.

## Related patterns

* Integration tests

## Useful resources
* A description of the pattern on [Martin Fowler's website](https://martinfowler.com/articles/consumerDrivenContracts.html)
* Consumer-driven contracts on the [thoughtworks tech radar](https://www.thoughtworks.com/radar/techniques/consumer-driven-contract-testing)
* [Introduction to consumer-driven contract testing](https://medium.com/kreuzwerker-gmbh/introduction-to-consumer-driven-contract-testing-3a130c8c2ea0)
* [Verifying microservice integration with contract testing](https://www.youtube.com/watch?v=-6x6XBDf9sQ)
* [Pact](https://docs.pact.io/#consumer-driven-contracts) - a tool for automating consumer-driven contracts
* [Pact nirvana](https://docs.google.com/document/d/e/2PACX-1vRf1kSDccImNipOOm1G-bjcSs-ifbZjf1v54K-dIcq8BLKeFPAAm_bf_p71UKqkRMIx30QWWL-kN8TI/pub)