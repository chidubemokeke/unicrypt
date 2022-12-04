---
sidebar_position: 3
title: Queries
description: Sample Queries
---

## Sample Queries

Here, you'll learn how to gather information from the Unicrypt subgraph by writing GraphQL queries on it.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

You can fetch data points like

- [Lockers](#lockers)
- [LPToken](#lptoken)
- [Users](#users)
- [Presales](#presales)
- [Vesting](#vesting)

## Lockers

Description: This query returns two types of locker contracts - UniswapV2Locker and TokenVesting.

```graphql
{
  lockers(first: 5) {
    id
    totalLocks
    totalTokens
  }
}
```

Currently, there is a single token vesting contract and multiple contracts deployed for each supported AMM (on eth it’s univ2 and sushi). Liquidity lockers only support lp pairs, tokenVesting is primarily for non-lp tokens.

## LPToken

Description: This query returns an LPToken with multiple locks. You can preview [here](https://app.unicrypt.network/amm/uni-v2/pair/0x05BE6820730b30086d6355C44c424230AaFf41fb). A locked LPToken is basically a uniswap pair entity with extra data related to Unicrypt. `LPToken` could easily be replaced by a Uniswap pair. Each locked LPToken can have multiple liquidity locks(LiquidityLock is a time locked portion of LPTokens).

```graphql
{
  lockedLPTokens(
    where: { lpToken: "0x05be6820730b30086d6355c44c424230aaff41fb" }
  ) {
    locks {
      amount
      unlockDate
    }
  }
}
```

Locks with expired unlockDate (unlockDate > current timestamp) mean the liquidity is no longer secured, the same applies to vested tokens. It would be ideal to filter by unlock timestamps.

## Users

The User entity tracks all protocol interactions by a wallet. This query fetches data for users presale participations.

```graphql
{
  users {
    id
    presaleParticipations {
      isWhitelisted
      baseDeposited
      tokensOwed
      unclOwed
    }
  }
}
```

Base token is usually eth or usdc that presale token is paired against once lp pair is created upon successful presale

## Presales

Description: This query returns presales that are active.

```graphql
{
  presales(where: { status: Active }) {
    UNCLAmountPerAllocation
    tokenAmountForPresale
    whitelistAssigned
    statusDetails
    tokenPrice
    hardcap
    softcap
    isEthPresale
    lockPeriod
    listingRate
    presaleToken {
      id
      name
      symbol
    }
  }
}
```

## Vesting

Description: This query returns vested locks for a token(one for each service).

```graphql
{
  tokens(where: { id: "0xf0f9d895aca5c8678f706fb8216fa22957685a13" }) {
    name
    symbol
    decimals
    vestedTokens {
      vestedLocks {
        amountShares
        startEmission
        endEmission
      }
    }
  }
}
```
