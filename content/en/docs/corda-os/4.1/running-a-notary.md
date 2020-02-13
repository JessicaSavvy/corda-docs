---
title: "Setting up a notary service"
date: 2020-01-08T09:59:25Z
---


# Setting up a notary service
Corda comes with several notary implementations built-in:


* **Single-node**: a simple notary service that persists notarisation requests in the node’s database. It is easy to set up
                    and is recommended for testing, and production networks that do not have strict availability requirements.


* **Crash fault-tolerant** *(experimental)*: a highly available notary service operated by a single party.


* **Byzantine fault-tolerant** *(experimental)*: a decentralised highly available notary service operated by a group of parties.



## Single-node
To have a regular Corda node provide a notary service you simply need to set appropriate `notary` configuration values
                before starting it:

```kotlin
notary : { validating : false }
```
For a validating notary service specify:

```kotlin
notary : { validating : true }
```
See [Validation]({{< relref "key-concepts-notaries#key-concepts-notaries-validation" >}}) for more details about validating versus non-validating notaries.

For clients to be able to use the notary service, its identity must be added to the network parameters. This will be
                done automatically when creating the network, if using [Network Bootstrapper]({{< relref "network-bootstrapper" >}}). See [Networks]({{< relref "corda-networks-index" >}})
                for more details.


## Crash fault-tolerant (experimental)
Corda provides a prototype [Raft-based](http://atomix.io/) highly available notary implementation. You can try it out on our
                [notary demo](https://github.com/corda/corda/blob/release/os/4.1/samples/notary-demo) page. Note that it has known limitations
                and is not recommended for production use.


## Byzantine fault-tolerant (experimental)
A prototype BFT notary implementation based on [BFT-Smart](https://github.com/bft-smart/library) is available. You can
                try it out on our [notary demo](https://github.com/corda/corda/blob/release/os/4.1/samples/notary-demo) page. Note that it
                is still experimental and there is active work ongoing for a production ready solution. Additionally, BFT-Smart requires Java
                serialization which is disabled by default in Corda due to security risks, and it will only work in dev mode where this can
                be customised.

We do not recommend using it in any long-running test or production deployments.

