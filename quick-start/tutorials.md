---
icon: basketball
---

# Tutorials

## Input에 따라 다른 검사 방식

Herbicide를 이용하기 위해, 두가지 Input 방식을 선택할 수 있습니다.



### PoolKey

Unichain에 Hook Contract가 배포되어 있어야 합니다.\
해당 Hook은 입력받은 PoolKey를 이용해 [Pool Manager](https://unichain-sepolia.blockscout.com/address/0x38EB8B22Df3Ae7fb21e92881151B365Df14ba967)(0x38EB8B22Df3Ae7fb21e92881151B365Df14ba967)에 Initialize 되어있거나, Initialize 가능해야 합니다.

PoolKey에는 교환할 2개의 토큰 주소( currnecy 0, currency 1), LP 수수료, 틱 간격, Hook Contract 주소가 포함됩니다.

특정 주소로 Initialize Test를 수행하려면, Deployer 주소를 추가적으로 전달하면 됩니다. 이를 전달하지 않을 경우, Default Address로 대신하여 검사가 수행됩니다.

#### Detection Available

1. Malicious Hook Detection : 사용자의 자금을 빼앗거나, 사용자가 낼 의향이 있는 토큰의 양을 초과하여 가져갈 경우 경고합니다.
2. Price Abnormality Detection : Herbicide가 Simulation한 Price와 실제 이루어질 Swap에 대한 Price의 차이가 클 경우 경고합니다.
3. Hook Delta Simulation : Swap/ModifyLiquidity 시에 이동하는 자금의 양을 Simulation하여 나타내, 사용자가 직접 해당 Hook의 자금 흐름의 특성을 파악할 수 있습니다.
4. Static Analysis w. Slither : BlockScout에 verify된 Hook Contract에 대해 [Slither](https://github.com/crytic/slither)를 이용해 보안 검사/Contract Information 등, Hook Contract에 대한 가공된 정보를 보여주어 Audit을 편리하게 수행할 수 있습니다.



### Hook Contract written in Solidity

Hook Contract를 입력하면 Herbicide Semgrep Script를 통해 Static Analysis을 수행하여 위협 탐지, Hook Contract Information 정보를 가공하여 보여줍니다.

#### Detection Available

1. onlyPoolManager : Checks if `onlyPoolManager` is implemented for hook function access control.
2. Double Initialize Storage Check : Hook Initialize 시, `beforeInitialize`/`afterInitialize` 함수가 접근하는 Storage가 PoolId로 관리되고 있는지 확인합니다.
3. tx.origin : Access Control을 `tx.origin`으로 수행할 경우 경고합니다.



{% hint style="info" %}
모든 테스트는 실제 체인에 영향을 주지 않습니다.
{% endhint %}





### Types of integrations

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th></tr></thead><tbody><tr><td><strong>Analytics</strong></td><td>Track analytics from your docs</td><td><a href="https://www.gitbook.com/integrations#analytics">https://www.gitbook.com/integrations#analytics</a></td><td></td><td></td></tr><tr><td><strong>Support</strong></td><td>Add support widgets to your docs</td><td><a href="https://www.gitbook.com/integrations#support">https://www.gitbook.com/integrations#support</a></td><td></td><td></td></tr><tr><td><strong>Interactive</strong></td><td>Add extra functionality to your docs</td><td><a href="https://www.gitbook.com/integrations#interactive">https://www.gitbook.com/integrations#interactive</a></td><td></td><td></td></tr><tr><td><strong>Visitor Authentication</strong></td><td>Protect your docs and require sign-in</td><td><a href="https://www.gitbook.com/integrations#visitor-authentication">https://www.gitbook.com/integrations#visitor-authentication</a></td><td></td><td></td></tr></tbody></table>
