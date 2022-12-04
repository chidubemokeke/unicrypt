---
sidebar_position: 2
title: Entities
description: Entities
---

## Entities

## Locker

| Field       | Type    | Description            |
| ----------- | ------- | ---------------------- |
| id          | ID!     | Locker.address         |
| totalLocks  | BigInt! | Total number of locks  |
| totalTokens | BigInt! | Total number of Tokens |

## LockedLPToken

| Field         | Type              | Description                                  |
| ------------- | ----------------- | -------------------------------------------- |
| id            | ID!               | Locker + Pair                                |
| lpToken       | LPToken!          | LpToken address                              |
| locker        | Locker!           | Locker address                               |
| numberOfLocks | BigInt!           | Total number of locks for a pair address     |
| amountLocked  | BigDecimal!       | Total amount of LP tokens vested in the lock |
| locks         | [LiquidityLock!]! | Get all locks for LP token                   |

## LiquidityLock

| Field         | Type           | Description                                    |
| ------------- | -------------- | ---------------------------------------------- |
| id            | ID!            | Locker + Pair + LockID                         |
| locker        | Locker!        | Locker address                                 |
| lockedLPToken | LockedLPToken! | Pair address of the LP tokens locked           |
| lockID        | BigInt!        | LockID of a Lock                               |
| amount        | BigDecimal!    | Amount of LP tokens vested in the lock         |
| initialAmount | BigDecimal!    | Initial amount of LP tokens vested in the lock |
| lockDate      | BigInt!        | Creation timestamp                             |
| unlockDate    | BigInt!        | Unlock timestamp                               |
| owner         | User!          | Lock owner address                             |

## VestedToken

| Field         | Type           | Description                                |
| ------------- | -------------- | ------------------------------------------ |
| id            | ID!            | Locker + Token                             |
| token         | Token!         | Vested token address                       |
| locker        | Locker!        | Locker address                             |
| numberOfLocks | BigInt!        | Total number of locks for a token address  |
| sharesLocked  | BigDecimal!    | Total amount of shares vested in the token |
| vestedLocks   | [VestedLock!]! | Get all locks for a token                  |

## VestedLock

| Field         | Type         | Description                         |
| ------------- | ------------ | ----------------------------------- |
| id            | ID!          | Locker + ID (Nonce)                 |
| locker        | Locker!      | Locker address                      |
| vestedToken   | VestedToken! | Vested Token                        |
| lockID        | BigInt!      | LockID of a Lock (Nonce)            |
| amountShares  | BigDecimal!  | Amount of shares vested in the lock |
| startEmission | BigInt!      | Emission start timestamp            |
| endEmission   | BigInt!      | Emission end timestamp              |
| owner         | User!        | Lock owner address                  |

## PresaleFactory

| Field | Type | Description             |
| ----- | ---- | ----------------------- |
| id    | ID!  | Presale factory address |

## Presale

| Field                        | Type                   | Description                                               |
| ---------------------------- | ---------------------- | --------------------------------------------------------- |
| id                           | ID!                    | Presale address                                           |
| isEthPresale                 | Boolean!               | Is presale in native chain currency                       |
| baseToken                    | Token!                 | Base token the presale is raising                         |
| presaleToken                 | Token!                 | Token for sale                                            |
| totalBaseCollected           | BigDecimal!            | Current base amount collected                             |
| tokenAmountForPresale        | BigDecimal!            | Amount of tokens available for presale                    |
| maxSpendPerBuyer             | BigDecimal!            | Max amount each buyer is allowed to spend                 |
| numberOfBuyers               | BigInt!                | Current number of buyers                                  |
| tokenPrice                   | BigDecimal!            | PresaleTokens per BaseTokens                              |
| listingRate                  | BigDecimal!            | Listing price                                             |
| softcap                      | BigDecimal!            | Minimum raise to count presale as a success in base token |
| hardcap                      | BigDecimal!            | Maximum raise in base token                               |
| owner                        | User!                  | Presale admin / owner                                     |
| startBlock                   | BigInt!                | Start block of the presale                                |
| endBlock                     | BigInt!                | Presale raise deadline                                    |
| liquidityPercent             | BigInt!                | Percent of the liquidity locked on Unicrypt               |
| lockPeriod                   | BigInt!                | Duration of the liquidity lock                            |
| round0Start                  | BigInt!                | Round0 start block                                        |
| UNCLMaxParticipants          | BigInt!                | Max number of UNCL reserve allocation participants        |
| UNCLParticipants             | BigInt!                | Number of uncl reserve allocation participants            |
| UNCLAddress                  | Bytes!                 | Address of the utility token                              |
| UNCLAmountPerAllocation      | BigDecimal!            | Utility token cost per allocation                         |
| countryCode                  | BigInt!                | Country code of the project                               |
| creationBlock                | BigInt!                | Block at which the presale was created                    |
| creationTimestamp            | BigInt!                | Timestamp at which the presale was created                |
| lpGenerationTimestamp        | BigInt!                | Timestamp of the LP generation                            |
| whitelistCurrentParticipants | BigInt!                | Number of whitelisted users that deposited funds          |
| whitelistAssigned            | BigInt!                | Number of whitelisted users assigned                      |
| whitelistMaxParticipants     | BigInt!                | Maximum number of whitelist participants                  |
| status                       | PresaleStatus!         | Current presale status                                    |
| statusDetails                | PresaleStatusDetailed! | Presale status in detail                                  |
| UNCLBurnOnFail               | BigDecimal!            | Amount of utility token burned on presale fail            |
| tokenSold                    | BigDecimal!            | Amount of presale tokens sold                             |
| tokensWithdrawn              | BigDecimal!            | Tokens withdrawn after a successful presale               |
| baseTokensWithdrawn          | BigDecimal!            | Total base tokens withdrawn on presale failure            |
| participations               | [Participations!]!     | All user participations in a presale                      |

## Participation

| Field           | Type        | Description                                                           |
| --------------- | ----------- | --------------------------------------------------------------------- |
| id              | ID!         | ILO + User address                                                    |
| user            | User!       | Address of a user                                                     |
| presale         | Presale!    | Presale that counts the participation                                 |
| unclOwed        | BigDecimal! | Amount of utility tokens owed to the user                             |
| unclWithdrawn   | BigDecimal! | Amount of utility token withdrawn by a user upon a failed presale     |
| tokensOwed      | BigDecimal! | Amount of presale tokens owed to the user                             |
| tokensWithdrawn | BigDecimal! | Amount of presale token withdrawn by a user upon a successful presale |
| baseDeposited   | BigDecimal! | Amount of base tokens deposited by the user                           |
| baseWithdrawn   | BigDecimal! | Amount of base token withdrawn by a user upon a failed presale        |
| isWhitelisted   | Boolean!    | Is user whitelisted to participate in the presale                     |

## User

| Field                      | Type              | Description                            |
| -------------------------- | ----------------- | -------------------------------------- |
| id                         | ID!               | User address                           |
| presaleParticipations      | [Participation!]! | Presale participations by a user       |
| presaleCreations           | [Presale!]!       | Presales created by a user             |
| totalPresaleParticipations | BigInt!           | Total number of presale participations |
| totalPresalesCreated       | BigInt!           | Total presales creations               |
| vestedLocks                | [VestedLock!]!    | Vested locks user owns                 |
| liquidityLocks             | [LiquidityLock!]! | Liquidity locks user owns              |

## Token

| Field               | Type            | Description                              |
| ------------------- | --------------- | ---------------------------------------- |
| id                  | ID!             | Token address                            |
| symbol              | String!         | Token symbol                             |
| name                | String!         | Token name                               |
| decimals            | BigInt!         | Token decimals                           |
| lpToken0s           | [LPToken!]!     | All LP tokens where token is token0      |
| lpToken1s           | [LPToken!]!     | All LP tokens where token is token1      |
| vestedTokens        | [VestedToken!]! | All VestedToken entities for this token  |
| presalesSalesTokens | [Presale!]!     | All presales where token is a sale token |
| presalesBaseTokens  | [Presale!]!     | All presales where token is a base token |

## LPToken

| Field          | Type              | Description                        |
| -------------- | ----------------- | ---------------------------------- |
| id             | ID!               | Pair address                       |
| token0         | Token!            | Token0 address                     |
| token1         | Token!            | Token1 address                     |
| lockedLPTokens | [LockedLPToken!]! | Locked LP Tokens for an LP address |
