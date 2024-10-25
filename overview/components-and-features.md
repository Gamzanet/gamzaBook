# Components & Features

해당 페이지에서는 Herbicide의 각 구성요소와 테스트에 대한 간단한 설명을 진행합니다.



Herbicide는 Uniswap V4의 PoolKey를 입력으로 주어야 동작합니다.

분석을 요구하는 Hook Contract를 Uni Chain Sepolia Network(Chain ID : 1301)에 배포되어야 하고, Uni Chain의 Uniswap V4 Pool Manager Contract에 Initialize 할 것을 권장합니다.

정적 분석은 [UniChain Blockscout](https://unichain-sepolia.blockscout.com/)Contract가 verify되어 소스코드가 업로드되어야 합니다.



정적분석의 경우 [Semgrep](https://semgrep.dev)과 [Slither](https://github.com/crytic/slither)를 기반으로 동작합니다.







