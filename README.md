# ethereum-2.0-validator-setup-guide
Ultimate guide about the ethereum 2.0 validator setup
# Ethereum 2.0 resources

## Introduction

Ethereum 2.0 is the next step in the evolution of the Ethereum platforms. It brings with it many changes, including Proof-of-Stake, Sharding, new client implementations, new cryptography and more.

There are a lot of write ups, and lot of information regarding Ethereum 2.0. This repository aims to be a curated and concise list of resources, with minor introductions.

## Generally on Ethereum 2.0

Ethereum 2.0 introduces several important changes to the way the current system is operated:

- Proof-of-Stake: Instead of the current mechanism of Proof-of-work, where dedicated hardware is requires to participate in the consensus protocol, Ethereum 2.0 switches to Proof-of-Stake. Validators (instead of miners) are chosen to propose and to attest to blocks according to their proportional holdings of ETH. Validators who deviate from the protocol will be punished -- slashed.
- Sharding: Instead of a single monolithic chain, several chains (shards) will run in parallel. They will run independently from each other, and moving information from one shard to another will require special lock-step transactions
- eWasm execution: Instead or in addition to the currently running Ethereum-Virtual-Machine, Ethereum 2.0 is planned to allow execution of Web Assembly instructions, making it easier to develop smart contracts in a verity of programming languages.

The transformation to Ethereum 2.0 is done in several stages, each introducing a different aspect

- Phase 0: The beacon chain. The beacon chain is the backbone of the proof-of-stake and sharding protocols of Ethereum2.0. The beacon chain will only hold information on the current set of validators, and links to blocks on all future shards.
- Phase 1: Shards. During this stage, several Shards will operate as independent but linked blockchains. Validators will be assigned (pseudo) randomly to shards, and will attest to blocks on each shard. The head of the shards are linked to the beacon chain
- Phase 2: Execution. Only at this stage will the platform be fully operational, enabling transfers and smart contract execution.

A good all-in-one intro to Ethereum 2.0, the beacon chain and sharding: https://ethos.dev/beacon-chain/

## Staking

The change to proof-of-stake, mandates a change in block generation process. To participate, validators lock-up (stake) ETH, and are then allowed to sign and propose blocks. Validators are assigned slots for block proposition and attestation in a pseudo-random process.

A minimal number of validators is required to maintain the security of the system. A small number of validator could give an advantage to the adversary, and break the system. The system thus first undergoes a "bootstrapping" process, where validators stake ETH but the beacon chain is not yet operational. The beacon chain only begins generating blocks after enough ETH is locked, and enough validators have sight up.

To participate in Ethereum2.0 staking as an independent validator, the process is as follows:

1. Obtain 32 ETH
2. Generate keys for ETH validation and deposit
3. Deposit 32 ETH in a special depositing smart contract
4. Run a beacon chain client
5. Run a validator client

- Each user can run more than one validator. Each validator requires 32 ETH.

- Validators expected to behave according to the protocol. This requires them to be online for voting, and to not attempt to sign and invalid block. To enforce these rules, validators who deviate from the protocol are slashed:
  - Minor slashing for liveness: About 50% uptime is requires to be profitable
  - Massive slashing for double spend attempts: an attempt to double spend might lead to slashing of all 32 ETH

Important to note that at the moment, depositing ETH into the smart contract is non-reversible. Staked ETH will be locked up at least until stage 1.5, but will still gain staking rewards and/or slashing.

### Staking walk-through

You can experiment with participating in staking on Ethereum 2.0, by joining the latest testnet.
The testnet requires Goerli ETH in order to participate.

The easiest way to participate in staking on the latest testnet _medalla_ is by following the official Ethereum 2.0 launchpad

- Ethereum org Launchpad: https://medalla.launchpad.ethereum.org

- Launchpad explanatory Blog: https://blog.ethereum.org/2020/07/27/eth2-validator-launchpad/

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
