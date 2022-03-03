# LNS Deployments

Most of the time you can use a [LNS library](dapp-developer-guide/lns-libraries.md) to do what you need. If for whatever reason, you need to interact with LNS directly, details for the currently supported deployments are detailed here.

The LNS registry is deployed at TODO.

On mainnet, the following registrars are deployed:

* .bch, using the .bch Permanent registrar.

To find out the contract address of each tld, check the "controller" address of the tld \(eg: [https://app.bch.domains/name/bch](https://app.bch.domains/name/bch) for `.bch`

In addition, the test networks also have a deployment of the .bch registrar for testing purposes.

For other contract addresses such as root, multisig, controller, public resolver, and so on, you can see their address under [https://app.bch.domains/name/lns.bch/subdomains](https://app.bch.domains/name/lns.bch/subdomains)
