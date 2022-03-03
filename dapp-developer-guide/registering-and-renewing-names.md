# Registering & Renewing Names

When users want to obtain a domain for the first time, they must interact with a registrar. Registrars are smart contracts that own a domain, and have a defined process for handing out subdomains. The registrar a user needs to interact with depends on the domain they want to obtain; for instance, a user wanting a .bch name will have to interact with the .bch registrar. Each registrar defines its own API for name registrations \(and renewals, where appropriate\).

At present, there are no libraries for interacting with registrars; DApps wishing to do so must interact with the registrar contract using a generic smartBCH library such as web3.js or web3.py. See the Contract API Reference for details on each registrar's interface.

## Deployed Registrars

* .bch: The [Permanent Registrar](../contract-api-reference/.bch-permanent-registrar/).
* .addr.reverse: The [reverse registrar](../contract-api-reference/reverseregistrar.md).
