# Vulnerable Hook Detection

## Vulnerable Hook Detection

### StopLoss

이 StopLoss 컨트랙트는 Uniswap V4의 **사용자 정의 훅(User Hook)** 기능을 활용하여 **스톱 로스(stop loss)** 기능을 구현한 것입니다. 이 훅은 특정 풀의 가격 변화에 따라 사용자가 설정한 스톱 로스 조건을 만족할 때 자동으로 토큰을 매도하여 손실을 방지합니다. 해당 훅의 기능을 요약하면 다음과 같습니다.

* 사용자는 `placeStopLoss()`함수를 실행하여 스탑 로스 주문을 생성합니다.
* 스왑 이후 `afterSwap`함수에서 이전 틱과 현재 틱으로 주문을 실행합니다.

```json
{
    "currency0": "0x0197481B0F5237eF312a78528e79667D8b33Dcff",
    "currency1": "0xA56569Bd93dc4b9afCc871e251017dB0543920d4",
    "fee": 3000,
    "hooks": "0xA3da6f46f93C7B3090A48D7bFeC0345156ED5040",
    "tickSpacing": 60,
    "deployer":"0x4e59b44847b379578588920cA78FbF26c0B4956C"
}
```

[Code Details](https://unichain-sepolia.blockscout.com/address/0xA3da6f46f93C7B3090A48D7bFeC0345156ED5040?tab=contract)

해당 훅의 `afterSwap` 함수를 살펴봅시다.

```javascript

    function afterSwap(
        address,
        PoolKey calldata key,
        IPoolManager.SwapParams calldata params,
        BalanceDelta,
        bytes calldata
    ) external override returns (bytes4, int128) {
        int24 prevTick = tickLowerLasts[key.toId()];
        (, int24 tick,,) = poolManager.getSlot0(key.toId());
        int24 currentTick = getTickLower(tick, key.tickSpacing);
        tick = prevTick;

        int256 swapAmounts;

        // fill stop losses in the opposite direction of the swap
        // avoids abuse/attack vectors
        bool stopLossZeroForOne = !params.zeroForOne;

        // TODO: test for off by one because of inequality
        if (prevTick < currentTick) {
            for (; tick < currentTick;) {
                swapAmounts = stopLossPositions[key.toId()][tick][stopLossZeroForOne];
                if (swapAmounts > 0) {
                    fillStopLoss(key, tick, stopLossZeroForOne, swapAmounts);
                }
                unchecked {
                    tick += key.tickSpacing;
                }
            }
        } else {
            for (; currentTick < tick;) {
                swapAmounts = stopLossPositions[key.toId()][tick][stopLossZeroForOne];
                if (swapAmounts > 0) {
                    fillStopLoss(key, tick, stopLossZeroForOne, swapAmounts);
                }
                unchecked {
                    tick -= key.tickSpacing;
                }
            }
        }
        return (StopLoss.afterSwap.selector, 0);
    }

```

해당 함수는 `modifier` 뿐만 아니라, 별도의 ACL 장치가 존재하지 않습니다. 또한, 해당 함수를 통해 `fillStopLoss`함수를 별도로 호출할 수 있으며, 스토리지 값을 변화시킬 수 있습니다. 이는 해당 훅의 예기치 않은 동작을 야기할 수 있으며, 적절한 조치가 필요합니다. Herbicide는 이러한 점을 감지하여 사용자에게 위험성을 알려줄 수 있습니다.

### ArrakisHook

해당 ArrakisHook은 `initialize` 직전에 `beforeInitialize`에서 poolkey에 대한 정보를 저장하고, 이를 통해 ERC1155로 유동성을 관리할 수 있게 구현한 훅입니다.

```json
{
    "currency0": "0x0197481B0F5237eF312a78528e79667D8b33Dcff",
    "currency1": "0xA56569Bd93dc4b9afCc871e251017dB0543920d4",
    "fee": 3000,
    "hooks": "0x7Ba42C294124A8037707399823D56b8a589b6080",
    "tickSpacing": 60,
    "deployer": "0x4e59b44847b379578588920cA78FbF26c0B4956C"
}
```

[Code Detail](https://unichain-sepolia.blockscout.com/address/0x7Ba42C294124A8037707399823D56b8a589b6080?tab=contract)

해당 훅의 `beforeInitialize`를 살펴봅시다.

```javascript
    function beforeInitialize(
        address,
        PoolKey calldata poolKey_,
        uint160 sqrtPriceX96_,
        bytes calldata
    ) external override returns (bytes4) {
        poolKey = poolKey_;
        lastSqrtPriceX96 = sqrtPriceX96_;
        lastBlockNumber = block.number;
        return this.beforeInitialize.selector;
    }
```

해당 컨트랙트는 poolkey에 대한 정보를 `beforeInitialize`에서 초기화 할 수 있도록 구현한 훅입니다. 하지만 해당 훅은, `beforeInitialize`에 대한 어떠한 접근제어도 구현되어있지 않으며, `initialize` 횟수에 대한 별도의 조치를 취하고 있지 않습니다. `beforeInitialize`에서 poolkey를 초기화하므로, 해당 훅에 새로운 initialize가 수행되면, 기존의 hook 자산은 모두 lock 상태에 빠지게 될 것입니다. 이러한 케이스들의 스토리지 값을 감지하여, 사용자가 훅을 안전하게 사용될 수 있도록 합니다.
