# Expand-contract pattern

## Intent
Expand-contract is a pattern for [evolving APIs](evolving-apis.md) while temporarily maintaining backwards compatibility for existing clients. 

__Also known as__: Parallel change

## Motivation

Change is inevitable. Even in a scenario where an API starts off with a well designed interface, the world in which the API lives will keep changing so at some point it is likely that the current interface will be no longer fit for purpose. 

If the change is a breaking change, any clients that use the API will be affected and will also need to change to accomodate the new interface.  

It may be possible to continuously maintain backwards compatible APIs, but that has the disadvantage of increasing the complexity of the service. It also is likely to increase the future cost of change to the service as each version of the API must be accounted for during development, testing and deployment. These costs are compounded if the API undergoes multiple breaking changes over a number of years. 

At the same time, coupling the change of the API with the change of every single client significantly increases the size of the change and the cost of rolling it out. It's ideal to iterate. First to focus on making the change to the service and then on rollng out the change to the clients as a separate step.

It's often not acceptable to interupt a service to make a breaking change. Supporting multiple versions of the interface makes it possible to update a service while it is running. The intial change is invisible to any clients and they can choose when they would like to move to consuming the new interface. 

## Pattern

The solution is to initially *expand* the API to include the new fields or endpoints while still maintaining compatibility with the existing API, and then at some point *contract* the API to remove the items that are now obsolete. 

### Expand

If the change is very small, it may be possible to evolve an existing API:

* Add an additional duplicate field to an existing API
* Map or split two fields into one field
* Map existing parameters to new ones
* Ignore extra parameters that are no longer relevant

If the changes are significant or completely incompatible with the current schema, it may be preferable to support separate versions of the API endpoint. Supporting multiple ways of calling the same API can quickly become very confusing and lead to combinations of properties that are not valid. Having completely separate APIs makes the differences between the versions very explicit, but can make more work for clients to keep up to date. 

## Contract

Once the change is completed, the difficult part is working with clients to migrate to the new API. This can be especially difficult if some of the clients are still important but no longer actively maintained. 

There are some approaches that may or may not help depending on who your clients are: 

* Notify or agree with clients a time period which the old version will be available
* Mark fields as obsolete in documentation and with meta-data in the API itself
* Agreeing to support a set number of versions of the API
* Publishing roadmaps of changes to the service

## Applicability

This pattern is useful in many situations where the owner of the API and the client are independently deployable:

* Within a single codebase when refactoring
* Being able to releasing changes to a data store that an application or service relies on
* Changing the independently deployable parts of a single service in an iterative way
* Evolving internal or publically available APIs

## Challenges

The biggest risk with this pattern is you may have good intentions when you expand the API, but then find you are never able to remove the obsolete parts of the API either because work moves on to something different or some of your clients never upgrade. In that case you end up having to carry the complexity indefinitely and over time it will degrade the integrity and usability of the API, particularly if it happens multiple times. 

It is possible that it will be very difficult to convince some clients to move to the new API. This is particularly a problem for clients which are no longer maintained by any team or for clients that are maintained by teams focused on different business priorities. 

Services with many different clients will struggle more than ones with fewer clients. Public services with external clients will struggle more than services with internal clients. At the same time, services with many clients and services with external clients will probably find backwards compatibility of most value. 

Supporting multiple variations or versions of your API may be inevitable in some situations, but it also creates complexity for both teams maintaining the service and clients calling it. Teams supporting the service will need to keep any variations in mind when making changes, which will make change slower, riskier and more expensive. Clients calling the API will need to understand which features are current and which are obsolete. 

As change is inevitable this will probably not be a choice that is made only once and each variation increases complexity and makes future change more difficult. 

That said, the value of decoupling the deployment of the service changes and the client changes while maintaining a continuous service makes this a valuable pattern in many situations. 

## Related patterns

* Non-breaking changes
* Aggressive obsolescence

## Useful resources
* A description of the pattern on [Martin Fowler's website](https://martinfowler.com/bliki/ParallelChange.html)