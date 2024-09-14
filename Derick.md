### Derick
- web3开发者
- 希望通过这次共学能使用move在aptos部署一个应用


## Notes

<!-- Content_START -->

### 2024.09.07
 -  [x] 推荐的aptos钱包  ：https://petra.app/
 -  [x] 在jbIDE中安装move on aptos
 -  [x] move[学习文档](https://aptos.dev/en/build/smart-contracts/why-move)
 -  [x] aptos[浏览器](https://explorer.aptoslabs.com/analytics?network=mainnet)
 -  [ ] aptos讨论区：https://github.com/aptos-labs/aptos-developer-discussions/discussions
- Move 合约升级的特点
- 包（Package）为单位: Move 合约是以包为单位进行组织和部署的。升级时，需要重新部署整个包。
- 严格的类型系统: Move 的严格类型系统确保了合约升级的安全性，防止意外的数据损坏或逻辑错误。
- 资源的移动和销毁: Move 中的资源不能被随意复制，只能通过明确的移动操作进行传递。这使得在升级过程中对资源的管理更加安全。
- 灵活的升级方式: Move 提供了多种升级方式，可以根据不同的需求选择合适的升级策略。
- Move 合约升级的常见方式
- 重新部署:

- 直接覆盖: 将新的包部署到相同的地址，覆盖旧的包。这种方式简单直接，但需要注意，所有状态数据都会丢失。
- 数据迁移: 在部署新包之前，将旧包中的状态数据迁移到新的包中。这种方式比较复杂，但可以保留原有的数据。
- 分阶段升级:

- 逐步升级: 将升级分成多个阶段，每个阶段只修改部分功能，以降低风险。
- 兼容性考虑: 在升级过程中，需要确保新旧版本之间的兼容性，避免出现不兼容的问题。
### 2024.09.08
Aptos采用了一种改进的BFT(拜占庭容错)共识机制,称为AptosBFT或DiemBFT,具有以下几个关键特点来确保网络安全:

1. 领导者轮换机制改进:
   AptosBFT增加了节点信誉系统(State-Machine Replication, SMR),通过检查链上数据来跟踪活跃节点,并从中选举领导者. 这可以避免故障节点被选为领导者,提高网络稳定性.

2. 快速区块确认:
   通过改进的协议,区块只需两次网络往返即可提交,实现亚秒级的最终确定性. 这大大缩短了交易确认时间.

3. 容错能力:
   AptosBFT可以容忍最多1/3的验证者节点出现故障或恶意行为. 只要有2/3以上的诚实节点,网络就能正常运行.

4. 主动起搏器:
   AptosBFT添加了主动起搏器,使用超时来同步验证器,比等待增加的超时更快.

5. 安全性验证:
   AptosBFT的共识协议已经过审计和正式验证,确保其安全性.

6. 网络活性与安全分离:
   Aptos的协议将网络活性与安全性清晰分开,即使网络中断,只要BFT机制的诚实保证得到维护,就不需要分叉区块链.

### 2024.09.09
 -  [ ] 学习[Move Tutorial](https://github.com/aptos-labs/aptos-core/tree/main/aptos-move/move-examples/move-tutorial) 前三章
### 2024.09.10
```
module 0xCAFE::basic_coin {
    struct Coin has key {
        value: u64,
    }

    public entry fun mint(account: &signer, value: u64) {
        move_to(account, Coin { value })
    }
}
```
- 创建一个move合约，定义了一个名为 basic_coin 的模块，属于地址 0xCAFE。在 Move 中，模块是代码的基本组织单位。
- 名为 Coin 的结构体。它有一个 key 能力，意味着它可以作为全局存储中的顶级资源。结构体包含一个名为 value 的字段，类型为 u64（64位无符号整数）。
- 定义了一个名为 mint 的公共入口函数。它有两个参数：account: &signer：代表交易发送者的签名者引用。 value: u64：要铸造的代币数量。函数体使用 move_to 操作将新创建的 Coin 资源移动到 account 的存储中。这effectively "铸造"了新的代币并将其分配给指定账户。
### 2024.09.11
```
#[test(account = @0xC0FFEE)]
fun test_mint_10(account: &signer) acquires Coin {
    let addr = signer::address_of(account);
    mint(account, 10);
    assert!(borrow_global<Coin>(addr).value == 10, 0);
}
```
- #[test(account = @0xC0FFEE)] 声明这是一个测试，并为测试提供一个地址为 0xC0FFEE 的签名者。
acquires Coin 表示这个函数会访问 Coin 资源。
测试逻辑：
获取账户地址
调用 mint 函数铸造 10 个代币
使用 assert! 检查该地址下的 Coin 资源的 value 是否为 10
### 2024.09.12
```
public fun mint(module_owner: &signer, mint_addr: address, amount: u64) acquires Balance { .. }
这个函数用于铸造代币。只有模块所有者可以调用此函数。它需要访问 Balance 资源。
public fun balance_of(owner: address): u64 acquires Balance { .. }
这个函数用于查询指定地址的余额。它需要访问 Balance 资源。
public fun transfer(from: &signer, to: address, amount: u64) acquires Balance { .. }
这个函数用于转账。它需要访问 Balance 资源。
```
### 2024.09.13
 -  [ ] 
### 2024.09.14
 -  [ ] 
### 2024.09.15
 -  [ ] 
### 2024.09.16
 -  [ ] 
### 2024.09.17
 -  [ ] 
### 2024.09.18
 -  [ ] 
### 2024.09.19
 -  [ ] 
### 2024.09.20
 -  [ ] 
### 2024.09.21
 -  [ ] 
### 2024.09.22
 -  [ ] 
### 2024.09.23
 -  [ ] 
### 2024.09.24
 -  [ ] 
### 2024.09.25
 -  [ ] 
### 2024.09.26
 -  [ ] 
### 2024.09.27
 -  [ ] 

<!-- Content_END -->
