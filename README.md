# Ancon Protocol v1.5 Whitepaper
## Decentralized Verifiable Data Agent

## Abstract

This document contains a proposal for managing the diverse set of technologies require to implement decentralize data unions using Ancon Protocol v1.0 and named `Decentralized Verifiable Data Agent`, where like Verified Credentials agents, you have a network of agents, where an agent can be a smartphone, IoT, browser, server or edge application.

It describes separating Ancon Protocol v1.0 into layers, which separate concerns and aspects such as consensus and proofs, storage and data, and computation and jobs.

We will explain the next version of the protocol, which includes removing the dependency of Graphsync, incorporating SQLite APIs, Indexed DB, VFS and Waku (a libp2p library). Additionally we will include separating the Dag Storage Nodes, Indexers and Merkle Trees consensus in Tendermint or Polkadot.

## Problem

For the last 40 days the team has been working on implementing a use case for protocol v1 with great results and confirmations of the protocol choice of technology stack.

However we left some pendings protocol features for later, which we assume was not going to be a blocker for implementing dapps as the initial plan. The following items are major paint points to consider:

- Distributed Data Query
- Incomplete Dag syncronization
- Partial suppport for offchain computation
- Dag Indexing, publishing and privacy

### Distributed Data Query

Previously, we propose [DAG Chain Redux](https://github.com/anconprotocol/dag-chain-redux) as a way to consolidate indexing using smart contracts events. While this will work in server side scenarios it does not cover client side or light client nodes like browsers or smartphones. It also does not have any compatibility with for example enterprise ethereum trusted offchain computing specification.

### Incomplete Dag syncronization

Currently Ancon Protocol v1 only synchronizes with IPFS pinning services. While Ancon Protocol is compatible with Graphsync it will only work for server side scenarios because the current Graphsync is only available with Go Language SDKs.

### Partial suppport for offchain computation

Ancol Protocol v1 + [DAG Chain Redux](https://github.com/anconprotocol/dag-chain-redux) in its current iteration is implemented using JEXL which is an expression language for javascript.
IdeaLly a complete feature will have to include QuickJS compile WASM artifacts and will have to be run in a specific client side node.

### Dag Indexing, publishing and privacy

Besides storage and computation a succesful data union must include: Data indexing, Data Publishing, Security and Privacy controls which are nice to haves to the core protocol features.

### Deprecating IAVL

As per [ADR-040](https://docs.cosmos.network/master/architecture/adr-040-storage-and-smt-state-commitments.html), Cosmos is migrating towards SMT (Sparse Merkle Trees) using [Celestia SMT](https://github.com/celestiaorg/smt). This change makes newer ICS23 Proof storage DB agnostic.

## Prior Work

V1.5 takes major inspiration from [Static torrent website with peer-to-peer queries over BitTorrent on 2M records](https://boredcaveman.xyz/post/0x2_static-torrent-website-p2p-queries.html) and [A future for SQL on the web](https://jlongster.com/future-sql-web). Also we will take ideas from [Datasette](https://datasette.io/) publishing feature.

## Ancon Protocol v1.5 - Javascript reference implementation

### Implementing Ancon Data Agent Library

- Implement a concrete Typescript class from [blockstore-core](https://github.com/ipfs/js-blockstore-core) interface, using  [AbsurdSQL](https://github.com/jlongster/absurd-sql). This blockstore becomes a fsstore-like storage, with [Waku](https://docs.wakuconnect.dev/docs/guides/03_store_retrieve_messages/)  as networking layer and [JS IPLD](https://github.com/ipld/js-dag-json) and [multiformats](https://github.com/multiformats/js-multiformats) as DAG block  layer.

- Permanent sync and large assets of data using adapters to Arweave, Filecoin and/or  Subspace using $ANCON + cross chain liquidity bridges

- Implement SQLite queries  with gas  consumption and estimation

- Implement block sync with Waku (ideas: [Litestream](https://litestream.io/))

- Implement dual layer data-execution module: a DAG layer (immutable) and a DB layer (read-only), where (a) Any insert or updates are signed and created as DAG blocks, and a linkeable and versioned JSON data model is stored in the DB Layer. (b) Read-only queries are executed on DB layer (c) GraphQL is used as execution layer and lower level  QuickJS Smart Contracts for other use cases.

### Implement DID enable local keyring

-  Manages account keys, DID compatible with Ed25519 crypto suite


### Implement incentivized network for relayers

- Relayers will in v1.5 query the state commitments from Ancon Node chain, with the incentives  ocurring when posting root blocks from Ancon Node chain to Ancon relayers


### Ancon Node IAVL/Celestia as a chain (Tendermint/Gossamer)

- We propose, a gasless chain, that only stores state commitments separate from the state storage, taking inspiration from  ADR-040. 
- DAG blocks commit transactions and relayers submit roots to protocol smart contracts


### Support HPKE and BBS+

- Messages encrypted with recently announced `HPKE` for secure forward secrecy.
- Add BBS+ for selective disclosure



## Use Case

### A better DAG Chain redux

- Offloads server nodes indexing to edge devices, together with Waku and Ancon Data Agent library, allow indexing to happen close to the owner, maintains privacy, and only publish public datasets or collections to data marketplaces (like eg NFT marketplaces).


### Next Generation NFT Marketplaces

- Allows for Ancon Protocol v2.0 - Content Provenance and Authenticity to be fulfilled, by creating proof of android or ios with SafetyNet or DeviceCheck, maintaing access control and origin signing of content, like images, audios or videos creating with smartphones or IoT devices.

### Data Unions

- Perfects the use case for ad-hoc networks of data unions, and preserves security, privacy and integrity by separating state commitments (proofs) from state storage (DAGs).




## Summary

In this whitepaper we described Ancon Protocol v1.5, which integrates v1.0 paradigm shift of verifiable, offchain metadata  and vector commitments proof for cross chain scenarios, with features to expand into data unions and trusted offchain computing, while also being open for futures roadmap related to content provenance and authenticity for Web 3.0 data economies.

## Authors

Rogelio Morrell,Kendall Kant,Ricardo Menotti for Industrias de Firmas Electronicas SA , 2022.
  
