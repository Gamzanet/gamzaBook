---
description: What does Herbicide detect?
---

# Key Features

## **Analyzable Hook Condition**

The analysis is supported for Uniswap V4 Hook Contracts interacting with the Uniswap V4 [Pool Manager. ](https://github.com/Uniswap/v4-core/blob/9293e5ab1deed87e03c176d8af94b1af19eb3900/src/PoolManager.sol)The exact initialized values in the Pool Manager must be correctly entered. Each hook should be implemented per the `IHook` and `BaseHook` interfaces, interacting with [`v4-core:9293e5a`](https://github.com/Uniswap/v4-core/tree/9293e5ab1deed87e03c176d8af94b1af19eb3900) and [`v4-periphery:1dc3a34`.](https://github.com/Uniswap/v4-periphery/tree/1dc3a344efd901664427d59e41a58364ef0f16ec)

## Detectable Security Threat

### ReInitializable

Detects changes in the Hook's storage due to the actions of `beforeInitialize / afterInitialize` if the same Hook can be deployed to the `PoolManager`. Confirms whether the storage accessed by the `beforeInitialize/afterInitialize` functions during Hook initialization is managed by PoolId.

### Time Lock

Detects cases where a specific Hook does not operate after a certain period has elapsed.

### External Callable Hook Functions

For Hook functions such as `beforeInitialize` / `afterInitialize` / `beforeSwap` / `afterSwap` / `etc.`, detects whether entities other than the PoolManager can execute each function.

### Malicious Hook Detection

Can identify risks of gas griefing through gas usage and warns if it can steal user funds or take more tokens than the user intends to pay.&#x20;

### Price Abnormality

Warns when there is a significant difference between the price simulated by Herbicide and the actual price at which the swap occurs.

### Proxy Detection

Detects and warns if the Hook Contract is implemented as a proxy.&#x20;



## Contract Information Analysis

### With PoolKey

1. Hook Delta Simulation: Simulates the amount of funds moved during `Swap/ModifyLiquidity`, allowing users to directly understand the characteristics of the fund flow in the Hook.
2. Static Analysis with Slither: Provides processed information such as security checks and contract information for Hook Contracts verified on BlockScout using Slither, making audits more convenient.&#x20;

### With Hook Contract

1. Static Analysis with Semgrep: Based on the Herbicide Semgrep Script, it extracts and displays information about the Contract as follows.
   1. Library Information
   2. Modifier Information
   3. Inheritance Information
   4. Variable Information
