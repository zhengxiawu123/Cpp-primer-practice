﻿#C++ primer 第四章 表达式 

标签（空格分隔）： C++ 编程

---

### 基础

---

C++当中表达式分为一元运算符与二元运算符，一元运算符类似于取地址，或者取值。二元运算符类似于== + - > <等等。

* 运算对象转换：一般来说，运算对象常常转换成另外的类型 ，某些类型会获得提升

* 用户可以根据自己的喜好，来定义新的重载运算符。
* C++对象有左值右值，**当一个对象被用作右值的时候，使用的是这个对象的值，当一个对象被用作左值，用的是对象的身份（在内存当中的位置）**，例如：赋值运算的左边就是左值，右边就是右值。取地址符号，作用在一个左值上面，但是取到地址之后，变成右值。解引用符号，下表结果以及应用对象都是左值。内置类型以及迭代器递增递减用的都是左值。
* 在表达式当中有优先级与结合律，一般来说优先级定义我们需要先运行那些操作，结合律则告诉我们当优先级一致的时候，我们需要从左往右运算。

>练习 4.1 20
>练习4.2  （a） *(vec.begin()) (b) (*vec.begin())+1

* 当我们使用一些没有求值顺序的运算符号的时候，C++编译器会随机的对于表达式进行求职。比如<<没有定义何时运算，所以当我们输出的时候可能出现不一样的结构 Int i=0;cout<<i<<" "<<i++<<endl;可能输出1 1 也可能输出0 1
* 有四种运算符号定义了求值顺序，&& || ?: ,

>练习4.3 可以接受，因为我们在大部分的时候，定义的时候不需要明确指出求值顺序，只需要一般的指定就可以了。

---

### 算术运算符

* 我们需要注意的是，一元运算符 对于Bool来说，没影响。true加一个符号，会被提升为1 最后变成-1bool类型-1就是true

> 练习4.5 -86 -18 0 -2
>练习4.6 if(i%2==0){偶数}else{奇数}
>练习 4.7 short i = 32767;

---

### 逻辑和关系运算符

* **在我们使用判断的时候，使用if(val)而不使用if(val==true)后面的会把true转换成1**

>练习4.8 相等运算等级最大，先运算。然后总做往右运算。
>练习4.9 首先运算取值符号，然后转换成布尔类型，最后判断，最后结果为true
>练习4.10 int i;while(i==42){cin>>i;}
>练习4.11while(a>b&&b>c&&c>d){}
>练习4.12 首先从左往右，假如i==j那就变成了0<k如果i!=j变成了1<k

---


### 赋值运算符

* 赋值运算的左侧必须是一个可以修改的值。
* 赋值运算满足右结合律
>练习4.13 d=3 i=3  d=3.15 i=3
>练习4.14 if(42=i) 错误 if(i=42) 相当于if(true)
>练习4.15 修改成 dval = ival = 0；pi=nullptr；
>练习4.16 （a）if((p=getPtr())!=0) (b)if(i==1024)

---

### 递增和递减运算符

* 递增和递减有两个版本，前置版本和后置版本，**前置版本的运算更快**
* 当我们在具体的程序当中，既让变量+1-1又要获得原来的值，这个时候就可以使用后置的项目。
* 如果一条子表达式改变了某个运算对象的值，另一条子表达式又要使用该值的话，这样的话，编译器可能会产生错误，会用任意一种方式来运行程序。

>练习4.17 前置运算符一般来说在没有赋值的时候都一样，但是当需要赋值或者作为子语句的时候，++i代表先进行自增运算，i++代表先进行另外的子语句。
>练习4.18 会先得到移动后的值。
>练习4.19 (a)首先判断 ptr 是否为控指针，然后判断ptr是否为0 然后ptr指向的整数自加一
>(b)首先判断ival是否为0然后i自加。原意的话，应该是(ival+1) && ival
>(c)等价于vec[ival]<=vec[ival] 但是本意应该是 vec[ival+1]<=vec[ival]

### 成员访问运算符

* 成员访问运算符的优先级很低，所以我们在运算的时候，应该要先解引用（针对于指针），然后再进行成员访问。

>练习4.20 
>(a) 合法，后置自加的运算优先级大于取值
>(b)不合法，无法自加。
>(c)非法，iter是一个迭代器，没有empty
>(d)合法，看当前的元素是否为空
>(e)合法 前置自加的运算优先级大于取值。
>(f)合法 判断iter是否为空，然后自加

### 条件运算符

* cond?expr1:expr2;来进行具体的运算
* **需要注意的是，这种方式在进行混合语句的时候，它的优先级很低，所以我们最好要把它用括号括起来，比如cout<<grade<60?"fail":"pass"就会产生错误**

>练习4.23 （首先，编译应该是通过的，但是和原来的意思不符合） 因为加的优先级比较大，所以在进行运算的时候，会优先算加，应该把后面括号括起来。
>练习4.24 从左边往右加

### 位运算符

---

* 位运算符作用于整数类型的对象。
* 位运算符号对于有符号类型的符号位没有明确定位。所以建议不要在有符号的情况下进行位运算
* 其实我们经常使用的IO中的<<其实是一种重载的移位操作。在这里，我们也要知道，io当中的<<满足做结合律，当使用优先级比自己小的时候，可能会出现错误的情况。

>练习4.25 会变成int 之后再进行补码的转换，编程-7296
>练习4.26 unsigned int占了16位，这样的话就不足够了
>练习4.27 (a) 4 (b) 7 (c) true (d) true

>练习 4.29 第一个输出是10 第二个输出是指针的大小，比上数组中第一个元素的大小
>练习4.30 (a)什么也不用改变 (b) sizeof (p->mem[i]) (c)sizeof (a<b)如果比较a的尺寸和B的大小的话，什么也不用改变。(d)不用改变

>练习4.31在这个程序当中，前置后置结果一样，一般来说，使用前置，方便运算。
>练习4.32通过指针以及下表来遍历数组
>练习4.33判断somevalue是否为真，如果为真，那么x 和y 自加如果为假，自减

---

### 类型转换

算数之间的转换：
int ival = 3.5+3
当int 和double之间进行运算，为了不损失精度，会把int先转换成doble但是在进行初始化的时候，又会把double转换成Int
当下列条件会发生转换：
* 大多数情况下，比int小的类型转换成较大的类型
* 条件中，非bool转换成bool
* 初始化的时候，转换成初始类型，赋值的时候转换成左边的值。
* 如果算是关系多种类型，转换成同一种类型

---

#### 算数转换

---

整型提升:当比整型类型小的与整型进行运算的时候，我们需要提升称为Int 比较大的char转换成 所能容纳的最小的类型。

无符号类型的转换

无符号类型的转换，要看具体的大小，如果无符号类型大，那么有符号类型转换成无符号类型。反之，如果有符号可以容纳下无符号的，转换成无符号，反之，有符号转成无符号。

>练习4.34(a)转换成为布尔类型(b)首先ival转换成float然后因为左边转换成double(c) 首先cval转换成int类型，然后转换成double类型。
>练习4.35(a)没有发生(b)ival转换成float然后ui，然后如果ui转成float（c）ui转成float 然后转成dobule (d) ival转成float然后和转成double 然后最后转为cchar

---

####其他隐式转换

---

* 数组被自动转换成指针 当被用作decltype的时候，或者作为& sizeof typeid 等的运算对象的时候，就不会进行转换
* 指针可以被转换：0 nullptr转为任意类型的指针 任意非常量的指针可以转为void* 指向任意对象的指针可以转换为const *void
* 指针可以自动被转换成布尔类型
* 引用和指针可以转换成指向常量的指针或者引用。
* cin可以转换成为bool类型

---

#### 显示转换

命名的强制类型转换：
cast-name< type >(expression)：

* static_cast不包括底层const的都可以用这个语句进行转换，static_cast也有一个新的用处，就是找回void*指针，我们可以通过static_cast来找回原来的指针。只要类型正确的话。
* const_cast:这个主要用来来找底层const，当是底层const的时候，我们可以使用这个来转换回去，常常用于函数重载中。
* reinterpret_cast是一个危险的行为，当我们定义的时候，我们必须要记住它原来的指针。因为它会跳过编译器的类型检查。
* 旧版本的类型转换如同C语言中的

>练习 4.36 i* = static_const< int >(d);
>练习4.37 (a) pv = static_const< void* >ps;(b) i = static_const< int >(*pc)(c) pv = static_const< void* >(d) pc = static< char* >(pv)
>练习4.38 直接强制转换成double








