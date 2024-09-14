---
timezone: Asia/Shanghai # 北京时间 (UTC+8)
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)

timezone: America/Anchorage # 阿拉斯加标准时间 (UTC-9)

timezone: America/Los_Angeles # 太平洋标准时间 (UTC-8)

timezone: America/Denver # 山地标准时间 (UTC-7)

timezone: America/Chicago # 中部标准时间 (UTC-6)

timezone: America/New_York # 东部标准时间 (UTC-5)

timezone: America/Halifax # 大西洋标准时间 (UTC-4)

timezone: America/St_Johns # 纽芬兰标准时间 (UTC-3:30)

timezone: America/Sao_Paulo # 巴西利亚时间 (UTC-3)

timezone: Atlantic/Azores # 亚速尔群岛时间 (UTC-1)

timezone: Europe/London # 格林威治标准时间 (UTC+0)

timezone: Europe/Berlin # 中欧标准时间 (UTC+1)

timezone: Europe/Helsinki # 东欧标准时间 (UTC+2)

timezone: Europe/Moscow # 莫斯科标准时间 (UTC+3)

timezone: Asia/Dubai # 海湾标准时间 (UTC+4)

timezone: Asia/Kolkata # 印度标准时间 (UTC+5:30)

timezone: Asia/Dhaka # 孟加拉国标准时间 (UTC+6)

timezone: Asia/Bangkok # 中南半岛时间 (UTC+7)

timezone: Asia/Shanghai # 中国标准时间 (UTC+8)

timezone: Asia/Tokyo # 日本标准时间 (UTC+9)

timezone: Australia/Sydney # 澳大利亚东部标准时间 (UTC+10)

timezone: Pacific/Auckland # 新西兰标准时间 (UTC+12)

---

# {你的名字}

1. 自我介绍
    Qiao Pengjun 乔鹏军。有Python、Go、Rust、solidity的开发经验。大约是去年开始了解Web3，最近在学习solidity。对区块链技术很感兴趣。了解了一点Solana、Sui、Starknet... 正在继续学习。希望本次学习能让我更深入的了解Web3。拥抱Web3，拥抱未来。
2. 你认为你会完成本次残酷学习吗？
   我认为我会完成本次残酷学习，因为我有信心，并且我相信我能够克服任何困难。

## Notes

<!-- Content_START -->

### 2024.09.07

Aptos 区块链上的每个账户都由一个 32 字节的账户地址标识。
与其他区块链中账户和地址隐式不同，Aptos 上的账户是显式的，需要先创建才能执行交易。
可以通过将 Aptos 代币 (APT) 转移到 Aptos 来显式或隐式创建账户。

Aptos 上有三种类型的账户：

标准账户——这是一个典型的账户，对应一个地址和一对相应的公钥/私钥。
资源账户- 一个没有对应私钥的自主账户，供开发者存储资源或上链发布模块。
对象- 存储在代表单个实体的单个地址内的一组复杂资源。

帐户地址为 32 字节。它们通常显示为 64 个十六进制字符，每个十六进制字符为一个半字节。有时地址以 0x 为前缀。
Aptos区块链默认采用Ed25519签名交易。

Aptos 区块链存储三种类型的数据：

交易：交易表示区块链上的账户正在执行的预期操作（例如转移资产）。
状态：（区块链账本）状态代表交易执行输出的累积，即存储在所有资源内的价值。
事件：交易执​​行时发布的辅助数据。
只有交易才能改变账本状态。

<https://aptos.dev/en/build/get-started/developer-setup>

Install the Aptos CLI on Mac

```bash
brew update
brew install aptos

aptos help

brew update
brew upgrade aptos

intensive-colearning-aptos on  main via 🅒 base took 4.3s 
➜ aptos --version              
aptos 4.1.0


Code/Aptos/hello_aptos via 🅒 base
➜
aptos init
Configuring for profile default
Choose network from [devnet, testnet, mainnet, local, custom | defaults to devnet]
devnet
Enter your private key as a hex literal (0x...) [Current: None | No input: Generate new key (or keep one if present)]

No key given, generating key...
Account 0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35 doesn't exist, creating it and funding it with 100000000 Octas
Account 0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35 funded successfully

---
Aptos CLI is now set up for account 0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35 as profile default!
 See the account here: https://explorer.aptoslabs.com/account/0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35?network=devnet
 Run `aptos --help` for more information about commands
{
  "Result": "Success"
}
                                                                                                                                              

Code/Aptos/hello_aptos via 🅒 base took 1m 32.7s
➜
aptos account list
{
  "Result": [
    {
      "0x1::account::Account": {
        "authentication_key": "0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35",
        "coin_register_events": {
          "counter": "0",
          "guid": {
            "id": {
              "addr": "0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35",
              "creation_num": "0"
            }
          }
        },
        "guid_creation_num": "2",
        "key_rotation_events": {
          "counter": "0",
          "guid": {
            "id": {
              "addr": "0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35",
              "creation_num": "1"
            }
          }
        },
        "rotation_capability_offer": {
          "for": {
            "vec": []
          }
        },
        "sequence_number": "0",
        "signer_capability_offer": {
          "for": {
            "vec": []
          }
        }
      }
    }
  ]
}
                                                                                                                                              

Code/Aptos/hello_aptos via 🅒 base took 2.5s
➜
aptos account fund-with-faucet --account 0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35
{
  "Result": "Added 100000000 Octas to account 0xee6c038b66df7ed8aa91eb700938003ce29647f402c090ededd89b87a3c70e35"
}
                                                                                                                                              

Code/Aptos/hello_aptos via 🅒 base took 2.8s
➜
touch StudyAptosNotes.md
                                                                                                                                              

Code/Aptos/hello_aptos via 🅒 base
➜
open -a Typora StudyAptosNotes.md
                                                                                                                                              


Code/Aptos/hello_aptos via 🅒 base
➜
ls
StudyAptosNotes.md assets

Code/Aptos/hello_aptos via 🅒 base
➜
ls -a
.                  ..                 .aptos             StudyAptosNotes.md assets

Code/Aptos/hello_aptos via 🅒 base
➜
cd .aptos/

Aptos/hello_aptos/.aptos via 🅒 base
➜
ls
config.yaml

Aptos/hello_aptos/.aptos via 🅒 base
➜
c
```

<https://aptos.dev/en/build/cli/install-cli/install-cli-mac>
<https://www.youtube.com/watch?v=_EFoVYcrbiY>
<https://plugins.jetbrains.com/plugin/14721-move-on-aptos>
<https://move-developers-dao.gitbook.io/aptos-move-by-example>
<https://marketplace.visualstudio.com/items?itemName=movingco.move-analyzer-plus>
<https://www.youtube.com/watch?v=87eeYsstBD4>

### 2024.09.08

[idea 配置 aptos](https://docs.pontem.network/02.-move-language/intellij_ide_extension)

创建项目

```bash
mkdir hello_optos
cd hello_aptos
```

初始化项目

```bash
aptos move init --name hello_aptos
```

初始化账户

```shell
aptos init
```

编译

```shell
aptos move compile
```

测试

```shell
aptos move test
```

部署

```shell
aptos move publish --named-address hello_aptos
➜ aptos move publish --named-addresses my_addrx=3b551727cac1bd5dc45023b869c9e37dd9e1830fc02ffe32f19597a668ba906d
```

运行

```shell
aptos move run --function-id 0x1::hello_aptos::greet --args "hello"
```

### 2024.09.09

Move 语言与变量
变量是什么？
变量是存储数据值的容器，可以用来存储和操作数据。在 Move 语言中，变量可以用来存储整数、布尔值、字符串等数据类型。
变量：是有名字的对象
对象：存储某个类型值的内存区域
值：按照类型进行解释的bytes集合
类型：定义可能值的操作
类型系统：定义类型和值之间的关系
值类型是如何存储的？
值类型，意为简单的类型，其主要特征是数量量较小，常见有以下类型：
布尔类型
整数
浮点数
枚举
字符串
堆类型值的指向
...

引用类型是如何存储的？
引用类型，意为复杂类型，其主要特征是数量量较大，常见有以下类型：
结构体
数组
向量
函数
模块
对象
类
...

Move 语言中的变量是如何存储的？
Move 语言中的变量分为值类型变量和引用类型变量，它们的存储方式有所不同。
值类型变量：直接存储在栈上，不需要额外的内存分配。
引用类型变量：存储在堆上，需要通过引用来访问。

值类型与引用类型的关系
通常我们定义一个变量为对象时，其对象的值存储在堆上，其堆内存的索引存储在栈上，用栈上的索引指向堆上存储的引用类型数据。

Move 的核心差异之一
在值类型与引用类型关系上，不同于其他语言的索引方式。而是以“所有权”来作为引用类型的操作。

1. 所有权只能同时由 1 “人” 拥有
2. 所有权以转移的形式流转给其他变量

这样做有什么好处？

1. 避免内存泄露，不同于其他语言，在编译阶段就可以告知什么时候可以回收内存
2. 提高内存使用效率，避免对引用类型的不必要拷贝
3. 更好的可读性和可维护性

### 2024.09.10

UINT/ STRING/ BOOL 与 ADDRESS 四大类型

```rust
module 0x42::Types {
    use std::debug::print;
    use std::string;
    use std::string::{String, utf8};

    #[test]
    fun test_num() {
        let num_u8: u8 = 42; // 0~2**8-1
        let num_u8_2 = 43u8;
        let num_u8_3 = 0x2A; // hash

        let num_u256: u256 = 100_000;

        let num_sum = (num_u8 as u256) + num_u256;
        print(&num_u8);
        print(&num_u8_2);
        print(&num_u8_3);
        print(&num_u256);
        print(&num_sum);
    }

    #[test]
    fun test_bool() {
        let bool_true: bool = true;
        let bool_false: bool = false;
        print(&bool_true);
        print(&bool_false);
        print(&(bool_true == bool_false));
    }

    #[test]
    fun test_string() {
        let str: String = utf8(b"Hello, Move!");
        print(&str);
    }

    #[test]
    fun test_addr() {
        let addr: address = @0x42;
        let addr_2: address = @0x00000000000000000000000000000000000000000A;

        print(&addr);
        print(&addr_2);
    }
}

```

### 2024.09.11

APTOS-MOVE
VECTOR 向量核心特性 1
基础概念
Vector（向量）类似其它语言中的数组， 内部存储的是同一类型的数据。

| 语法              | 描述                 |
| ----------------- | -------------------- |
| vector[]          | 空数组               |
| vector[e1,...,en] | 具有同类型元素的数组 |

增删改查功能

<https://aptos.dev/en/build/smart-contracts/book/vector>

函数修饰符
核心概念
函数修饰符是用来赋予函数特殊能力的一组关键字。主要有以下几类

- 可见性
  - 无Public，私有函数，仅限 module 内部调用
  - friend public，模块内部函数，同包模块之间可以调用
  - Public，模块公开函数，所有模块都可以调用
- 全局存储引用
  - acquires，当需要使用 move_from，borrow_global，borrow_global_mut 访问地址下的资源的时候，需要使用 acquires 修饰符
- 链下
  - entry，修饰后，该方法可由链下脚本调用

### 2024.09.12

APTOS-MOVE
STRUCT 特性解读
核心概念
Aptos Move 的 Struct 结构体用于存储结构化数据。Struct 可以相互嵌套，并可以作为资源存储在特定地址下。”

1. 命名必须以大写字母开头
2. 可以通过 has 关键字赋予能力

```rust
struct Person {
  ape: u8,
  birthday: u32,
}

struct People {
  people: vector<Person>,
}
```

修饰符
Copy - 值能够被复制
Drop - 值可以在作用域结束时被自动清理
Key - 值可以用作于全局存储的键 Key
Store - 值可以存储在全局存储中

除 Struct 类型外，其他的类型默认具备 store、drop、copy 的能力，Struct 最终是存储在用户的地址上（或者被销毁），不存在 Aptos 合约里，Aptos 合约是一个全纯的函数。

Drop
值能够在使用结束后被销毁

```rust
//drop
struct Coin {
  b: bool
}

#[test]
fun test6() {
  let c = Coin { b: true }; // 会报错
}

//drop
struct Coin has drop {
  b: bool,
}

#[test]
fun test6() {
  let c = Coin { b: true };
}

```

copy
值能够在使用结束后被复制

```rust
//copy
struct CanCopy has drop {
  b: bool,
}

#[test]
fun test5() {
  let c = CanCopy { b: true };
  let c1 = c; // no copy
  let CanCopy { b } = &mut c1;
  *b = false;
  debug::print(&c1.b);
}
```

```rust
// copy
struct CanCopy has copy, drop {
  b: bool,
}

#[test]
fun test5() {
  let c = CanCopy { b: true };
  let c1 = c; // copy
  let CanCopy { b } = &mut c1;
  *b = false;
  debug::print(&c1.b);
  debug::print(&c.b);
}
```

Key
值可以用作于全局存储的键 Key

```rust
//key
struct Coin has key {
  value: u64,
}

public entry fun mint(account: &signer, value: u64) {
  move_to(account, Coin { value });
}

#[test(account = @0x42)]
public fun test_mint(account: &signer) acquires Coin {
  let addr = signer::address_of(account);
  mint(account, 100);
  let coin = borrow_global<Coin>(addr).value;
  debug::print(&coin);
}
```

store
值可以被全局存储，通常配合Key使用

```rust
//store
struct Key has key, drop {
  a: Store,
}

struct Store has store, drop {
  b: bool,
}

#[test]
fun test6() {
  let k = Key {
    a: Store { b: true },
  };
  debug::print(&k.a.b);
}
```

父 的有 Key 子的必须有 stare

```rust
//store
struct Key has key, drop {
  a: Store,
}

struct Store has drop {
  b: bool,
}

#[test]
fun test6() {
  let k = Key {
    a: Store { b: true },
  };
  debug::print(&k.a.b); // 会报错
}
```

<https://aptos.dev/en/build/smart-contracts/book/structs-and-resources>
<https://aptos.dev/en/build/smart-contracts/book/abilities>

### 2024.09.13

函数操作流IF、WHILE、LOOP

```rust
module 0x42::Demo3 {
    use std::debug;

    #[test]
    fun test_if() {
        let x = 5;
        let x2 = 10;
        if (x == 5) {
            debug::print(&x);
        } else {
            debug::print(&x2);
        }
    }

    #[test]
    fun test_while() {
        let  x = 0;
        while (x < 10) {
            debug::print(&x);
            x = x + 1;
        }
    }

    #[test]
    fun test_while2() {
        let  x = 5;
        while (x < 10) {
            debug::print(&x);
            x = x + 1;

            if (x == 7) {
                break;
            }
        }
    }

    #[test]
    fun test_while3() {
        let  x = 5;
        while (x < 10) {
            x = x + 1;
            if (x == 7) {
                continue;
            };
            debug::print(&x);
        }
    }

    #[test]
    fun test_loop() {
        let x = 5;
        loop {
            x = x + 1;
            if (x == 7) {
                break;
            };
            debug::print(&x);
        }
    }

    #[test]
    fun test_loop2() {
        let x = 5;
        loop {
            x = x + 1;
            if (x == 7) {
                continue;
            };
            if (x == 10) {
                break;
            };
            debug::print(&x);
        }
    }
}
```

模块的特性
引用
可以通过以下三种方式导入模块，用来更好的进行管理。注意命名不能重复。

```rust
use std::debut;
use std::debug::print;
use std::debug::{print as P, native_print, print};

fun main() {
  debug::print(&v);
  print(&v);
  P(&v);
}
```

作用域
可以在全局定义，也可以定义在函数内部，只在所在的作用域内有效。

```rust
fun main() {
  use std::debug::print;
  print(&v);
}

public(friend) 
声明当前模块信任用模块，受信任模块可以调用当前模块中具有 public(friend) 的可见性函数

public
声明当前模块对外供其他接口调用的方法。

entry
声明可被链下调用的模块方法。

模块的发布与交互
发布流程
1. 配置账户，并为其发送 gas
  可以通过 aptos init 来初始化一个账户。
2. 编译并测试模块
  可以通过以下命令来编译
  aptos move compile --named-addresses hello_blockchain=default
3. 发布模块
  aptos move publish --named-addresses hello_blockchain=default

交互流程
1. 区块链浏览器
  https://explorer.aptoslabs.com/
2. 终端
  aptos move run --function-id 'default::message::set_message' --args 'string:hello, blockchain'

3. SDK
  https://aptos.dev/en/build/sdks

### 2024.09.14

认识 OBJECT
什么是 Aptos object？
1. 对象是单个地址的资源容器，用于储存资源
2. 对象提供了一种集中式资源控制与所有权管理的方法

创建并转移对象实例
我们可以通过 aptos_framework 库下的 object 来实现对象的功能。
```rust
module my_addr::object_playground {
  use std::signer;
  use aptos_framework::object::{self, ObjectCore};

  entry fun create_and_transfer(caller: &signer, destination: address) {
    // Create object
    let caller_address = signer::address_of(caller);
    let constructor_ref = object::create_object(caller_address);

    // Set up the object

    // Transfer to destination
    let object = object::object_from_constructor_ref<ObjectCore>(&constructor_ref);
    object::transfer(caller, object, destination);
  }
}
```

两类对象
可删除对象
不可删除对象

- 命名对象，通过固定的 signer 和特定的 seed 生成唯一地址的对象，1个地址只能生成1个
- 粘性对象，通过 signer 生成的对象，1个地址可以生成多个
  
### 2024.09.15

笔记内容

### 2024.09.16

笔记内容

### 2024.09.17

笔记内容

### 2024.09.18

笔记内容

### 2024.09.19

笔记内容

### 2024.09.20

笔记内容

### 2024.09.21

笔记内容

### 2024.09.22

笔记内容

### 2024.09.23

笔记内容

### 2024.09.24

笔记内容

### 2024.09.25

笔记内容

### 2024.09.26

笔记内容

### 2024.09.27

笔记内容

### 2024.09.28

笔记内容

### 2024.09.29

笔记内容

### 2024.09.30

笔记内容

### 2024.10.01

笔记内容

### 2024.10.02

笔记内容

### 2024.10.03

笔记内容

### 2024.10.04

笔记内容

### 2024.10.05

笔记内容

### 2024.10.06

笔记内容

### 2024.10.07

笔记内容

### 2024.10.08

笔记内容

### 2024.10.09

笔记内容

<!-- Content_END -->
