# TRON-ETH raw txn Adapters & Interfaces

## TLDR

Experimental project, we aim to understand and demonstrate the fundamental differences between Ethereum and TRON in regards of their transaction life cycle to eventually improve TRON EVM compatibility trough json-rpc interfaces

## Goal

Create a basic Ethereum --> TRON raw transaction adapter POC to ultimately serve as interface mock up to enable the following json-rpc methods on TRON:

* eth_sendRawTransaction
* eth_signTransaction


## Motivation

TRON has known limitations on its json-rpc interface and state management, causing critical Ethereum tooling incompatibility, which prevents both, EVM developers and TRON developers to utilize Ethereum tooling, such as:

* Foundry/Alloy
* viem
* Hardhat
* etc


## Research

Ethereum JSON-RPC methods fall into three main categories:

1. Gossip: These methods track the latest block of the chain, no history or state is needed
   1. eth_blockNumber --> Fully supported on TRON
   2. eth_sendRawTransaction --> Not supported on TRON (Neded in Foundry)
2. State: These methods get the chain "state" as per specif block hight, TRON doesn't track state as of now, so only "latest" data is available, efforts are being made based on Erigon to allow this. Archive node WiP [here](https://github.com/tronprotocol/java-tron/issues/6289):
   1. eth_getTransactionCount --> Not supported on TRON (Needed in Foundry)
   2. eth_call --> Partially implemented, only "latest" QUANTIT/TAG is available
3. History:
