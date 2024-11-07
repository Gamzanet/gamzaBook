---
icon: bullseye-arrow
---

# Introduction

## Motivation

This project aims to identify and address vulnerabilities arising from the lack of standardization- in Uniswap v4 hooks, enabling proactive threat mitigation within the web3 ecosystem.

## Summary of Herbicide

<figure><img src="../.gitbook/assets/master_page_m – 3.png" alt="" width="563"><figcaption></figcaption></figure>

The Hook function, a key feature introduced in Uniswap V4, allows developers to apply custom business logic before and after actions like adding or removing liquidity, token swaps, and liquidity donations. In Uniswap V4, liquidity is managed by PoolKeys, which includes the addresses of two tokens to be exchanged, fees, tick spacing, and the address of the implemented Hook Contract.

Using Hook-applied liquidity, our project analyzes Uniswap V4 to define and address potential threats. The solution enables users to input a PoolKey corresponding to their Hook Contract deployed on the Uni Chain, then dynamically and statically analyze it to detect possible threats.

Dynamic testing is conducted across N categories with M tests, while static analysis follows with N categories and M tests, ultimately displaying results for the user. Uniswap continues to enhance the Uni Chain and blockchain ecosystem through initiatives like the Infinite Hackathon and Retro Program. We aim to assist Uniswap V4 users and Hook developers in creating safer Hook Contracts.



## Performance

Our Herbicide platform has identified security issues among various Uniswap v4 hooks detected through our platform. We conducted a direct triage process on each identified issue to verify their validity as vulnerabilities. The following outlines the results of this process.



{% include "../.gitbook/includes/untitled (1).md" %}



