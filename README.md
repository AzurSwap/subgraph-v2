# Azurswap Subgraph

This repository has been forked from [UniswapV2 , Quickswap]()

[ETH SUBGRAPH](https://thegraph.com/hosted-service/subgraph/azurswap/azurswap-eth-v2)
[BSC SUBGRAPH](https://thegraph.com/hosted-service/subgraph/azurswap/azurswap-bsc-v2)
[AVAX SUBGRAPH](https://thegraph.com/hosted-service/subgraph/azurswap/azurswap-avax-v2)


This subgraph dynamically tracks any pair created by the Azurswap factory. It tracks of the current state of Azurswap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on Azurswap, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Key Entity Overviews

#### AzurswapFactory

Contains data across all of Azurswap V2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on Azurswap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated Azurswap Data

This query fetches aggredated data from all Azurswap pairs and tokens, to give a view into how much activity is happening within the whole protocol.

```graphql
{
  AzurswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```
