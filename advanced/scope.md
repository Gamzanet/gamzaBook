---
description: What does Herbicide detect?
---

# Scope

## Analyzable Hook Condition

Uniswap V4 [Pool Manager](https://github.com/Uniswap/v4-core/blob/9293e5ab1deed87e03c176d8af94b1af19eb3900/src/PoolManager.sol)와 상호작용하는 Uniswap V4 Hook Contract를 대상으로 분석을 지원합니다. Pool Manager에 Initialize 한 값을 정확하게 입력해야 합니다.

각 Hook은 [v4-core:9293e5a](https://github.com/Uniswap/v4-core/tree/9293e5ab1deed87e03c176d8af94b1af19eb3900) 와 [v4-periphery:1dc3a34](https://github.com/Uniswap/v4-periphery/tree/1dc3a344efd901664427d59e41a58364ef0f16ec) 와 상호작용하고 [`IHook`](https://github.com/Uniswap/v4-core/blob/9293e5ab1deed87e03c176d8af94b1af19eb3900/src/interfaces/IHooks.sol), [`BaseHook`](https://github.com/Uniswap/v4-periphery/blob/1dc3a344efd901664427d59e41a58364ef0f16ec/src/base/hooks/BaseHook.sol)의 Interface에 맞춰 구현되어야 합니다.



## Detectable Security Threat

#### Double Initializable

동일한 Hook을 PoolManager에 배포 가능할 경우, `beforeInitialize` / `afterInitialize` 의 동작으로 Hook의 Storage가 변화하는 것을 탐지합니다.&#x20;



#### Time Lockable

특정 Hook이 특정 시간 경과 후에 작동하지 않는 경우를 탐지합니다.



#### External Callable Hook Functions

`beforeInitialize` / `afterInitialize` / `beforeSwap` / `afterSwap` / ... etc. Hook 함수에 대해서, PoolManager 외의 주체가 각 함수 실행이 가능한지 탐지합니다.



#### Gas Griefing



#### Price Abnormality











## Contract Inforamtion Analysis



