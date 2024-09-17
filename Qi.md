---
timezone: Asia/Shanghai
---

# Qi

1. 自我介绍 hello everyone, you can call me Qi
2. 你认为你会完成本次残酷学习吗？ Yep

## Notes

<!-- Content_START -->

### 2024.09.07

获得 aptos 的第一个钱包：0x25d20bff83e0e95f51fc69dd5cd12c5b681369645d1d0e0a217bc7a7d3c9f4e2

了解 Aptos 一点点..

- 节点类型：Validator nodes、Fullnodes
- 共识协议：BFT
- 账户类型：Standard account 、Resource account、Object
- GAS 费：max_gas_amount、gas_price

### 2024.09.08

在测试网部发布了第一个交易
0x659e1887a3c9737df1dd66b7807fe60936b87ed0a256c4a99964634136489e61

### 2024.09.09

初始化了一个前端项目，进行合约调用
(https://github.com/Gkok-king/hello_aptos)

### 2024.09.10

熟悉了 move 的相关语法
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

### 2024.09.11

新学了一点基础语法
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

### 2024.09.12

又新学了一点基础语法：函数和范型
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

### 2024.09.13

又新学了一点基础语法 Struct Methods
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

add new grammar learning and try to know Aptos Stdlib

### 2024.09.14

基础语法过完了，尝试了解 Aptos 的标准库
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

### 2024.09.15

了解 object model
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/move.md

### 2024.09.16

learn Aptos Fungible Asset (FA) Standard
https://github.com/Gkok-king/hello_aptos_back/blob/master/study/FA.md

### 2024.09.17

在使用这个教程
https://aptos.dev/en/build/guides/first-coin
走到了 step4

=== Addresses ===
Alice: 0x5912bc41804b4354f8d7a7bad39c4d8245cba456db33fada7728849938b14659
Bob: 0x9d32e0ae58f405eff761b42e44a28daf9b265cefcd0c1cb2821a5dc22b34fac0

=== Compiling MoonCoin package locally ===
In order to run compilation, you must have the `aptos` CLI installed.
Running the compilation locally, in a real situation you may want to compile this ahead of time.
aptos move build-publish-payload --json-output-file move/moonCoin/moonCoin.json --package-dir move/moonCoin --named-addresses MoonCoin=0x5912bc41804b4354f8d7a7bad39c4d8245cba456db33fada7728849938b14659 --assume-yes
Compiling, may take a little while to download git dependencies...
UPDATING GIT DEPENDENCY https://github.com/aptos-labs/aptos-core.git
INCLUDING DEPENDENCY AptosFramework
INCLUDING DEPENDENCY AptosStdlib
INCLUDING DEPENDENCY MoveStdlib
BUILDING MoonCoin

=== Publishing MoonCoin package to devnet network ===
Publish package transaction hash: 0xf547b213fc08b8532b6db13ba590e41d9373ecee5419e88c328bdf453d30ec4b
Bob's initial MoonCoin balance: 0.
Alice mints herself 100 MoonCoin.
Alice transfers 100 MoonCoin to Bob.
Bob's updated MoonCoin balance: 100.

明天继续尝试

<!-- Content_END -->
