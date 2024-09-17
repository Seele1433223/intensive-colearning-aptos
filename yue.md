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

# {yue}

1. 自我介绍
  你好，我是一個萌新小白，我也是founder of diffusion ，希望可以讓我的項目更加高的完成度和提升對move語言的了解
2. 你认为你会完成本次残酷学习吗？
那是當然的
## Notes

<!-- Content_START -->

### 2024.09.07

- 学习主题： Aptos & Move 模組學習
- 学习内容总结：
move 到模組學習，從一開始配置aptos cli 和move 的ide環境
```move
module 0x42::HELLOWWORLD{

    use std::debug::print;
    use std::string::utf8;

    #[test]
    fun test_hello_eorld(){
        print(&utf8(b"Hello World")); 
    }
}
````
一開始寫個hellow world 的move 來作為残酷学习的開始，這個可以print hellow world，然後就沒有了XD

### 2024.09.08

今天是學習如何在move裡面print出來，這樣才可以更好的去把bug和error解決

```move
module 0x42::lesson2{
 use std::debug::print;

  struct Wallet has drop{
    balance:u64

  }
    #[test]
    fun test_Wallet(){
        let wallet  = Wallet {balance: 1000};
        let wallet2 = wallet;
        print (&wallet.balance);
        //print (&wallet.balance);

    }

}
```

### 2024.09.09

今天來學習一下move裡面不同的類型， string ， u64，u32，u8 ，vector等等
```move
module 0x42::Type{
    use std::debug::print;
    use std::string;
    use std::string::{utf8};
    #[test_only]
    use std::string::String;

    #[test]
    fun test_num(){
        let num_u8 : u8 = 42; //
        let num_u8_2 =43u8;
        let num_u8_3 :u8 =0x2A; //hash

        let num_u256:u256  = 100_000;
        let num_sum  = (num_u8 as u256) + num_u256 ;

        print(&num_u8);
        print(&num_u8_2);
        print(&num_u8_3);
        print(&num_u256);
        print(&num_sum);
    }

    #[test]
    fun test_bool(){
        let bool_true : bool = true;
        let bool_false : bool =false ;
        print(&bool_true);
        print(&bool_false);
        print(&(bool_true == bool_false));
    }

    #[test]
    fun test_String(){
        let str:String =utf8(b"hellow world");
        print(&str);
    }

    #[test]
    fun test_address(){

        let add:address =@0x2A;
        print(&add);
    }

}
```

### 2024.09.10

今天來寫move 裡面vector的操作
```move
module 0x42::Type{
    use std::debug;
    use std::vector;
    #[test_only]
    use std::bit_vector::is_index_set;

    const APR:vector<u64> = vector[1,2,3,4,5,6,7,8,9,10];
    #[test]
    fun ss(){
        debug::print(&APR)
    }

    #[test]

    fun test_empty_vector(){
        let bools:bool = vector::is_empty(&APR);
        debug::print(&bools);

    }
    #[test]

    fun test_vector_length(){
        let len:u64 =vector::length(&APR);
        debug::print(&len);
    }

    #[test]
    fun test_vector_borrow(){
        let val = vector::borrow(&APR,3);
        debug::print(val)
    }

    #[test]
    fun test_vector_borrow_mut(){
        let arr:vector<u64> = vector[1,2,3,4,5,6,7,8,9,10];
        let val = vector::borrow_mut(&mut arr,3);
        *val=100;
        debug::print(&arr);
    }

    #[test]
    fun test_vector_contain(){
        let n:u64 =3;
        let n2:u64=11;
        let bools:bool = vector::contains(&APR,&n);
        let bools2:bool  = vector::contains(&APR,&n2);
    }

    #[test]
    fun test_vextor_index_of(){
        let n:u64 = 3;
        let n2:u64 = 11;
        let (isIndex,index) = vector::index_of(&APR,&n);
        let (isindex2,index2) = vector::index_of(&APR,&n2);
        debug::print(&isIndex);
        debug::print(&isindex2);
        debug::print(&index);
        debug::print(&index2);


    }

}
```

#### 2024.09.11
```move
module 0x42::Demo{
    use std::debug;
    use std::vector;

    #[test]
    fun test_push_back(){
        let vec = vector[1,2,3];
        vector::push_back(&mut vec ,4);
        debug::print(&vec);

    }

    #[test]
    fun test_append(){
        let vec1= vector[1,2,3];
        let vec2 = vector[4,5,6];
        vector::append(&mut vec1,vec2);
        debug::print(&vec1);

    }

    #[test]
    fun test_rev(){
        let ver1 =vector[1,2,3];
        let ver2 = vector[4,5,6];
        vector::reverse_append(&mut ver1,ver2);
        debug::print(&ver1)

    }
    #[test]
    fun test_pop_back(){
        let vec =vector[1,2,3];
        let x=vector::pop_back(&mut vec);
        debug::print(&x);
        debug::print(&vec);

    }

    #[test]

    fun test_swap(){
        let vec1 = vector[1,2,3,4,5];
        vector::swap(&mut vec1,0,2);
        debug::print(&vec1);
    }
    #[test]
    fun test_reverse(){
        let vec1 = vector[3,5,2,1,4];
        vector::reverse(&mut vec1);
        debug::print(&vec1);


    }


}
```

### 2024.09.12

今天學struct的用法
```move
address 0x42{
    module main{
        use std::debug;
        use std::signer;


        struct Foo has drop{
            u:u64,
            b:bool
        }
        #[test]
        fun oo(){
            let f =Foo{u:42,b:true};
            let Foo{u,b}=f;
            debug::print(&u);
            debug::print(&b);
        }
        #[test]

        fun test2(){
            let f=Foo{u:42,b:true};
            let Foo{ u,b}=&mut f;
            *u=43;
            debug::print(&f.u);
            debug::print(&f.b);

        }

        //copy

        struct Cancopy has copy, drop{
            u:u64,
            b:u64
        }
        #[test]
        fun test3(){
            let f = Cancopy{u:1,b:8};
            let f2 = copy f;
            debug::print(&f2.u);
            debug::print(&f2.b);
            debug::print(&f.u);
            debug::print(&f.b);

        }

        struct Key has key,drop{
            s:Store

        }
        struct Store has store,drop{
            s:u64,y:u64
        }
        #[test]
        fun test4(){
            let y=Store{s:1,y:2};
            let k = Key{s:y};
            debug::print(&k.s.s);
            debug::print(&k.s.y);

        }
    }



}
```

### 2024.09.13

```move
address 0x42{
    module main{
        use std::debug;
        use std::signer;
        #[test]
        fun test_if(){
            let x=6;
            if(x==5){
                debug::print(&x);
            }else{
                debug::print(&10);
            }

        }

        #[test]
        fun test_while(){
            let x= 5;
            while(x>0){
                x=x-1;
                if (x==3){
                    // break;
                    continue;
                };
                debug::print(&x);
            }

        }

        #[test]
        fun test_loop(){
            let x=10;
            loop{
                x=x-1;
                if(x<=5){

                    break
                };
                debug::print(&x);
            };
        return
        }

    }
}
```

### 2024.09.14

friend 的用法

```move
 module MyPacke::main{
        use std::debug;
        friend MyPacke::m2;
        friend MyPacke::m3;
        public fun num():u64{
            66
        }

        public(friend) fun num2():u64{
            88
        }

    }

module MyPacke::m2{

    #[test]
    fun main2(){
        use std::debug;
        use MyPacke::main::num;
        let n=num();
        debug::print(&n);
    }

    #[test]
    fun test2(){
        use std::debug;
        use MyPacke::main::num2;
        let n= num2();
        debug::print(&n);
    }


}

module MyPacke::m3{
    use std::debug;
    #[test]
    fun main3(){
        use std::debug;
        use MyPacke::main::num;
        let n=num();
        debug::print(&n);

    }
    #[test]
    fun test2(){
        use std::debug;
        use MyPacke::main::num2;
        let n= num2();
        debug::print(&n);
    }


}
```
### 2024.09.15

```move
module mynft::mynft{

        use std::string::{String,utf8};
        use std::string;
        use std::option;
        use std::error;

        use std::vector;
        use std::signer;
        use aptos_framework::object::{Self,Object, LinearTransferRef};
        use aptos_token_objects::collection;
        use aptos_token_objects::token;
        use aptos_token_objects::token::Token;
        use aptos_token_objects::property_map;
        use aptos_framework::event;
        use aptos_framework::account;
        use aptos_std::string_utils::{to_string};
        use aptos_std::type_info::struct_name;
        use aptos_framework::fungible_asset::{BurnRef, TransferRef};
        use aptos_token_objects::collection::MutatorRef;
        use aptos_framework::account::SignerCapability;

    #[test_only]
        use aptos_token_objects::aptos_token::create_collection;

        //the token not exist
        const Token_does_not_exist:u64 =1;
        //the provide signer is cretor
        const Not_creator:u64=2;
        const Mycollection:vector<u8> =b"mycollection";
        const Project:address=@0x1;
         struct CollectionRefsStore has key {

             mutator_ref:collection::MutatorRef,

         }
    struct Content has key,drop{
        content:string::String
    }
    #[event]
    struct Mintevent has drop ,store{
        owner:address,
        token_id:address,
        content:string::String
    }
    #[event]
    struct SetContentEvent has drop, store {
        owner: address,
        token_id: address,
        old_content: string::String,
        new_content: string::String
    }
    #[event]
    struct BurnEvent has drop,store {
        owner:address,
        token_id:address,
        content:string::String
    }
    struct Resoucecap has key{
        cap:SignerCapability
    }
    struct Tokenstore has key{
        mutator_ref: token::MutatorRef,
        burn_ref: token::BurnRef,
        extend_ref: object::ExtendRef,
        transfer_ref: option::Option<object::TransferRef>
    }


    fun init_module(caller:&signer){

        let (resource_signer, resource_cap) = account::create_resource_account(
            caller,
            Mycollection
        );

        move_to(&resource_signer,Resoucecap{cap:resource_cap});
        // if (exists<Resoucecap>(signer::address_of(&resource_signer))){
        //     debug::print(&utf8(b"1.yes ResourceCap"));
        // }else{
        //     debug::print(&utf8(b"1.no ResourceCap"));
        // };
        // debug::print(&utf8(Mycollection));

        let max_supply = 1000;
        let des:String = utf8(b"test nft");
        let name:String =utf8(b"nft");
        let web_Addr :String = utf8(b"https://pot-124.4everland.store/IMG_0714.JPG");
        let collection=collection::create_fixed_collection(
            &resource_signer,
            utf8(b"test nft"),
            1000,
            utf8(b"nft"),
            option::none(),
            utf8(b"https://pot-124.4everland.store/IMG_0714.JPG")
        );
        let collection_signer = object::generate_signer(&collection );
        let mutator_ref = aptos_token_objects::collection::generate_mutator_ref(&collection);
        move_to(&collection_signer,CollectionRefsStore{mutator_ref});


        // if (exists<CollectionRefsStore>(signer::address_of(&collection_signer))){
        //     debug::print(&utf8(b"2.yes CollectionRefsStore"));
        // }else{
        //     debug::print(&utf8(b"2.no CollectionRefsStore"));
        // };
    }

    // #[test(caller=@0x1)]
    // fun test_mint(caller:&signer)acquires Resoucecap {
    //     init_module(caller);
    //     let yee : String=utf8(b"1");
    //     mint(caller,yee);
    // }
    //&@mynft
    entry public fun mint(caller :&signer,content:string::String)acquires Resoucecap {
        //let resourf = aptos_framework::account::create_resource_address(&@mynft,Mycollection);

        // debug::print(&utf8(Mycollection));
        // if (exists<Resoucecap>(resourf)){
        //     debug::print(&utf8(b"3.yes Resoucecap"));
        // }else{
        //     debug::print(&utf8(b"3.no Resoucecap"));
        // };

        let resource_cap = &borrow_global<Resoucecap>(aptos_framework::account::create_resource_address(&@mynft,Mycollection)).cap;
        let resource_signer = &account::create_signer_with_capability(resource_cap);
        let token_cref = token::create(resource_signer,utf8(b"nft"),utf8(Mycollection),utf8(b"test nft"),option::none(),utf8(b"https://pot-124.4everland.store/IMG_0714.JPG"));
        let token_signer = object::generate_signer(&token_cref);
        let token_mutator_ref = token::generate_mutator_ref(&token_cref);
        let token_burn_ref =token::generate_burn_ref(&token_cref);
        move_to(
            &token_signer,
            Tokenstore {
                mutator_ref: token_mutator_ref,
                burn_ref: token_burn_ref,
                extend_ref: object::generate_extend_ref(&token_cref),
                transfer_ref: option::none()
            }
        );
        move_to(
            &token_signer,
            Content {
                content
            }
        );


        event::emit(
            Mintevent{
                owner:signer::address_of(caller),
                token_id:object::address_from_constructor_ref(&token_cref),
                content}
        );
        object::transfer(
            resource_signer,
            object::object_from_constructor_ref<Token>(&token_cref),
            signer::address_of(caller),
        );

    }

    entry fun burn(caller:&signer,object:Object<Content>)acquires Tokenstore,Content {
        assert!(object::is_owner(object,signer::address_of(caller)),1);
        let Tokenstore{
            mutator_ref: _,
            burn_ref,
            extend_ref: _,
            transfer_ref: _
        } = move_from<Tokenstore>(object::object_address(&object));

        let Content {
            content
        } = move_from<Content>(object::object_address(&object));
        event::emit(
            BurnEvent {
                owner: object::owner(object),
                token_id: object::object_address(&object),
                content
            }
        );
        token::burn(burn_ref);
    }

    entry fun set_content(
        caller: &signer,
        object: Object<Content>,
        content: string::String
    )acquires Content{
        let old_content =borrow_content(signer::address_of(caller),object).content;
        event::emit(
            SetContentEvent {
                owner: object::owner(object),
                token_id: object::object_address(&object),
                old_content,
                new_content: content
            }
        );
        borrow_mut_content(signer::address_of(caller), object).content = content;
    }
    #[view]
    public fun get_content(object: Object<Content>): string::String acquires Content {
        borrow_global<Content>(object::object_address(&object)).content
    }
    inline fun borrow_content(owner: address, object: Object<Content>): &Content {
        assert!(object::is_owner(object, owner), 1);
        borrow_global<Content>(object::object_address(&object))
    }
    inline fun borrow_mut_content(owner: address, object: Object<Content>): &mut Content {
        assert!(object::is_owner(object, owner), 1);
        borrow_global_mut<Content>(object::object_address(&object))
    }
    #[test_only]
    public fun init_for_test(sender: &signer) {
        init_module(sender)
    }




```

### 2024.09.16

prove 的用法

```move
module 0x1::prove_demo {

    use std::signer;
    use aptos_framework::aptos_coin::AptosCoin;
    use aptos_framework::coin;
    #[test_only]
    use std::string;
    #[test_only]
    use std::string::utf8;
    #[test_only]
    use aptos_std::debug;
    #[test_only]
    use aptos_framework::account::create_account_for_test;
    #[test_only]
    use aptos_framework::system_addresses;
    #[test_only]
    use aptos_framework::timestamp;

    ///Error Code /////
    const To_address_cant_same_with_caller : u64 = 1 ;
    const Amount_must_large_than_zero :u64 = 2 ;
    ///Error Code /////


    spec coin_transfer_to_other( caller:&signer, to_address:address, amount:u64 ) {
        pragma verify = true;

        let addr = signer::address_of(caller);

        ensures  amount > 0 ;
        ensures  addr != to_address;

    }

    public entry fun coin_transfer_to_other (caller:&signer, to_address:address, amount:u64){
        assert!(signer::address_of(caller) != to_address , To_address_cant_same_with_caller);
        assert!(amount >  0 , Amount_must_large_than_zero);

        coin::transfer<AptosCoin>(caller,to_address,amount);

    }

    /////// Unit  Test  /////////

    #[test(aptos_framework=@aptos_framework,caller=@0x2,to_address_signer=@0x3)]
    fun test_coin_transfer(aptos_framework:&signer,caller:&signer,to_address_signer:&signer){
        create_account_for_test(signer::address_of(caller));
        create_account_for_test(signer::address_of(to_address_signer));

        prepare_for_apt(aptos_framework,caller);
        coin::register<AptosCoin>(to_address_signer);

        // 0  transfer
        //coin_transfer_to_other(caller,signer::address_of(to_address_signer),0);

        // self transfer
        //coin_transfer_to_other(caller,signer::address_of(caller),1);

        // transfer 1 APT
        coin_transfer_to_other(caller,signer::address_of(to_address_signer),100000000);

        test_print(caller,to_address_signer);
    }

    #[test_only]
    fun test_print(caller:&signer,to_address:&signer){
        debug::print(&utf8(b"balance of AptosCoin   -  dapp"));
        debug::print(&coin::balance<AptosCoin>(signer::address_of(caller)));
        debug::print(&utf8(b"balance of AptosCoin   -  to address"));
        debug::print(&coin::balance<AptosCoin>(signer::address_of(to_address)));
    }




    #[test_only]
    fun prepare_for_apt(aptos_framework:&signer,caller:&signer){
        timestamp::set_time_has_started_for_testing(aptos_framework);
        let (burn_cap, freeze_cap, mint_cap) = coin::initialize<AptosCoin>(
            aptos_framework,
            string::utf8(b"TC"),
            string::utf8(b"TC"),
            8,
            false,
        );
        coin::register<AptosCoin>(caller);
        let coins = coin::mint<AptosCoin>(200000000, &mint_cap);
        coin::deposit(signer::address_of(caller), coins);
        coin::destroy_freeze_cap(freeze_cap);
        coin::destroy_burn_cap(burn_cap);
        system_addresses::assert_aptos_framework(aptos_framework);
        coin::destroy_mint_cap(mint_cap);
    }
}

```

### 2024.09.17

寫一個test 的用法

```move
module 0x1::test {

    use std::signer;
    use std::string::utf8;
    use aptos_framework::coin;
    use aptos_framework::coin::{destroy_burn_cap, destroy_freeze_cap, register, destroy_mint_cap};
    #[test_only]
    use aptos_std::debug;
    #[test_only]
    use aptos_framework::account::create_account_for_test;

    //// Const /////

    const Coin_name : vector<u8> = b"diffusion";
    const Coin_symbol :vector<u8> = b"dfc";
    const Coin_decimals :u8 = 8;

    //// Const /////

    struct Diffusion_coin has key {}

    fun init_module (caller:&signer){
        let (burn,freeze,mint) = coin::initialize<Diffusion_coin>(caller,utf8(Coin_name),utf8(Coin_symbol),Coin_decimals,false);
        destroy_burn_cap(burn);
        destroy_freeze_cap(freeze);
        let coins = coin::mint<Diffusion_coin>(1000,&mint);
        register<Diffusion_coin>(caller);
        coin::deposit(signer::address_of(caller),coins);
        destroy_mint_cap(mint);
    }
    public entry fun coin_transfer_to_other(caller:&signer,to_address:address){
        coin::transfer<Diffusion_coin>(caller,to_address,100);
    }


    /////// Unit Test  /////////

    // #[test(caller=@0x1,to_address=@0x2)]
    //  fun test_coin_transfer_to_other(caller:&signer,to_address:&signer){
    //     create_account_for_test(signer::address_of(caller));
    //     create_account_for_test(signer::address_of(to_address));
    //     init_module(caller);
    //     register<Diffusion_coin>(to_address);
    //     //test_print(caller,to_address);
    //     coin_transfer_to_other(caller,signer::address_of(to_address));
    //      test_print(caller,to_address);
    //  }

    #[test_only]
    fun test_print(caller:&signer,to_address:&signer){
        debug::print(&utf8(b"balance of diffusion coin   -  dapp"));
        debug::print(&coin::balance<Diffusion_coin>(signer::address_of(caller)));
        debug::print(&utf8(b"balance of diffusion coin   -  to address"));
        debug::print(&coin::balance<Diffusion_coin>(signer::address_of(to_address)));
    }


}

```

```move
module 0x1::demo {
    use std::signer;
    use std::string;
    use std::string::utf8;
    use aptos_std::debug;

    struct Profile has key{
        name:string::String,
        icon:string::String
    }

    fun init_module(caller:&signer){
        let new_Profile = Profile{
            name:utf8(b"hello"),
            icon:utf8(b"is me")
        };
        move_to(caller,new_Profile);
    }

    public entry fun read_profile (caller:&signer) acquires Profile {
        let borrow_name = borrow_global<Profile>(signer::address_of(caller)).name;
        let borrow_icon = borrow_global<Profile>(signer::address_of(caller)).icon;
        debug::print(&utf8(b"name"));
        debug::print(&borrow_name);
        debug::print(&utf8(b"icon"));
        debug::print(&borrow_icon);
    }


    /////// Unit Test  /////////

    // #[test(caller=@0x1)]
    // fun test_read_profile(caller:&signer) acquires Profile {
    //     //init_module(caller);
    //     read_profile(caller);
    // }

}

```

<!-- Content_END -->
