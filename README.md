# Introduction

The EthPoW Name Service (UNIWENS) is a distributed, open, and extensible naming system based on the EthereumPoW blockchain. It is a fork of the [ENS](https://ens.domains) project.

UNIWENS’s job is to map human-readable names like ‘alice.ethw’ to machine-readable identifiers such as EthereumPoW addresses, other cryptocurrency addresses, content hashes, and metadata. UNIWENS also supports ‘reverse resolution’, making it possible to associate metadata such as canonical names or interface descriptions with EthereumPoW addresses.

UNIWENS has similar goals to DNS, the Internet’s Domain Name Service, but has significantly different architecture due to the capabilities and constraints provided by the EthereumPoW blockchain. Like DNS, UNIWENS operates on a system of dot-separated hierarchical names called domains, with the owner of a domain having full control over subdomains.

Top-level domains, like ‘.ethw’ are owned by smart contracts called registrars, which specify rules governing the allocation of their subdomains. Anyone may, by following the rules imposed by these registrar contracts, obtain ownership of a domain for their own use. UNIWENS also supports importing in DNS names already owned by the user for use on UNIWENS.

Because of the hierarchical nature of UNIWENS, anyone who owns a domain at any level may configure subdomains - for themselves or others - as desired. For instance, if Alice owns 'alice.ethw', she can create 'pay.alice.ethw' and configure it as she wishes.

UNIWENS is deployed on the EthereumPoW main network and on several test networks. If you use a library such as the [ensjs](https://www.npmjs.com/package/@ensdomains/ensjs) Javascript library, or an end-user application, it will automatically detect the network you are interacting with and use the UNIWENS deployment on that network.

You can try UNIWENS out for yourself now by using the [UNIWENS Manager App](https://app.ethwdomains.wf), or by using any of the many UNIWENS enabled applications on [our homepage](https://uniwens.domains).

## UNIWENS Architecture

UNIWENS has two principal components: the [registry](contract-api-reference/dns.md), and [resolvers](contract-api-reference/publicresolver.md).

![](<.gitbook/assets/ens-architecture.png>)

The UNIWENS registry consists of a single smart contract that maintains a list of all domains and subdomains, and stores three critical pieces of information about each:

> * The owner of the domain
> * The resolver for the domain
> * The caching time-to-live for all records under the domain

The owner of a domain may be either an external account (a user) or a smart contract. A registrar is simply a smart contract that owns a domain and issues subdomains of that domain to users that follow some set of rules defined in the contract.

Owners of domains in the UNIWENS registry may:

> * Set the resolver and TTL for the domain
> * Transfer ownership of the domain to another address
> * Change the ownership of subdomains

The UNIWENS registry is deliberately straightforward and exists only to map from a name to the resolver responsible for it.

Resolvers are responsible for the actual process of translating names into addresses. Any contract that implements the relevant standards may act as a resolver in UNIWENS. General-purpose resolver implementations are offered for users whose requirements are straightforward, such as serving an infrequently changed address for a name.

Each record type - cryptocurrency address, IPFS content hash, and so forth - defines a method or methods that a resolver must implement in order to provide records of that kind. New record types may be defined at any time via the EIP standardization process, with no need to make changes to the UNIWENS registry or to existing resolvers in order to support them.

Resolving a name in UNIWENS is a two-step process: First, ask the registry what resolver is responsible for the name, and second, ask that resolver for the answer to your query.

![](<.gitbook/assets/resolver-graph.png>)

In the above example, we're trying to find the EthereumPoW address pointed to by 'foo.ethw'. First, we ask the registry which resolver is responsible for 'foo.ethw'. Then, we query that resolver for the address of 'foo.ethw'.

### Namehash

Resource constraints in smart contracts make interacting directly with human-readable names inefficient, so UNIWENS works purely with fixed length 256-bit cryptographic hashes. In order to derive the hash from a name while still preserving its hierarchal properties, a process called Namehash is used. For example, the namehash of 'alice.ethw' is _0x787192fc5378cc32aa956ddfdedbf26b24e8d78e40109add0eea2c1a012c3dec_; this is the representation of names that is used exclusively inside UNIWENS.

Namehash is a recursive process that can generate a unique hash for any valid domain name. Starting with the namehash of any domain - for example, 'alice.ethw' - it's possible to derive the namehash of any subdomain - for example 'iam.alice.ethw' - without having to know or handle the original human-readable name. It is this property that makes it possible for UNIWENS to provide a hierarchal system, without having to deal with human-readable text strings internally.

Before being hashed with namehash, names are first normalized, using a process called UTS-46 normalization. This ensures that upper- and lower-case names are treated equivalently, and that invalid characters are prohibited. Anything that hashes and resolves a name **must** first normalize it, to ensure that all users get a consistent view of UNIWENS.

For details on how namehash and normalization works, see the developer documentation on [name processing](contract-api-reference/name-processing.md).

## Getting Started

UNIWENS has documentation for a variety of audiences, including dapp developers and contract developers, as well as reference documentation.

#### I'm a dapp developer and want to add UNIWENS support to my dapp

Check out the dapp developer guide, starting with [UNIWENS Enabling your Dapp](dapp-developer-guide/dns-enabling-your-dapp.md). You'll want to choose one of the many available [UNIWENS Libraries](dapp-developer-guide/dns-libraries.md) to get started working with UNIWENS.

#### I'm a contract developer and want to interact with UNIWENS from my contract code

Check out the Contract Developer Guide, starting with [Resolving Names On-chain](contract-developer-guide/resolving-names-on-chain.md). You can also [write your own resolver](contract-developer-guide/writing-a-resolver.md) (to customise the process of looking up names), or your own [registrar](contract-developer-guide/writing-a-registrar.md) (to customise the process of registering new names).

#### I want reference documentation for the UNIWENS smart contracts

Check out the Contract API Reference. We have reference documentation for UNIWENS's core contract, the [registry](contract-api-reference/dns.md), for [resolvers](contract-api-reference/publicresolver.md), and for commonly-used registrars such as the [reverse registrar](contract-api-reference/reverseregistrar.md), and the [.ethw registrar](contract-api-reference/.dns/g-permanent-registrar/).
