# Static Analysis

## [Slither Solidity](https://github.com/crytic/slither)

### Threat Detection

Slither에서 제공하는 Detector를 활용하여, Hook Contract 내부의 위협 Detection을 수행할 수 있습니다.\
Herbicide에서는 아래의 Detector를 자동으로 실행하여, 위협을 찾고 경고합니다.

*   #### [`encode-packed-collision`](https://github.com/crytic/slither/wiki/Detector-Documentation#abi-encodepacked-collision)

    Detect collision due to dynamic type usages in `abi.encodePacked`
*   #### [`shadowing-state`](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing)

    Detection of state variables shadowed.
*   #### [`uninitialized-state`](https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-state-variables)

    Uninitialized state variables.
*   #### [`delegatecall-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#controlled-delegatecall)

    `Delegatecall` or `callcode` to an address controlled by the user.
*   #### [`delegatecall-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#payable-functions-using-delegatecall-inside-a-loop)

    Detect the use of `delegatecall` inside a loop in a payable function.
*   #### [`msg-value-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#msgvalue-inside-a-loop)

    Detect the use of `msg.value` inside a loop.
*   #### [`reentrancy-eth`](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities)

    Detection of the [reentrancy bug](https://github.com/trailofbits/not-so-smart-contracts/tree/master/reentrancy). Do not report reentrancies that don't involve Ether (see `reentrancy-no-eth`)
*   #### [`unchecked-transfer`](https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-transfer)

    The return value of an external transfer/transferFrom call is not checked
*   #### [`shadowing-abstract`](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing-from-abstract-contracts)

    Detection of state variables shadowed from abstract contracts.
*   #### [`divide-before-multiply`](https://github.com/crytic/slither/wiki/Detector-Documentation#divide-before-multiply)

    Solidity's integer division truncates. Thus, performing division before multiplication can lead to precision loss.



### Information Printer

Slither에서 제공하는 Printer를 활용하여, Contract의 Access control에 중요한 정보들을 보여줍니다.\
Herbicide에서는 아래의 Printer를 자동으로 실행하여, 정보를 추출하고 보여줍니다.

* [**`require statements`**](https://github.com/crytic/slither/wiki/Printer-documentation#require)\
  Prints require statements in the function.
* [**`modifiers`**](https://github.com/crytic/slither/wiki/Printer-documentation#modifiers)\
  Prints modfiers applied to the function.
* [**`state variables and authentication`**](https://github.com/crytic/slither/wiki/Printer-documentation#variables-written-and-authorization)\
  Prints require statements with msg.sender, in the function which writes state variables.



## Semgrep Solidity + Python

Simple Contract Analyzer에서, 사용자가 Solidity Contract 코드를 입력하면 Herbicide에서 미리 정의한 Semgrep 규칙에 따라, Contract 주요 정보를 가공하여 제공합니다. 이를 통해 사용자는 Contract에 선언된 Function, Storage Variable에 대한 정보를 편리하게 검토할 수 있습니다.

### Threat Detection

* `info-layer2-assignee`\
  Checks storage re-used while double-initializing the hook.
* `low-call`\
  Checks if the hook is low-calling to other addresses.
* `getSlot0-check`\
  Checks if the hook is calling getSlot0 function, as it is dangerous if the hook operates as an oracle, returning the getSlot0 value as the price of the pool.
* `missing-token-transfer-while-burnt`\
  Checks if the hook is not transfering the underlying token while the token is burnt.
* `missing-onlyPoolManager-modifier`\
  Checks if onlyPoolManager modifier is not applied to the hook functions.
* `misconfigured-hook`\
  Checks if the hook functions are not yet implemented, while the function flag of `getHookPermissions` returns `true`.

### Contract Information

* `info-variable`\
  Prints state variables and the functions using them.&#x20;
* `info-inline-access-control`\
  Checks require\&assert\&revert conditions.
* `info-inheritance`\
  Prints the contract's inheritance information.
* `info-library`\
  Prints the usage of libraries of the contract.











