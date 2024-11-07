# Static Analysis

## Threat Detection

Using the Detectors provided by Slither, it is possible to detect threats within the Hook. Herbicide automatically executes the following Detectors to find and warn about threats.

* #### [`encode-packed-collision`](https://github.com/crytic/slither/wiki/Detector-Documentation#abi-encodepacked-collision)
  * #### Detect collision due to dynamic type usages in `abi.encodePacked`
* #### [`shadowing-state`](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing)
  * #### Detection of state variables shadowed.
* #### [`uninitialized-state`](https://github.com/crytic/slither/wiki/Detector-Documentation#uninitialized-state-variables)
  * #### Uninitialized state variables.
* #### [`delegatecall-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#controlled-delegatecall)
  * #### `Delegatecall`  to an address controlled by the user.
* #### [`delegatecall-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#payable-functions-using-delegatecall-inside-a-loop)
  * #### Detect the use of `delegatecall` inside a loop in a payable function.
* #### [`msg-value-loop`](https://github.com/crytic/slither/wiki/Detector-Documentation#msgvalue-inside-a-loop)
  * #### Detect the use of `msg.value` inside a loop.
* #### [`reentrancy-eth`](https://github.com/crytic/slither/wiki/Detector-Documentation#reentrancy-vulnerabilities)
  * #### Detection of the [reentrancy bug](https://github.com/trailofbits/not-so-smart-contracts/tree/master/reentrancy). Do not report reentrancies that don't involve Ether (see,`reentrancy-no-eth`)
* #### [`unchecked-transfer`](https://github.com/crytic/slither/wiki/Detector-Documentation#unchecked-transfer)
  * #### The return value of an external transfer/transferFrom call is not checked
* #### [`shadowing-abstract`](https://github.com/crytic/slither/wiki/Detector-Documentation#state-variable-shadowing-from-abstract-contracts)
  * #### Detection of state variables shadowed from abstract contracts.
* #### [`divide-before-multiply`](https://github.com/crytic/slither/wiki/Detector-Documentation#divide-before-multiply)
  * #### Solidity's integer division truncates. Thus, performing division before multiplication can lead to precision loss.

## Informational Gathering

Using the Slither-Printer, it displays critical information regarding the access control of the contract.\
In Herbicide, the Printer is automatically executed to extract and display.

* [**`require statements`**](https://github.com/crytic/slither/wiki/Printer-documentation#require)
  * Printer require statements in the function.
* [**`modifiers`**](https://github.com/crytic/slither/wiki/Printer-documentation#modifiers)
  * Printer modify applied to the function.
* [**`state variables and authentication`**](https://github.com/crytic/slither/wiki/Printer-documentation#variables-written-and-authorization)
  * Printer require statements with `msg.sender`, in the function which writes state variables.

#### Contract Information

* `info-variable`
  * Prints state variables and the functions using them.&#x20;
* `info-inline-access-control`
  * Checks require\&assert\&revert conditions.
* `info-inheritance`
  * Prints the contract's inheritance information.
* `info-library`
  * Prints the usage of libraries of the contract.

## Semgrep Solidity + Python

In the Simple Contract Analyzer, users can input contract to receive processed key information according to predefined Semgrep rules by Herbicide. This lets users easily review details about functions and storage variables declared in

### Threat Detection

* `info-layer2-assignee`
  * Checks storage re-used while double-initializing the hook.
* `low-call`
  * Checks if the hook is low-calling to other addresses.
* `getSlot0-check`
  * Checks if the hook is calling getSlot0 function, as it is dangerous if the hook operates as an oracle, returning the getSlot0 value as the price of the pool.
* `missing-token-transfer-while-burnt`
  * Checks if the hook is not transfering the underlying token while the token is burnt.
* `missing-onlyPoolManager-modifier`
  * Checks if onlyPoolManager modifier is not applied to the hook functions.
* `misconfigured-hook`
  * Checks if the hook functions are not yet implemented, while the function flag of `getHookPermissions` returns `true`.
