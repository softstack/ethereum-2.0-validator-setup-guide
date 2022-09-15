# How to setup a fast and secure Ethereum 2.0 validator node with OVHcloud

`code()`
## Introduction

Ethereum 2.0 is the next step in the evolution of Ethereum. It brings with it many changes, including Proof-of-Stake, Sharding, new client implementations, new cryptography and more.

<details><summary>## Staking</summary>
<p>
- Each user can run more than one validator. Each validator requires 32 ETH.
- Validators expected to behave according to the protocol. This requires them to be online for voting, and to not attempt to sign and invalid block. To enforce these rules, validators who deviate from the protocol are slashed:
  - Minor slashing for liveness: About 50% uptime is requires to be profitable
  - Massive slashing for double spend attempts: an attempt to double spend might lead to slashing of all 32 ETH

</p>
</details>

## Keys

Unlike Ethereum 1.0, where each address had only one pair of public in private keys, validators in Ethereum 2.0 have two pairs:

- A validator key signing blocks
- A withdrawal key for depositing and withdrawing funds

The separation is to increase security. The validator key needs to be kept “hot” to always be available to sign blocks, while the withdrawal can be kept in cold storageBoth keys are derived from the same mnemonic by following the spec of EIP-2333.

Keys use the BLS12-381 curve, which makes signature aggregation more efficient. Required to allow multiple validators to attest on a block.

Blog on Ethereum keys: https://blog.ethereum.org/2020/05/21/keys/

Ethereum 2.0 keys summary on BeaconChain: https://kb.beaconcha.in/ethereum-2-keys

EIP: https://eips.ethereum.org/EIPS/eip-2333

BLS for the rest of us: https://hackmd.io/@benjaminion/bls12-381

Key generation and deposit repository: https://github.com/ethereum/eth2.0-deposit-cli

## Consensus

- Gasper paper (Ethereum 2.0 consensus): https://arxiv.org/abs/2003.03052

## Sharding

The introduction of shards in planned at phase 1. At the moment, the plan is to operate 64 shards, all linked to the beacon chain.
Ethereum 1.0 is planned to be ported as the first of the 64 shards. Unlike the current execution model, where each transaction is completely atomic, executions on Ethereum 2.0 shards are only going to be atomic on the shards they are launched on. Transition of information between shards will be asynchronous. DApp developers will have to conceder which shards they would like to launch their contracts on, based on the use case and the ecosystem of the shards.

- Sharding FAQ: https://eth.wiki/sharding/Sharding-FAQs
- Sharding research links: https://notes.ethereum.org/@serenity/H1PGqDhpm?type=view

## Knowledge bases

Links to aggregators of knowledge with additional information on topics above and more

- ConsenSys: https://consensys.net/knowledge-base/ethereum-2
- BeaconChain: https://kb.beaconcha.in
- Ethhub: https://docs.ethhub.io/ethereum-roadmap/ethereum-2.0/eth-2.0-phases/
- Calculator + resources: https://docs.google.com/spreadsheets/d/15tmPOvOgi3wKxJw7KQJKoUe-uonbYR6HF7u83LR5Mj4/edit#gid=1548910165

## Ethereum 2.0 block explorers

- Etherscan: https://beaconscan.com
- Beacon Chain: https://beaconcha.in

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
