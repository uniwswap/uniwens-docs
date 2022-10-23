# POWNS Deployments

Most of the time you can use a [POWNS library](dapp-developer-guide/dns-libraries.md) to do what you need. If for whatever reason, you need to interact with POWNS directly, details for the currently supported deployments are detailed here.

The POWNS registry is deployed at `0xd3d3cF6937015593b3424F81e5F44CefB8A90588`

On mainnet, the following registrars are deployed:

* .ethw, using the .ethw Permanent registrar.

To find out the contract address of each tld, check the "controller" address of the tld \(eg: [https://app.powns.domains/name/powns](https://app.powns.domains/name/powns) for `.ethw`

In addition, the test networks also have a deployment of the .ethw registrar for testing purposes.

For other contract addresses such as root, multisig, controller, public resolver, and so on, you can see their address under [https://app.ethwdomains.wf/name/powns.ethw/subdomains](https://app.powns.domains/name/powns.ethw/subdomains)
