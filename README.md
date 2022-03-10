# Ancon Protocol v1.5
### Distributed Data Client with Verifiable ICS-23 Vector Commitment Proof over any store

## Abstract

This document contains a proposal for managing the diverse set of technologies require to implement decentralize data unions using Ancon Protocol.

We will explain the next version of the protocol, which includes removing the dependency of GraphSync, incorporating SQLlite APIs, Indexed DB, VFS and libp2p. Additionally we will include separating the Dag Storage Nodes, Indexers and Merkle Trees consensus in Tendermint or Polkadot.

## Problem

For the last 40 days the team has been working on implementing a use case for protocol v1 with great results and confirmations of the protocol choice of technology stack.

However we left some pendings protocol features for later, which we assume was not going to be a blocker for implementing dapps as the initial plan. The following items are major paint points to consider:

- Distributed Data Query
- Incomplete Dag syncronization
- Partial suppport for offchain computation
- Dag Indexing, publishing and privacy

### Distributed Data Query

Previously, we propose Dag-chain-redux as a way to consolidate indexing using smart contracts events. While this will work in server side scenarios it does not cover client side or light client nodes like browsers or smartphones. It also does not have any compatibility with for example enterprise ethereum trusted offchain computing specification.

### Incomplete Dag syncronization

Currently Ancon Protocol v1 only synchronizes with IPFS pinning services. While Ancon Protocol is compatible with Graphsync it will only work for server side scenarios because the current Graphsync is only available with Go Language SDKs.

### Partial suppport for offchain computation

Ancol Protocol v1 + dag-chain-redux in its current iteration is implemented using JEXL which is an expressiong language for javascript.
Idealy a complete feature will have to include QuickJs compile WASM artifacts and will have to be run in a specific client side node.

### Dag Indexing, publishing and privacy

Besides storage and computation a succesful data union must include: Data indexing, Data Publishing, Security and Privacy controls which are nice to haves to the core protocol features.

### Deprecating IAVL

As per [ADR-040](https://docs.cosmos.network/master/architecture/adr-040-storage-and-smt-state-commitments.html), Cosmos is migrating towards SMT (Sparse Merkle Trees) using [Celestia SMT](https://github.com/celestiaorg/smt). This change makes newer ICS23 Proof storage DB agnostic.

## Prior Work

V1.5 takes major inspiration from [Static torrent website with peer-to-peer queries over BitTorrent on 2M records](https://boredcaveman.xyz/post/0x2_static-torrent-website-p2p-queries.html) and [A future for SQL on the web](https://jlongster.com/future-sql-web).

## Ancon Protocol v1.5 reference implementation

### Implement Ancon DataClientDB

- Implement a concrete Typescript class from [blockstore-core](https://github.com/ipfs/js-blockstore-core) interface, using  [AbsurdSQL](https://github.com/jlongster/absurd-sql). This blockstore becomes a fsstore-like storage, with [libp2p](https://github.com/libp2p/js-libp2p)  as networking layer and [JS IPLD](https://github.com/ipld/js-dag-json) and [multiformats](https://github.com/multiformats/js-multiformats) as DAG block  layer.

- Implement permanent sync to Arweave, Filecoin and  Subspace using $ANCON + cross chain liquidiity bridges

- Implement SQLite queries over libp2p with gas    consumption and estimation

### Implement local keyring

### Implement incentivized network for relayers

### Ancon Node IAVL/Celestia as a chain (Tendermint/Gossamer)

### Support HPKE


## Use Case

todo

## Summary

todo

## Authors

Rogelio Morrell,Kendall Kant,Ricardo Menotti for Industrias de Firmas Electronicas SA , 2022.
  
