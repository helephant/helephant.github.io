#  Breaking change

## Intent

Breaking change is a pattern that forces clients to move to the new contract at the same time as the service or accepts that clients will cease to function until they upgrade to the new API.

## Motivation

Much of the content around [evolving service APIs](evolving-service-apis.md) is focused around doing so with minimum disruption to consumers, but it is important to remember that making a breaking change is a tool in the service API toolbox which will sometimes be the appropriate one to use. 

## Pattern

Make the change to the service API without maintaining the original contract, breaking any clients that do not immediately upgrade. 

## Applicability

This may be worth considering if allowing the service and the consumer to change independently adds unacceptably high levels of complexity to the service. 

This may be a good idea if down time is acceptable between the consumer and the service. There will be consumer-service relationships where re-trying failed transactions will not be expensive or difficult to do. The service may not be a real-time service that responds to the client right away or the client may not need a response right away. It may just be that the information the consumer and service exchange is transitory or perhaps not critical. 

This may be more likely an option where both consumer and service are owned by the same team or where both teams are within the same organisation. Having a service with only a small number of consumers also makes this more likely. 

Creating a breaking change is not only an option at the time of making a change to an API. If you are using an [expand-contract technique](expand-contract.md) you might decide that after a [sunset period](planned-obsolescence.md) to retire the original API, which then becomes a breaking change for clients that have not upgraded. 

## Challenges

Down time is usually a big issue in systems, so techniques that allow clients to seamlessly upgrade at a time which is convenient to the client  are usually preferable. 

Even if both service and client are upgraded at the same time, there will likely be a small amount of down time just because neither release will happen instantly. It will be likely that some calls from the client to the old API will be sent to the new API and some of the new requests will be sent to the old API. 

Coupling service and client upgrades often makes changing either more difficult because the owners of both systems must collaborate closely. It also increases the likelihood of issues because both must succeed or both must roll back. If there are more than one or two clients, the coordination overhead will most likely outweigh the complexity of evolving the API in a non-breaking way. 

## Related patterns

* [Planned obsolescence](planned-obsolescence.md) - a breaking change may be neccessary at the end of a sunset period

## Useful resources

n/a