---
icon: basketball
---

# Tutorials

## Inspection Methods Based on User Input

To utilize Herbicide, users can select between two input methods.

### PoolKey

<figure><img src="../.gitbook/assets/master_page_m – PF - 4 (1).png" alt="" width="563"><figcaption></figcaption></figure>

* The Hook Contract must be deployed on the Unichain.
* The specified Hook should be initialized (or be eligible for initialization) with the Pool Manager at [`0x38EB8B22Df3Ae7fb21e92881151B365Df14ba967`](https://unichain-sepolia.blockscout.com/address/0x38EB8B22Df3Ae7fb21e92881151B365Df14ba967) using the provided PoolKey.
* The PoolKey includes the two token addresses to be exchanged (currency0, currency1), LP fees, tick spacing, and the Hook Contract address.
* To run an Initialize Test with a specific deployer address, provide the address as an additional parameter. If omitted, the test will default to the standard address for execution.

**Detection Available**

1. **Malicious Hook Detection**: Issues a warning if the Hook attempts to misappropriate user funds or withdraws more tokens than the user intended.
2. **Price Abnormality Detection**: Alerts users if there is a significant discrepancy between the simulated price calculated by Herbicide and the actual swap price.
3. **Hook Delta Simulation**: Simulates the amounts transferred during Swap/ModifyLiquidity operations, allowing users to understand the specific fund flow characteristics of the Hook.
4. **Static Analysis with Slither**: Provides security inspections and detailed contract information using [Slither](https://github.com/crytic/slither) on verified Hook Contracts from BlockScout, facilitating efficient auditing of the Hook Contract.

### Hook Contract written in Solidity

<figure><img src="../.gitbook/assets/master_page_m – PF - 5 (1).png" alt="" width="563"><figcaption></figcaption></figure>

When a Hook Contract is provided, Herbicide uses its Semgrep script to perform static analysis, detecting potential threats and processing Hook Contract information for review.

#### Detection Available

* **onlyPoolManager:** Confirms that onlyPoolManager is implemented to ensure access control for hook functions.
* **Double Initialize Storage Check:** Verifies if the Storage accessed by `beforeInitialize/afterInitialize` functions is managed by PoolId during Hook initialization.
* **tx.origin Warning:** Issues a warning if access control relies on `tx.origin`, which can introduce security vulnerabilities.

{% hint style="info" %}
All tests are conducted without impacting the actual chain.
{% endhint %}





### Types of integrations

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th></tr></thead><tbody><tr><td><strong>Analytics</strong></td><td>Track analytics from your docs</td><td><a href="https://www.gitbook.com/integrations#analytics">https://www.gitbook.com/integrations#analytics</a></td><td></td><td></td></tr><tr><td><strong>Support</strong></td><td>Add support widgets to your docs</td><td><a href="https://www.gitbook.com/integrations#support">https://www.gitbook.com/integrations#support</a></td><td></td><td></td></tr><tr><td><strong>Interactive</strong></td><td>Add extra functionality to your docs</td><td><a href="https://www.gitbook.com/integrations#interactive">https://www.gitbook.com/integrations#interactive</a></td><td></td><td></td></tr><tr><td><strong>Visitor Authentication</strong></td><td>Protect your docs and require sign-in</td><td><a href="https://www.gitbook.com/integrations#visitor-authentication">https://www.gitbook.com/integrations#visitor-authentication</a></td><td></td><td></td></tr></tbody></table>
