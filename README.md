# Ancon Protocol v1.5
### Distributed Data Client with Verifiable ICS-23 Vector Commitment Proof

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

Previously, we propose Dag-chain-redux as a way to consolidate indexing using smart contracts events. While this will work in server side scenarios it does not cover client side or light client nodes like browsers or smartphones. It also does not have any compatability with for example enterprise ethereum trusted offchain computing specification.

### Incomplete Dag syncronization

Currently Ancon Protocol v1 only synchronizes with IPFS pinning services. While Ancon Protocol is compatible with GraphGync it will only work for server side scenarios because the current GraphSync is only available with Go Language SDKs.

### Partial suppport for offchain computation

Ancol Protocol v1 + dag-chain-redux in its current iteration is implemented using JEXL which is an expressiong language for javascript.
Idealy a complete feature will have to include QuickJs compile WASM artifacts and will have to be run in a specific client side node.

### Dag Indexing, publishing and privacy

Besides storage and computation a succesful data union must include; Data indexing, Data Publishing, Security and Privacy controls which are nice to haves to the core protocol features.

## Prior Work

TODO
https://github.com/ipfs/js-blockstore-core
https://jlongster.com/future-sql-web
https://github.com/libp2p/js-libp2p
https://github.com/ipld/js-dag-json
https://github.com/multiformats/js-multiformats
https://developers.google.com/web/tools/workbox
https://blog.cloudflare.com/using-hpke-to-encrypt-request-payloads/
https://github.com/rhashimoto/wa-sqlite/blob/master/README.md

## Use Case

todo

## Summary

todo

## Authors

Rogelio Morrell, Ricardo Menotti for Industrias de Firmas Electronicas SA , 2022.
