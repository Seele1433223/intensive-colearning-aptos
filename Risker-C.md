---
timezone: Asia/Shanghai
---

# Risker-C

1. 自我介绍
> 5年传统Web2开发者，熟练掌握CV大法，擅长在摸鱼中工作，喜欢接触新鲜事物，常年5天打鱼2天晒网选手

2. 你认为你会完成本次残酷学习吗？
> 坚持完成

## Notes

<!-- Content_START -->

### 2024.09.07

1. 学习了残酷学习的学习、打卡方式和机制
2. 了解了aptos的基础知识
3. 确认开发工具idea以及插件Move on Aptos
4. 获得了一些aptos学习有关的地址
   1. 问题搜索地址：https://github.com/aptos-labs/aptos-developer-discussions/discussions
   2. 交易查询地址：https://explorer.aptoslabs.com/?network=mainnet
5. 学习了上链操作相关流程

### 2024.09.08
1. 今日按照文档要求搭建了本地的环境
2. 编写、运行并部署了TodoList的demo
```
{
  "Result": {
    "transaction_hash": "0x742a8b3f0a0c2c230d99941d73435c99f3446d554c9f4d8240ee7af519fbdac6",
    "gas_used": 1910,
    "gas_unit_price": 100,
    "sender": "c0910143714a05b5acf337081d3f073fe13803dca207061a46e8a94f10a7b72c",
    "sequence_number": 0,
    "success": true,
    "timestamp_us": 1725801761892122,
    "version": 59281741,
    "vm_status": "Executed successfully"
  }
}
```
3. 后续进行React前端项目的开发，并实现与合约的交互功能

### 2024.09.09
1. 按照官方文档创建了React Client项目
2. 根据指引安装了 **@aptos-labs/wallet-adapter-react**, **@aptos-labs/wallet-adapter-ant-design**用于提供钱包连接能力和UI组件的依赖包
3. 浏览器安装petra钱包，并在client项目中安装了**petra-plugin-wallet-adapter**钱包适配器依赖，并实现了钱包的连接

### 2024.09.10
1. 在Client项目中，实现与部署在devnet上的合约进行交互，首先实现获取账户的todolist列表
2. 实现为当前账户创建todolist的功能，实现调用合约方法，并成功使用钱包进行了支付操作，使用react成功做成了第一笔交易
```
0xc0910143714a05b5acf337081d3f073fe13803dca207061a46e8a94f10a7b72c
```
### 2024.09.11
1. 成功完成React与合约TodoList的所有方法交互，实现task新增和状态修改等功能
2. 将本次的项目代码发布到仓库: <https://github.com/Risker-C/my-first-dapp>
### 2024.09.12

1. 今日通宵加班，请假

### 2024.09.13

1. 学习Modules 和 Scripts的区别：Modules用于定义函数，Scripts用于调用Modules中的函数
2. 学习基础变量知识
### 2024.09.14

1. 学习地址类型、向量、作用域等概念

### 2024.09.15

1. 系统学习基础语法：相等、中止、循环、函数

### 2024.09.16

1. 学习了结构和资源内容

### 2024.09.17

1. 学习枚举类型和常量
   
### 2024.09.18

1. 参加今日课程 构建并部署代币水龙头

### 2024.09.19

### 2024.09.20
1. 学习FA内容
```
<!-- Content_END -->
