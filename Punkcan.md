---
timezone: Asia/Shanghai
---


---

# {Punkcan}

1. 自我介绍
	1. 单纯喜欢Aptos的设计，自学Aptos中
2. 你认为你会完成本次残酷学习吗？
	1. 可以，一定可以，一年总得要有个Flag完成吧

## Notes

<!-- Content_START -->

### 2024.09.07

就我理解到的Aptos特点
- 模组化设计，这也是比较吸引我的，主要是安全管理，当一个模组被判断为安全时，后续沿用模组就没有安全上的顾虑
- Block-STM，一种并行方式，可以为整个链的吞吐量提供弹性（但细节我还不清楚）
- 储存模式，EVM的储存是所有用户的数据都储存在一个合约中，如果是Mapping还好但如果是数组等数据，会随着时间的演进，效能越来越差，但是Aptos的数据是储存在用户的帐号上，提升了并行条件跟执行效率（当然如果ORE这类的去干他，我不确定会不会也被干挂）
- AptosBFT，共识基于拜占庭共识协议设计，有快速验证，快速恢复的特性

Move上模组更新的时机点：
- Move语言更新
- MoveVM更新

##### Aptos是什么？

Aptos 的历史可以追溯到 Facebook 于 2019 年发布的区块链项目 **Libra**。
Libra 旨在推出一种全球化的数字货币，并计划与各大国际企业、金融机构合作。
希望能通过区块链技术构建一个可扩展的支付网络，支持全球数十亿用户的跨境交易。

然而，由于监管压力和各国政府对稳定币的担忧，Libra 项目在多方阻力下经历了多次修改和调整，最终于 2020 年更名为 **Diem**，并将项目重心从全球货币转移到更加合规和可监管的支付系统上。尽管进行了调整，Diem 仍然面临着监管挑战，最终 Meta 于 2022 年决定终止该项目。

在 Diem 项目停止之后，**Aptos Labs** 由前 Diem 团队成员成立，特别是区块链研究人员 **Mo Shaikh** 和 **Avery Ching**，他们是 Diem 项目中负责技术架构和开发的关键人物。
Aptos 的目标是延续 Diem 的技术优势，并将其打造为一个面向开发者和用户的高性能公链。

（另外还有一组人是Sui，他们更着重在数据结构的设计，两者使用的加密跟共识法并不一样，虽然开发都是Move）

Aptos 的技术架构继承了 Diem 的诸多核心理念，并进一步优化了这些技术，尤其是在共识协议、并行执行、智能合约和安全性方面。

- **Move 编程语言**：Aptos 延续了 Diem 开发的 Move 语言，作为其智能合约编程语言。Move 的资源管理和安全特性，使其成为一个高度可靠的区块链编程语言。
- **高性能共识机制**：Aptos 基于 Diem 的 **HotStuff 共识协议**，并通过优化改进为 AptosBFT，共识速度更快，吞吐量更高。
- **并行交易执行**：Aptos 的并行执行引擎 **Block-STM**，允许多个交易同时处理，极大提高了链上交易的效率。

Aptos 在项目启动后，迅速得到了区块链领域的广泛关注。2022 年，Aptos 通过多轮融资，获得了大规模的资金支持。参与投资的著名机构包括 **a16z（Andreessen Horowitz）**、**Multicoin Capital**、**FTX Ventures** 等。

- **2022 年 3 月**：Aptos 宣布完成了 2 亿美元的融资，由 a16z 领投，其他知名风投公司如 Multicoin Capital 和 Coinbase Ventures 参与。
- **2022 年 7 月**：Aptos 再次获得 1.5 亿美元的融资，这次融资由 FTX Ventures 和 Jump Crypto 领投，使得其估值大幅提升。

这些融资帮助 Aptos 构建了一个强大的开发生态，并推动了技术的进一步迭代和创新。

经过数月的开发和测试，Aptos 于 **2022 年 10 月 17 日** 正式推出其主网，命名为 **Aptos Autumn**。在主网上线之前，Aptos 已经通过多轮测试网和社区的合作，完善了基础设施、开发工具和网络安全性。


自主网上线以来，Aptos 致力于构建一个强大的开发者和用户生态系统。其愿景是成为支持去中心化金融（DeFi）、游戏、NFT 和其他去中心化应用的核心基础设施。

- **开发者友好性**：Aptos 通过提供详细的开发文档、工具和资源，吸引了大量开发者社区的参与，并且许多项目基于 Aptos 开发智能合约和去中心化应用。
- **合作伙伴与集成**：Aptos 与多个主流项目和企业达成了合作，以推动生态系统的扩展，并且吸引了包括开发工具、钱包、桥接工具、和去中心化交易所在内的多个合作伙伴。


不过我觉得目前节点的中心化程度有点高，这似乎是近期在各个公链的一些现象

### 2024.09.08

- 我现在第一个要解决的就是，如何编程，如何编译
Aptos 在编译 Move 合约和代码时，提供了一系列的命令行工具，特别是 Aptos CLI 和 Move CLI。以下是一些主要的编译相关指令：

### 1. `aptos move compile`
这是 Aptos CLI 用于编译 Move 合约的命令。

- **基本用法**：
  ```bash
  aptos move compile --package-dir <package_path> --named-addresses <addresses>
  ```

- **选项**：
  - `--package-dir <package_path>`：指定要编译的 Move 包的路径，默认路径为当前目录。
  - `--named-addresses <addresses>`：为合约中使用的命名地址提供映射。例如：`Alice=0x1`.

### 2. `aptos move test`
用于运行 Move 代码的单元测试。

- **基本用法**：
  ```bash
  aptos move test --package-dir <package_path> --named-addresses <addresses>
  ```

- **选项**：
  - `--package-dir <package_path>`：指定包含测试的 Move 包路径。
  - `--named-addresses <addresses>`：同样为命名地址指定映射。

### 3. `move build`
Move CLI 中的构建命令，用于编译 Move 包。

- **基本用法**：
  ```bash
  move build
  ```

- **选项**：
  - `--package-dir <path>`：指定 Move 包的路径。
  - `--named-addresses <addresses>`：同样为命名地址指定映射。

### 4. `move clean`
清理之前的构建输出。

- **基本用法**：
  ```bash
  move clean
  ```

### 5. `move check`
Move CLI 用于检查代码是否符合 Move 的类型和语法要求，类似于静态分析。

- **基本用法**：
  ```bash
  move check
  ```

### 6. `aptos move publish`
发布 Move 合约到 Aptos 网络。

- **基本用法**：
  ```bash
  aptos move publish --package-dir <package_path> --profile <profile_name>
  ```



Aptos 的 Move 项目的包结构一般遵循 Move 框架的标准项目结构。一个典型的 Move 项目包会包含多个文件夹和文件，用于存储 Move 代码、单元测试以及依赖管理等。以下是一个标准的 Move 项目的包结构：

### 1. 项目根目录
这是项目的根目录，包含整个 Move 包。文件和文件夹的命名方式和组织有助于管理和编译 Move 合约。

```
my_move_project/
│
├── Move.toml
├── sources/
├── tests/
├── scripts/
└── build/
```

### 2. `Move.toml`
这是项目的配置文件，用于定义包的元数据、依赖关系、命名地址等信息。它类似于其他语言中的包管理配置文件，比如 Rust 的 `Cargo.toml`。

**示例内容**：
```toml
[package]
name = "MyMovePackage"
version = "0.1.0"
authors = ["Author Name"]

[addresses]
# 映射 Move 代码中的命名地址
Alice = "0x1"
Bob = "0x2"

[dependencies]
# 引入外部的 Move 包依赖
AptosFramework = { git = "https://github.com/aptos-labs/aptos-core.git", subdir = "aptos-move/framework" }
```

### 3. `sources/`
这个文件夹包含 Move 模块和脚本的源代码文件。Move 模块以 `.move` 结尾，通常是应用的核心业务逻辑。

**示例结构**：
```
sources/
│
├── MyModule.move
└── AnotherModule.move
```

**示例代码**（`MyModule.move`）：
```move
module MyModule {
    public fun my_function() {
        // function logic
    }
}
```

### 4. `tests/`
`tests/` 文件夹包含 Move 的单元测试。测试文件可以是 Move 源文件或 `.move` 后缀的文件。

**示例结构**：
```
tests/
│
└── my_test.move
```

**示例测试文件**（`my_test.move`）：
```move
script {
    use 0x1::MyModule;

    fun test_my_function() {
        MyModule::my_function();
    }
}
```

### 5. `scripts/`
`scripts/` 文件夹包含用于与链交互的 Move 脚本。Move 脚本是独立的逻辑片段，可以部署到链上执行。

**示例结构**：
```
scripts/
│
└── deploy.move
```

**示例代码**（`deploy.move`）：
```move
script {
    use 0x1::MyModule;

    fun deploy() {
        MyModule::init();
    }
}
```

### 6. `build/`
`build/` 文件夹用于存放编译后的 Move 包和字节码文件。它通常不会手动编辑，且是在运行 `aptos move compile` 或 `move build` 后自动生成。

### 7. 其他可能的文件夹
- **`examples/`**：存放示例代码或参考实现。
- **`storage/`**：一些项目会使用 `storage/` 来管理本地的链状态。



感谢GPT，这个清晰了很多


- 第二个问题：Aptos上的合约如何让用户觉得已经不可变更，是安全的
	- 方法一，透过多签帐号去布署合约，这样如果要更新合约，也需要多签
	- 方法二，不可变合约 (Immutable Contracts)，标示成不可升级
	- Aptos特有的DAO投票升级
	- 逻辑分离模式，将模组分离，让模组不可更改


### 2024.09.09

尝试create-aptos-dapp@latest

目前提供四种版型：
1. 单纯跟钱包交互的模型
2. NFT铸造模型
3. 代币铸造模型
4. 代币质押模型

我们选择铸币模型吧，应该比较简单些（自己想象的....）

接下来选择是主网还是测试网（后续可以在config中改）
其他先不变动，选择最简单的

目前开发的流程的就是先透过create-aptos-dapp建立范本后，再用IDEA打开project

公司网不好，今天先搞定本机的自行编译版本吧
https://aptos.dev/en/build/cli/install-cli/install-cli-specific-version

### 2024.09.10

缺课
### 2024.09.11

尝试编译发布
RR 很不错，会提示用户下一步可以做些什么，而且蛮符合需求的
先尝试Init，发现他找不到cli
找一下用python安装的aptos cli 在home 的 .local/bin下
但是现在有一个很奇怪的地方就是，RR每次都会说没有CLI，然后又重新帮我安装一次

完成了第一次布署合约
https://explorer.aptoslabs.com/txn/5966782531/changes?network=testnet

测试可以领取

完成代币铸造

累了
休息
### 2024.09.12

找一下线上编辑器，听说movebit有出品 https://ide.bitslab.xyz/
可惜目前只支援Sui

https://github.com/caoyang2002/movelgo 群友的作品
安装后可以获得一个Web IDE，所以远端可以安装编译器
目前是半成品，为了节省时间，以后有空再测试

于是今天不写程式，找找相关的方案

https://playground.pontem.network/

好吧，目前只找到这个，但是挺好用的（只有合约的部分的话）


### 2024.09.13

哎，https://playground.pontem.network/ 版本有点老旧，编译不了
只能回到VM上编写了

不折腾这个问题了

### 2024.09.14
练习合约的布署

usdk的测试
### 2024.09.15

又有点绕圈圈了
### 2024.09.16

重新学习module 0x1::coin的做法开始
有一种绕不出去的感觉

### 2024.09.17
### 2024.09.18
### 2024.09.19
### 2024.09.20
### 2024.09.21
### 2024.09.22

<!-- Content_END -->
