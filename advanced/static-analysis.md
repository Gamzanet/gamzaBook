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







