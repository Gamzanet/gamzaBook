---
description: What does Herbicide detect?
---

# Scope

## **Analyzable Hook Condition**

The analysis is supported for Uniswap V4 Hook Contracts interacting with the Uniswap V4 [Pool Manager. ](https://github.com/Uniswap/v4-core/blob/9293e5ab1deed87e03c176d8af94b1af19eb3900/src/PoolManager.sol)The exact initialized values in the Pool Manager must be correctly entered. Each hook should be implemented per the `IHook` and `BaseHook` interfaces, interacting with [`v4-core:9293e5a`](https://github.com/Uniswap/v4-core/tree/9293e5ab1deed87e03c176d8af94b1af19eb3900) and [`v4-periphery:1dc3a34`.](https://github.com/Uniswap/v4-periphery/tree/1dc3a344efd901664427d59e41a58364ef0f16ec)

## Detectable Security Threat

### ReInitializable

동일한 Hook을 PoolManager에 배포 가능할 경우, `beforeInitialize` / `afterInitialize` 의 동작으로 Hook의 Storage가 변화하는 것을 탐지합니다.&#x20;

Hook Initialize 시, `beforeInitialize`/`afterInitialize` 함수가 접근하는 Storage가 PoolId로 관리되고 있는지 확인합니다.

### Time Lock

### 특정 Hook이 특정 시간 경과 후에 작동하지 않는 경우를 탐지합니다.

### External Callable Hook Functions

`beforeInitialize` / `afterInitialize` / `beforeSwap` / `afterSwap` / ... etc. Hook 함수에 대해서, PoolManager 외의 주체가 각 함수 실행이 가능한지 탐지합니다.

### Malicious Hook Detection

gas griefing의 위험을 gas 사용량을 통해 확인할 수 있고, 사용자의 자금을 빼앗거나, 사용자가 낼 의향이 있는 토큰의 양을 초과하여 가져갈 경우 경고합니다.

#### Price Abnormality

Herbicide가 Simulation한 Price와 실제 이루어질 Swap에 대한 Price의 차이가 클 경우 경고합니다.

#### Proxy Detection

Hook Contract가 Proxy로 구현되어있는 경우, 이를 탐지하여 경고합니다.





## Contract Inforamtion Analysis

#### With PoolKey

1. Hook Delta Simulation : Swap/ModifyLiquidity 시에 이동하는 자금의 양을 Simulation하여 나타내, 사용자가 직접 해당 Hook의 자금 흐름의 특성을 파악할 수 있습니다.
2. Static Analysis w. Slither : BlockScout에 verify된 Hook Contract에 대해 [Slither](https://github.com/crytic/slither)를 이용해 보안 검사/Contract Information 등, Hook Contract에 대한 가공된 정보를 보여주어 Audit을 편리하게 수행할 수 있습니다.

#### With Hook Contract

1. Static Analysis w. Semgrep : Herbicide Semgrep Script을 기반으로, 아래와 같은 Contract의 정보를 추출하여 보여줍니다.

* Library Information
* Modifier Information
* Inheritance Information
* Variable Information





