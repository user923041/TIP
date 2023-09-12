# TIP-2 - Cap TARA's Total Supply

Author(s): Steven Pu [@reedvoid](https://github.com/reedvoid)

Created: 2023-09-12

Discussion: [https://discord.com/channels/419749122556297216/1143250004585218128](https://discord.com/channels/419749122556297216/1143250004585218128)


## Table of Contents

- [Summary](#summary)
- [Motivation](#motivation)
- [Specification](#specification)
- [Rationale](#rationale)
- [Backwards Compatibility](#backwards-compatibility)
- [Security Considerations](#security-considerations)
- [Copyright](#copyright)


## Summary

Cap TARA's totaly supply to 12 billion, and adopt the staking yield curve as defined by: $\ Y_c=\left(S_m-Sc\right) \left(D_c \over S_c\right) \left(Δt \over T_r\right)$




If you haven’t already, please read the article [on Staking Yields](https://www.taraxa.io/posts/blockchain101/on-staking-yields-2bb2d2c9db449d20d17d1a82fe4193bb) to get some background information on staking, yield curves, and references to how a few well-known PoS Layer-1 projects are handling this piece of their economic design. 


## Taraxa’s Current Staking Yield Curve 

Currently the Taraxa mainnet has a fixed staking yield of ~18% APY, which is a little less than the originally intended annualized staking yield of 20% due to natural networking conditions and diminishing returns of difficulty reduction based on validator delegation. 

The fixed staking yield had always been introduced during the 2021 bull cycle when the crypto community at large demanded a high rate of return for any staking or “staking-like” activities in order to attract participation. It was meant to attract staking participation, it was never meant to be permanent. 


## Proposed Design Goals

To help make the Taraxa ecosystem more sustainable, this proposal targets the following set of design goals. 

1. Capped maximum supply 
2. Yield curve decays and asymptotically approaches zero 
3. Total inflation decays and asymptotically approaches zero


## Proposed Yield Curve Design

According to the stated design goals, I propose the following yield curve design. 

### Definitions

$\ S_c →$ current total supply

$\ S_m →$ maximum supply

$\ D_c →$ current total delegation (staking)

$\ Δt →$ reward time window

$\ T_r →$ number of time windows for max yields to be given out

$\ Y_c →$ current yield for reward time window

### Proposed Yield Equation 

$\ Y_c=\left(S_m-Sc\right) \left(D_c \over S_c\right) \left(Δt \over T_r\right)$


This design gives you the total staking yield to be given out at any given reward time window. 

First, we can gut-check this design by plugging in a few min/max assumptions into the equation. 

- Sm=Sc means the current supply has reached the maximum supply, making all future staking yields zero
- Dc=0 means there is no delegation / staking, which again means all staking  yields are zero
- Dc=Sc means, if ever the total current supply were to be fully delegated (impossible), then the maximum possible yield at that given moment is being given out in the time interval t, and if Dc=Sc is sustained for a period of Tr then all remaining possible staking yields will be given out in the period Tr

Second, we can plot a few graphs to gain further intuition for this design. 



In [1], keeping staking levels constant, we see that staking yields and overall ecosystem inflation rate decays over time and both asymptotically approach zero. 




In [2], if we assume increasing staking levels - which is what has been happening in the Taraxa ecosystem, then the staking yields and inflation rates decay much more rapidly. This is because as staking levels rise, given the same staking yields, more of the remaining supply is given out. 




In [3], we illustrate that, if staking rate is increasing, then staking yields are given out much faster and the ecosystem reaches maximum supply much faster than if staling rate stays fixed. 


Proposed Design Variables

Among all the variables, Sm and Tr are assumptions that need to be defined. The remaining variables are naturally occurring. We propose the following, 

Sm=12 billion TARA
Tr1 calendar year (365 days) worth of t, with t3.7s currently

Rationale for  Sm:  

The selection of the total supply cap to be 12 billion TARA was done to ensure there’s a relatively smooth transition between the current yield to this future yield. In implementing any large change, it’s important to make sure that the transition is gradual, so that all ecosystem participants have time to adjust. A selection of 12 billion TARA cap ensures that given the current staking level, the annualized yield would not be too far off from what it is right now. 

Given current staking and supply numbers, 

Sc= 10.246 billion
Sm= 12 billion
Dc= 1.968 billion
tTr=1 for simplicity, assuming we give out rewards once a year

We see that the annualized staking yield rate is, 

YcDc=17.1%

So this is very close to what stakers and validators expect right now. 

Rationale for  Tr:  

The rationale for selecting Tr to be 1 calendar year (365 days) worth of t is simply because people are used to thinking in terms of calendar years. The smaller Tr is, the faster yields are given out, and vice versa. It’s useful to think that, if Dc=Sc for a whole year, that is, the total current supply was to be fully delegated (impossible but let’s assume it is) for a whole year, then all remaining coins from the current supply and the maximum will be given out in a single year. 


Consolidated Proposed Yield Curve Design

Sccurrent total supply
Smmaximum supply
Dccurrent total delegation
treward time window
Trnumber of time windows for max yields to be given out 
Yccurrent yield for reward time window

Yc=Sm-ScDcSctTr



with, 

Sm=12 billion TARA
Tr1 calendar year (365 days) worth of t, with t3.7s currently
