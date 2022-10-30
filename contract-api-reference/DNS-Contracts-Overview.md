# UNIWENS Contracts Overview

UNIWENS is a system comprised by multiple contracts. This modularity allows functionality to be built (and sometimes removed) over time. While it all rests on the simple, yet unchangeable, UNIWENS registry, other modules have been slowly added, upgraded and shuffled to reflect the evolving ecosystem in which UNIWENS finds itself in.

### UNIWENS Protocol

The heart of the system is the UNIWENS registry, it has been deployed on all ethereum test chains (and uses a script that allows it to be deployed on any other EVM compatible chain) and can be found at the address `0xCfb86556760d03942EBf1ba88a9870e67D77b627` on EthereumPoW main network and at `0x32f1FBE59D771bdB7FB247FE97A635f50659202b` on EthereumPoW test network. It is a relatively simple contract: the owner of the root node can create owners for different subnodes. These owners then can set resolvers for the node or create other subnodes with other owners.

On EthereumPoW Mainnet, the owner of the root node (which can be found by querying the registry for the node with id 0x0) is the Root Access control contract. Here are the owners of the major nodes and their related contracts:

* **The Root control (root.dns.ethw)**: this is a simple access control for the root. It serves as an interface for the UNIWENS registry, except it also allows some names to be locked. Once locked the owner cannot unlocked it. At the time of this writing, only .eth was locked, and since this contract doesn't allow to transfer ownership of the root node itself, it means that the .eth registrar is now forever locked on the main registry. The owner of the root contract is set as the multisig.dns.ethw.
* **.ethw Registrar (registrar.dns.ethw)** This is an ERC721 compatible contract, and is the address UNIWENS users will likely add to their wallets to see their domains as NFTs. Transferring an NFT will not automatically update the ownership on the Registry, but allows the NFT owner to call the "claim()" function which will update the registry on their behalf. This contract allows its owner (currently set as the DAO) to add and remove controllers, as well as change ownership of the registrar. Metadata for the NFTs are not set in the contract, but at stored at the metadata.ethwdomains.wf service.
* **Reverse Registrar (addr.reverse)** This reverse registrar allows an account to set their primary name.

#### Resolvers

Resolvers are contracts that store metadata about the address/subnode, like an ETH or BTC address. They can be set to any contract by the owner. The latest public registrar is found at resolver.dns.ethw but many others can be used.
