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

### 2024.09.18

寫個hackthon 要用到的move 函數，先寫view
```move
    ////////////////// view fun /////////////////////////////////
    #[view]
    public fun check_user_card(user_address:address,card_name:string::String,expired_date:u64):(bool,Bet_card) acquires Account_tree {
        let have_or_not = false;
        let i =0;
        let index =99;
        let length = vector::length(&borrow_global<Account_tree>(user_address).save_2);
        while(i < length){
            let borrow = vector::borrow(&borrow_global<Account_tree>(user_address).save_2,i);
            if(borrow.expired_time == expired_date){
                if(borrow.pair.pair_name == card_name){
                    index =i;
                    have_or_not=true;
                }
            };
            i = i +1;
        };
        let null_bet = Bet_card{
            account:@0x1,
            which:99,
            pair:Pair{
                pair_type:utf8(b""),
                pair_name:utf8(b""),
                left_url:utf8(b""),
                right_url:utf8(b""),
                left:0,
                left2:0,
                middle:0,
                middle2:0,
                right:0,
                right2:0,
                can_bet:false,
                expired_time:0
            },
            bet:0,
            a_win:0,
            b_win:0,
            c_win:0,
            time:0,
            expired_time:0,
        };
        if(i != 99 ){
            return (have_or_not,*vector::borrow(&borrow_global<Account_tree>(user_address).save_2,i))
        }else{return (have_or_not,null_bet)}
    }
    #[view]
    public fun check_user_badges(user_address:address,badges_name:string::String):(bool,Badges,vector<Badges>) acquires Diffusion_store_tree, Account_tree {
        let borrow = borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list;
        let i=0;
        let length = vector::length(&borrow);
        let right = false;
        let index = 99;
        while(i < length) {
            let specfic = vector::borrow(&borrow, i);
            if (specfic.save_Badges.Name == badges_name) {
                let f = 0;
                let length2 = vector::length(&specfic.save_list);
                index = i;
                while (f < length2) {
                    let specfic_address = vector::borrow(&specfic.save_list, f);
                    if (specfic_address == &user_address) {
                        right = true;
                    };
                    f = f + 1;
                };
            };
            i = i + 1;
        };
        if(index != 99){return (right,  vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_Badges,borrow_global<Account_tree>(user_address).save_4)}else{
            let new_badges = Badges{ Name:utf8(b""),url:utf8(b"")};
            return(false , new_badges,vector::empty<Badges>())
        }

    }
    #[view]
    public fun check_helper_list(helper_address:address):(bool,bool) acquires Diffusion_store_tree {
        let borrow = borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list;
        let i=0;
        let length = vector::length(&borrow);
        let right1=false;
        let right2 = false;
        while(i < length){
            let specfic_helper = vector::borrow(&borrow,i);
            if(specfic_helper.account == helper_address){
                right1=true;
                if(specfic_helper.pay_margin == true){
                    right2=true
                };
            };

            i=i+1;
        };
        return (right1,right2)
    }
    #[view]
    public fun helper_upload_which_result(helper_address:address):Helper  acquires Diffusion_store_tree {

        let i=0;
        let length = vector::length(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list);
        let index= 99;
        while(i < length){
            let specfic_helper = vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,i);
            if(specfic_helper.account == helper_address){
                index = i ;
            };
            i=i+1;
        };
        if(index !=99){*vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,index)}else{
            let new_helper = Helper{
                account:@0x1,
                helper_contribute:vector::empty<Helper_upload_result>(),
                helper_point:0,
                upload_times:0,
                wrong_times:0,
                pay_margin:false,
                need_admin:false,
            };
            return new_helper
        }

    }
    #[view]
    public fun get_pair_data(pair_name:string::String,expire_data:u64):(Pair,Chips,bool,bool) acquires Diffusion_store_tree {
        let borrow = borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_pair;
        let i = 0 ;
        let length = vector::length(&borrow);
        let index= 99;
        while(i < length ){
            let specfic_pair = vector::borrow(&borrow,i);
            if(specfic_pair.pair_name == pair_name){
                    if(specfic_pair.expired_time == expire_data){
                        index =i
                    };
                };
            i=i+1;
        };
        if(index !=99){
            return (*vector::borrow(&borrow,index),*vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_chips,index),*vector::borrow( &borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_admin_set_result,index),*vector::borrow( &borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_can_claim,index))}
        else{
            let new_pair = Pair{
                pair_type:utf8(b""),
                pair_name:utf8(b""),
                left:0,
                left2:0,
                middle:0,
                middle2:0,
                right:0,
                right2:0,
                left_url:utf8(b""),
                right_url:utf8(b""),
                expired_time:0,
                can_bet:false
            };
            let new_chips = Chips{
                left:0,
                middle:0,
                right:0,
                given:0
            };
            return (new_pair,new_chips,false,false)
        }

    }
```

### 2024.09.19

```move  ////////////////// Helper fun /////////////////////////////////
    public entry fun helper_upload_result(caller:&signer,pair_name1:string::String,which:u8,expired_time:u64) acquires Diffusion_store_tree, Account_tree {
        // if(vector::length(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list) >= (Least_helper as u64)){
        //     all_helper_result(caller);
        // };
        // all_helper_result(caller);
        assert!(exists<Account_tree>(signer::address_of(caller)  )== true,Create_account_first);
        assert!(exists<Diffusion_store_tree>(create_resource_address(&@dapp,Seed))== true,Not_exists_diffusion_store_tree);

        too_much_wrong_is_time_to_click_it_out(caller);
        asc3(caller);

        let helper_index = check_helper_index(caller);
        assert!(helper_index !=99,NOT_HELPER);
        assert!(which==1||which==2||which==3,NOT_RIGHT_INPUT);


        let pair_index = check_pair_index(caller,pair_name1,expired_time);
        assert!(pair_index!=99,NOT_exist_pair);
        assert!(vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_pair,pair_index).can_bet == false , Still_Bet_time);
        let helper_upload_result_index  = check_helper_upload_result_index(caller,pair_index,helper_index);

        assert!(helper_upload_result_index==99,ALREADY_UPLOAD);

        let admin_set =vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_admin_set_result,pair_index) ;
        let can_claim = vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_can_claim,pair_index) ;

        assert!(admin_set != &true && can_claim!=&true,Pair_finish);

        let borrow_helper_list = borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed));
        let specfic_helper = vector::borrow_mut(&mut borrow_helper_list.save_Helper_list.list,helper_index);

        assert!(specfic_helper.pay_margin==true,Helper_not_pay_margin);

       // let borrow_pair_reult = borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store;
        let spedcfic_pair = vector::borrow(&borrow_helper_list.save_Pair_result_store.save_pair,pair_index);

        let new_upload_result = Helper_upload_result{
            pair:Pair{
                pair_type:spedcfic_pair.pair_type,
                pair_name:spedcfic_pair.pair_name,
                left_url:spedcfic_pair.left_url,
                right_url:spedcfic_pair.right_url,
                left:spedcfic_pair.left,
                left2:spedcfic_pair.left2,
                middle:spedcfic_pair.middle,
                middle2:spedcfic_pair.middle2,
                right:spedcfic_pair.right,
                right2:spedcfic_pair.right2,
                can_bet:spedcfic_pair.can_bet,
                expired_time:spedcfic_pair.expired_time
            },
            result:which,
            upload_time:timestamp::now_seconds(),
            right_or_not:vector::empty<bool>()
        };


        vector::push_back(&mut specfic_helper.helper_contribute,new_upload_result);
        // debug::print(&utf8(b"upload result"));
        // debug::print(&specfic_helper.helper_contribute);
        specfic_helper.upload_times = specfic_helper.upload_times + 1;

    }

    public entry fun apply_to_be_helper(caller:&signer) acquires Diffusion_store_tree, Account_tree {
        let helper_index = check_helper_index(caller);
        assert!(helper_index!=99,NOT_HELPER);
        assert!(exists<Account_tree>(signer::address_of(caller)),Create_account_first);

        // let helper_vector = borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed));
        // let specfic_helper = vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,helper_index);
         if(vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,helper_index).pay_margin == false){
            pay_margin_to_account(caller);
            vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,helper_index).pay_margin=true;
            let helper_badges = Badges{Name:utf8(b"Helper"),url:utf8(b"https://pot-124.4everland.store/helper_badges.png")};
            vector::push_back(&mut borrow_global_mut<Account_tree>(signer::address_of(caller)).save_4,helper_badges);
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_helper_chance.heler_number = borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_helper_chance.heler_number+1;
        }else{
            assert!(vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,helper_index).pay_margin != true,Already_pay_margin);
        }


    }


    public entry fun mint_badges(caller:&signer,badges:string::String) acquires Diffusion_store_tree, Account_tree {
        let i= 0;
        let length =vector::length(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list);
        let index =99;
        while(i < length ){
            let specfic = vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,i);
            if(specfic.save_Badges.Name ==badges){
                index = i;
            };
            i=i+1;
        };
        assert!(index != 99 ,Dont_have_this_badges);
        if (vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_can_mint == true){
            let e = 0 ;
            let length3 = vector::length(&vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_allow_list);
            while(e < length3 ) {
                let specfi_borrow = vector::borrow(
                    &vector::borrow(
                        &borrow_global_mut<Diffusion_store_tree>(
                            create_resource_address(&@dapp, Seed)
                        ).save_badges_list,
                        index
                    ).save_allow_list,
                    e
                );
                if (specfi_borrow == &signer::address_of(caller)) {
                    let f = 0 ;
                    let length2 = vector::length(&borrow_global<Account_tree>(signer::address_of(caller)).save_4);
                    let where = 99;
                    while(f < length2){
                        let specfic = vector::borrow(&borrow_global<Account_tree>(signer::address_of(caller)).save_4,f);
                        if(specfic.Name == badges){
                            where = f;
                        };
                        f=f +1;
                    };
                    assert!(where == 99 ,Already_exists_this_badges);
                    let new_badges = Badges{
                        Name:vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_Badges.Name,
                        url:vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_Badges.url,
                    };
                    push_back(&mut borrow_global_mut<Account_tree>(signer::address_of(caller)).save_4,new_badges);
                    vector::push_back(&mut vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_list , signer::address_of(caller));
                };
                e = e + 1;
            }
        }else{
            let f = 0 ;
            let length2 = vector::length(&borrow_global<Account_tree>(signer::address_of(caller)).save_4);
            let where = 99;
            while(f < length2){
                let specfic = vector::borrow(&borrow_global<Account_tree>(signer::address_of(caller)).save_4,f);
                if(specfic.Name == badges){
                    where = f;
                };
                f=f +1;
            };
            assert!(where == 99 ,Already_exists_this_badges);
            let new_badges = Badges{
                Name:vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_Badges.Name,
                url:vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_Badges.url,
            };
            push_back(&mut borrow_global_mut<Account_tree>(signer::address_of(caller)).save_4,new_badges);
            vector::push_back(&mut vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_list , signer::address_of(caller));
        }
    }
    ////////////////// Helper fun /////////////////////////////////

```

寫一下helper會用到的function

### 2024.09.20
```move
////////////////// Admin fun /////////////////////////////////

    public entry fun admin_set_badges(caller:&signer,job:string::String,badges:string::String,target:address,set_can_mint:bool) acquires Diffusion_store_tree {
        let admin_index = check_admin_index(signer::address_of(caller));
        assert!(admin_index !=99 ||signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin1,Not_admin);
        let i= 0;
        let length =vector::length(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list);
        let index =99;
        while(i < length ){
            let specfic = vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,i);
            if(specfic.save_Badges.Name ==badges){
                index = i;
            };
            i=i+1;
        };
        assert!(index != 99 ,Dont_have_this_badges);
        if(job == utf8(b"add")){
            vector::push_back(&mut vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_allow_list,target);
        }
        else if(job == utf8(b"minus")){
            let f =0;
            let length2 = vector::length(&vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_allow_list);
            let where =99;
            while(f < length2 ){
                let borrow = vector::borrow(&vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_allow_list,f);
                if(borrow == &target){
                    where = f;
                };
                f= f+1;
            };
            assert!(f != 99 ,Dont_have_this_address_in_allow_list);
            vector::remove(&mut vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_allow_list,where);
        }
        else if(job == utf8(b"set")){
            vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,index).save_can_mint = set_can_mint;
        }

    }
    fun check_admin_index(target:address):u64 acquires Diffusion_store_tree {
        let i = 0;
        let length =vector::length(& borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.admin_list);
        while(i < length){
            let borrow = vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.admin_list,i);
            if(&target == borrow){
                return i
            };
            i=i+1;
        } ;
        return 99
    }
    public entry fun admin_set_admin (caller:&signer,add_or_delete:string::String,target_address:address) acquires Diffusion_store_tree {
        assert!(signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin1,Not_lages_admin);
        assert!(exists<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)) == true,Not_exists_diffusion_store_tree);
        let admin_index = check_admin_index(target_address);

        if(add_or_delete == utf8(b"add")){
            assert!(admin_index ==99 ,Already_have_this_admin);
            vector::push_back(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.admin_list,target_address);
        }else if(add_or_delete == utf8(b"delete")){
            assert!(admin_index !=99,Dont_have_this_admin );
            vector::remove(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.admin_list,admin_index);
        }
    }
    public entry fun admin_said_times_up(caller:&signer,pair:string::String,expired_time:u64) acquires Diffusion_store_tree {
        let admin_index = check_admin_index(signer::address_of(caller));
        assert!(admin_index !=99 || signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin1,Not_admin);
        let index = check_pair_index(caller,pair,expired_time);
        assert!(index != 99 ,NOT_exist_pair);
        vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Pair_result_store.save_pair,index).can_bet = false ;
    }
    public entry fun create_or_delete_badges (caller:&signer,create_or_delete:string::String,badges:string::String,url1:string::String,can_mint:bool) acquires Diffusion_store_tree {
        assert!(signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin1,Not_admin);
        let i= 0;
        let length =vector::length(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list);
        let index =99;
        while(i < length ){
            let specfic = vector::borrow(&borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,i);
            if(specfic.save_Badges.Name ==badges){
                index = i;
            };
            i=i+1;
        };

        if(create_or_delete == utf8(b"create")){
            assert!(index == 99 ,Already_exists_this_badges);
            let new_badges=Badges_list{
                save_Badges:Badges{Name:badges,url:url1},
                save_can_mint:can_mint,
                save_allow_list:vector::empty(),
                save_list:vector::empty(),
            };
            push_back(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_badges_list,new_badges);
        }
        else if(create_or_delete == utf8(b"delete")){
            if(length != 0) {
                assert!(index != 99, Dont_have_this_badges);
                vector::remove<Badges_list>(
                    &mut borrow_global_mut<Diffusion_store_tree>(
                        create_resource_address(&@dapp, Seed)
                    ).save_badges_list,
                    index
                );
            }
        }
    }
    public entry fun set_chance(caller:&signer,which_one:string::String,fee1:u64,fee2:u64) acquires Diffusion_store_tree {
        assert!(signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin2 ,Not_admin);
        assert!(exists<Diffusion_store_tree>(create_resource_address(&@dapp,Seed))==true,Not_exists_diffusion_store_tree);
        if(which_one==utf8(b"margin")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.margin=fee1;
        }else if(which_one==utf8(b"fee")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.fees_1=fee1;
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.fees_2=fee2;
        }else if(which_one==utf8(b"share")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.allocation_share_1=fee1;
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.allocation_share_2=fee2;
        }else if(which_one==utf8(b"max helper")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_helper_chance.maximun_helper_num=fee1;
        }else if(which_one==utf8(b"least helper")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_helper_chance.least_helper_result= (fee1 as u8);
        }else if(which_one==utf8(b"wrong")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_helper_chance.chance_for_wrong_time= (fee1 as u8);

        }else if(which_one==utf8(b"nft chance")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.nft_chance_1 = fee1 ;
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.nft_chance_2 = fee2 ;
        }else if(which_one==utf8(b"bank share")){
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.bank_share_1 = fee1 ;
            borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).fee.bank_share_2 = fee2 ;
        };
    }
    public entry fun set_cylinder_sav_number(caller:&signer,save_number:u64,coin1:string::String,coin_address1:address,send_coin_amount1:u64) acquires Diffusion_store_tree {
        assert!(signer::address_of(caller) == @admin1 ||signer::address_of(caller) == @admin2 ,Not_admin  );
        assert!(save_number > 1 ,Save_number_must_large_than_1 );
        let index = find_coin_index_in_main_tree(coin1,coin_address1,send_coin_amount1);
        assert!(index != 99 ,Dont_have_this_cylinder);
        vector::borrow_mut(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Cylinder_Pairs,index).save_number = save_number;
    }
    public entry fun create_cylinder(caller:&signer,coin1:string::String,coin_address1:address,send_coin_amount1:u64) acquires Diffusion_store_tree {
        let admin_index = check_admin_index(signer::address_of(caller));
        assert!(admin_index != 99 ||signer::address_of(caller) == @admin1 ||signer::address_of(caller) == @admin2 ,Not_admin  );
        let index = find_coin_index_in_main_tree(coin1,coin_address1,send_coin_amount1);
        assert!(index == 99 ,Already_have_this_cylinder);
        let new_cylinder = Cylinder_Pairs{
            coin:coin1,
            coin_address:coin_address1,
            pair_number:send_coin_amount1,
            save_number:1,
            save_total:0,
            send_amount_vector:vector::empty<u64>(),
            send_address_vector:vector::empty<address>(),
            already_send:0
        };
        // vector::push_back(&mut new_cylinder.send_address_vector,@admin1);
        // vector::push_back(&mut new_cylinder.send_amount_vector,1);
        vector::push_back(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Cylinder_Pairs,new_cylinder);
    }
    public entry fun create_helper(caller:&signer,add_or_delete:string::String,helper_adddress:address) acquires Diffusion_store_tree {
        assert!(signer::address_of(caller)==@admin1 || signer::address_of(caller)==@admin2 ,Not_admin);
        if(add_or_delete == utf8(b"add")) {
            assert!(
                (vector::length(
                    &borrow_global_mut<Diffusion_store_tree>(
                        create_resource_address(&@dapp, Seed)
                    ).save_Helper_list.list
                ) < borrow_global_mut<Diffusion_store_tree>(
                    create_resource_address(&@dapp, Seed)
                ).save_helper_chance.maximun_helper_num),
                Too_Much_Helper
            );
            let borrow_helper_list = borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp, Seed));
            let length = vector::length(&borrow_helper_list.save_Helper_list.list);
            let i = 0;
            let done = false;
            if (length == 0) {
                let new_helper = Helper {
                    account: helper_adddress,
                    helper_contribute: vector::empty<Helper_upload_result>(),
                    helper_point: 0,
                    upload_times: 0,
                    wrong_times: 0,
                    pay_margin: false,
                    need_admin: false
                };
                vector::push_back(&mut borrow_helper_list.save_Helper_list.list, new_helper);
            }else {
                while (i < length) {
                    let borrow = vector::borrow(&borrow_helper_list.save_Helper_list.list, i);
                    if (borrow.account == helper_adddress) {
                        return
                    };
                    if (i == length - 1) {
                        done = true
                    };
                    i = i + 1;
                };

                if (done == true) {
                    let new_helper = Helper {
                        account: helper_adddress,
                        helper_contribute: vector::empty<Helper_upload_result>(),
                        helper_point: 0,
                        upload_times: 0,
                        wrong_times: 0,
                        pay_margin: false,
                        need_admin: false
                    };
                    vector::push_back(&mut borrow_helper_list.save_Helper_list.list, new_helper);
                };
            };
        }else if(add_or_delete == utf8(b"delete")){
            let i =0;
            let length = vector::length(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list);
            let index= 99;
            while(i < length){
                let specfic = vector::borrow(&borrow_global<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,i);
                if(specfic.account ==helper_adddress){
                    index = i;
                };
                i=i+1;
            };
            assert!(index != 99 , Dont_have_this_helper);
            vector::remove(&mut borrow_global_mut<Diffusion_store_tree>(create_resource_address(&@dapp,Seed)).save_Helper_list.list,index);
        }
        // let helper_index = check_helper_index(caller);
        // assert!(helper_index!=99,NOT_HELPER);
    }

    ////////////////// Admin fun /////////////////////////////////
```
寫admin會用到的function

### 2024.09.21

今天來學習 object 的用法和理解
`https://www.youtube.com/watch?v=bny8hBEpBmw`

```
<!-- Content_END -->
