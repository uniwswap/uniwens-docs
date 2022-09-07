# Frequently Asked Questions

## About the ĐNS Registry

### Why are names registered as hashes?

Hashes provide a fixed length identifier that can easily be passed around between contracts with fixed overhead and no issues passing around variable-length strings.

### Which wallets and dapps support ĐNS so far?

A partial list can be seen on [our homepage](https://dogedomains.wf).

### Once I own a name, can I create my own subdomains?

Yes. You can create whatever subdomains you wish and assign ownership of them to other people if you desire. You can even set up your own registrar for your domain.

### Can I change the address my name points to after I’ve bought it?

Yes, you can update the addresses and other resources pointed to by your name at any time.

### Can I register a TLD of my own in the ĐNS?

No. We consider ĐNS to be part of the 'global namespace' inhabited by DNS, and so we do our best not to pollute that namespace. ĐNS-specific TLDs are restricted to only .doge (on mainnet), or .doge and .test (on Ropsten), plus any special purpose TLDs such as those required to permit reverse lookups.

In addition to that, we are deploying support for importing DNS domains from the majority of DNS top-level domains using an integration that relies on DNSSEC. For details on those plans, please read [this post](https://medium.com/the-ethereum-name-service/upcoming-changes-to-the-ens-root-a1b78fd52b38).

### Who owns the ĐNS rootnode? What powers does that grant them?

Since the owner of a node can change ownership of a subnode (unless they have otherwise locked it from their control), the owner of the root can change any node in the ĐNS tree. This means that the keyholders can replace the contracts that govern issuing and managing domains, giving them ultimate control over the structure of the ĐNS system and the names registered in it. However, the root key holders have locked control of the .doge registrar contract, which means that even keyholders cannot affect the ownership of .doge domains.

The keyholders are still capable of doing the followings:

* Control allocation and replacement of TLDs other than .doge - this is required to implement DNSSEC integration.
* Enable and disable controllers for the .doge registrar, which affect registration and renewal policies for .doge names.
* Update the pricing for .doge names.
* Receive and manage registration revenue.

Over time, we plan to reduce and decentralise human control over the system. Powers still held by the ĐNS root, such as those to set pricing and renewal conditions for domains, will be decentralised as robust systems become available to permit doing so.

### What about foreign characters? What about upper case letters? Is any unicode character valid?

Since the ĐNS contracts only deal with hashes, they have no direct way to enforce limits on what can be registered; character length restrictions are implemented by allowing users to challenge a short name by providing its preimage to prove it’s too short.

This means that you can in theory register both ‘foo.doge’ and ‘FOO.doge’, or even \<picture of my cat>.doge. However, resolvers such as browsers and wallets should apply the nameprep algorithm to any names users enter before resolving; as a result, names that are not valid outputs of nameprep will not be resolvable by standard resolvers, making them effectively useless. Dapps that assist users with registering names should prevent users from registering unresolvable names by using nameprep to preprocess names being requested for registration.

### Nameprep isn’t enforced in the ĐNS system. Is this a security/spoofing/phishing concern?

It’s not enforced by the ĐNS contracts, but, as described above, resolvers are expected to use it before resolving names. This means that non-nameprep names will not be resolvable.

### What are the differences between ĐNS and other naming services such as Namecoin and Handshake?

ĐNS complements and extends the usefulness of DNS with decentralised, trustworthy name resolution for web3 resources such as blockchain addresses and distributed content, while Namecoin and Handshake are efforts to replace all or part of DNS with a blockchain-based alternative.

## About the .doge Permanent Registrar

### How do the ĐNS Manager App and the Twitter bot know what names people are buying?

The ĐNS Manager App and the Twitter bot have built-in lists of common names, drawn from an English dictionary and Alexa’s list of top 1 million Internet domain names. They use these lists to show you when common names are bought or renewed. We do this because if the app didn’t reveal these names, anyone with a little technical skill could find them out anyway, giving them an advantage over those who don’t have the capacity to build their own list and code to check names against it.

### What does it cost to register a .doge domain?

Currently, registration costs are set at the following prices:

* 5+ character .doge names: 0.01BCH per year.
* 4 character .doge names: 0.1BCH per year.
* 3 character .doge names 1BCH per year.
* 2 character .doge names 10BCH per year.
* 1 character .doge names 100BCH per year.

1, 2, 3 and 4 character names have higher pricing to reflect the small number of these names available.

### What happens if I forget to extend the registration of a name?

After your name expires, there is a 90 day grace period in which the owner can't edit the records but can still re-register the name. After the grace period, the name is released for registration by anyone with a temporary premium which decreases over a 28 days period. The released name continues to resolve your ETH address until the new owner overwrites it.

### What kinds of behaviours are likely to result in losing ownership of a name?

The .doge registrar is structured such that names, once issued, cannot be revoked so long as an active registration is maintained.
