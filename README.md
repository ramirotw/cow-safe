# Workshop to trade in cowswap using gnosis-safe through SDK

The purpose of this workshop is to present how to easily create a market order using [Meta DEX cowswap](https://cowswap.exchange/#/swap?chain=rinkeby) through its [SDK](https://github.com/cowprotocol/cow-sdk). With a simple transaction it encapsulates the steps of pre-signing, approval, even wrapping.

The **slides** presented at the EthLatam Buenos Aires workshop are [**available here**](https://docs.google.com/presentation/d/1ANvWjFz5z0PsWg73VGwvrCeZO6WrgbHXYsl7uyl0q5Y/edit#slide=id.g1439ea46373_1_297).

> This workshop is inspired by a [CLI working in progress repository](https://github.com/anxolin/cow-safe) from a member of the [**CoW protocol**](https://cow.fi/es) core team.

## Overview

Right now there is a large group of DAO's managing their treasury with a secure multi-signature wallet.
Multi-signature orders can suffer from several drawbacks:

- Waste of gas cost when tx fails, (due to lack of signature and expiration).
- Bots eat all the slippage (due to lax slippage trying to cover volatility).

This is solved with the professional [CoW Protocol](https://docs.cow.fi/) settlement layer, that is why we present how to package a series of actions in a simple transaction using [gnosis-safe](https://gnosis-safe.io/app/), this unlock a range of possibilities that we encourage you to try.

## 📝 Requirements

- [yarn](https://classic.yarnpkg.com/lang/en/docs/install/)
- [infura](https://infura.io/dashboard) key account
- [mnemonic seed](https://iancoleman.io/bip39)
- [gnosis-safe](https://gnosis-safe.io/app/welcome) wallet (for the gnosis-safe example)

## 🚀 Setting up

1. Install the packages with yarn

```bash
    yarn install
```

2. Copy `.env.example` variable file and rename to `.env` then put necessary variables into it.

```txt
    INFURA_KEY=yourRinkebyNetworkInfuraKey
    MNEMONIC=your rinkeby test seed phrase
```

## 🧑‍💻 Let's get to work

> For these example we will sell 0.1 **WETH** per **GNO** in the rinkeby network

### 1. Create a market order with a external owned account (EOA)

```bash
yarn sell examples/eoa-rinkeby-market-order.json
```

The input data is fed from [eoa-rinkeby-market-order.json](./examples/eoa-rinkeby-market-order.json)

### 2. Create a market order using a gnosis-safe wallet

```bash
yarn sell examples/safe-rinkeby-market-order-1owner.json
```

A single signatory account of gnosis-safe is now used

```json
...
"account": {
    "accountType": "SAFE_WITH_EOA_PROPOSER",
    "safeAddress": "yourSingleSignatoreAddress"
  },
...

```

The data is fed from [safe-rinkeby-market-order-1owner.json](./examples/safe-rinkeby-market-order-1owner.json)

### 3. Create a market order using a multisignature safe wallet

```bash
yarn sell examples/safe-rinkeby-market-order-2owners.json
```

A multi-signature account is now used

```json
...
"account": {
    "accountType": "SAFE_WITH_EOA_PROPOSER",
    "safeAddress": "yourMultiSignatureAccount"
  },
...

```

The data is fed from [safe-rinkeby-market-order-2owners.json](./examples/safe-rinkeby-market-order-2owners.json)

## 😎 That's it for now

---

## 📔 References

- [Signing orders via API](https://docs.cow.fi/tutorials/how-to-submit-orders-via-the-api)
- [Post orders with CLI](https://github.com/anxolin/cow-safe), created by @anxolin
- EthDenver Talk [Why All DAOs Should Use](https://www.youtube.com/watch?v=xP3j1e3oNwo) by Anna George
