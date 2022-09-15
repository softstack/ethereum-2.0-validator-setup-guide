# How to setup a fast and secure Ethereum 2.0 validator node with OVHcloud


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

| :white_check_mark: Benefits  | :x: Disadvantages |
| ------------- | ------------- |
| Cost optimization | Electricity and internet suppliers reliability  |
| Possibility of reselling the equipment | Price of electricity |
| Optimal participation to decentralization | Equipment maintenance  |
| Physical security | Risk of having unsuitable equipment  |

Using a dedicated server

| :white_check_mark: Benefits  | :x: Disadvantages |
| ------------- | ------------- |
| Electrical, network, and hardware security  | Premium to pay  |
| Upgradability | Money invested is wasted |
| No additional cost on your electricity bill | Less decentralization but mostly 99% up-time  |
| Physical security | Risk of having unsuitable equipment  |

Regarding physical security: https://docs.ovh.com/gb/en/dedicated/securing-a-dedicated-server/

### 1.3 Buy a dedicated server

Go to https://www.ovhcloud.com/en/bare-metal/prices/

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190447406-dbb77299-1632-4c54-a223-3e3b655ee025.png">

**Compare** <br>

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190447790-cf0b5d81-8ecb-4513-b1c8-b65549ed58ca.png">

Advance-1 gen2 for fast sync and Rise-1 for medium sync speed, you can decide 

We have chosen Advance-1 Gen2 with 1Gbit/s unmetered, guaranteed traffic and enough disk space to keep up with the chain increase for a while. 

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190448972-0b325283-0cdb-4795-8599-3099db19aab2.png">

Rent for 24 months and pay all upfront to earn in total 15% discount + free setup fee

<img width="249" alt="image" src="https://user-images.githubusercontent.com/33572557/190449264-27ef97b5-c31a-452a-ad63-199e9039d4d4.png">

It will take around 24h until the dedicated server is ready for setup

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190449918-da7debac-4886-4081-ae1b-f59701a11cfb.png">

### 1.4 Initial Setup
Once you got an email regarding the successful creation of the server, go to your dedicated server dashboard and start the initial setup.<br>
**Go to:** https://www.ovh.com/manager/#/dedicated/server/.. 

<img width="450" alt="image" src="https://user-images.githubusercontent.com/33572557/190451473-a0326871-81a1-4eef-a076-da0c4b5e1a3c.png">

Install the preferred OS, via “Last operating system (OS) installed by OVHcloud” 

> **Note**
> Creating a server requires you to add an SSH Key, follow the guide https://docs.ovh.com/gb/en/dedicated/creating-ssh-keys-dedicated/ 


We recommend **Ubuntu Server 20.04 LTS "Focal Fossa" - ubuntu2004-server 64 bit.** 
In the last step you must set the SSH key and host name, before you are able to install the OS.

<img width="452" alt="image" src="https://user-images.githubusercontent.com/33572557/190453011-fb3bcebb-0871-4156-b95a-b92995611a79.png">

## 2. Hardening you node

### 2.1 Login via SSH to your server. Run the following command:
```
ssh ubuntu@162.19.19.1
```
### 2.2 Create a non-root user with sudo privileges. Run the following commands:
```
sudo useradd -m -s /bin/bash ethereum
```
Set the password for ethereum user
```
sudo passwd ethereum
```
Add ethereum to the sudo group
```
sudo usermod -aG sudo ethereum
```
### 2.3 Disable SSH password Authentication and Use SSH Keys only

The basic rules of hardening SSH are:

* No password for SSH access (use private key)
*	Don't allow root to SSH (the appropriate users should SSH in, then su or sudo)
*	Use sudo for users so commands are logged
*	Log unauthorized login attempts (and consider software to block/ban users who try to access your server too many times, like fail2ban)
*	Lock down SSH to only the ip range your require (if you feel like it)

Transfer the public key to your remote node. Update keyname.pub appropriately.
```
ssh-copy-id -i $HOME/.ssh/keyname.pub ethereum@server.public.ip.address
```




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
