---
timezone: Asia/Shanghai
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
我叫kizy，是一名在校大学生。
2. 你认为你会完成本次残酷学习吗？
我会尽力学习的。


<!-- Content_START -->

### 2024.09.07

今日学习了解内容：
1.较为推荐的开发环境：IDEA
2.推荐的aptos钱包：https://petra.app/
3.aptos讨论区：https://github.com/aptos-labs/aptos-developer-discussions/discussions
4.APTOS定义与介绍//中文
5. 更多的还是了解到aptos网站—— https://learn.aptoslabs.com/zh




课后学习内容：
一． 移动合约升级的常见方式介绍：
1.	直接部署
2.	直接覆盖
3.	数据迁移
4.	阶段升级——降低风险——考虑兼容性（主要是版本方面）

未解决问题&待完成工作：
1.	验证器和信标链是同个东西吗？
2.	根据直播剪辑视频及群文档回归内容

### 2024.09.10
关于这几天环境配置小结
下载安装aptos cli
1.	下载aptoscli参考网站：https://aptos.dev/ （下载windows版本）
2.	复制aptos.exe文件路径 配置到环境变量path中
3.	在终端输入aptos help——有指令返回时，确认aptos能用
 
4.	进入终端
•  创建或进入你的 Move 项目目录：
cd D:/aptosmove
•  初始化项目（如果还未初始化）：
复制代码
aptos move init --package-name my_move_project

这个操作会在根目录自动生成Move.toml和source文件夹
5.	安装后 在idea下载配置aptos插件
 
 
环境变量路径与刚刚配置的一致
 
6.	随便写一小段 尝试运行
script {
use 0x1::Debug;

fun main(){
  let num:u64 = 1024;
Debug ::print(&num);
    }
}
7.	运行显示：
Compiling, may take a little while to download git dependencies...
FETCHING GIT DEPENDENCY https://github.com/aptos-labs/aptos-core.git

最后出现error报错
 
8.在终端尝试重新编译：
aptos move compile
报错仍然相同

9.	在根目录找到Move.toml文件（我用的记事本编辑）
编辑，把 move.toml 的地址改成 https://gitee.com/WGB5445/aptos-core.git

[dependencies.AptosFramework]
#git = "https://github.com/aptos-labs/aptos-core.git"#rev = "devnet"
#subdir ="aptos-move/framework/aptos-framework"Local ="../aptos-core/aptos-move/framework/aptos-framework"


ps:关于build 和 compile 的时候 --named-addresses 这个参数是不是必须的？
A：带不带取决于 move.toml 写的是 “_” 还是 0x1234 这种地址，是地址就不用带

### 2024.09.11

配置环境：
1.	rust环境
https://www.rust-lang.org/
2.	aptos move环境
https://aptos.dev/tools/aptos-cli/use-cli/use-aptos-cli 
3.	初始化move项目
Aptos move init -- name lesson1
 
4.	初始化账户
Aptos init
得到地址：0x528d636f35c74440ec5978aafaf2e40d49bb68abb32c5c3b93569bcaeb12e800

认识项目结构
	Move.toml //项目的配置，如项目名称，项目地址，第三方包
	.aptos // 模块所指向的账户及项目配置信息（通过aptos init生成）
——config.yaml
	-scripts // 脚本文件，用来调用模块(用的少)-sources // 模块文件夹，模块和测试可以放在这里面
	-tests // 测试文件，用来写测试用例(用的少)

config.yaml：
保存账户的私钥，公钥，账户，节点以及水龙头地址
当账号创建好后，会自动在水龙头领取测试token


Move.toml:
Addresses:常规环境
Dev-addresses:开发环境
git 拉取的仓库
rev 分支名
subdir 相对路径

### 2024.09.12
利用use引入标准库，std即标准库的意思
引入string库 use：：std：：string::utf8

Test时需要使用魔法：在终端使用命令（clash-port-powershell）

书写helloworld代码并编译测试成功
 
【Helloworld代码.代码仓库1-002】

Move语言与变量
值类型：布尔类型，整数，浮点数，枚举，字符串，堆类型的指向……
引用类型：对象，类，数组，函数……
二者关系：可以通过值类型找到堆类型。
当定义一个变量为对象时，其对象的值存储在栈上，用栈上的索引指向堆上存储的引用类型数据

在值类型与引用类型的关系上，move特别的索引方式：以“所有权”来作为引用类型的操作。
 
1.	所有权只能同时由1“人”拥有（两人不能同时拥有一个苹果）
2.	所有权以转移的方式流转给其他变量

这样做有什么好处?
1.避免内存泄露，不同于其他语言，在编译阶段就可以告知什么时候可以回收内存
2.提高内存使用效率，避免对引用类型的不必要拷贝;
3.更好的可读性和可维护性;


用代码演示：
 
【代码.代码仓库2-001】
通过代码可以看出当wallet所有权转移给wallet2时，wallet就被移除



<!-- Content_END -->
