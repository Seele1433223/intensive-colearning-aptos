---
timezone: Asia/Shanghai
---

---

# Zemmer

1. 一名程序猿 + 一名自洽的产品。技术栈：web3：solidity相关。web2：vue3、fastapi。
2. 可以完成。

## Notes

<!-- Content_START -->

### 2024.09.07

1、了解了aptos链的历史
2、对比了共识机制
3、下载IDE，安装环境

### 2024.09.08
# move和solidity合约的不同点

## token的账本balance存储在用户账户中

1、ERC20存储在合约中，是一个总账形式。mapping(address => uint256)

2、Aptos的token balance是分账，存储在各自用户的账户中。

3、这么做的原因是因为Aptos中将token视为资源，利用区块交易的确定性，将所有权和资源绑定。

4、当move的合约需要token的总数，这个话题需要之后回答，我觉得可能的形式是单独维护一个总账，或进行链上计算所有的分账？

## 转账需要接收人确认

1、EVM上转账不需要接收人确认。

2、EVM这种机制的问题是可能恶意转账：多次小额转、转没用的资产、转违法收入比如洗钱。

3、Move转账需要接收人确认。


### 2024.09.09
起步，明天开始吧，今天把layer2和aptos的所有区别捋了一遍，从理论上解决了非以太坊公链和以太坊二链的区别。包括生态、技术、共识、交易对手、品牌等。
### 2024.09.10
### 2024.09.11
安装aptos，开始move编程。
### 2024.09.12
# 整体流程命令

## 创建项目

### 创建整体项目（可省略）

进入指定的目录

```
aptos init
```

### 再创建合约项目

在项目目录下

```
aptos move init
```

结果：

创建了move.toml等文件

## 编写合约

写代码

## 编译合约

在项目目录下

```
aptos move compile
```

```
aptos move build
```

### 这两个命令的区别

#### aptos move compile

主要用于编译 Move 源代码，并生成字节码文件（`.mv` 文件）。

只关注 Move 代码的语法和逻辑正确性，不会将模块或脚本发布到链上。

开发阶段使用：常用于开发过程中测试代码是否能通过编译，以及生成字节码供其他操作使用。

输出的是编译后的 Move 模块（例如 `.mv` 文件），这些文件不会包含包管理相关的信息。

语法格式：`aptos move compile --package-dir <package_path>`

### aptos move build

这是一个更高层次的命令，它除了编译 Move 代码外，还会对整个 Move 包进行构建。

它会处理 Move 包的依赖关系、生成构建工件（artifact），并打包输出编译好的模块或脚本。

在构建过程中，它会生成一些额外的元数据和包管理信息，方便后续的模块发布或部署。

生产阶段使用：适用于打包、准备发布 Move 项目，构建结果可以直接用于链上发布。

语法格式：`aptos move build --package-dir <package_path>`

## 部署合约前准备

### 1、生成账户

生成特定前缀的账户（部署人用于部署合约的账户，因为aptos里没有contract address的概念）

--vanity-prefix参数是自定义的账户名的前缀，在这里值是--vanity-prefix

--output-file是自定义的生成的保存账户地址的文件，在这里值是ace.key

```zsh
aptos key generate --vanity-prefix 0xace --output-file ace.key
```

结果

```json
{
  "Result": {
    "Account Address:": "0xacef1b9b7d4ab208b99fed60746d18dcd74865edb7eb3c3f1428233988e4ba46",
    "PublicKey Path": "ace.key.pub",
    "PrivateKey Path": "ace.key"
  }
}
```

### 2、为账户提供资金

#### 拷贝地址

```zsh
ace_addr=0xacef1b9b7d4ab208b99fed60746d18dcd74865edb7eb3c3f1428233988e4ba46
```

#### 给地址水

```zsh
aptos account fund-with-faucet --account $ace_addr
```

结果

```json
{
  "Result": "Added 100000000 Octas to account acef1b9b7d4ab208b99fed60746d18dcd74865edb7eb3c3f1428233988e4ba46"
}
```

## 部署合约

1、使用aptos move publish部署

2、参数--named-addresses：部署人地址

3、--private-key-file：私钥

4、--assume：不清楚

```
aptos move publish \
    --named-addresses test_account=$ace_addr \
    --private-key-file ace.key \
    --assume-yes
```

结果

```json
{
  "Result": {
    "transaction_hash": "0x1d7b074dd95724c5459a1c30fe4cb3875e7b0478cc90c87c8e3f21381625bec1",
    "gas_used": 1294,
    "gas_unit_price": 100,
    "sender": "acef1b9b7d4ab208b99fed60746d18dcd74865edb7eb3c3f1428233988e4ba46",
    "sequence_number": 0,
    "success": true,
    "timestamp_us": 1685077849297587,
    "version": 528422121,
    "vm_status": "Executed successfully"
  }
}
```



# 
### 2024.09.13
# 资源resources

1、是move语言中的数据结构！

2、唯一所有性：只能被一个账户所拥有。不可复制，所以没有双花。

3、资源生命周期管理：只有合约才能CRUD资源。

4、资源包含token、认证秘钥、序列号等。

## 关于唯一所有权

这是move语言特定的。

是资源所有的权层面，而不是类似于erc20这种同质化的经济层面。

所以只要是资源，无论他是什么，他都具备唯一所有权性。

# 模块modules

1、智能合约的逻辑单位

2、其实就是各种函数、规则等代码。

3、可以CRUD资源。

4、提供接口对外操作。

5、有权限控制

6、可以复用。

# 账户和地址

## 定义

地址的定义：32位字节标识符，用于定位区块链上账户或资源。

账户的定义：与某些地址相关联的完整的状态和资源的集合。

## 地址到账户的转化

以太坊上，只要有一个私钥就能创建一个新的地址字符串（公钥），而且这个新的地址字符串在交易之前是无需“上链”这个操作的。链上交易可以直接和这个地址进行交易，此时该地址显性出现在链上，而在交易之前，此地址对于链上是隐性的。

aptos中，也是通过私钥创建地址，但是地址在交易前必须“上链”（aptos account create），这时候地址就是对于链上显性的，只有上链的地址才能进行交易。
### 2024.09.14
## aptos-cli关于账户相关操作

aptos account开头

| 命令                              | 说明                                         |
| --------------------------------- | -------------------------------------------- |
| `create`                          | 在链上创建一个新账户                         |
| `create-resource-account`         | 在链上创建一个资源账户                       |
| `derive-resource-account-address` | 推导资源账户的地址                           |
| `fund-with-faucet`                | 使用水龙头为账户提供代币                     |
| `balance`                         | 显示账户持有的不同代币的余额，默认是默认账户 |
| `list`                            | 列出一个地址所拥有的资源、模块或余额         |
| `lookup-address`                  | 通过链上查找表查找账户地址                   |
| `rotate-key`                      | 旋转账户的认证密钥                           |
| `transfer`                        | 在账户之间转移 APT 代币                      |
| `help`                            | 打印此消息或指定子命令的帮助信息             |
### 2024.09.15
# Move（基于aptos和sui的合约编程）

## 定义

### 模块module

数据结构struct type，和操作数据结构的函数function。

模块只能发布published

### 结构类型struct type

定义了全局存储的策略。

### 模块函数module function

定义了更新存储的规则（其实就是操作数据结构）

### 全局存储global storage

地址层面的树状结构存储

每个地址存储资源数据值resource data values和模块代码值module code values。

每种资源只能保存唯一一份，不能重复。

操作这个资源的模块可以多个，但是不能重名。



# 脚本

## 脚本定义

类似于别的语言的main文件，是入口文件。

通常是调用已经发布（published或理解为部署deployed）的模块

对全局存储进行了更新

脚本只能执行execute。

注意这不是像ethers.js一样在链下调用，脚本是在链上执行的，像是一种链上调用，每次执行脚本只运行一次。

使用场景：无需部署全部合约，去测试合约中部分功能。

## 脚本语法结构

```rust
script {
    <use>*
    <constants>*
    fun <identifier><[type parameters: constraint]*>([identifier: type]*) <function_body>
}
```

1、声明：以use开头

2、声明常量：

3、声明函数：自定义函数名称，每个脚本只能有一个函数。可以有参数，不能有返回值。

## 脚本语法示例

```rust
script {
    // Import the debug module published at the named account address std.
    use std::debug;
 
    const ONE: u64 = 1;
 
    fun main(x: u64) {
        let sum = x + ONE;
        debug::print(&sum)
    }
}
```

## 脚本的限制功能

1、不能直接读写全局存储，而是通过调用已经发布的module的function来间接实现操作全局存储的。

2、不能定义新的好友（模块之间的关系）friends、数据结构类型struct type。
### 2024.09.16
# 模块modules

## 模块定义

1、智能合约的逻辑单位

2、其实就是各种函数、规则等代码。

3、可以CRUD资源resources。

4、提供接口对外操作。

5、有权限控制

6、可以复用。

7、总结的说：定义数据结构struct type，和操作数据结构的函数function。

8、模块只能发布published

9、绑定一个地址

## 模块语法结构

```rust
module <address>::<identifier> {
    (<use> | <friend> | <type> | <function> | <constant>)*
}
```

# 整数

## 整数的类型

1、整数都是无符号整数unsigned integer，其实就是非负整数。

2、u开头，8，16，32，一直到256.

3、如果不注明类型，那么就从上下文推断类型，如果推断不出来就默认u64。

| Type   | Value Range    | 十进制范围 |
| ------ | -------------- | ---------- |
| `u8`   | 0 to 2^8- 1    | 255        |
| `u16`  | 0 to 2^16 - 1  | 65535      |
| `u32`  | 0 to 2^32 - 1  | 42亿       |
| `u64`  | 0 to 2^64 - 1  | /          |
| `u128` | 0 to 2^128 - 1 | /          |
| `u256` | 0 to 2^256 - 1 | /          |

### 不注明整数类型的类型推断方式

1、函数名中函数类型

```rust
let a_u16 = 299;
```

### 类型转换

语法：整数表达式 as 整数类型

```rust
x as u8;
25u64 as u16;
4/2 +12345 as y256;
```

## 整数的值

1、数字序列（推荐）

```rust
let a: u64 = 2;
```

2、数字后带类型（声明变量时候不注明类型）

```rust
let b = 1u256;
```

3、数字的值除了是十进制的，也可以是十六进制的

```rust
let c: u8 = 0x1;
```

### 可以加分隔符的数字值（推荐）

```rust
let hex_u256: u256 = 0x1123_456A_BCDE_F;
let simple_u64: u64 = 1_234_5678;
```

## 整数的运算

### 算数运算

前提：类型必须一致，比如都是u256

```
+ - * / %
```

### 位运算

#### 本位运算

运算会自动换成二进制后进行位运算

| 语法 | 解释 | 详述                         |
| ---- | ---- | ---------------------------- |
| `&`  | 与   | 对每个位进行布尔与运算       |
| `|`  | 或   | 对每个位进行布尔或运算       |
| `^`  | 异或 | 对每个位逐对执行布尔异或运算 |

```rust
module BitwiseExample {
    public fun bitwise_operations() {
        let a: u8 = 0b1100; // 二进制表示的 12
        let b: u8 = 0b1010; // 二进制表示的 10

        let and_result = a & b; // 0b1000 = 8
        let or_result = a | b;  // 0b1110 = 14
        let xor_result = a ^ b; // 0b0110 = 6

        assert(and_result == 8, 1);
        assert(or_result == 14, 2);
        assert(xor_result == 6, 3);
    }
}

```

#### 移位运算

左边是变量，右边是移的位数	

| 语法 | 解释 | 限制条件                                 |
| ---- | ---- | ---------------------------------------- |
| `<<` | 左移 | 要移位的位数大于整数类型的大小，否则终止 |
| `>>` | 右移 | 要移位的位数大于整数类型的大小，否则终止 |

```rust
module ShiftExample {
    public fun shift_operations() {
        let a: u8 = 0b0001_0000; // 二进制表示的 16

        let left_shift_result = a << 2;  // 左移 2 位：0b0100_0000 = 64
        let right_shift_result = a >> 2; // 右移 2 位：0b0000_0100 = 4

        assert(left_shift_result == 64, 1);
        assert(right_shift_result == 4, 2);
    }
}

```

### 比较运算

```
>  < <= >= == !=
```

# 布尔

## 布尔值

true false

## 布尔表达式

值为布尔值的表达式

用于if、while、assert这三个场景。

## 布尔运算

ports three logical operations:

| 语法 | 描述   | 相等操作               |
| ---- | ------ | ---------------------- |
| `&&` | 布尔与 | if (p) q else false    |
| `||` | 布尔或 | if (p) true else q     |
| `!`  | 布尔逆 | if (p) false else true |

# 地址

1、是全局存储global storage中用来表达账户所有权的类型。

2、格式：256-bit，也叫做256比特，256位。同时也是32byte，也叫做32字节。地址的值是16进制，因此是64个十六进制字符。因为比特是二进制的，而字节是八进制的。

## 地址的分类

分为数值地址numerical address和命名地址named address

### 数值地址

其实就是地址以字面量形式来展示，比如

```
0xCAFE
```

### 命名地址

1、用变量名来代表一个地址

2、真实的赋值过程来自于Move.toml这个配置文件的addresses字段或者dev-addresses字段。注意这个赋值不来自于代码中。

#### 示例

配置文件Move.toml进行赋值

```toml
[addresses]
MyAddress = "0x78ab28452bb4ea270fdaaf0459c9cca388011f9982496c441d3cad65f131e731"
```

代码中使用

```rust
module MyModule {
    public fun use_named_address() {
        let named_addr = @MyAddress;  // 使用命名地址
    }
}
```

## 地址在代码中使用（引用）

### 非表达式的地址（直接使用）

1、在非表达式的地址上，直接使用地址

2、无论地址是数值地址还是命名地址

3、非表达式的地址场景包括：模块声明、资源声明、引用命名地址，即use后、module后和resource后。

```rust
// 模块声明
address 0xCAFE {         // 这里的地址是模块所属
    module MyModule {
    }
}
```

```rust
// 模块声明
module OtherModule {
    use MyAddress::MyModule;  // 这里 MyAddress 是命名地址
}
```

```rust
// 资源声明（这个代码可能错误）
resource MyResource { ... }
```

### 表达式地址（前面加@）

表达式中使用地址，前面加@

这和solidity不同，solidity直接使用字面量地址或者变量地址，无论在哪都不加符号区别。

move中无论地址是数值地址还是命名地址，只要在表达式中都加@

表达式的地址场景包括：地址赋值给变量、地址作为参数调用函数、地址作为判断条件、地址参与其它表达式计算

```rust
// 地址赋值
module MyModule {
    public fun use_address() {
        let addr = @0xCAFE;  // 这是一个数值地址表达式，@0xCAFE
        let named_addr = @MyAddress; // 这是一个命名地址表达式，@MyAddress
    }
}
```

```
my_function(@0x123);
```

```
if (@0x789 == some_var) {...}
```

## 
### 2024.09.17
中秋节快乐
### 2024.09.18
## 地址相关操作

### 创建新地址

1、创建一个指定的新地址

生成特定前缀的账户（部署人用于部署合约的账户，因为aptos里没有contract address的概念）

--vanity-prefix参数是自定义的账户名的前缀，在这里值是--vanity-prefix

--output-file是自定义的生成的保存账户地址的文件，在这里值是ace.key

```zsh
aptos key generate --vanity-prefix 0xace --output-file ace.key
```

结果

```json
{
  "Result": {
    "Account Address:": "0xacef1b9b7d4ab208b99fed60746d18dcd74865edb7eb3c3f1428233988e4ba46",
    "PublicKey Path": "ace.key.pub",
    "PrivateKey Path": "ace.key"
  }
}
```

### 

### 地址上链

命令：

```
aptos account create --account 地址
```



```json
{
  "Result": {
    "transaction_hash": "0x4321d286cfc12ee405dfa09ed50375403bf1d180c2d564af3ae0fcbdaf0d9e90",
    "gas_used": 1069,
    "gas_unit_price": 100,
    "sender": "2f49d65a6520b3d13e989fc028d8395eadb9281d8053c1ed6007f3a47b4d4189",
    "sequence_number": 1,
    "success": true,
    "timestamp_us": 1726214222997777,
    "version": 64214470,
    "vm_status": "Executed successfully"
  }
}

```


### 2024.09.19
### 2024.09.20

### 2024.09.21

### 2024.09.22

### 2024.09.23

### 2024.09.24

### 2024.09.25

### 2024.09.26

### 2024.09.27



<!-- Content_END -->
