# Working with ĐNS

Before you can begin interacting with ĐNS, you will need to obtain a reference to the ĐNS registry. How you do this depends on the library you are using.

Example code for the Javascript-based APIs \(ensjs, web3.js, ethjs-ens, and ethers.js\) here expect that they are being run inside a DApp browser, such as Chrome with [metamask installed](https://metamask.github.io/metamask-docs/Main_Concepts/Getting_Started), which exposes the `ethereum` object.

In all cases when using a library designed for ENS, you will have to provide the ĐNS registrar contract address to the library.

{% tabs %}
{% tab title="ensjs" %}
```javascript
import ENS from '@ensdomains/ensjs'
import ENS_REGISTRAR_ADDRESS from '@mistswapdex/sdk'

const ens = new ENS({ provider, ensAddress: ENS_REGISTRAR_ADDRESS[10000] })
```
{% endtab %}

{% tab title="web3.js" %}
```javascript
var Web3 = require("web3")
var { ENS_REGISTRAR_ADDRESS } = require('@mistswapdex/sdk');

var accounts = ethereum.enable();
var web3 = new Web3(ethereum);
web3.eth.ens.registryAddress = ENS_REGISTRAR_ADDRESS[10000];
var ens = web3.eth.ens;

```
{% endtab %}

{% tab title="ethjs-ens" %}
```javascript
const ENS = require('ethjs-ens');
const { ENS_REGISTRAR_ADDRESS } = require('@mistswapdex/sdk');
// Currently requires both provider and
// either a network or registryAddress param
var accounts = ethereum.enable();
const ens = new ENS({ ethereum, network: '1', registryAddress: ENS_REGISTRAR_ADDRESS[10000] });
```
{% endtab %}

{% tab title="ethers.js" %}
```javascript
const { ethers } = require('ethers');
const { ENS_REGISTRAR_ADDRESS } = require('@mistswapdex/sdk');

const provider = new ethers.providers.JsonRpcProvider('https://smartbch.fountainhead.cash/mainnet', {
    name: 'smartbch',
    chainId: 10000,
    ensAddress: ENS_REGISTRAR_ADDRESS[10000],
});

(async () => {
    const resolver = await provider.getResolver('kasumi.doge');
    console.log(resolver.address);
    console.log(await provider.lookupAddress('0x8370DAE31693A8BbB9630b7052de52aCBcEC7525'));
})()
```
{% endtab %}

{% tab title="go-ens" %}
```go
import (
  ens "github.com/wealdtech/go-ens/v2"
  ethereum "github.com/ethereum/go-ethereum"
)

// Can dial up a connection through either IPC or HTTP/HTTPS
client, err := ethereum.Dial("/home/ethereum/.ethereum/geth.ipc")
registry, err := ens.Registry(client)
```
{% endtab %}

{% tab title="web3.py" %}
```python
from ens.auto import ns
```
{% endtab %}

{% tab title="web3j" %}
```java
EnsResolver ens = new EnsResolver(web3j, 300 /* sync threshold, seconds */);
```
{% endtab %}
{% endtabs %}

Some web3 libraries - e.g., ethers.js, web3j, and web3.py - have integrated support for name resolution. In these libraries, you can pass in an ĐNS name anywhere you can supply an address, meaning you do not need to interact directly with their ĐNS APIs unless you want to manually resolve names or do other ĐNS operations.

If no library is available for your platform, you can instantiate the ĐNS registry contract directly using the interface definition [here](https://github.com/ensdomains/ens/blob/master/contracts/ENS.sol). Addresses for the ĐNS registry on each supported network are available in the [ĐNS Deployments](../dns-deployments.md) page.

