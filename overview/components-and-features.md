# Components & Features

## Before Use

해당 페이지에서는 Herbicide의 각 구성요소와 테스트에 대한 간단한 설명을 진행합니다.

Herbicide는 기본적으로 Uniswap V4의 PoolKey를 입력으로 주어야 동작합니다.

분석을 요구하는 Hook Contract를 Unichain Sepolia Network(Chain ID : 1301)에 배포한 후, Unichain Sepolia의 Uniswap V4 Pool Manager Contract에 Initialize 할 것을 권장합니다.

전체적인 Project에 대한 정적 분석은 [UniChain Blockscout](https://unichain-sepolia.blockscout.com/) Contract가 verify되어 소스코드가 업로드되어야 합니다.



정적분석은 [Semgrep](https://semgrep.dev)과 [Slither](https://github.com/crytic/slither)를 기반으로, 동적분석은 [Foundry](https://book.getfoundry.sh/) 기반으로 동작합니다.Uniswap V4 Hook에서 발생할 수 있는 위협들은 [Uniswap V4 Hook Securit](../learn-internal-researcher/uniswap-v4-hook-security.md)[y](../learn-internal-researcher/uniswap-v4-hook-security.md)에 기재하였습니다.



## Features

### Hook Token Delta Simulation

특정 Hook을 사용할 때, `afterSwap / beforeSwap / beforeAddLiquidity / afterAddLiquidity / beforeRemoveLiquidity / afterRemoveLiquidity` 의 로직이 토큰의 이동에 영향을 줄 수 있는 Delta Amount를 추적합니다.&#x20;

Dynamic Analysis를 통해, swap/modifyLiquidity 시에 실제로 사용자가 낼 토큰의 양과 받을 토큰의 양, 각 실행 주체(Hook Contract, PoolManager, Router)의 자금 이동을 Simulation합니다.&#x20;

Simulation 결과로 나온 amountIn과 amountOut을 통해, 특정 Pool을 이용할 때 실제로 낼 토큰과 받을 토큰 양에 대한 Actual Price를 확인할 수 있습니다. 또한, 시중 가격 (Pyth Oracle 활용)을 함께 나타내 사용자에게 편의성을 제공합니다.

$$actualPrice = amountOut / amountIn$$

$$oraclePrice = (token1/usdc) / (token0/usdc)$$

$$expectedPrice = expectedAmountOut / expectedAmountIn$$



### Hook Contract Scanner

Solidity로 작성된 Hook Contract code에 대해, 간단한 위협 탐지 및 정보 추출 기능을 제공합니다.

Hook Contract Scanner는 개발자가 작성한 Hook Contract에 대한 Libraries, Modifiers, require/assert/revert condition, Access Control Logic을 쉽게 파악할 수 있도록 도와줍니다.&#x20;

* &#x20;Modifiers



* &#x20;Access Control Logic



* &#x20;If-nested Condition



* &#x20;Hook&#x20;









