---

layout: post
title:  "Smart Contracts Notes for noobs"
date:   2022-03-21 13:05:18 +0700
categories: smartcontract
---
# Smart contract weaknesses in short 

1. SWC-136: Private variables are not that private, everyone can see your private variables. Private variables only mean that they are not visible in derived contracts, but they are still there. 
2. SWC-135: `msg.sender.call{value : 100}` will not send anything if it does not have `("")`.
3. SWC-134: Don't use `msg.sender.transfer(amount);` or `send()`, use `call()` with *check-effect-interact* and re-entrance guard.
4. SWC-132:  Never assume your contract's ether balance with exact value, anyone can forcibly send ether to your contract (using `selfdestruct(address)`) and potentially render it useless and lock ethers.
5. SWC-130: Smart contracts may behave differently than it looks if it uses the `Right-To-Left-Override control character (U+202E)`
6. SWC-129: Beware of typos or similar variable names.
7. SWC-128: Always beware of the block gas limit problem when develop contracts. If your contract exceed the block gas limit, it is not deployable. Or if a function use too much gas that exceed the block gas limit, that's a DoS problem.
8. SWC-127: Don't try to use assembly unless you know what you are doing.
9. SWC-126: Always `require(success);` when use low level `call("")`. Griefing attack is when a relay contract does not have enough gas to call the target contract using low level call.
10. SWC-125: Inheritance order of contract matters. If two base contracts define the same function, then the child contract should call which function? the right most base contract will override the left one. `contract A is B, C, D, E, F {}` the `F` contract will override all of its left contract function if there is any same-name function.



## Other confusing things to me

1. There is a fundamental difference between casting an address to a contract type and instantiate an object of the contract type. 
   1. Casting: `ContractName(address);`.
   2. Instantiate: `new ContractName(arguments of the constructor);`
2. When to use `calldata` and `memory`?
   1. An external function must use `calldata` location for its dynamic parameters
   2. `calldata` can only be used in function parameters, not in the logic of the function.
   3. More [here](https://ethereum.stackexchange.com/questions/74442/when-should-i-use-calldata-and-when-should-i-use-memory).
3. Function overriding: 
   1. Base contracts can have `virtual` functions that marked with `virtual` keyword, to explicitly signal that this function can be override. An inheriting contract which want to override a virtual function of its parent must explicitly use the `override` keyword in its function declaration. 
   2. Functions with `private` visibility can not be `virtual`
   3. Functions without implementing must be marked with `virtual` outside of interfaces. In interfaces, all functions are automatically considered `virtual`.

## When writing smart contracts

1. Always split the `withdraw` and `deposit/lock/fund` to two functions, [see this](https://docs.soliditylang.org/en/v0.8.13/common-patterns.html#withdrawal-from-contracts) 
2. Consider using the [Fail-safe mode](https://docs.soliditylang.org/en/v0.8.13/security-considerations.html#include-a-fail-safe-mode): add checks in functions, if something unexpected happened, pause the contract immediately, wait for the owners to unpause it.


## Gas optimizing
1. [Tight Variable Packing](https://fravoll.github.io/solidity-patterns/tight_variable_packing.html). One storage slot is 32 bytes in size, and the state variables of contracts are packed together starting from the 0 position. For example, `uint128`, `uint128`, `uint256` is better than `uint128`, `uint256`, `uint128` because the former takes 2 storage slots and the later takes 3 storage slots.
2. Avoid repeatedly referencing to an array's length in a for loop. For example: `for(uint256 i; i < arr.length; i++) {}` is bad because it repeatedly accesses to the storage. You should do `uint256 length = arr.length;` then use that `length` memory variable instead. It can save up to 90% of gas usage for array length of more than 100 elements. 
3. Do not copy the whole storage array into memory. Just access the storage array instead.
## References

1. [Smart Contract Weakness Classification and Test Cases](https://swcregistry.io/)