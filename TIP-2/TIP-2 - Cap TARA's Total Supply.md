# TIP-2 - Cap TARA's Total Supply

Author(s): Steven Pu [@reedvoid](https://github.com/reedvoid)

Created: 2023-09-12

Discussion: [https://discord.com/channels/419749122556297216/1143250004585218128](https://discord.com/channels/419749122556297216/1143250004585218128)
<br><br><br>

## Table of Contents

- [Summary](#summary)
- [Motivation](#motivation)
- [Specifications](#specifications)
- [Rationale](#rationale)
- [Backwards Compatibility](#backwards-compatibility)
- [Security Considerations](#security-considerations)
- [Copyright](#copyright)
<br><br><br>

## Summary

Cap TARA's totaly supply to 12 billion, and adopt the staking yield curve as defined by: $\ Y_c=\left(S_m-Sc\right) \left(D_c \over S_c\right) \left(Δt \over T_r\right)$
<br><br><br>

## Motivation

Currently the Taraxa mainnet has a fixed staking yield of ~18% APY, the fixed staking yield was introduced during the 2021 bull cycle when the crypto community at large demanded a high rate of return for any staking or “staking-like” activities in order to attract participation. It was meant to attract staking participation in the short-term and was never meant to be permanent. A constant staking yield leads to infinite supply and is detrimental to an ecosystem's sustainability. 

If you haven’t already, please read the article [on Staking Yields](https://www.taraxa.io/posts/blockchain101/on-staking-yields-2bb2d2c9db449d20d17d1a82fe4193bb) to get some background information on staking, yield curves, and references to how a few well-known PoS Layer-1 projects are handling this piece of their economic design.
<br><br><br>

## Specifications

### Proposed Design Goals

To help make the Taraxa ecosystem more sustainable, this proposal targets the following set of design goals. 

1. Capped maximum supply 
2. Yield curve decays and asymptotically approaches zero 
3. Total inflation decays and asymptotically approaches zero
<br><br>

### Proposed Yield Curve Design

According to the stated design goals, we propose the following yield curve design. 
<br><br>

#### Definitions

- $\ S_c →$ current total supply
- $\ S_m →$ maximum supply
- $\ D_c →$ current total delegation (staking)
- $\ Δt →$ reward time window
- $\ T_r →$ number of time windows for max yields to be given out
- $\ Y_c →$ current yield for reward time window
<br><br>

#### Proposed Yield Equation

$\ Y_c=\left(S_m-Sc\right) \left(D_c \over S_c\right) \left(Δt \over T_r\right)$
<br><br>

#### Proposed Variable Values 

Among all the variables, $\ S_m$ and $\ T_r$ are assumptions that need to be defined. The remaining variables are naturally occurring. We propose the following, 

- $\ S_m$ = 12 billion TARA
- $\ T_r$ = 1 calendar year (365 days) worth of Δt, with Δt=3.7s currently
<br><br><br>

## Rationale

### Gut-Checks

We can gut-check this design by plugging in a few min/max assumptions into the equation. 

- $\ S_m=S_c$ means the current supply has reached the maximum supply, making all future staking yields zero
- $\ D_c=0$ means there is no delegation / staking, which again means all staking  yields are zero
- $\ D_c=S_c$ means, if ever the total current supply were to be fully delegated (impossible), then the maximum possible yield at that given moment is being given out in the time interval $\ Δt$, and if $\ D_c=S_c$ is sustained for a period of Tr then all remaining possible staking yields will be given out in the period $\ T_r$
<br><br>

### Sample Simulations 

We can plot a few simulated graphs to gain further intuition for this design. 

![Staking Yield Rate and Overall Inflation Rate with Fixed Staking Levels](https://github.com/Taraxa-project/TIP/blob/main/TIP-2/tip-2-figure_1.png)

In [1], keeping staking levels constant, we see that staking yields and overall ecosystem inflation rate decays over time and both asymptotically approach zero. 
<br><br>

![Staking Yield Rate and Overall Inflation Rate with Increasing Staking Levels](https://github.com/Taraxa-project/TIP/blob/main/TIP-2/tip-2-figure_2.png)

In [2], if we assume increasing staking levels - which is what has been happening in the Taraxa ecosystem, then the staking yields and inflation rates decay much more rapidly. This is because as staking levels rise, given the same staking yields, more of the remaining supply is given out. 
<br><br>

![Cumulative Staking Yields for Fixed vs. Increasing Staking Levels](https://github.com/Taraxa-project/TIP/blob/main/TIP-2/tip-2-figure_3.png)

In [3], we illustrate that, if staking rate is increasing, then staking yields are given out much faster and the ecosystem reaches maximum supply much faster than if staling rate stays fixed. 
<br><br>

### Supply Cap Rationale 

The selection of the total supply cap to be 12 billion TARA was done to ensure there’s a relatively smooth transition between the current yield to this future yield. In implementing any large change, it’s important to make sure that the transition is gradual, so that all ecosystem participants have time to adjust. A selection of 12 billion TARA cap ensures that given the current staking level, the annualized yield would not be too far off from what it is right now. 

Given current staking and supply numbers, 

- $\ S_c$ = 10.246 billion
- $\ S_m$ = 12 billion
- $\ D_c$ = 1.968 billion
- $\ Δt \over T_r$ = 1 for simplicity, assuming we give out rewards once a year

We see that the annualized staking yield rate $\ Y_c \over D_c$ = 17.1%, which is very close to what stakers and validators expect right now. 
<br><br>

### Time Window Factor Rationale

The rationale for selecting $\ T_r$ to be 1 calendar year (365 days) worth of $\ Δt$ is simply because people are used to thinking in terms of calendar years. The smaller $\ T_r$ is, the faster yields are given out, and vice versa. It’s useful to think that, if $\ D_c=S_c$ for a whole year, that is, the total current supply was to be fully delegated (impossible but let’s assume it is) for a whole year, then all remaining coins from the current supply and the maximum will be given out in a single year. 
<br><br><br>


## Backwards Compatibility

This TIP will require a hardfork. 
<br><br><br>


## Security Considerations

Security implication is minimal. The only potential problem is that, as staking yields decline over time, if transaction fees do not increase accordingly to make up the difference, it may create a disincentive in the ecosystem to stake to and operate validators, leading to a potential loss of decentralization. 
<br><br><br>


## Copyright

All Taraxa Improvement Proposals follow the same [license](https://github.com/Taraxa-project/TIP/blob/main/LICENSE). 

