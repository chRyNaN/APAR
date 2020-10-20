# APAR
**A**ctivity**P**ub **A**ddress **R**egistry - A de-centralized registrar for servers implementing the ActivityPub Specification.

This repository proposes this technology and may include an implementation in the future. APAR is meant to compliment [ActivityPub](https://www.w3.org/TR/activitypub/) by providing a de-centralized location, for servers implementing the ActivityPub specification, to register so that their content is easier to find. Which enables applications and tools to retrieve the registered ActivityPub servers in the [Fediverse](https://en.wikipedia.org/wiki/Fediverse) and query their data. Note that while [ActivityPub](https://www.w3.org/TR/activitypub/) is a W3C Recommendation, APAR is currently not.

### Naming
The name **APAR** is an acronym for ActivityPub Address Registry. After a search, I learned that the [definition](https://www.merriam-webster.com/dictionary/APAR) for an APAR is 
> the three-banded armadillo (Tolypeutes tricinctus) of South America

So that might make a good mascot for this repository in the future. 

## Background
APAR is designed to compliment ActivityPub, but what is [ActivityPub](https://www.w3.org/TR/activitypub/)?

ActivityPub is a W3C Specification, in the Recommendation stage, that details a common protocol for federated social applications. This means that a server that implements the ActivityPub defined protocols is typically interoperable with other servers and clients that also implement the protocols. ActivityPub establishes a standardized, yet extensible, communication protocol for the [Fediverse](https://en.wikipedia.org/wiki/Fediverse).

The Fediverse is a federated network of social applications that can intercommunicate. The ActivityPub specification provides a common approach for that communication. Unlike a traditional and centralized social network (Twitter, Facebook, etc), a federated social network (Mastadon, Diaspora, etc) allows anyone to host their own server and own their own content. These servers can communicate with other servers in the federated network that use the same protocol. In effect, giving the User the ability to interact with other Users from the same or different servers.

![Centralized vs Federated](assets/centralized_vs_federated.png)

One of the most popular federated social networks, that also implements the ActivityPub specification, is [Mastadon](https://joinmastodon.org/). Mastadon is an open-source micro-blogging social network (with some similarities to Twitter). A User can either host their own Mastadon server or join one of the existing Mastadon communities. Either way, the User has the ability to follow, interact, and communicate with any User, even if that User is in another Mastadon community. This ability of server-to-server communication is what makes Mastadon, and the Fediverse in general, so impressive. And with the standardized specification of ActivityPub, it should be possible to communicate between entirely different federated social networks. 

This federated network approach effectively makes these de-centralized social networks. There's no centralized entity that has complete control over all of the network and there's no single point of failure on the network. If one part of the federated network goes down, the rest can remain unaffected. Each server in the network can define their own rules and have their own moderators. If a User chooses that a server doesn't work for them, they can migrate to another server or even create their own and still remain a part of the overall network. This is akin to how the Internet works in general, being de-centralized to some degree, but provides the added benefit of inter-communication between the different parts of the network.

However, a federated social network isn't without it's problems. Some issues that arise on the User level are locating the available communities, displaying the trending content from across communities of interest, and querying for specific information throughout the network. This is where **APAR** comes in. APAR is a registrar for social applications that conform to the ActivityPub Specification. These federated social applications would register their web address with APAR so that their application and content can be found by Users. An application or tool could query APAR to provide a User with this information. This would allow Users to view trending content from across federated social networks, search for specific content, communicate with Users in different communities, and find and join new communities.

Similarities between APAR and a domain registrar may be apparent. In fact, APAR was loosely based on the concept of a domain registrar. However, there are major differences. One important distinction is that APAR doesn't provide Domain Names. The Domain Names must already be registered with a domain registrar before registering the name with APAR. Another distinction between the two technologies is that a domain registrar is typically centralized, whereas, APAR is de-centralized. To be consistent with a federated network's de-centralized nature, APAR was designed to be de-centralized as well. Blockchain is what enables APAR to be de-centralized.

## How does it work?
APAR is a de-centralized registry for ActivityPub implementing social application servers. These social application servers that implement the ActivityPub specification may register with APAR for no cost. Client applications can then use APAR to view the available application servers and load content from them. This would happen "behind the scenes" in the client application, so from the User's perspective, this would be no different than a centralized application. Though the underlying technology APAR uses is a de-centralized Blockchain. This enforces that there is no centralized entity with complete control over the registry; Preventing censorship and creating a level playing field for organizations large and small.

![APAR Basic Flow](assets/apar_app_bg_white.png)

### Blockchain
APAR utilizes [Blockchain](https://en.wikipedia.org/wiki/Blockchain) to store all of the registration transactions. Every time an ActivityPub Server Domain is registered with APAR, it is stored on APAR's Blockchain. Anyone can register an ActivityPub Server Domain and Nodes will mine the hash using the Proof-of-work (PoW) consensus approach, as well as, verify that the provided Domain is valid. When a Domain is considered valid and has been mined, the registration transaction, along with the related data, will be added as a Block to the Blockchain. The APAR Blockchain is public and permissionless, similar to [Bitcoin](https://bitcoin.org/en/). Anyone can host a Node and mine the Blocks to add to the Blockchain.

#### Consensus - Proof of Work
The consensus mechanism used by APAR is the common [Proof-of-work (PoW)](https://en.wikipedia.org/wiki/Proof_of_work) algorithm. POW is most notably used by [Bitcoin](https://bitcoin.org/en/). With cryptocurrencies, such as, Bitcoin, PoW solves the double spend problem and helps ensure the integrity of the Blockchain. Also, PoW can be used in certain scenarios to help prevent spamming. APAR uses PoW to ensure the integrity of the underlying Blockchain and to essentially rate-limit the amount of registrations that can occur over a period of time. In fact, there are already some Blockchain Domain Registrar's, such as, [Ethereum Name Service](https://ens.domains/) and [Unstoppable](https://unstoppabledomains.com/). 

#### Time - Registration Period
A Domain Name in a Domain Registrar can technically be registered to only one User at a time. If a User does not re-register a Domain Name, or that User sells the Domain Name, then the Domain Name belongs to someone else, either the User who bought the Domain Name or the company that the Name was leasing the Domain. In this way, each transfer of the Domain Name could be registered as a Transaction on the Blockchain so that the ownership and history can be stored. However, APAR doesn't actually have control over the Domain Name. Instead a Server is simply registering to make a note that they implement the ActivityPub protocol at a provided Domain Address. But what if the Domain changes hands and no longer implements the ActivityPub protocol? In that case it would no longer be valid to be kept in the registry but with no ownership of the Domain, there's no effective way of knowing that the Address should be removed from the registry. The solution to this problem is a time-based approach.

Instead of registering only once and leaving the possibility of the data being stale, a Server would have to re-register periodically. So a registration is time-based (similar to a car registration in some States). When a registration transaction is added to the Blockchain, it is stored with time information. This information contains the **expiration** and **renewal** time. If a Server didn't re-register before the **expiration time**, then it's registration is considered invalid and would remain invalid until it is re-registered. To prevent over registration, a Server cannot register before the **renewal time**. The period of time between **renewal** and **expiration** time is called the **Registration Period**. 

Even if a registration is invalid, it's last, and now invalid, registration is still stored in the Blockchain. This provides a complete history of all the registrations. An application that is querying APAR and listing all of the valid Servers should exclude any Servers that have an invalid registration. Also, if the Registration Period happens at the same interval for every registration, the iterative process for listing all valid Servers would be faster, since once the first invalid registration is reached, the process can be finished.

#### Incentive - Golden Rule
Most Blockchains, especially those that require mining, provide some incentive to encourage Nodes to mine the new blocks. In cryptocurrencies like Bitcoin, the incentive is usually financial one, typically in the form of a cryptocurrency reward. The incentive to mine for a Blockchain that isn't a cryptocurrency is more difficult to provide. The incentive structure decided on for APAR is the [Golden Rule](https://en.wikipedia.org/wiki/Golden_Rule):
> the principle of treating others as you want to be treated.

APAR provides a desirable solution for de-centralized and federated social networks. It provides a means for applications to load content from across the Fediverse, essentially serving as a marketing strategy for these social networks. Because of the benefits provided to federated social networks and the time-based structure of APAR, they each have a vested interest in running Nodes and performing mining for additional blocks. In order to use APAR to promote your federated social network's content and allow the connection between other networks, you would have to register your domain. In order to register your domain, there needs to Nodes that are willing to mine the new transaction Block in the Blockchain. If a registered server refuses to participate in the mining process for fellow servers, then there may be no servers to mine for them when it comes time for them to re-register. In this way, each registered server is incentivised to participate in the mining process, otherwise they wouldn't be able to reap the rewards of using APAR. Since the mining process, with a reasonable Registration Period, shouldn't be as demanding as a cryptocurrency's, this incentivization structure should prove to be satisfactory. 

#### Verification
In addition to mining and consensus mechanisms, there needs to be verification that the information proposed for registration is valid. The verification should happen before the mining process starts and performed by a Node that intends to mine, this way there isn't unnecessary work and time wasted. When a Node completes the mining process and submits the solution to the other peers for validation, the other peer Nodes can also perform the verification (perhaps a simplified variant?) to ensure that the added registration is valid. Some things to consider for verification include the following:
* Is the first time this Server is being registered, is it in it's Registration Period, or has it's previous registration expired?
* Is the Server to be registered a valid Server address that implements the ActivityPub specification?

#### Data
Along with the Block's Header, the following information is required for registration:
* `serverUrl` - A mandatory `String` URL value for the root application server that implements the ActivityPub Specification (ex: `https://www.example.com`).
* `webFingerUrl` - An optional `String` URL value pointing to the location of the [Webfinger](https://en.wikipedia.org/wiki/WebFinger) endpoint (ex: `https://www.example.com/.well-known/webfinger`).
* `feedUrl` - An optional `String` URL value pointing to the location of an ActivityPub outbox that is for the entire application and not just a particular User. This could provide a means to accessing a public feed of information, such as, a "trending section". If this value is provided, accessing this endpoint should return an [ActivityStreams Collection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-collection).
* `searchUrl` - An optional `String` URL value pointing to the location of an endpoint where searches can be performed for the entire application. If this value is provided, accessing this endpoint with a query parameter of `q` (ex: `q=SEARCH_QUERY`) should return an [ActivityStreams Collection](https://www.w3.org/TR/activitystreams-vocabulary/#dfn-collection).
* `renewal` - A mandatory `String` in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format. This value represents the time when registration opens up again for this Server. This value will be provided by the Node that performs the mining, if this is provided by the registration proposer, then it will either be ignored or validated.
* `expiration` - A mandatory `String` in [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601) format. This value represents the time when the registration becomes expired for this Server.This value will be provided by the Node that performs the mining, if this is provided by the reigstration proposer, then it will either be ignored or validated.
* `name` - An optional `String` name value for this registration.

## License
```
Copyright 2020 chRyNaN

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
