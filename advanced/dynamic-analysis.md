# Dynamic Analysis

{% hint style="info" %}
This page describes the contents related to dynamic analysis
{% endhint %}

{% hint style="info" %}
Dynacmic analysis operates based on Foundry, and 199 tests are conducted in 7 categories.
{% endhint %}

### Minimum Test

1. Verifies whether the liquidity pool corresponding to the PoolKey is functioning correctly.
2. Tests `modifyLiquidity` and swap for [ERC-6909.](https://eips.ethereum.org/EIPS/eip-6909)
3. Tests `modifyLiquidity`, swap, and donate for [ERC-20.](https://eips.ethereum.org/EIPS/eip-20)

### Time Based Minimum Test

1. The above basic tests are conducted periodically. The intervals for each period are as follows:&#x20;
   1. 1 hour, 3 hours, 6 hours, 12 hours, 1 day, 1 week, 1 month, 1 year, 3 years, 5 years, 7 years, 10 years After a certain period of time, it is confirmed whether the liquidity pool operates normally, and a warning is issued for Hooks with implemented Time Locks.&#x20;

### Only PoolManger Test

Each Hook Function is executed by calling the Hook Contract through the `unlockCallback` in the `PoolManager`. If Hook Functions are called by other Users or Contracts, unintended behavior may occur, so the function caller should be restricted using the `onlyPoolManager` modifier or require statement.&#x20;

Herbicide warns if Hook Functions can be called externally.

### ReInitializable Test

Although the same `PoolKey` cannot be used to initialize a Pool in the `PoolManager`, if storage is not managed by `PoolID`, side effects may occur when initializing the same Hook with a different `PoolKey`.&#x20;

Herbicide changes the tick interval of the Pool key you entered to check if it can be initialized, and warns if the same storage is used.&#x20;

If the Hook Contract does not manage storage by `PoolID`, it should be checked and managed based on `PoolID`, or additional measures should be taken to prevent reinitialization.

### Proxy Hook Test

If the Hook Contract operates using the Proxy Pattern, it warns that the logic of the Hook may change.

### Hook Gas Comparison

It compares the gas usage of `modifyLiquidity` and swap without using the Hook, and the gas usage of `modifyLiquidity` and swap when using the Hook. This allows the detection of malicious Gas Griefing by the Hook, and users can predict the gas usage when using the Hook.

### Swap Price Comparison

When performing a Swap for a Pool using the Hook, the use of the Hook may cause fluctuations in the token price. Additionally, the Swap may be executed at a price different from the predicted one.&#x20;

Herbicide can be used to predict such token prices in advance.

* If the predicted price by Herbicide and the Simulated Actual Price differ by more than 5%, a warning is issued.
* It provides market token price information calculated through Pyth Oracle for convenient comparison.











