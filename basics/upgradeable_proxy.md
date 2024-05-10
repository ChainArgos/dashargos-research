# Upgradeable Proxy Contracts

This post works through the technical details of "upgradeable proxy contacts" on the Ethereum Virtual Machine and how this concept applies to two controversial public examples:

* <img src="https://images.ctfassets.net/q5ulk4bp65r7/3TBS4oVkD1ghowTqVQJlqj/2dfd4ea3b623a7c0d8deb2ff445dee9e/Consumer_Wordmark.svg" alt="" data-size="line">'s base L2 blockchain
* Tornado Cash

## Introduction To Proxies

The OpenZeppelin documentation provides an excellent detailed overview [here](https://blog.openzeppelin.com/proxy-patterns). To quote them:

> One of the biggest advantages of Ethereum is that every transaction of moving funds, every contract deployed, and every transaction made to a contract is immutable on a public ledger we call the blockchain.

> Although it is not possible to upgrade the code of your already deployed smart contract, it is possible to set-up a proxy contract architecture that will allow you to use new deployed contracts as if your main logic had been upgraded.

Because:

1. Ethereum smart contacts are "immutable"
2. Software is generally buggy and needs to be upgraded over time

this is a common problem.

### Standards

There are a few relevant EIP "standard" solutions to these problems. [EIP-1822](https://eips.ethereum.org/EIPS/eip-1822) is the base setup to look at. [EIP-1967](https://eips.ethereum.org/EIPS/eip-1967) has a bit more detail and nuance.

The basic structure of these things is as follows:

```solidity
contract Proxy {
    owner; // the owner
    implementation; // where the real contact lives

    // change the owner
    function setOwner(newowner) {owner = newowner;}

    // upgrade the code
    function setImplementation(newImpl) {
        require(caller == owner);
        implementation = newImplementation;
    }

    // function call through to the real contract
    function indirectCall(...) {
        implementation.Call(...)
    }
}
```

If everyone using the system works through `indirectCall()` the protocol is, in practice, upgradeable.

### Renouncing Ownership

Sometimes a project wants to crystallize a given implementation and give up ownership. They do not want to be in charge anymore. Maybe the project is stable. Maybe no bugs have been found for X months. Maybe they just do not want the legal responsibilities that come with ownership anymore. Whatever reason.

They can:

```solidity
setOwner(0x0000000000000000000000000000000000000000);
```

Now the null address - an address nobody has the private keys for - is the owner. Functionally this means it is no longer possible to upgrade the contract.

If you look at [this current Tornado Cash contract](https://etherscan.io/address/0xA160cdAB225685dA1d56aa342Ad8841c3b53f291#readContract) there is a field `operator`. It is currently set to null. Ownership of this contract was renounced in May 2020 in line with this [Tornado Cash blog post](https://tornado-cash.medium.com/tornado-cash-is-finally-trustless-a6e119c1d1c2). You can see the call on [this transaction](https://etherscan.io/tx/0xa5adf0aa5aecac6dbe3d6a31ea91589bb7c54b10050afec839dad0957ebceb6f) and check the state change [here](https://etherscan.io/tx/0xa5adf0aa5aecac6dbe3d6a31ea91589bb7c54b10050afec839dad0957ebceb6f#statechange).

## Tornado Cash ![](https://miro.medium.com/v2/resize:fill:36:36/2\*CE0d\_LiVIbqYH7PzIpRToQ.png)

[Here](https://etherscan.io/address/0xb541fc07bc7619fd4062a54d96268525cbc6ffef#code) is a Tornado Cash mixer contract.
You can read the code there on etherscan.
Sometimes, if a given proxy conforms to EIP-1822 or a different standard, etherscan can help us out.
Other times, like here where the proxy implementation is non-standard, we need to read for ourselves.

So how can we tell?
By reading the code.
We find a `Proxy` contract type, alongside a `BaseUpgradeabilityProxy` and `AdminUpgradeabilityProxy`.
There are small wrapper functions which change ownership addresses and update implementation details.
There is even a function:

```solidity
function upgradeTo(address newImplementation) external ifAdmin {
    _upgradeTo(newImplementation);
}
```

You do not need to be a solidity expert, or even have programming experience, to figure this out. All you need is to understand the vocabulary and basic concepts.

So that contract was upgradeable.
That means **it was not immutable**.
And per etherscan it processed 962 transactions over a period of about two months. You can see that [here](https://etherscan.io/txs?a=0xb541fc07bc7619fd4062a54d96268525cbc6ffef\&p=1).

## Base <img src="https://images.mirror-media.xyz/publication-images/cgqxxPdUFBDjgKna_dDir.png?height=1200&#x26;width=1200" alt="" data-size="line">

Coinbase's base is a more complex example of the same sort of behavior.

### Standard Contracts

base is built on <img src="https://assets-global.website-files.com/611dbb3c82ba72fbc285d4e2/611fd32ef63b79b5f8568d58_OPTIMISM-logo.svg" alt="" data-size="line">. We can see in those docs [here](https://community.optimism.io/docs/protocol/protocol-2.0/) that a basic optimism setup involves 4 addresses on the L1 chain:

1. L2OutputOracle
2. OptimismPortal
3. L1CrossDomainMessenger
4. L1StandardBridge

Some of these are tagged on etherscan or in the base docs. We can start with the bridge [here](https://etherscan.io/address/0x3154cf16ccdb4c6d922629664174b904d80f2c35#readProxyContract). It is immediately apparent this is an upgradeable proxy contract because they used a standard template and etherscan detects it immediately. Note the "Read as Proxy" and "Write as Proxy" buttons above the code.

Then we can click through to find the [actual implementation code](https://etherscan.io/address/0x3f3c0f6bc115e698e35038e1759e9c31032e590c#code). In there we find a `messenger` variable. Checking the proxy we find it points to [this contract](https://etherscan.io/address/0x866E82a600A1414e583f7F13623F1aC5d58b0Afa#code). So that is the (untagged on etherscan) messenger. Note it is also an upgradeable proxy.

The [portal contract](https://etherscan.io/address/0x49048044d57e1c92a77f79988d21fa8faf74e97e#readProxyContract) is tagged. And using a similar technique we can find [the oracle](https://etherscan.io/address/0x56315b90c40730925ec5485cf004d835058518A0). Both of these, again, are upgradeable proxies.

### Other Components

base is built on optimism. But it goes well beyond being just a deployment of that stack. If you go back and read those contracts you can find 3 more interesting untagged addresses:

1. [Guardian](https://etherscan.io/address/0x14536667Cd30e52C0b458BaACcB9faDA7046E056) which acts as a kill switch
2. [System config](https://etherscan.io/address/0x73a79Fab69143498Ed3712e519A88a918e1f4072#readProxyContract) which governs some parameters of the system
3. [Block proposer](https://etherscan.io/address/0x642229f238fb9de03374be34b0ed8d9de80752c5) which publishes data from the L2 on the L1.

How can we tell? Again go read the code and it is right there.
The Block proposer is stored in the oracle.
The Guardian and System config are stored in the portal.
Etherscan even decodes this stuff for you.
You do not need to read the code - you can just use etherscan's nice UI.

Both Guardian and System config are upgradeable proxies.
The Proposer is not even a contract - it is just a plain old address and someone is firing off transactions with a private key from off the chain.

This is a 100% centralized custodial system.
Coinbase could wipe all the contracts and take all money if they wanted to or were hacked or made a mistake (or were forced to).

## How Big Are The Flows?

[Here](https://dashargos.chainargos.com/looks/516) we can see that there is a lot of volume in USDC and Coinbase-wrapped-USDC on Base.
