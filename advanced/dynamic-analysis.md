# Dynamic Analysis

해당 페이지는 동적 분석에 관련한 내용들을 기술합니다.

동적분석은 [Foundry](https://book.getfoundry.sh/)기반으로 동작합니다.

7개의 범주에서 199개의 테스트가 동작합니다.



### 기초 테스트&#x20;

해당 poolkey에 해당하는 유동성 풀이 정상적으로 동작하는지 확인합니다.

[ERC-6909](https://eips.ethereum.org/EIPS/eip-6909)에 대한 유동성 추가, 제거, 교환을 테스트합니다.

[ERC-20](https://eips.ethereum.org/EIPS/eip-20)에 대한 유동성 추가, 제거, 교환을 테스트합니다.&#x20;

각 ERC-6909, ERC-20에 해당하는 유동성 기부에 대해서 테스트합니다.&#x20;

### 시간 기반 기초 테스트

위 기초 테스트를 시간별로 진행합니다. 각 시간의 주기는 아래와 같습니다.

1일,1주일,1달,1년,3년,5년,7년,10년

정상적으로 시간이 지났을 때 정상적으로 유동성 풀이 동작하는지 확인합니다.



### Pool Manager 테스트

각 Hook Function들은 Pool Manager에서 Hook Contract를 호출하는 방식으로 실행됩니다. 하지만 각 Hook Function들이 Pool Manager만 호출하는 것이 아니라 다른 사람이나 Contract가 호출하면 문제가 발생할 수 있습니다.&#x20;

### double init

동일한 Pool key로 Pool Manager에 Initialize 할 수 없지만 Pool ID로 Storage를 관리하지 않는다면 다른 Pool key로 Initialize 할 때 side effect가 발생할 수 있습니다. 입력한 Pool key의 틱 간격을 1 증가시켜 Initialize가 되는지 확인합니다. Storage를 Pool ID로 관리하지 않는 Hook Contract라면 이를 확인하고 Pool ID를 기반으로 Storage를 관리하거나, 추가적으로 Initialize되지 않도록 처리해야 합니다.

### proxy

Hook Contract가 만약 Proxy Patturn으로 동작한다면, \~\~

### Hook compare







### price compare





