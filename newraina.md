---
timezone: Asia/Tokyo
---


---

# Newraina

1. 自我介绍
我是 Newraina

2. 你认为你会完成本次残酷学习吗？
会

## Notes

<!-- Content_START -->

### 2024.08.31

完成报名。

### 2024.09.07

共识机制
- AptosBFT
- 拜占庭容错

账户模型
- 地址格式：32字节的十六进制字符串
- 显式账户，需要先创建账户，然后才能交易
  - 认证私钥可修改，类似修改密码
  - 支持多签
- 三种账户
  - 标准账户
  - Resource 账户
  - Object 账户， address 就是 ObjectID
- Ed25519 和 Secp256k1 ECDSA
  - 两种不同的椭圆曲线签名算法
  - Ed25519 更快，更节省空间，更安全
  - Secp256k1 在比特币和以太坊中使用

### 2024.09.09

资源模型

- key 能力的 Struct 被视为 Resource，可以存储在账户或者全局存储里
- store 能力的 Struct 可以被存储在其他 Resource 里

```move
struct Coin has key {
  value: u64
}

struct CoinStore has key {
    coin: Coin,
}

CoinStore 是 Resource，Coin 是代币本身，可以存储在 CoinStore 里。

```

### 2024.09.10

尝试部署一个合约到 devnet：

https://explorer.aptoslabs.com/txn/0x122e90a603d7dba158a5cc564c3858a96723d50d92b7aba22c63aae740db3602?network=devnet

### 2024.09.11

学习 [Move Tutorial](https://github.com/aptos-labs/aptos-core/tree/main/aptos-move/move-examples/move-tutorial)

Step 2 Exercises

1. Find a flag that you can pass to the aptos move test command that will dump the global state when the test fails

```bash
aptos move test --dump
```

2. Find a flag that allows you to gather test coverage information

```bash
aptos move test --coverage
```

### 2024.09.12

学习 Move Tutorial step 3 & 4

- friend 语法
  - script 不能调用 friend 函数
-　数据存储模型
  - 每一个地址下，一个类型只能有一个值，因为它的存储模型是 type 到 value 的 Map


### 2024.09.14

今天看了一个待办事项列表的代码示例。其中有一点比较特别：在创建待办事项时，并不需要传入待办事项列表的ID，而是传入了待办事项列表的索引。

我猜这样做的原因是因为不容易拿到用户账号下所有的 to do list 的ID，因为To Do List合约可以部署到多个地址下。

那只使用一个序号的情况下，如何才能得到真实的To Do List地址呢？

在代码中，它使用了一个“create object address”方法，通过合约的部署地址和索引来获取一个确定的地址。这个地址会作为初始化以及后续使用的To Do List地址。

### 2024.09.16

Object
- 默认可以transfer
- 使用transfer_ref可以禁用transfer
- 使用LinearTransferRef可以实现一次性转移（灵魂绑定）

<!-- Content_END -->
