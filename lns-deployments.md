# LNS Deployments

Most of the time you can use a [LNS library](dapp-developer-guide/lns-libraries.md) to do what you need. If for whatever reason, you need to interact with LNS directly, details for the currently supported deployments are detailed here.

The DNS registry is deployed at `0x834C46666c1dE7367B252682B9ABAb458DD333bf` on mainnet, and `0x08850859CE6B62A39918c8B806AfbE3442fE7b0b` on testnet.

On mainnet, the following registrars are deployed:

* .doge, using the .doge Permanent registrar.

To find out the contract address of each tld, check the "controller" address of the tld \(eg: [https://app.dogedomains.wf/name/doge](https://app.dogedomains.wf/name/doge) for `.doge`

In addition, the test networks also have a deployment of the .bch registrar for testing purposes.

For other contract addresses such as root, multisig, controller, public resolver, and so on, you can see their address under [https://app.dogedomains.wf/name/dns.doge/subdomains](https://app.dogedomains.wf/name/dns.doge/subdomains)
