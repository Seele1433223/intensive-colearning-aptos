---
timezone: Asia/Shanghai
---

# Jack

1. 自我介绍：
被裁大叔
2. 你认为你会完成本次残酷学习吗？
应该能吧

## Notes

<!-- Content_START -->

### 2024.09.07
学习Account相关内容：

1.Ed25519

2.Secp256k1 ECDSA

3.K-of-N multi-signatures

aptos的私钥可以更改，但是对应的地址不变。

参加线上Aptos共学群首次会议

### 2024.09.08
配置开发环境，初始化程序。

### 2024.09.09

熟悉aptos的devnet,testnet,mainnet不同的网络环境。

熟悉aptos的区块链浏览器的使用。

### 2024.09.10

1.使用aptos move init --name <PROJECT_NAME>创建一个aptos工程。

工程内部在 Move.toml 文件中，填入以下关键信息：

name: 包的名称

version: 包的版本（默认值为 "0.0.0"）

addresses: 描述模块将部署到的地址

dependencies: 你可能会想使用 AptosFramework

在sources文件内创建move并编写代码。

2.使用aptos move compile进行编译。

### 2024.09.13

Aptos测试
1.#[test]（预期执行成功）和注释都#[expected_failure]（预期失败）可以带参数或不带参数使用。

2.带有参数的测试注释采用以下形式#[test(<param_name_1> = <address>, ..., <param_name_n> = <address>)]

3.$ aptos move test 执行操作

<!-- Content_END -->
