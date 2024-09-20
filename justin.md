---
timezone: Asia/Shanghai
---

---

# justin

1. 自我介绍 <br>
   我是justin
2. 你认为你会完成本次残酷学习吗？<br>
   可以

## Notes

<!-- Content_START -->

### 2024.09.06
了解Aptos残酷共学的规则，并报名。

### 2024.09.07
参与了aptos 101会议分享，了解了大致学习资料和内容

### 2024.09.08

学习aptos文档 https://aptos.dev/en/network/blockchain

### 2024.09.09

学习 aptos 账户

aptos 账户
有两个first-class features
1. 更改认证密钥 类似于web2的改密码
2. 原生多签支持

三种类型的账户
1. 标准账户 Standard account
带有public/private keys
2. Resource账户
没有private key，开发者用来存储资源或者发布模块到链上
3. Object
一系列资源存储在一个地址上

### 2024.09.10
Signer 里面有一个address
module 0x1::signer {
    struct signer has drop { a: address }
}

signer::address_of(&signer): address
signer::borrow_address(&signer): &address

Global Storage
move_to<T>(&signer, T)
move_from<T>(address): T
borrow_global_mut<T>(address): &mut T
borrow_global<T>(address): &T
exists<T>(address): bool

### 2024.09.11
Move Objects 
可以往地址转入object

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

### 2024.09.12
创建object
有三种类型
1. normal Object 
可删除、随机地址
let caller_address = signer::address_of(caller);
let constructor_ref = object::create_object(caller_address);

2. named Object
自定义名字的object
不可删除、固定地址
const NAME: vector<u8> = b"MyAwesomeObject";

entry fun create_my_object(caller: &signer) {
    let caller_address = signer::address_of(caller);
    let constructor_ref = object::create_named_object(caller, NAME);
    // ...
}

3. sticky Object
不可删除、随机地址
let caller_address = signer::address_of(caller);
let constructor_ref = object::create_sticky_object(caller_address);

### 2024.09.13
通过object::generate_signer可以创建singer来允许你往object传递资源过去
let caller_address = signer::address_of(caller);

// Creates the object
let constructor_ref = object::create_object(caller_address);

// Retrieves a signer for the object
let object_signer = object::generate_signer(&constructor_ref);

// Moves the MyStruct resource into the object
move_to(&object_signer, MyStruct { num: 0 });

### 2024.09.16
扩展性 ExtendRef
ContructorRef 只有创建object的时候存在，后面就销毁了
ExtendRef可以作为资源发给object储存下来，后面可以继续拿出来对object进行新的操作

// 往object传入一个extend_ref资源
let extend_ref = object::generate_extend_ref(&constructor_ref);
move_to(&object_signer, ObjectController { extend_ref });

### 2024.09.18
aptos sdk学习
async mintCoin(minter: AptosAccount, receiverAddress: HexString, amount: number | bigint): Promise<string> {
    const rawTxn = await this.generateTransaction(minter.address(), {
      function: "0x1::managed_coin::mint",
      type_arguments: [`${minter.address()}::justin_coin::JustinCoin`],
      arguments: [receiverAddress.hex(), amount],
    }, customOpts);

    await this.simulateTransaction(minter, rawTxn).then((sims) =>
      sims.forEach((tx) => {
        if (!tx.success) {
          throw new Error(`Transaction failed: ${tx.vm_status}\n${JSON.stringify(tx, null, 2)}`);
        }
      }),
    );

    const bcsTxn = await this.signTransaction(minter, rawTxn);
    const pendingTxn = await this.submitTransaction(bcsTxn);

    return pendingTxn.hash;
  }

### 2024.09.19
async transferCoin(sender: AptosAccount, receiverAddress: HexString, amount: number | bigint): Promise<string> {
    const rawTxn = await this.generateTransaction(sender.address(), {
      function: "0x1::aptos_account::transfer_coins",
      type_arguments: [`${sender.address()}::justin_coin::JustinCoin`],
      arguments: [receiverAddress.hex(), amount],
    });

    const bcsTxn = await this.signTransaction(sender, rawTxn);
    const pendingTxn = await this.submitTransaction(bcsTxn);

    return pendingTxn.hash;
  }
  
### 2024.09.20
Global Storage
move_to<T>(&signer, T)
move_from<T>(address): T
borrow_global_mut<T>(address): &mut T
borrow_global<T>(address): &T
exists<T>(address): bool

T要求有key的能力

Global Storage返回的ref不能作为函数的参数返回

acquires 要求类型
m::f 要求 acquires T 
1. m::f 包含 move_from<T> borrow_globnal_mut<T> borrow_global<T>
2. m::f 调用的 m::g 在同一个模块中acquires T

<!-- Content_END -->
