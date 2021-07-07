# RAI Uniswap V3 Mint + LP Incentives Program

## Overview

The RAI Mint + LP strategy requires that participants mint RAI **and** provide RAI/ETH or RAI/DAI liquidity on Uniswap v3 at the same time in order to accrue retroactive rewards.  
  
The RAI/ETH Uniswap v3 pool for this program is [here](https://info.uniswap.org/#/pools/0x14de8287adc90f0f95bf567c0707670de52e3813) and the RAI/DAI one is [here](https://info.uniswap.org/#/pools/0xcb0c5d9d92f4f2f80cce7aa271a1e148c226e19d). 

**The program will demo for 2 weeks starting on 9th of July 2021 and will distribute 400 FLX for RAI/ETH LPs and another 400 FLX for RAI/DAI LPs. After the demo, we will gather results and reassess.**

## How It Works

1. Go to [app.reflexer.finance](https://app.reflexer.finance/) or [DeFi Saver](https://app.defisaver.com/reflexer/manage) and mint some RAI.
2. Go to the [RAI/ETH Uniswap v3 pool](https://info.uniswap.org/#/pools/0x14de8287adc90f0f95bf567c0707670de52e3813) or the [RAI/DAI Uniswap v3 pool](https://info.uniswap.org/#/pools/0xcb0c5d9d92f4f2f80cce7aa271a1e148c226e19d) and add the RAI you minted as liquidity

You do **not** accrue rewards if:

* You provide RAI/ETH or RAI/DAI liquidity without minting RAI \(e.g buy from the pool and LP\)
* You mint RAI without adding RAI/ETH or RAI/DAI liquidity
* The RAI/ETH or RAI/DAI price is outside or shifted of your liquidity band

You accrue **less** rewards if:

* If the RAI/ETH or RAI/DAI price shifts, resulting in the position owning less underlying RAI compared to your debt
* Your debt goes down due to repaying your debt or liquidation 

The exact relevant metric used for rewards is: 

$$
min(\frac{\texttt{Sum of all safe debt}}{\texttt{Sum of all active RAI in LP}}, 1)\times \texttt{Sum of active UniV3 virtual liquidity}
$$

## LP Strategy

The rewards will be distributed considering how much each LP concentrates liquidity around RAI's redemption price. To visualize this, let's take the example of Alice \(red\), Bob \(purple\) and Charlie \(green\) who LP in the RAI/ETH pool.

![Alice accrues the most rewards because she LPed close to the redemption price](../.gitbook/assets/bob.png)

You can see that:

* Alice accrues the most rewards because she concentrated liquidity really close to the current redemption price
* Bob is not accruing any rewards because none of his liquidity includes the tick where the current redemption price is
* Charlie is accruing some rewards but less than Alice because he has a wider liquidity distribution around the redemption price

To maximize rewards, LPs have to concentrate liquidity closer to the redemption price \(**at the risk of higher impermanent loss**\). To get the current RAI redemption price, you can visit our [stats page](https://stats.reflexer.finance/).

## Important Notes

* You **must** use the same address to mint RAI and provide Uniswap v3 RAI/ETH or RAI/DAI liquidity
* The Uniswap v3 RAI/ETH or RAI/DAI LP tokens **must** stay on the same address that you used to mint RAI and provide liquidity
* To see the minimum amount of RAI you must mint on mainnet, check the [parameters page](https://docs.reflexer.finance/current-system-parameters#quick-glance)
* If you open multiple Safes with the same address, your total RAI debt will be the sum of all RAI minted by each of your Safes
* If you have several LP positions with the same address, the total sum of the liquidity will be considered for rewards.
* Only positions from the official Uniswap V3 NFT manager are supported \(used by the official UI at [https://app.uniswap.org/\#/pool](https://app.uniswap.org/#/pool)\). Positions directly minted on the pool contract are **not** supported.
* If your Safe gets liquidated, the amount of minted RAI you have decreases by the amount of RAI that got confiscated
