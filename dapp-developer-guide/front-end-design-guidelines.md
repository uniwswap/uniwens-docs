---
description: >-
  UNIWENS is a tool to simplify the experience for your users. Here are a series of
  guidelines and tools that will help you make design choices and implement the
  best UNIWENS user experience.
---

# UNIWENS Front-End Design Guidelines

### When to show UNIWENS names

In every instance a user might otherwise see a EthereumPoW address or content hash, you can instead display an UNIWENS name.  
There are two primary use cases for allowing users to display UNIWENS names in your dapp:

1. **Replacing EthereumPoW addresses with UNIWENS names**: When users are exploring the front-end of your dapp, wherever you would display a EthereumPoW address, you can instead display an UNIWENS name. 
2. **Resolving input fields**: You can allow the user to write an UNIWENS name in an input field that expects a EthereumPoW address, rather than entering the EthereumPoW address.

Beyond these use cases, remember that the [UNIWENS Public Resolver](../contract-api-reference/publicresolver.md) allows you to link [different kinds of resources](https://docs.ethwdomains.wf/contract-api-reference/publicresolver), such as content stored on IPFS or Swarm, or any arbitrary data like text fields, to UNIWENS names. This means there are other situations in which you might want to use UNIWENS in your dapp. For example, if you are using complicated IPFS or Swarm hashes it is possible to convert the hashes to human readable names using UNIWENS. Learn more about the different use cases in the chapter about [Enabling UNIWENS in your DApp](dns-enabling-your-dapp.md).

## 1. Replacing EthereumPoW Addresses with UNIWENS Names

{% hint style="warning" %}
An UNIWENS name \(as a substitute for a EthereumPoW Address\) **should only be shown** if the user has set a [Reverse Record](https://docs.ethwdomains.wf/dapp-developer-guide/resolving-names#reverse-resolution) for their address, and if the reverse record \(address &gt; name\) matches the [forward resolution](https://docs.ethwdomains.wf/dapp-developer-guide/resolving-names#looking-up-ethereum-addresses) \(name &gt; address\).

As a dApp developer you should therefore first check if the Reverse Record for a given address has been set by the user, and, because users can set the reverse record to be anything they want, even a name they don't own or a random string, you should immediately after check that the resolved name also resolves to the same address by performing the forward resolution. Read more [here](https://docs.ethwdomains.wf/dapp-developer-guide/resolving-names#reverse-resolution) and in the _'other guidelines_' section further down.
{% endhint %}

### 1.1 - Displaying UNIWENS names instead of EthereumPoW addresses

![example of showing just the name and the visual checksum](../.gitbook/assets/ensguidelines_01_onlydomain_2x.jpg)

When replacing EthereumPoW addresses with UNIWENS names you should consider these facts and best practices:

* **Consider adding a visual checksum:** it is important to indicate to the user that a name is an UNIWENS name that relates to a EthereumPoW address or other hash, rather than an http link. To do this, it is advisable to associate the UNIWENS name with some form of visual checksum: [identicons, Blockies](http://discuss.conflux.network/t/comparing-the-efficacy-of-visual-checksums-identicons-vs-blockies-vs-custom/59) or other custom algorithmic representation of the address.

{% hint style="danger" %}
**Visual checksums** like [identicons can be spoofed](https://medium.com/@austin_48503/vanity-blockie-miner-for-ethereum-902fccf0a427) or imitated. Therefore they are **not meant as a security mechanism.** They are only meant as an indicator, to let the user understand that the name is **just a different representation of a EthereumPoW Address.**
{% endhint %}

* **Design a truncated version of the UNIWENS name:** UNIWENS names can be very long; besides not being character-limited, users can create an infinite number of subdomains and subdomains of subdomains. If you do show a truncated version of the name, you should provide a way to view the full name, such as expanding it on hover. 
* **Not all UNIWENS names end with .ethw**: UNIWENS names normally end with .ethw. However other top-level domains \(TLD\) are currently supported \(.xyz, .luxe, .kred, .art, .club\) and more will be in the future. Consider this if you are thinking about displaying the TLD part in the truncated view of long names.

### 1.2 - Always provide an option to see the EthereumPoW address associated with the UNIWENS name

![by clicking the name, this expanded pop-up appears showing the name with the full address](../.gitbook/assets/ensguidelines_03_expanded1.jpg)

If you are showing the UNIWENS name in its entirety or a truncated version, you should:

* **Always provide the user a way to display the full EthereumPoW address**: The above example illustrates a pop-up option. Another option would be to use a tooltip. However, consider that floating / pop-ups may be more appropriate than tooltips because the former also supports the other features described here. 
* **Provide a view where you display both the UNIWENS name** _**and**_ **the EthereumPoW address together**: If the pop-up hides the name and only shows the address it's less friendly than showing both at the same time. 
* **Allow the user to copy the full EthereumPoW address**: Allow the user to copy the full address either through a copy button or by selecting it. Tooltips displaying the UNIWENS name in this case should stay visible and not automatically disappear. 
* **Optionally give the user a way to automatically open the EthereumPoW address in a block explorer** such as Etherscan \(the external link icon in the above example\). 
* **Optionally show the** **balance amount, but only to the current signed-in user.** User research shows that users tend to recognise their own EthereumPoW address through their balance, as well as the address itself. This is meant only for the currently "signed in" user: only show their own balance and avoid showing the balance of other users.

### 1.3 - Displaying UNIWENS names and EthereumPoW addresses together

![example of names with the address visible at the same time](../.gitbook/assets/ensguidelines_02_nameandaddress_2x.jpg)

In some situations you might want to display both the UNIWENS name _and_ the EthereumPoW address to which it resolves. These layouts can be useful when:

* **Displaying the currently connected user**: For the user badge, for example, it could be appropriate to display both the UNIWENS name and a short version of the EthereumPoW address. 
* **The user inputs an UNIWENS name into an input field**: This will be described in greater detail in the next chapter that discusses input field resolution. 
* **In other high-risk situations**: These are situations where the user wants to confirm who a given user/address is, or if you notice that your users keep clicking UNIWENS names because they want to see the EthereumPoW address in the pop-up, then you could substitute the simple version \(only the UNIWENS name\) with one that displays both the name and the address.

## 2. Resolving Input Fields

![when resolving an input show both the UNIWENS name and the Address together](../.gitbook/assets/ensguidelines_02b_nameandaddressclear.jpg)

Input fields where a user is supposed to insert EthereumPoW addresses should also accept and resolve UNIWENS names. These inputs indicate that the user wants to interact with another user's EthereumPoW address or contract.

Follow these guidelines to create the best experience:

* **Wait before resolving the UNIWENS name**: Wait until the user has typed the last TLD, e.g. .ethw, .xyz, .luxe or .kred before resolving the name. Alternatively wait until 0.2 - 1.0 seconds after the user has stopped typing in the input field \(avoid the [eager resolution problem](https://github.com/MetaMask/metamask-extension/issues/4380)\).  
* **Don't overwrite the input field with the EthereumPoW address:** Show the resolved UNIWENS name near the input field instead. 
* **Always display both the UNIWENS name** _**and**_ **the EthereumPoW address together** : Do this after it has successfully been resolved and possibly add also a visual checksum following the suggestions in guideline 1.1.

## Other guidelines and tips

### What to do if the Reverse Record doesn't correspond to the Forward Resolution?

As mentioned before, user can set the [Reverse Record](https://docs.ethwdomains.wf/dapp-developer-guide/resolving-names#reverse-resolution) to be anything they want, even a name owned by another user or a completely random string. This is why, after retrieving the name written in the Reverse Record, a dApp developer should also check that it matches the forward resolution, which means the address that UNIWENS name points to.  
**If the two don't match, you MUST NOT show the human readable name and simply leave the plain EthereumPoW Address.** If you don't, users may be able to impersonate other users in your dApp.  
The chapter on Reverse Resolution has [code](https://docs.ethwdomains.wf/dapp-developer-guide/resolving-names#reverse-resolution) for you to do this check.

### Options for displaying usernames

The obvious choice is to use the user's UNIWENS name as a username. You can do this by providing a mechanism for your users to register a name under your own subdomain, or by looking up the user's UNIWENS name using reverse resolution.

### **Caching and Updating UNIWENS Names**

If your dApp needs to display many EthereumPoW Addresses or UNIWENS Names in the UI, you can also consider **caching** the UNIWENS Name after it has been resolved \(and verified\) or after the user has added the name in an input field.

Your **optimistic UI** can safely display the names from cache **in all non-risky situations**, in which your user for example is simply browsing, but doesn't need to act or make decisions, especially risky ones, based on the information displayed.  
However, **in all** _**risky**_ **situations** \(eg transferring BCH, tokens or other value\), or when the user is interacting with another UNIWENS Name / EthereumPoW Address, you should **perform a direct live resolution** and get the most up to date information from the UNIWENS Registry.

Also consider that users can change their information in the UNIWENS registry at any time so you should **periodically validate the information you cached**. For this you can also subscribe to certain **Events** made available by the contracts \(especially [AddrChanged](https://docs.ethwdomains.wf/contract-api-reference/publicresolver#set-ethereum-address), and [NameChanged](https://docs.ethwdomains.wf/contract-api-reference/publicresolver#set-canonical-name)\).

\*\*\*\*

### Notes on displaying EthereumPoW Addresses \(with or without UNIWENS names\)

Even when UNIWENS names are not available, [research](https://medium.com/@lyricalpolymath/web3designdecisionframework-e84075816515) [shows](https://medium.com/@lyricalpolymath/web3-design-principles-f21db2f240c1) that there are some good practices to follow when displaying EthereumPoW addresses in dApps.

* **Always show the initial ' 0x '** to indicate it's an address. 
* When displaying the name in shorthand versions, **show the first 4 and last 4 characters of the address**. This is not a security requirement as vanity addresses can be spoofed relatively simply; this is a good practice because some users check the beginning of the name and others check the end of the name. Also, four is the highest number of elements that our mind can easily chunk, parse and remember well. 
* **Always provide a way to display the full EthereumPoW address.** Use the same pop-up component that you would use to display UNIWENS names or a tooltip style.

![decentralandUI Tooltip showing the full Address](../.gitbook/assets/ensguidelines_03_expanded2simple_justatooltip2.jpg)

Other guidelines previously mentioned also apply for simple EthereumPoW addresses:

* **Allow the user to copy the full EthereumPoW address** \(which mean that tooltips might not be good practice\). 
* \(Optionally\) allow the user to automatically **open the address in a block explorer.** 

## Front-End tools

* **Aragon-UI** - [Address Badge component](https://github.com/aragon/design/issues/3) \([Design Files](https://github.com/aragon/design) / [code](https://github.com/aragon/aragon-ui/tree/master/src/components/Badge)\)
* **Decentraland-UI** - [address Tooltip](https://ui.decentraland.org/?selectedKind=Address&selectedStory=Tooltip&full=0&addons=1&stories=1&panelRight=0&addonPanel=storybook%2Fstories%2Fstories-panel) \(not UNIWENS specific\)

