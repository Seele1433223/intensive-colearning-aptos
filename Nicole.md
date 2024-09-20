---
timezone: Asia/Shanghai
---

# Nicole

1. 自我介绍
   * 大家好，我是Nicole，对于Defi感兴趣，希望可以get一些前沿技术在玩儿什么hh。
   
3. 你认为你会完成本次残酷学习吗？
   * 努力！

## Notes

<!-- Content_START -->

### 2024.09.07

1. 学习了残酷学习的学习、打卡方式和机制
2. 了解了aptos的基础知识
* 确认开发工具idea以及插件Move on Aptos
* 明确了学习资料的地址
  问题搜索地址：https://github.com/aptos-labs/aptos-developer-discussions/discussions
  
  交易查询地址：https://explorer.aptoslabs.com/?network=mainnet

### 2024.09.08

1. 学习配置开发环境
2. 浏览Aptos白皮书
    Aptos 区块链设计原则：扩展性、安全性、可靠性和可升级性。
  * 首先，Aptos 区块链原生集成并在内部使用 Move 语言进行快速和安全的交易执行。Move 验证器是一个用于用 Move 语言编写的智能合约的形式验证器，为合约不变量和行为提供额外的保障。这种对安全的关注使开发者能够更好地保护他们的软件免受恶意实体的攻击。
  * 其次，Aptos 数据模型支持灵活的密钥管理和混合托管选项。这与在签名前的交易透明度和实用的轻客户端协议一起，提供了更安全和更值得信赖的用户体验。
  * 第三，为了实现高吞吐量和低延迟，Aptos 区块链在交易处理的关键阶段采用流水线和模块化方法。具体来说，交易传播、块元数据排序、并行交易执行、批量存储和账本认证都同时进行。这种方法充分利用所有可用的物理资源，提高硬件效率，并实现高度并行执行。
  * 第四，与其他需要预先知道要读写的数据从而打破交易原子性的并行执行引擎不同，Aptos 区块链不会对开发者施加这样的限制。它可以有效地支持任意复杂交易的原子性，为实际应用提供更高的吞吐量和更低的延迟，并简化开发。
  * 第五，Aptos 模块化架构设计支持客户端的灵活性，并针对频繁和即时升级进行了优化。此外，为了快速部署新技术创新并支持新的 Web3 用例，Aptos 区块链提供了嵌入式链上变更管理协议。最后，Aptos 区块链正在试验未来的举措，以超越单个验证器的性能进行扩展：其模块化设计和并行执行引擎支持验证器的内部分片，同质状态分片为水平吞吐量可扩展性提供了潜力，而不会给节点运营商增加额外的复杂性。
   
### 2024.09.09

1. Aptos 节点是 Aptos 生态系统的一个实体，用于跟踪 Aptos 区块链的状态。客户端通过 Aptos 节点与区块链交互。有两种类型的节点：
* Validator nodes 验证节点
* Fullnodes 全节点
** 每个Aptos节点都包括几个逻辑组件
  REST API service
  Mempool
  Execution
  Virtual Machine
  Storage
  State synchronize 状态同步器
##### 讨论区资料补充：https://github.com/aptos-labs/aptos-developer-discussions/discussions

### 2024.09.10

1. 交易从构建到链上执行需要经历5个步骤：构建、模拟、签名、提交、等待。
2. 节点网络和同步：验证器节点和全节点形成层次结构，验证器节点位于根，全节点位于其他位置。验证器全节点直接连接到验证器节点，并提供可扩展性和 DDoS 缓解功能。公共全节点连接到验证器全节点（或其他公共全节点）以获得对 Aptos 网络的低延迟访问。
3. Move 是一种安全可靠的 Web3 编程语言，强调稀缺性和访问控制。 Move 中的任何资产都可以由 resources 表示或存储在resources中。默认情况下会强制实施稀缺性，因为结构不会被意外复制或删除。只有在字节码层明确定义为copy 的结构才可以分别被复制和drop 。
4. 交易和状态：
   * 交易：交易代表区块链上的账户执行的预期操作（例如，转移资产）。（只有交易才能改变账本状态）
   * 状态：（区块链账本）状态代表交易执行输出的累积，即存储在所有资源中的值。
   * 事件：执行交易时发布的辅助数据。


### 2024.09.11

### 2024.09.12
1. 区块：
   - Aptos 是一个按交易版本控制的数据库。执行交易时，每笔交易的结果状态都会单独存储，从而允许更精细的数据访问。这与其他区块链不同，其他区块链只存储区块（一组交易）的结果状态。
   - 区块仍然是 Aptos 的基本单位。交易被分批处理并在一个区块中一起执行。此外，存储中的证明处于区块级粒度。区块内的交易数量取决于网络活动和可配置的最大区块大小限制。
2. 质押：任何人都可以参与 Aptos 共识过程，只要他们质押了足够的实用币，即将他们的实用币存入托管账户。为了鼓励验证者参与共识过程，每个验证者的投票权重与验证者的质押金额成正比。作为交换，验证者将按质押金额的比例获得奖励。因此，区块链的性能与验证者的利益（即奖励）保持一致。
   - Owner
   - Operator
   - Voter
4. Aptos 主网纪元设置为 7200 秒（两小时）。
5. 奖励公式
```text
    Reward = staked_amount * rewards_rate per epoch * (Number of successful proposals by the validator / Total number of proposals made by the validator) 
```
### 2024.09.13
- 边学边忘🤦，简单复习了一下最初的直播内容
- 下周多抽时间来研究

### 2024.09.14
补充
### 2024.09.15
1. 安装Aptos CLI
2. Create package
 - aptos move init
   - aptos move init --name <PROJECT_NAME>
 - Update Move.toml
```
[package]
name = "Examples"
version = "0.0.0"
 
[addresses]
hello_blockchain = "_"
 
[dependencies.AptosFramework]
git = "https://github.com/aptos-labs/aptos-core.git"
rev = "mainnet"
subdir = "aptos-move/framework/aptos-framework"
```
 - Add to sources directory
   - https://github.com/aptos-labs/aptos-core/tree/afd3706c17bcccfb39a9d6059aecbfa648ed295d/aptos-move/move-examples

### 2024.09.16

### 2024.09.17
中秋节快乐！

### 2024.09.18
参加会议：构建并部署代币水龙头

### 2024.09.19
在 Aptos 区块链上创建 NFT 市场
1. Listing NFTs: NFT owners list their NFTs in the marketplace, making them available for potential buyers to purchase.
2. Buying NFTs: Users can buy any NFT listed with the price set by the NFT owner.
3. Minting NFTs: For the demo purpose, we also built a Mint feature where you can mint NFTs to sell.
```
module marketplace_addr::marketplace {
    use std::error;
    use std::signer;
    use std::option;
    use aptos_std::smart_vector;
    use aptos_framework::aptos_account;
    use aptos_framework::coin;
    use aptos_framework::object;

    #[test_only]
    friend marketplace_addr::test_marketplace;

    const APP_OBJECT_SEED: vector<u8> = b"MARKETPLACE";

    /// There exists no listing.
    const ENO_LISTING: u64 = 1;
    /// There exists no seller.
    const ENO_SELLER: u64 = 2;

    // Core data structures

    struct MarketplaceSigner has key {
        extend_ref: object::ExtendRef,
    }

    // In production we should use off-chain indexer to store all sellers instead of storing them on-chain.
    // Storing it on-chain is costly since it's O(N) to remove a seller.
    struct Sellers has key {
        /// All addresses of sellers.
        addresses: smart_vector::SmartVector<address>
    }

    #[resource_group_member(group = aptos_framework::object::ObjectGroup)]
    struct Listing has key {
        /// The item owned by this listing, transferred to the new owner at the end.
        object: object::Object<object::ObjectCore>,
        /// The seller of the object.
        seller: address,
        /// Used to clean-up at the end.
        delete_ref: object::DeleteRef,
        /// Used to create a signer to transfer the listed item, ideally the TransferRef would support this.
        extend_ref: object::ExtendRef,
    }

    #[resource_group_member(group = aptos_framework::object::ObjectGroup)]
    struct FixedPriceListing<phantom CoinType> has key {
        /// The price to purchase the item up for listing.
        price: u64,
    }

    // In production we should use off-chain indexer to store the listings of a seller instead of storing it on-chain.
    // Storing it on-chain is costly since it's O(N) to remove a listing.
    struct SellerListings has key {
        /// All object addresses of listings the user has created.
        listings: smart_vector::SmartVector<address>
    }

    // Functions

    // This function is only called once when the module is published for the first time.
    fun init_module(deployer: &signer) {
        let constructor_ref = object::create_named_object(
            deployer,
            APP_OBJECT_SEED,
        );
        let extend_ref = object::generate_extend_ref(&constructor_ref);
        let marketplace_signer = &object::generate_signer(&constructor_ref);

        move_to(marketplace_signer, MarketplaceSigner {
            extend_ref,
        });
    }

    // ================================= Entry Functions ================================= //

    /// List an time for sale at a fixed price.
    public entry fun list_with_fixed_price<CoinType>(
        seller: &signer,
        object: object::Object<object::ObjectCore>,
        price: u64,
    ) acquires SellerListings, Sellers, MarketplaceSigner {
        list_with_fixed_price_internal<CoinType>(seller, object, price);
    }

    /// Purchase outright an item from a fixed price listing.
    public entry fun purchase<CoinType>(
        purchaser: &signer,
        object: object::Object<object::ObjectCore>,
    ) acquires FixedPriceListing, Listing, SellerListings, Sellers {
        let listing_addr = object::object_address(&object);

        assert!(exists<Listing>(listing_addr), error::not_found(ENO_LISTING));
        assert!(exists<FixedPriceListing<CoinType>>(listing_addr), error::not_found(ENO_LISTING));

        let FixedPriceListing {
            price,
        } = move_from<FixedPriceListing<CoinType>>(listing_addr);

        // The listing has concluded, transfer the asset and delete the listing. Returns the seller
        // for depositing any profit.

        let coins = coin::withdraw<CoinType>(purchaser, price);

        let Listing {
            object,
            seller, // get seller from Listing object
            delete_ref,
            extend_ref,
        } = move_from<Listing>(listing_addr);

        let obj_signer = object::generate_signer_for_extending(&extend_ref);
        object::transfer(&obj_signer, object, signer::address_of(purchaser));
        object::delete(delete_ref); // Clean-up the listing object.

        // Note this step of removing the listing from the seller's listings will be costly since it's O(N).
        // Ideally you don't store the listings in a vector but in an off-chain indexer
        let seller_listings = borrow_global_mut<SellerListings>(seller);
        let (exist, idx) = smart_vector::index_of(&seller_listings.listings, &listing_addr);
        assert!(exist, error::not_found(ENO_LISTING));
        smart_vector::remove(&mut seller_listings.listings, idx);

        if (smart_vector::length(&seller_listings.listings) == 0) {
            // If the seller has no more listings, remove the seller from the marketplace.
            let sellers = borrow_global_mut<Sellers>(get_marketplace_signer_addr());
            let (exist, idx) = smart_vector::index_of(&sellers.addresses, &seller);
            assert!(exist, error::not_found(ENO_SELLER));
            smart_vector::remove(&mut sellers.addresses, idx);
        };

        aptos_account::deposit_coins(seller, coins);
    }

    // ================================= Friend Functions ================================= //

    public(friend) fun list_with_fixed_price_internal<CoinType>(
        seller: &signer,
        object: object::Object<object::ObjectCore>,
        price: u64,        
    ): object::Object<Listing> acquires SellerListings, Sellers, MarketplaceSigner {
        let constructor_ref = object::create_object(signer::address_of(seller));

        let transfer_ref = object::generate_transfer_ref(&constructor_ref);
        object::disable_ungated_transfer(&transfer_ref);

        let listing_signer = object::generate_signer(&constructor_ref);

        let listing = Listing {
            object,
            seller: signer::address_of(seller),
            delete_ref: object::generate_delete_ref(&constructor_ref),
            extend_ref: object::generate_extend_ref(&constructor_ref),
        };
        let fixed_price_listing = FixedPriceListing<CoinType> {
            price,
        };
        move_to(&listing_signer, listing);
        move_to(&listing_signer, fixed_price_listing);

        object::transfer(seller, object, signer::address_of(&listing_signer));

        let listing = object::object_from_constructor_ref(&constructor_ref);

        if (exists<SellerListings>(signer::address_of(seller))) {
            let seller_listings = borrow_global_mut<SellerListings>(signer::address_of(seller));
            smart_vector::push_back(&mut seller_listings.listings, object::object_address(&listing));
        } else {
            let seller_listings = SellerListings {
                listings: smart_vector::new(),
            };
            smart_vector::push_back(&mut seller_listings.listings, object::object_address(&listing));
            move_to(seller, seller_listings);
        };
        if (exists<Sellers>(get_marketplace_signer_addr())) {
            let sellers = borrow_global_mut<Sellers>(get_marketplace_signer_addr());
            if (!smart_vector::contains(&sellers.addresses, &signer::address_of(seller))) {
                smart_vector::push_back(&mut sellers.addresses, signer::address_of(seller));
            }
        } else {
            let sellers = Sellers {
                addresses: smart_vector::new(),
            };
            smart_vector::push_back(&mut sellers.addresses, signer::address_of(seller));
            move_to(&get_marketplace_signer(get_marketplace_signer_addr()), sellers);
        };

        listing
    }

    // View functions

    #[view]
    public fun price<CoinType>(
        object: object::Object<Listing>,
    ): option::Option<u64> acquires FixedPriceListing {
        let listing_addr = object::object_address(&object);
        if (exists<FixedPriceListing<CoinType>>(listing_addr)) {
            let fixed_price = borrow_global<FixedPriceListing<CoinType>>(listing_addr);
            option::some(fixed_price.price)
        } else {
            // This should just be an abort but the compiler errors.
            assert!(false, error::not_found(ENO_LISTING));
            option::none()
        }
    }

    #[view]
    public fun listing(object: object::Object<Listing>): (object::Object<object::ObjectCore>, address) acquires Listing {
        let listing = borrow_listing(object);
        (listing.object, listing.seller)
    }

    #[view]
    public fun get_seller_listings(seller: address): vector<address> acquires SellerListings {
        if (exists<SellerListings>(seller)) {
            smart_vector::to_vector(&borrow_global<SellerListings>(seller).listings)
        } else {
            vector[]
        }
    }

    #[view]
    public fun get_sellers(): vector<address> acquires Sellers {
        if (exists<Sellers>(get_marketplace_signer_addr())) {
            smart_vector::to_vector(&borrow_global<Sellers>(get_marketplace_signer_addr()).addresses)
        } else {
            vector[]
        }
    }

    #[test_only]
    public fun setup_test(marketplace: &signer) {
        init_module(marketplace);
    }

    // Helper functions

    fun get_marketplace_signer_addr(): address {
        object::create_object_address(&@marketplace_addr, APP_OBJECT_SEED)
    }

    fun get_marketplace_signer(marketplace_signer_addr: address): signer acquires MarketplaceSigner {
        object::generate_signer_for_extending(&borrow_global<MarketplaceSigner>(marketplace_signer_addr).extend_ref)
    }

    inline fun borrow_listing(object: object::Object<Listing>): &Listing acquires Listing {
        let obj_addr = object::object_address(&object);
        assert!(exists<Listing>(obj_addr), error::not_found(ENO_LISTING));
        borrow_global<Listing>(obj_addr)
    }
}

// Unit tests

#[test_only]
module marketplace_addr::test_marketplace {
    use std::option;
    use aptos_framework::aptos_coin;
    use aptos_framework::coin;
    use aptos_framework::object;
    use aptos_token_objects::token;
    use marketplace_addr::marketplace;
    use marketplace_addr::test_utils;

    // Test that a fixed price listing can be created and purchased.
    #[test(aptos_framework = @0x1, marketplace = @0x111, seller = @0x222, purchaser = @0x333)]
    fun test_fixed_price(
        aptos_framework: &signer,
        marketplace: &signer,
        seller: &signer,
        purchaser: &signer,
    ) {
        let (_marketplace_addr, seller_addr, purchaser_addr) =
            test_utils::setup(aptos_framework, marketplace, seller, purchaser);

        let (token, listing) = fixed_price_listing(seller, 500); // price: 500

        let (listing_obj, seller_addr2) = marketplace::listing(listing);
        assert!(listing_obj == object::convert(token), 0); // The token is listed.
        assert!(seller_addr2 == seller_addr, 0); // The seller is the owner of the listing.
        assert!(marketplace::price<aptos_coin::AptosCoin>(listing) == option::some(500), 0); // The price is 500.
        assert!(object::owner(token) == object::object_address(&listing), 0); // The token is owned by the listing object. (escrowed)

        marketplace::purchase<aptos_coin::AptosCoin>(purchaser, object::convert(listing));

        assert!(object::owner(token) == purchaser_addr, 0); // The token has been transferred to the purchaser.
        assert!(coin::balance<aptos_coin::AptosCoin>(seller_addr) == 10500, 0); // The seller has been paid.
        assert!(coin::balance<aptos_coin::AptosCoin>(purchaser_addr) == 9500, 0); // The purchaser has paid.
    }

    // Test that the purchase fails if the purchaser does not have enough coin.
    #[test(aptos_framework = @0x1, marketplace = @0x111, seller = @0x222, purchaser = @0x333)]
    #[expected_failure(abort_code = 0x10006, location = aptos_framework::coin)]
    fun test_not_enough_coin_fixed_price(
        aptos_framework: &signer,
        marketplace: &signer,
        seller: &signer,
        purchaser: &signer,
    ) {
        test_utils::setup(aptos_framework, marketplace, seller, purchaser);

        let (_token, listing) = fixed_price_listing(seller, 100000); // price: 100000

        marketplace::purchase<aptos_coin::AptosCoin>(purchaser, object::convert(listing));
    }

    // Test that the purchase fails if the listing object does not exist.
    #[test(aptos_framework = @0x1, marketplace = @0x111, seller = @0x222, purchaser = @0x333)]
    #[expected_failure(abort_code = 0x60001, location = marketplace_addr::marketplace)]
    fun test_no_listing(
        aptos_framework: &signer,
        marketplace: &signer,
        seller: &signer,
        purchaser: &signer,
    ) {
        let (_, seller_addr, _) = test_utils::setup(aptos_framework, marketplace, seller, purchaser);

        let dummy_constructor_ref = object::create_object(seller_addr);
        let dummy_object = object::object_from_constructor_ref<object::ObjectCore>(&dummy_constructor_ref);

        marketplace::purchase<aptos_coin::AptosCoin>(purchaser, object::convert(dummy_object));
    }


    inline fun fixed_price_listing(
        seller: &signer,
        price: u64
    ): (object::Object<token::Token>, object::Object<marketplace::Listing>) {
        let token = test_utils::mint_tokenv2(seller);
        fixed_price_listing_with_token(seller, token, price)
    }

    inline fun fixed_price_listing_with_token(
        seller: &signer,
        token: object::Object<token::Token>,
        price: u64
    ): (object::Object<token::Token>, object::Object<marketplace::Listing>) {
        let listing = marketplace::list_with_fixed_price_internal<aptos_coin::AptosCoin>(
            seller,
            object::convert(token), // Object<Token> -> Object<ObjectCore>
            price,
        );
        (token, listing)
    }
}
```

### 2024.09.20

1. Aptos keyless
  Aptos Keyless 允许用户从现有的 OpenID Connect (OIDC) 帐户（例如，使用 Google 登录；使用 Apple 登录）获得 Aptos 区块链帐户的所有权，而不是通过传统的密钥或助记词。
  Aptos Keyless 预期的安全模型是“区块链账户=谷歌账户”。如果谷歌账户存在风险，则区块链账户也等同。

### 2024.09.21

### 2024.09.22

### 2024.09.23
<!-- Content_END -->
