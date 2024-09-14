---
timezone: Asia/Shanghai

---

# {你的名字}

1. 自我介绍

* vegetabledogdog

2. 你认为你会完成本次残酷学习吗？

* 会

## Notes

<!-- Content_START -->

### 2024.09.07
aptos使用的共识算法：[AptosBFT](https://pontem.network/posts/aptosbft-all-you-need-to-know-about-the-bft-consensus-in-aptos)

The Aptos blockchain uses a Byzantine Fault Tolerance (BFT) consensus protocol for validator nodes to agree on the ledger of finalized transactions and their execution results. Validator nodes process these transactions and include them in their local copy of the blockchain database. This means that up-to-date validator nodes always maintain a copy of the current [state](https://aptos.dev/en/network/glossary#state) of the blockchain, locally.

### 2024.09.08
安装aptos-cli，搭建开发环境。

### 2024.09.09
store和key关键字的区别

store:allows values of types with this ability to exist inside a struct (resource) in global storage, but not necessarily as a top-level resource in global storage. If a value has store, all values contained inside of that value have store

key:in order for a type to be used with move_to, borrow_global, move_from, etc., the type must have the key ability.If a value has key, all values contained inside of that value have store. This is the only ability with this sort of asymmetry.

### 2024.09.10
convert object type:

    object::convert<MyAwesomeStruct>(object)
    object::address_to_object<MyAwesomeStruct>(object_address)

unburn object:

    object::unburn(owner, object);
    
### 2024.09.14
学习move script: https://aptos.dev/en/build/smart-contracts/scripts/script-tutorial

<!-- Content_END -->
