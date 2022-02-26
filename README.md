# dag-chain-redux
An emergent design pattern based on Ancon Protocol, EIP-3668 and Account Abstraction

![DAG REDUX](https://user-images.githubusercontent.com/1248071/155858908-13282b5a-6612-4783-b9f3-9c4194f01ef3.svg)


## Abstract

There are already open source indexing tools like The Graph and TrueBlocks, which takes enough care of post processing of onchain events.

Ancon Protocol does support indexing features, but one feature we recently cut off was mutable DAG blocks using PUT, because we required full verifiable signatures. In reimagining the problem from another point of view, if we take onchain events as the ultimate proof of truth, we can mutate DAGs similar to the previously implemented Rust WASM Contracts, but instead, taking cues from EIP Account Abstraction, **a relayer gets paid to execute a Javascript smart contract** , these contracts compiled to JEXL or QuickJS WASM Containers.

The result is a signed output, verifiable both offchain and onchain (if used with Ancon Protocol offchain signatures or EIP-3668).


## Use Case

In our flagship NFT Marketplace, the redux flow without DAG Chain Redux looks like:

- POST DAG block to Ancon
- Submit proof to EVM if required
- Wait for transaction
- Listen for Events and sign again mutated block as new POST DAG block

The last action is outside the transaction, which makes it a bad design and very common one. Ideally, listeners or subscribers await web sockets or other messaging mechanism for updates (DISPATCHES) to be made to a DAG Block.

Marketplace needs to keep updated an users NFTs and also the entire most current NFT snapshot. With DAG Chain redux, you can create relayers or INDEXERS in Javascript or inside a WASM engine compatible with QuickJS (https://wasmedge.org/book/en/dev/js/quickstart.html) and execute REDUCERS.

## Summary

A DAG Chain redux is then made of:

- Smart contracts build with security VM isolation using QuickJS and executed in either Javascript or WASM
- Indexers listening for events to dispatch actions
- Which represent a specific reducer, meaning, it takes the current DAG block and reduces it to other data transformation
- Execution by an existing relayer takes care of payment fees, otherwise, an indexer must charge the execution fee directly.
- The state is stored in an Ancon DAG Node, which internal Merkle Tree makes it ICS23 Proof ready, or using an EIP-3668 request response, be available for secure offchain requests.
- Cycles repeats once again

## Alternatives

- Trueblocks
- The Graph
- Do your indexing and merge

## Authors

Rogelio Morrell, Kendall Kant, for Industrias de Firmas Electronicas SA , 2022. 

