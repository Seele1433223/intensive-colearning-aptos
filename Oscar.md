---
timezone: Asia/Shanghai
---

# [Oscar]

1. A eco-lifelong learner. To surf🏄‍♀️ better in the Web3 world. Enjoy this challenging vibe and become cooler 🆒. 
2. 你认为你会完成本次残酷学习吗？Yes

## Notes

<!-- Content_START -->

### 2024.09.07

- 学习主题： Aptos 白皮书学习
- 学习内容总结：框架总结
  - **愿景：**提供⼀个可以为 web3 带入主流采用，并授权构建一个去中心化应用程序生态系统来解决现实世界的用户问题。
    **使命：**通过提供灵活的模块化区块链架构来提升区块链可靠性、安全性和性能方面的最新技术⽔平。
    **验证：**在过去的三年中构建、推进、开发和部署 Diem 主网，2020 年曾部署到十多个节点运营商和多个钱包提供商，在没有停机的情况下进行两次重大升级，对技术堆栈彻底的改进，将安全、透明和升级作为核心功能，并且强调了交易处理、去中心化和网络治理的新方法。
    
  - 区块链作为一种新兴的互联网基础设施而崛起，让开发者得以惊人的速度部署了数万个去中心化的应用程序。不幸的是，**由于频繁的中断、高成本、低吞吐量限制和许多安全问题，区块链的使用还不普及。**为了在web3 时代实现大规模采用，区块链基础设施需要**遵循云基础设施**的路径，作为一个可信的、可扩展的、成本效益的、不断改进的平台来构建广泛使用的应用程序。我们提出了 Aptos 区块链，**设计以可伸缩性、安全性、可靠性和可升级性作为关键原则**，以解决这些挑战。Aptos 在过去三年中由全球的 350 多名开发人员共同开发。它在共识、智能合同设计、系统安全、性能和去中心化等方面有所创新。这些技术的结合将为 Web3 的普及提供一个重要的基础模块：
    
    - 第一，Aptos 区块链本地集成并在内部使用 Move 语言，用于快速和安全地执行交易。Move prover 是用MOVE 语言编写的智能合约的正式验证器，它为合约的常量和行为提供了额外的保护措施。这种对安全的关注使开发者更好地保护他们的程序免受恶意入侵。
    - 第二，Aptos 数据模型可以实现灵活的密钥管理和混合托管选项。这一点，以及签名之前的交易透明度和实用的轻客户端协议，为用户提供更安全、更值得信赖的体验。
    - 第三，为了实现高吞吐量和低延迟，Aptos 利用了一种流水线和模块化的方法来处理交易的关键阶段。具体来说，交易广播、块元数据排序、交易并行处理、批存储和分类帐认证都同时进行。这种方法充分利用了所有可用的物理资源，提高了硬件效率，并实现了高并发处理。
    - 第四，一些需要提前知道数据读写知识的并行引擎，打破了交易的原子性，而 aptos 对开发人员没有这种限制。它有效支持任意复杂事务的原子性，为实际应用程序提供更高的吞吐量、更低的延迟，并且简化开发。
    - 第五，Aptos 模块化架构设计支持客户的灵活性，并优化频繁和即时升级。此外，为了快速部署新的技术创新和支持新的 web3 用例，Aptos 提供了嵌入式的链上变更管理协议。
    - 最后，Aptos 区块链正在试验未来的举措，以提高单个验证器的性能：其模块化设计和并行执行引擎支持验证器的内部分片，同构状态分片提供了水平吞吐量可扩展性的潜力，而不增加节点操作员额外的复杂性。

### 2024.09.08

- 学习主题： 第一次 Aptos 公开课
- 学习内容总结：
  -  Aptos & Move 简介与开发者学习资料推荐
  -  在IntelliJ IDEA-中安装move on aptos 插件，参考 [IDEA 配置 Aptos 开发](https://learnblockchain.cn/article/9258)
  - 讨论交流：https://github.com/aptos-labs/aptos-developer-discussions/discussions


### 2024.09.09

- 学习主题： Aptos 公链机制特点
- 学习内容总结：
  - 语言系统：采用安全灵活的区块链语言——Move 语言；其专为在区块链上进行安全资源管理和可验证执行而设计。事务执行是确定性的、封闭的和计量的。确定性和封闭性意味着交易执行的输出完全可预测，并且仅基于交易中包含的信息和当前分类帐状态。
  - Proof-of-stake DiemBFT 拜占庭容错共识机制：过去的三年进行了四次迭代，提升了交易确认速度和区块链的稳定性，在三分之一的验证结点故障时，仍能保证稳定运行。
  - 安全性方面：支持任何帐户轮换其私钥的能力。验证者可以定期轮换他们的共识密钥，以提高安全性。多代理交易还可以实现更广泛的可组合模式和用例。
  - 可拓展性方面：通过并行账户交易，同时保留对交易排序的控制，考虑更灵活和可组合的并行性的替代实现，进行对轻量级、完整、归档和验证节点的快速灵活的状态管理支持。
  - 可升级性方面：以验证者的管理和配置通过链上状态进行管理，方便社区投票和快速执行升级。强大的测试和部署实践确保安全可靠的部署。
  - Gas 费：支持多币种来支付 gas，避免钱包中只有一种非 gas 代币而导致无法进行交易，原理为将其他代币按链上汇率标准化兑换为 Aptos 代币，然后根据标准化后的 gas 价格对所有交易进行排序并确认需执行的交易。

### 2024.09.10

- 学习主题： Move 语言了解
- 学习内容总结：目前采用Move 语言的区块链项目有：Aptos、Sui、Starcoin、0L Network等。Move 语言设计之初试图从程序语言的角度上去解决数字资产的保护问题。
  - Move 强调安全性和灵活性，受到 Rust 编程语言的启发，通过线性类型等概念在语言中明确数据的所有权，并强调资源稀缺、保存和访问控制，定义每个资源的生命周期、存储和访问模式。
  - 利用字节码验证器（表示指令发表传输时需要经过字节码的校验，如有一条未通过将不给予加载）来保证类型和内存的安全。并建设一个 Move 验证器，帮助不受信的代码进行更可信的编译。Aptos 的链上配置包括一组活动验证器、标记属性以及各种服务配置，支持对模块的可升级性和可编程性的无缝配置更改，并支持 Aptos 本身升级。
  - 阅读：[最近关于用户和 Move 智能合约交互，不需要授权(Approve) 是更安全还是更不安全的争论很多，这里尝试用通俗的方式来解释一下二者背后的区别以及 Move 这样设计背后的思想。](https://x.com/jolestar/status/1583034513122156544?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1583034513122156544%7Ctwgr%5Eaaeb5bb62de9074e8a1e2a7de3c89676d8c532b9%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fmirror.xyz%2F0xb54e978a34Af50228a3564662dB6005E9fB04f5a%2F_ZVhXxYTCyRM5_u2dO6KXLA9GWuWa6BiSp7vvNQ8XuU)



### 2024.09.11

- 学习主题： 第二次 Aptos 公开课

- 学习内容总结：安装开发环境、创建/编译/测试/部署工程  

  - [安装 Aptos CLI](https://aptos.web3doc.top/cli-tools/aptos-cli-tool/install-aptos-cli) 与 Aptos 网络交互

  - 克隆 Aptos 存储库。
  
    ```text
    git clone https://github.com/aptos-labs/aptos-core.git
    ```

  - `cd` 进入 `aptos-core` 目录。
  
    ```text
    cd aptos-core
    ```

  - 运行 `scripts/dev_setup.sh` Bash 脚本，如下所示。 这将通过安装构建、测试和检查 Aptos Core 所需的大部分依赖项来准备您的开发人员环境。 请注意，系统可能会提示您输入密码：
  
    ```text
    ./scripts/dev_setup.sh
    ```

    可以通过运行 `./scripts/dev_setup.sh --help` 查看脚本的可用选项。

  - 更新您当前的 shell 环境以运行 `cargo build` 和其他与 Aptos 相关的命令：
  
    ```text
    source ~/.cargo/env
    ```

  - （可选）签出发布分支以安装 Aptos 节点：
  
    - 开发网
    - 测试网

    使用如下命令切换到 `testnet` 分支: 现在您的基本 Aptos 开发环境已准备就绪。
  
    ```text
    git checkout --track origin/testnet
    ```
  
  - [Jetbrains IDE 的Move语言插件](https://plugins.jetbrains.com/plugin/14721-move-language)：支持语法高亮、代码导航、重命名、格式化、类型检查和代码生成。



### 2024.09.12

- 学习主题： Aptos 账户

- 学习内容总结：Aptos 区块链的设计强调账户的明确性和创建过程，确保用户在使用区块链之前必须先创建一个账户。这种方式与一些其他区块链（如以太坊）有所不同，后者允许隐式创建账户。在 Aptos 上，创建账户的过程可以通过转移 Aptos 代币（APT）来实现。具体而言，当用户将 APT 转移到一个新的账户地址时，该地址就会被创建并与相应的账户关联。这个过程确保了每个账户都是显式存在的，从而提高了安全性和可预测性。

  - Aptos 上有三种类型的账户：

    - 标准账户——这是一个典型的账户，对应一个地址和一对相应的公钥/私钥。
    - 资源账户- 一个没有对应私钥的自主账户，供开发者存储资源或上链发布模块。
    - 对象- 存储在代表单个实体的单个地址内的一组复杂资源。

    Aptos 区块链存储三种类型的数据：

    - 交易：交易表示区块链上的账户正在执行的预期操作（例如转移资产）。
    - 状态：（区块链账本）状态代表交易执行输出的累积，即存储在所有资源内的价值。只有交易才能改变账本状态。
    - 事件：交易执行时发布的辅助数据。

### 2024.09.13

- 学习主题： [APTOS 代币经济模型了解](https://aptosfoundation.org/currents/aptos-tokenomics-overview)

- 学习内容总结：

  - 主网于 2022 年 10 月 12 日启动。主网上的 Aptos 代币（APT）初始总供应量为 10 亿个代币。APT 将具有 8 位精度，作为最小单位称为 Octa 的分数的一部分。

  - APT 是 Aptos 的治理代币，51.02% 的代币将分配给社区、16.5% 分配给基金会、19% 分配给核心贡献者、13.48% 分配给投资人。代币池指定用于与生态系统相关的项目，如赠款、奖励和其他社区发展计划。社区及基金会共 410,217,359.767 枚代币由 Aptos 基金会持有，100,000,000 枚由 Aptos Labs 持有。预计将在十年内完成解锁。

    | **类别**          | **初始代币分配的百分比%** | **初始代币**    |
    | ----------------- | ------------------------- | --------------- |
    | Community         | 51.02%                    | 510,217,359.767 |
    | Core Contributors | 19.00%                    | 190,000,000.000 |
    | Foundation        | 16.50%                    | 165,000,000.000 |
    | Investors         | 13.48%                    | 134,782,640.233 |



### 2024.09.15

- 学习主题：Aptos可替代资产标准（FA）

- 学习内容总结：
  - 在去中心化金融的领域中，Aptos 可替代资产标准（FA），又称为可替代资产，成为嵌入 Aptos Move 中的关键的框架组件。这一技术，奇迹赋能了各种资产的代币化，包括大宗商品、房地产和金融工具，推动了去中心化金融应用程序的发展。
  - FA 促成的证券和大宗商品的代币化引入了所有权的概念，使市场更加民主化，扩大了投资机会。除了传统资产外，FA的实用性还扩展到了代表房地产所有权，为传统流动性较弱的市场注入了新的血液。即使在游戏领域，虚拟货币和角色也可以进行代币化，使玩家能够拥有、交易，并为游戏开发者和玩家创造更多的创新收入的机会。
  - 除了其上述特性以外，可替代资产（FA）被定位为加密货币的超集，运用了比传统货币更广泛的范围。这种灵活性有望在替代 Move 中的 Coin 模块方面得到体现，展示了 FA 框架的全面性。

### 2024.09.17

- 学习主题：继续理论，Move 语言了解，暂不 coding 👀
  - 学习内容总结：Move 语言目录由五个部分组成
    - [虚拟机](https://github.com/libra/libra/tree/master/language/vm) (VM), 它包含字节码格式、字节码解释器和执行交易块的基础设施。该目录还包含生成创世区块的基础设施
    - [字节码验证器](https://github.com/libra/libra/tree/master/language/bytecode_verifier), 其中包含一个静态分析工具，用于拒绝无效的Move字节码。虚拟机在执行新的Move代码前，会先运行字节码验证器。编译器运行字节码验证器则会把输出和错误显示给程序员。
    - Move 中间层表示 (IR： intermediate representation) [编译器](https://github.com/libra/libra/tree/master/language/stdlib), 它将可读的程序文本编译成Move字节码. *警告:IR编译器是一个测试工具。它会生成将被Move字节码验证器拒绝的无效字节码。IR语法工作仍在进行，或将经历重大的变化。*
    - [标准库](https://github.com/libra/libra/tree/master/language/stdlib), 其中包含 `LibraAccount` 和 `LibraCoin` 等核心系统模块的Move IR代码。
    - [一些测试](https://github.com/libra/libra/tree/master/language/functional_tests) ，用于虚拟机，字节码验证程序和编译器。 这些测试是用Move IR 编写的，由测试框架运行，该测试框架从注释中编码的特殊指令解析运行测试的预期结果。

### 2024.09.18

- 学习主题：Move 示例: 简单、类型安全且可替代的资产 Coins

  ```move
  module 0xCAFE::BasicCoin {
    // Only included in compilation for testing. Similar to #[cfg(testing)]
    // in Rust. Imports the `Signer` module from the MoveStdlib package.
    #[test_only]
    use std::signer;
    struct Coin has key {
        value: u64,
    }
    public fun mint(account: signer, value: u64) {
        move_to(&account, Coin { value })
    }
    // Declare a unit test. It takes a signer called `account` with an
    // address value of `0xC0FFEE`.
    #[test(account = @0xC0FFEE)]
    fun test_mint_10(account: signer) acquires Coin {
        let addr = signer::address_of(&account);
        mint(account, 10);
        // Make sure there is a `Coin` resource under `addr` with a value of `10`.
        // We can access this resource and its value since we are in the
        // same module that defined the `Coin` resource.
        assert!(borrow_global<Coin>(addr).value == 10, 0);
    }
  }
  ```


### 2024.09.19

- 学习主题：Objects 可组合的资源容器

  ```
  module 0xCAFE::BasicObject {
    /// Sets up the object, and returns the signer for simplicity
    fun setup_object(constructor_ref: &ConstructorRef, can_transfer: bool) {
        // Lets you get a signer of the object to do anything with it
        let extend_ref = object::generate_extend_ref(constructor_ref);
  
        // Lets you gate the ability to transfer the object
        let transfer_ref = if (can_transfer) {
            option::some(object::generate_transfer_ref(constructor_ref))
        } else {
            option::none()
        };
  
        // Lets you delete this object, if possible
        let delete_ref = if (object::can_generate_delete_ref(constructor_ref)) {
            option::some(object::generate_delete_ref(constructor_ref))
        } else {
            option::none()
        };
  
        // -- Store references --
        // A creator of the object can choose which of these to save, and move them
        // into any object.
        let object_signer = object::generate_signer(constructor_ref);
  
        move_to(&object_signer, ObjectController {
            extend_ref,
            transfer_ref,
            delete_ref,
        });
    }
  }
  ```

  Fungible Assets 高表现力、可替代的数字资产

  ```
  
  module 0xCAFE::BasicFungibleAsset {
    /// Swaps between two tokens in the pool
    /// This is friend-only as the returned fungible assets might be of an internal
    /// wrapper type. If this is not the case, this function can be made public.
    public(friend) fun swap(
        pool: Object<LiquidityPool>,
        from: FungibleAsset,
    ): FungibleAsset acquires FeesAccounting, LiquidityPool, LiquidityPoolConfigs {
        // ...
  
        // Deposits and withdraws.
        let pool_data = liquidity_pool_data(&pool);
        let k_before = calculate_constant_k(pool_data);
        let fees_accounting = unchecked_mut_fees_accounting(&pool);
        let store_1 = pool_data.token_store_1;
        let store_2 = pool_data.token_store_2;
        let swap_signer = &package_manager::get_signer();
        let fees_amount = (fees_amount as u128);
        let out = if (from_token == fungible_asset::store_metadata(pool_data.token_store_1)) {
            // User's swapping token 1 for token 2.
            fungible_asset::deposit(store_1, from);
            fungible_asset::deposit(pool_data.fees_store_1, fees);
            fees_accounting.total_fees_1 = fees_accounting.total_fees_1 + fees_amount;
            fungible_asset::withdraw(swap_signer, store_2, amount_out)
        } else {
            // User's swapping token 2 for token 1.
            fungible_asset::deposit(store_2, from);
            fungible_asset::deposit(pool_data.fees_store_2, fees);
            fees_accounting.total_fees_2 = fees_accounting.total_fees_2 + fees_amount;
            fungible_asset::withdraw(swap_signer, store_1, amount_out)
        };
  
        // ...
    }
  }
  ```

  学习主题： 第三次 Aptos 公开课  TODO

### 2024.09.20

### 2024.09.21

### 2024.09.22

### 2024.09.23

### 2024.09.24
### 2024.09.25
### 2024.09.26
### 2024.09.27

<!-- Content_END -->
