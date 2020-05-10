# Semantic versioning

## Intent
Semantic versioning is a convention to set expectations around how backwards compatibile new versions of an API will be. It is a useful convention when publishing code packages or [evolving service APIs](evolving-service-apis.md). 

## Motivation

Being able to reuse existing code in different places is a really important way to be effective as a developer. These packages can be the building blocks to assemble other systems without having to build everyhing from scratch, learn complicated domains in detail (think about TCP) or maintain the code as things change. 

Unfortunately the downside of reuse is having dependencies outside your control that may change in ways that are not compatible with the way they are used. Change is inevitable as technologies change, libraries enhance their features or improve their usability and bugs are discovered.

The more dependencies a system has, the bigger the challenge in keeping them up to date or the bigger risk in running old versions that may have security issues or may no longer be supported by the people who produce them. 

Semantic versioning is a way of communicating about changes in software between the people who produce the software and the people who consume it. It sets a consumer's expectations around the likelihood of a consuming system also needing to change to accomodate a new version and how much testing is neccessary when upgrading. It also gives the producers more freedom to keep improving their code, knowing that sometimes the cost of maintaining backwards compatibility is the inability to make certain types of changes.

Semantic versioning is a widely used convention, particularly in package management systems like NPM. This makes it ideal to manage sometimes very complicated dependencies between different packages. 

## Pattern

Declare an explicit public API for your code. This may be by documentation or through code. Semantic versioning communicates how this API has evolved. 

Create a version number for your code's API with the following pattern:
```
Major.Minor.Patch (ie. 2.20.1234)
```

Where you increment the version:
* **major** when making breaking changes to the API
* **minor** when you add new behaviour in a backwards compatible way or if you deprecate existing behaviour
* **patch** when making backwards compatible bug fixes

Once a version has been released, the code for that version will not ever change. Any changes will trigger a change to the version number. Consumers that reference a version by its full version number can be confident that the code they use will always be the same. 

Major number 0 is for initial development. Code with a version number of 0 is not stable and may change significantly with each new version. Once the version reaches 1.0.0, the public API is stable and any future changes will conform to the rules of semantic versioning.

## Applicability

This convention is useful in situations where code or APIs are produced by one set of people and consumed by other people, within an organisation or externally. If the consumers' systems are reliant on the behaviour of producer's code to function correctly, changes may break the consuming system. Semantic versioning tells the consumer how likely this is to happen.

This convention is useful for any type of code that is shared between different projects: 

* Libraries or packages
* Internal or external APIs 
* Command line programs

This becomes more important the further the consumer is away from the producer. Breaking changes between packages managed by the same team are easier to manage because the different members of the team will have lots of context around what both the consumer and producer are doing and can commmunicate easily. Unexpected breaking changes between an open source producer and possibly hundred of consumers will be much more disruptive. 

It is also particularly important when the producer's code changes regularly or is distributed through an automated system like a package manager. 

## Related patterns

* [Maintaining multiple versions](maiintaining-multiple-versions.md)

## Useful resources
* [The SemVer website](https://semver.org/)
* [Semantic versioning on NPM](https://docs.npmjs.com/about-semantic-versioning)