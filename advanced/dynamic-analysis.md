# Dynamic Analysis

{% hint style="info" %}
해당 페이지는 동적 분석에 관련한 내용들을 기술합니다.
{% endhint %}

{% hint style="info" %}
동적분석은 [Foundry](https://book.getfoundry.sh/)를 기반으로 동작하며, 7개의 범주에서 199개의 테스트가 동작합니다.
{% endhint %}

### Minimum Test

해당 PoolKey 해당하는 유동성 풀이 정상적으로 동작하는지 확인합니다.\
[ERC-6909](https://eips.ethereum.org/EIPS/eip-6909)에 대한 modifiyLiquidity, swap을 테스트합니다.\
[ERC-20](https://eips.ethereum.org/EIPS/eip-20)에 대한 modifiyLiquidity, swap, donate를 테스트합니다.&#x20;

### Time Based Minimum Test

위 기초 테스트를 시간별로 진행합니다. 각 시간의 주기는 아래와 같습니다.\
\-> `1일`, `1주일`, `1달`, `1년`, `3년`, `5년`, `7년`, `10년`

일정 시간이 지났을 때 정상적으로 유동성 풀이 동작하는지 확인하여, Time Lock이 구현되어 있는 Hook에 대해 경고합니다.

### Only PoolManger Test

각 Hook Function들은 PoolManager에서 unlockCallback을 통해 Hook Contract를 호출하는 방식으로 실행됩니다. Hook Fuction들이 다른 User나 Contract에 의해 호출된다면, 의도치 않은 동작이 발생할 수 있어 onlyPoolManager modifier 또는 require 문을 사용하여 함수 호출자를 제한하여야 합니다.

Herbicide는 Hook Function이 외부에서 호출 가능하다면 경고합니다.

### Double Initializable Test

동일한 PoolKey로는 PoolManager에 Pool을 Initialize 할 수 없지만, PoolID로 storage를 관리하지 않는다면 다른 Pool key로 동일한 Hook을 Initialize 할 때 side effect가 발생할 수 있습니다. Herbicide는 당신이 입력한 Pool key의 틱 간격을 변화시켜, Initialize가 되는지 확인하고, 동일한 storage가 사용될 경우 경고합니다.&#x20;

Storage를 PoolID로 관리하지 않는 Hook Contract라면 이를 확인하고 PoolID를 기반으로 storage를 관리하거나, 추가적으로 Initialize 되지 않도록 처리해야 합니다.

### Proxy Hook Test

Hook Contract가 만약 Proxy Pattern으로 동작한다면, Hook의 Logic이 변화할 수 있으므로 경고합니다.

### Hook Gas Comparison







### price compare





