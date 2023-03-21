---
id: supernets-deploy-bridge
title: Deploy the Native Bridge on Mumbai
sidebar_label: Deploy the native bridge on Mumbai
description: "An introduction to Polygon Supernets."
keywords:
  - docs
  - Polygon
  - edge
  - supernets
  - childchain
  - network
  - modular
---

:::caution Document is being updated
:::

This document outlines a full deployment of a testnet childchain in bridge mode, using the Mumbai PoS testnet as the rootchain.

:::info Testnet version only available

Currently, Supernets are only available as testnets. Mainnet is targetted for some time in Q2 2023, where the rootchain becomes Polygon PoS.

:::

:::tip Stay tuned for upcoming deployment guides

Deployment guides for Polygon Supernets are forthcoming, with cloud deployment scripts for AWS and Azure, and Terraform infrastructure-as-a-service guides to be included. Stay tuned for updates!
:::

---

## Genesis

```bash
polygon-edge genesis --consensus polybft --block-gas-limit 10000000 --epoch-size 10 \
      --bridge-json-rpc https://mumbai-rpc.com \
      --manifest <path to the manifest file>
      --premine 0x0000000000000000000000000000000000000000
```

## Childchain testnet

```bash
$ polygon-edge server
    --chain genesis.json [--data-dir <account secrets data directory> | --config <path to the account secrets config>] \
    --libp2p <lib p2p ip address and port> --json-rpc <json rpc ip address and port> ... \
    --num-block-confirmations 2
```

## Deposit

```bash
$ polygon-edge bridge deposit-erc20 \
      --data-dir ./rootchain-secrets \
      --amounts 1000000000000000000,1000000000000000000,1000000000000000000,1000000000000000000 \
      --receivers 0x762D91379bb4241d0A7C74A9FF8dc43d56B36375,0x762D91379bb4241d0A7C74A9FF8dc43d56B36375,0x762D91379bb4241d0A7C74A9FF8dc43d56B36375,0x762D91379bb4241d0A7C74A9FF8dc43d56B36375 \
      --root-token 0x1A04Fc0f2C99DDA4Da5B9cEE7c46F2FF8b15D8d7 \
      --root-predicate 0x6551D7E524aC1fFfCb821a543BCb014Dc17b0fEe \
      --json-rpc https://mumbai-rpc.com
```

## Withdraw

```bash
$ polygon-edge bridge withdraw-erc20 \
      --data-dir <child chain account data directory> [--config <child chain account config path>] \
      --amounts <amounts to withdraw>
      --receivers <list of receiving accounts addresses on the root chain> \
      --json-rpc <JSON RPC endpoint of one of the child chain validators> \
      [--child-token <address of child ERC20 token>]
      [--child-predicate <address of child ERC20 predicate>]
```

## Exit

```bash
polygon-edge bridge exit \
      --data-dir ./rootchain-secrets \
      --exit-helper 0xe9Ddc8039e24BBfb97D023fC883d2D98edd36B04\
      --exit-id <exit event id> \
      --root-json-rpc https://mumbai-rpc.com \
      --child-json-rpc http://childchain-rpc.com
```