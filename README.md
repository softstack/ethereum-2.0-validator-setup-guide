# How to setup a fast and secure Ethereum 2.0 validator node with OVHcloud

`code()`
## Introduction

Ethereum 2.0 is the next step in the evolution of Ethereum. It brings with it many changes, including Proof-of-Stake, Sharding, new client implementations, new cryptography and more.

## Be a validator
* have learned the essentials by watching ['Intro to Eth2 & Staking for Beginners' by Superphiz](https://www.youtube.com/watch?v=tpkpW031RCI)
* have passed or is actively enrolled in the [Eth2 Study Master course](https://ethereumstudymaster.com)
* and have read the [8 Things Every Eth2 validator should know.](https://medium.com/chainsafe-systems/8-things-every-eth2-validator-should-know-before-staking-94df41701487)

## 1.	Prerequisites

### 1.1 Recommended Hardware Setup
* **Operating system:** 64-bit Linux (i.e. Ubuntu 20.04 LTS Server or Desktop)
* **Processor:** Quad core CPU, Intel Core i7–4770 (3,40 GHz / Cores: 4 Threads: 8) or AMD FX-8310 or better
* **Memory:** 16GB DDR4 RAM or more
* **Storage:** 2TB NVMe or more, IOPS: 10,000 (medium speed) and 16,000 (fast)
* **Internet:** Broadband internet connections with speeds at least 10 Mbps without data limit.
* **Power:** Reliable electrical power with uninterruptible power supply (UPS)
* **ETH balance:** at least 32 ETH and some ETH for deposit transaction fees
* **Wallet:** Metamask installed

### 1.2 Self-hosting vs. Dedicated Server by OVH

Having your own hardware
First solution, buy equipment optimized for our needs and run it at home.
Benefits:
•	Cost optimization
•	Possibility of reselling the equipment
If you ever want to upgrade your equipment or stop your validator activity, you will be able to recover part of your investment by reselling your purchase.
•	Optimal participation to decentralization
Beyond the financial reward provided by a validator, we must not forget that we are there to support a decentralized network.
•	Physical security (OVH has no access to dedicated servers) 
Disadvantages:
•	Electricity and internet suppliers reliability
As you probably know, Ethereum proof of stake algorithm will punish validators when they go offline. Rest assured this punishment remains low, around 0.3% of the stake for a week offline according to Paul Hauner’s estimates. 
•	Price of electricity
•	Equipment maintenance
•	Risk of having unsuitable equipment
As explained above, we do not yet know what the final specs will be once the full roadmap goes into production. 
Using a dedicated server
Benefits:
•	Electrical, network, and hardware security 
•	Upgradability
•	No additional cost on your electricity bill
Disadvantages:
•	Premium to pay
Dedicated servers are generally more expensive in the long run than buying hardware and hosting it yourself. But let’s see how it turns out in the calculation.
•	Money invested is wasted
•	Less decentralization but mostly 99% up-time
•	Physical attack surface (OVH has no access to dedicated servers)



## Resources

<details>
  <summary>Knowledge Base</summary>
  Links to aggregators of knowledge with additional information on topics above and more

* ConsenSys: https://consensys.net/knowledge-base/ethereum-2
* BeaconChain: https://kb.beaconcha.in
* Ethhub: https://docs.ethhub.io/ethereum-roadmap/ethereum-2.0/eth-2.0-phases/
* Calculator + resources: https://docs.google.com/spreadsheets/d/15tmPOvOgi3wKxJw7KQJKoUe-uonbYR6HF7u83LR5Mj4/edit#gid=1548910165

</details>

<details>
  <summary>Ethereum 2.0 block explorers</summary> 
* Etherscan: https://beaconscan.com
* Beacon Chain: https://beaconcha.in
</details>

### Validator stats

- Eth2stats: https://eth2stats.io/medalla-testnet

## Ethereum 2.0 client implementations

- Prysm (Go): https://github.com/prysmaticlabs/prysm
- Lighthouse (Rust) https://github.com/sigp/lighthouse
- Teku (Java): https://github.com/PegaSysEng/teku
- LodeStart (TypeScript): https://github.com/ChainSafe/lodestar
- Trinity (Python): https://github.com/ethereum/trinity

## Forums

- Eth research: https://ethresear.ch
- Ethereum magicians: https://ethereum-magicians.org

## Spec

- Ethereum 2.0 spec: https://github.com/ethereum/eth2.0-specs
- Vitalik's annotated eth2 spec: https://github.com/ethereum/annotated-spec
- Ben Edgington's annotated spec: https://benjaminion.xyz/eth2-annotated-spec/

## Economics

- Economics: https://docs.ethhub.io/ethereum-roadmap/ethereum-2.0/eth-2.0-economics/

## Blogs

- Ethereum blog: https://blog.ethereum.org/
