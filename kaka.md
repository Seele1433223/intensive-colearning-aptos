---
timezone: Asia/Shanghai
---

---

# 卡卡

1. 自我介绍 <br>
   一名计算机技术爱好者，从事计算机安全领域的工作。不久前接触到区块链，被去中心化的愿景所吸引。打算深入学习相关的技术，期待与大佬们交流学习！
2. 你认为你会完成本次残酷学习吗？<br>
   包完成的，不完成倒立洗头！！！

## Notes

<!-- Content_START -->

### 2024.09.01
了解Aptos残酷共学的规则，并报名。

### 2024.09.07
学习内容：1) 参加会议; 2) 阅读文档，对Aptos初步了解; <br>
学习笔记：<br>
Aptos 上有三种类型的账户：标准账户、资源账户、对象。

Aptos区块链上的任何交易执行都需要支付手续费，该费用包括两部分：
1. 执行和IO成本：以Gas Units为单位进行计量，Gas Units的价格可能根据网络负载而波动。
2. 存储费：涵盖了在分布式区块链存储中持久存储验证记录的成本。以固定的$APT价格来衡量。

Aptos区块链存储三种类型的数据：
- 交易：交易表示区块链上的账户正在执行的预期操作（例如转移资产）
- 状态：（区块链账本）状态代表交易执行输出的累积，即存储在所有资源内的价值
- 事件：交易执行时发布的辅助数据

### 2024.09.08
**学习内容**：TypeScript SDK的使用，并实践模拟交易; <br>
**学习记录**：<br>
使用 TypeScript SDK 初始化一个项目:

```
npm init && npm add -D typescript @types/node ts-node && npx tsc --init && mkdir src && echo 'async function example() { console.log("Running example!")}; example()' > src/quickstart.ts
```
测试初始化：
```
npx ts-node src/quickstart.ts
```
按照aptos sdk：
```
npm i @aptos-labs/ts-sdk
```
模拟交易: 交易允许你修改链上数据或触发事件。<br>
一般来说，交易从构建到链上执行需要经历5个步骤：构建、模拟、签名、提交、等待。<br>
1、构建：创建一个交易
```typescript
const transaction = await aptos.transaction.build.simple({
	sender: sender.accountAddress,
	data: {
		// All transactions on Aptos are implemented via smart contracts.
		function: "0x1::aptos_account::transfer",  //这是什么？
		functionArguments: [destination.accountAddress, 100],
	},
});
```

2、模拟：可选的，在提交交易之前模拟交易，为了估算成本。

```
const [userTransactionResponse] = await aptos.transaction.simulate.simple({
	signerPublicKey: signer.publicKey,
	transaction,
});
```

3、签名：一旦交易建立并且费用合理，就可以使用`aptos.transaction.sign`签署交易。

```
const senderAuthenticator = aptos.transaction.sign{(
	signer: sender,
	transaction,
)};
```

4、提交：交易签名后，提交交易到网络

```
const committedTransaction = await aptos.transaction.submit.simple({
	transacton,
	senderAuthenticator,
});
```

5、等待结果：最后，可以使用`aptos.waitForTransaction`并指定刚刚提交的交易的哈希值来等待交易的结果。

```
const executedTransaction = await aptos.waitForTransaction({ transactionHash: committedTransaction.hash })
```

### 2024.09.09
**学习内容**：安装配置aptos CLI，创建一个项目，熟悉项目结构； <br>
**学习记录**：<br>
Aptos使用Move语言来开发智能合约。

`aptos`命令：Aptos CLI（命令行接口）是一个工具用于帮助编译和测试Move合约。

下载：https://aptos.dev/en/build/cli#-install-the-aptos-cli

```
aptos help // 命令行手册 （检查是否安装成功）
```

创建一个Move package :

```
aptos move init --name <PROJECT_NAME>
```

该命令生成了：`scripts\`、`sources\`、 `tests\` 和`Move.toml`

目录是空的，Move.toml内容如下：

```
[package]
name = "demo"
version = "1.0.0"
authors = []

[addresses]
hello_blockchain = "_"
[dev-addresses]

[dependencies.AptosFramework]
git = "https://github.com/aptos-labs/aptos-core.git"
rev = "mainnet"
subdir = "aptos-move/framework/aptos-framework"

[dev-dependencies]
```

- `name`：package的名字；
- `version`：package的版本；
- `addresses`：描述模块将部署到哪个地址；
- `dependencies`：可能需要使用AptosFramework和其他第三方依赖项；

编写智能合约代码：增加到sources目录。

### 2024.09.10
**学习内容**：编写合约，并编译、发布; <br>
**学习记录**：<br>
```
aptos move compile  //编译合约，需要指明模块的部署地址，可以在命令行指明，也可以在move.toml中
aptos move publish  //发布合约到个人账户
aptos move deploy-object --address-name hello_blockchain //发布合约到Object
```
Move有两种类型的程序：**Modules**和**Scripts**。

模块（Modules）是定义结构类型以及对这些类型进行操作的函数的库。结构类型定义了 Move 全局存储的模式，模块函数定义了更新存储的规则。模块本身也存储在全局存储中。

模块有如下语法：

```
module <address>::<identifier> {
    (<use> | <friend> | <type> | <function> | <constant>)*
}
```

`module <address>::<identifier>`部分指定模块`<identifier>`将在全局存储中的账户地址`<address>`下发布。

脚本（Scripts）是类似于传统语言中的主函数的可执行入口点。脚本通常调用已发布模块的函数来执行全局存储的更新。脚本是临时代码片段，未在全局存储中发布。

### 2024.09.11
**学习内容**：学习Aptos中Object的概念 <br>
**学习记录**：<br>
在Move中，对象将资源组合在一起，以便将它们视为链上的单一实体。相比于账户，官方鼓励将代码部署到object上。因为它抽象了部署模块所需的必要资源，以及升级和冻结模块所需的授权。

对象拥有自己的地址，并且可以拥有类似于账户的资源。

示例：

```
module my_addr::object_playground {
  use std::signer;
  use std::string::{Self, String};
  use aptos_framework::object::{Self, ObjectCore};
  
  struct MyStruct1 {
    message: String,
  }
  
  struct MyStruct2 {
    message: String,
  }
 
  entry fun create_and_transfer(caller: &signer, destination: address) {
    // Create object
    let caller_address = signer::address_of(caller);
    let constructor_ref = object::create_object(caller_address);
    let object_signer = object::generate_signer(constructor_ref);
    
    // Set up the object by creating 2 resources in it
    move_to(&object_signer, MyStruct1 {
      message: string::utf8(b"hello")
    });
    move_to(&object_signer, MyStruct2 {
      message: string::utf8(b"world")
    });
 
    // Transfer to destination
    let object = object::object_from_constructor_ref<ObjectCore>(
      &constructor_ref
    );
    object::transfer(caller, object, destination);
  }
}
```

> 在构建过程中，对象可以配置为可传输、可燃烧和可扩展。

有三种类型的对象是可以创建的：

- **normal Object**：该类型的对象可被删除，随机地址

  `0x1::object::create_object(owner_address: address)`

- **named Object**：不可删除、固定地址

  `0x1::object::create_named_object(creator: &signer, seed: vector<u8>`

- **sticky Object**：不可删除，随机地址

  `0x1::object::create_sticky_object(owner_address: address)`

### 2024.09.12
**学习内容**：学习Aptos中struct和abilities的概念 <br>
**学习记录**：<br>
在Move中，Abilities是一项可以给**类型**注入某种**能力**。类型可以注入多个能力。

有4种不同的能力：

- `copy`：可以被复制；
- `drop`：可以被弹出/丢弃 popped/dropped;
- `store`：允许该类型的值存储在全局变量的struct中
- `key`：允许类型作为全局存储操作的键（key）

https://aptos.dev/en/build/smart-contracts/book/abilities

### 2024.09.13
**学习内容**：学习assert和abort表达式 <br>
**学习记录**：<br>
Move中的`assert`语句：`assert!(<predicate>, <abort_code>);`如果`<predicate>`为false，以abort_code中止交易。

`return`和`abort`是结束执行的两种控制流结构，一种用于当前函数，一种用于整个事务。

`abort`是一个带有u64类型的**abort code**的表达式。eg：

```
abort 42
```

### 2024.09.14
**学习内容**：深入学习Object的概念 <br>
**学习记录**：<br>
abort 表达式停止当前函数的执行，并恢复当前事务对全局状态所做的所有更改。

在创建object时，将接收到`ConstructorRef`，你可以使用它其生成另外的`Ref`s 

使用`ConstructorRef`和`object::generate_signer`可以生成一个signer，signer允许你在Object上传输resource。

在后面，`Ref`s被使用于 enable / disable / execute 某些Object函数，比如传输资源、传输对象它自己、删除对象 等等....

`Ref`s常用点和启用的功能：https://aptos.dev/en/build/smart-contracts/objects/creating-objects

> Refs必须在Object的创建时刻生成。一旦创建对象的事务完成，用于生成其它Refs的ConstructorRef就会过期。

`ExtendRef`:可以让Object变得可编辑。`object::generate_extend_ref`

`TransferRef`：决定Object是否可传输。`object::generate_transfer_ref`

### 2024.09.15
**学习内容**：学习abort，错误码的规范 <br>
**学习记录**：<br>
`abort`表达式停止当前函数的执行，并恢复当前交易对全局状态所做的所有更改。`abort`是一个带有u64类型的**abort code**的表达式。eg：`abort 42`

Move中的`assert`语句：`assert!(<predicate>, <abort_code>);`如果`<predicate>`为false，以abort_code中止交易。本质上也是`abort`。

规范的错误码：对错误码进行了规范，错误码使用u64最低的3个字节（高位的5个字节用于其它）。其中，3个字节中的最高字节代表**错误类别**，较低的两个字节代表**错误原因**。

eg：`0x10003`，0x1为错误类别，0x3为错误原因

`std::error`模块定义了一些错误类别：

```
const ALREADY_EXISTS: u64 = 8; //The resource that a client tried to create already exists (http: 409)
const INVALID_ARGUMENT: u64 = 1; //Caller specified an invalid argument (http: 400)
const NOT_FOUND: u64 = 6; //A specified resource is not found (http: 404)
const PERMISSION_DENIED: u64 = 5; //client does not have sufficient permission (http: 403)
......
```

在程序中，你仅需定义错误原因，如：

```
const ENOT_OWNER: u64 = 0x1;
```

然后使用`std::error`模块中的对应函数转换为规范错误码：

```
assert!(signer::address_of(owner) == @address, error::permission_denied(ENOT_OWNER));
```

当然，你也可以在定义时进行规范：

```
const ENOT_OWNER: u64 = 0x50001;
```

（思考：即使是非规范错误码也可以运行，那两者具体区别是什么呢？）

### 2024.09.17
**学习内容**：学习创建FA标准的资产 <br>
**学习记录**：<br>
Aptos FA标准是`coin`模块的现代代替。

创建FA标准资产的过程：

```
// 创建对象,比如
let fa_obj_constructor_ref = &object::create_sticky_object(@address);
// 
primary_fungible_store::create_primary_store_enabled_fungible_asset(
    fa_obj_constructor_ref,
    max_supply,
    name,
    symbol,
    decimals,
    icon_uri,
    project_uri
);
// 获取权限并存储，以便后续进行操作
let mint_ref = fungible_asset::generate_mint_ref(fa_obj_constructor_ref);
let burn_ref = fungible_asset::generate_burn_ref(fa_obj_constructor_ref);
let transfer_ref = fungible_asset::generate_transfer_ref(fa_obj_constructor_ref);

let fa_obj_signer = object::generate_signer(fa_obj_constructor_ref);
move_to(&fa_obj_signer, FAController {
    mint_ref,
    burn_ref,
    transfer_ref,
});

// FAController为：
struct FAController has key {
    mint_ref: fungible_asset::MintRef,
    burn_ref: fungible_asset::BurnRef,
    transfer_ref: fungible_asset::TransferRef
}

// 进行mint操作时：
let config = borrow_global<FAController>(fa_obj_addr);
primary_fungible_store::mint(&config.mint_ref, sender_addr, amount);
```

### 2024.09.18
**学习内容**：学习Script的概念，以及编译和执行 <br>
**学习记录**：<br>
脚本（Scripts）是类似于传统语言中的主函数的可执行入口点。脚本通常调用已发布模块的函数来执行全局存储的更新。脚本是临时代码片段，未在全局存储中发布。

Scripts是在单个交易中运行多个public函数的一种方式。Script可以与合约一起编写，但强烈建议为其使用单独的Move包。

- scripts中只能有一个函数
- 参数只能为：[`u8`, `u16`, `u32`, `u64`, `u256`, `address`, `bool`, `signer`, `&signer`, `vector<u8>`]

```
aptos move compile
```

```
aptos move compile-script  // 合约中只有一个script时
```

运行脚本：

```
aptos move run-script --compiled-script-path build/run_script/bytecode_scripts/main.mv --args address:b078d693856a65401d492f99ca0d6a29a0c5c0e371bc2521570a86e40d95f823 --args u64:5
```

### 2024.09.19
**学习内容**：学习使用indexer查询数据<br>
**学习记录**：<br>
indexer跟踪链上发生的每笔交易，然后通过GraphQL API公开该交易。任何人都可以使用它来获取有关交易、可替代资产和链上代币的基本历史数据和汇总数据。

可以通过Hasura Explorer很方便地进行执行操作。

GraphQL API：

- **Mainnet:** `https://api.mainnet.aptoslabs.com/v1/graphql`
- **Testnet:** `https://api.testnet.aptoslabs.com/v1/graphql`
- **Devnet:** `https://api.devnet.aptoslabs.com/v1/graphql`
<!-- Content_END -->
