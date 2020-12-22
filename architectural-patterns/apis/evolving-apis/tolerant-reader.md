# Tolerant reader

__Also known as__: Must ignore

## Intent

Tolerant reader is a pattern for [evolving APIs](evolving-service-apis.md) that protects clients from changes to a service contract that they are not specifically using to reduce the frequency and cost of change for consumers. 

## Motivation

Most patterns focus on how the service can be designed to accommodate change. This is a pattern where the consumer can reduce the surface area of its dependency on a service and be forward compatible with contract changes that are unknown at the time of integration.

## Pattern

The code that consumes the service in the consumer should only bind to the parts of the interface that the consumer is interested in. It should ignore everything else. 

If this pattern is successfully applied, the consumer should continue working if the service changes a part of the interface that the consumer doesn't use. The service should be able to add new fields, omit optional items, rename fields the consumer doesn't use, change their types or remove them. If the consumer doesn't use it, it shouldn't need to change to accomodate the new schema. 

For example, imagine a service with a HTTP endpoint that looks like this:
```
GET /widget/2aeb0b97-7260-4717-83c7-77d0ccb5cf59 HTTP/1.1
Host: api.widgets.com
```

That returns a JSON response that looks like this:
```javascript
{
  'id': '2aeb0b97-7260-4717-83c7-77d0ccb5cf59',
  'name': 'thingamagig',
  'category': 'phalanges',
  'description': 'used for connecting dodads together',
  'created': '2020-01-01 17:05:46',
  'createdBy': 1234
}
```

And there is an *all widgets aggregator website* consumer that only uses the name and the category from the message:
```javascript
const { name, category } = widgets.get(id);
```

Now another consumer of the service needs to know when the widget was last updated, so the widget API team adds an `updated` field. The *all widgets aggregator website* consumer only binds to the part of the message that it needs, so it can continue to work without change. 

## Applicability

As the name suggests, tolerant reader is most applicable when reading from an API. When the client is providing information to the service or triggering an action, it is likely that the service will have restrictions on what constitutes a valid request. 

This is often useful when consuming a service over HTTP, but is not only useful in that context. The same principles apply to reading from databases, queues, topics or file transfers. 

When implementing a client, you can choose to bind to any service using tolerant reader, without needing to colaborate with the service provider. Doing so will protect you from changes which aren't related to the part of the contract you need. 

If you are implementing a service with clients outside your group or organisation, you may not be able to influence the way they consume your service. If your consumer is a team you work closely with, consider also using [consumer-driven contract tests](consumer-driven-contract-tests.md) to make it clear which part of the contract each client is using. 

When using tools that automatically map data in and out of a service, they might automatically bind to the entire message, even if the code that consumes them works in a tolerant way. Automatically applying a schema to the message before consuming it, may also bind the consumer to the entire message. 

Even with a perfect implementation of tolerant reader paired with a service that evolves using the [expand-contract](expand-contract.md) pattern, sometimes the service will need to make breaking changes that affect the part of the contract a particular client is using. In that case the service and client may need to change together if the service is practicing [aggressive obsolescence](aggressive-obsolescence.md) or the service may support [backwards compatible versions](backwards-compatible-versions.md).

There is also a risk that this can mean that consumers can potentially miss changes that alter the semantic meaning of a message. The consumer may continue to consume messages without surfacing an error, but the output of the client is now incorrect. It is not a good idea for service providers to use the [expand-contract](expand-contract.md) pattern in a way that fundementally alters the meaning of a message.

## Related patterns

* [Expand-contract](expand-contract.md) and tolerant reader work really well together. Expand-contract allows the service to slowly evolve the contract and tolerant reader allows the client to only respond to the changes that it is interested in. 
* When you have a tolerant reader, a [consumer-driven contract tests](consumer-driven-contract-tests.md) can help the service understand the part of the contract that each client requires. 

## Useful resources

* [Martin Fowler](https://martinfowler.com/bliki/TolerantReader.html) - definitive description of the pattern
