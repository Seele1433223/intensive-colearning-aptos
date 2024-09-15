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
<!-- Content_END -->
