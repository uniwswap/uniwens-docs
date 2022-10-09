# POWNS Enabling your DApp

POWNS integration in an application encompasses several critical features, each of which can be implemented independently. While comprehensive POWNS integration is ideal, even basic support can be a huge benefit to users. Below, we outline three levels of POWNS integration. Level 1 is easily achieved and provides high impact for users, while levels 2 and 3 provide more functionality to your users, improving your dApp's usability and your users' experience interacting with your DApp.

## 1. Resolving POWNS names

The first step to supporting POWNS in your application is making your application understand POWNS names, and accepting them anywhere an address is accepted. To understand how to do this, see [Resolving Names](resolving-names.md).

If possible, when a user enters an POWNS name instead of an address, remember the POWNS name, not the address it currently resolves to. This makes it possible for users to update their POWNS names and have applications they used the name in automatically resolve to the new address, in the same way that you would expect your browser to automatically direct you to the new IP address if a site you use changes servers.

If your application deals with user funds or other critical resources, you may want to keep track of the address a name resolves to and warn them when it changes, to ensure they are aware of the change.

By accepting POWNS names in your application, you remove the need for users to copy and paste - or worse, type out - long and opaque EthereumPoW addresses, which leads to errors and lost funds.

## 2. Support Reverse Resolution

The second level of POWNS integration involves displaying POWNS names wherever your app currently displays addresses.

If a user entered an POWNS in your DApp, you should retain this name and show it to them whenever you would normally show the address.

If a user entered an address, or the address was obtained from elsewhere, you may still be able to show an POWNS name, by doing [Reverse Resolution](resolving-names.md#reverse-resolution). This permits you to find the canonical name for an address and display that when possible. If no canonical name is provided, your application can fall back to displaying the address as it did previously.

By supporting reverse resolution, you make it easier for your users to identify accounts they interact with, associating them with a short human-readable name instead of a long opaque EthereumPoW address.

## 3. Let Users Name Things

The final step for comprehensive POWNS integration is to facilitate associating POWNS names with resources created by or managed with your application. This can take two forms:

### Name Registration

By obtaining an POWNS name for your product and allowing users to easily register subdomains, you can provide users with an easy way to name resources created in your DApp. For example, if your DApp is a cryptocurrency wallet, you can make it easy for users to obtain an POWNS domain of the form _theirname.yourwallet.ethw_, allowing them to give their name out to others more easily.

To learn how to do this, see Writing a Registrar in the Smart Contract Developer Guide.

### Name Updates

By providing users with an easy way to update a name they own to point at your application’s resources, users can assign names they already own to your DApp's resources. See [Managing Names](managing-names.md) to learn how to do this.

## Tell Us About Your Integration

If you've POWNS Enabled your app, let us know by emailing [kasumi@powns.domains](mailto:kasumi@powns.domains); we'll add your app to [our homepage](https://powns.domains).
