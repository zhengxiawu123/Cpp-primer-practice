﻿# C++ primer 第三章 

标签（空格分隔）： C++ 编程

---

### 命名空间using声明

我们可以使用using来访问命名空间当中的名字 using namespace::name;

**头文件一般不包含using，别的程序也一起使用的话会产生困惑**

---

### 标准库类型 string

---

* string的初始化有两种方式，一种直接是拷贝初始化，类似于string s1 = s2;也就是说，编译器把等式右边的值拷贝到等式左边去。另外一种是直接初始化，string s1("test")就是直接赋值
*  **string==与!=号对大小写敏感**
*  当我们用cin来读取字符串的时候，会自动过滤掉空格，当时当我们使用getline的时候，可以自动的保留所有的字符。getline输入一个输入流以及一个字符串。
*  empty判断是否为空，size判断长短，size返回的是一个string::size_type size_type是一个无符号类型的，所以要避免使用int 类型的。
*  string对象可以使用大于小于，大于等于或者小于等于，两个string对象长度不同，并且小的string对象与长的string对象类型上的字符一样，就说明短的string 小于长的string
*  如果两个对象在某些位置上不太一样，那么比较的是第一个字符的结果
*  string相加就是连接。

>练习 3.3 string 的输入忽略空格 getline 保留空格

* C++把C里面的东西命名为cxxx去掉了h后缀
* 在C++当中，我们具体访问string中每一个类型的时候，可以使用for(auto c:str)
* 当我们在改变字符里面具体的值的时候，我们可以使用引用的方式，来改变s里面具体的值。
*  **我们需要注意的是，我们在对于string类型进行操作的时候，应该总是设置成string::size_type类型，或者我们可以直接使用decltype(s.size())**

>练习3.9 不合法 s[0]没有字符
>练习3.10 c的类型是一个指向s的引用

### 标准类型库vector

---

* 标准类型库vector代表的是对象的集合，其中所有的类型都相同。**需要注意的是，早期的C++vector类里面，我们在具体定义vector的容器的时候，需要多加一个空格vector<vector<int> >**
* 在进行具体的初始化的时候，可以进行列别初始化，但是有一个例外，当花括号里面的值不允许被列表初始化的时候，自动转为构造初始化。

> 练习3.12 (a)正确 形成了一个空的ivec (b)错误，无法互相转换 (c)正确，构造初始化
> 练习3.13 (a) 0 0 (b) 10 0 (c) 10 42 (d) 1 10 (e) 2 {10,42}(f) 10 ''(g) 10 "hi"

* 在vector当中，我们可以使用 push_back来对于vector进行添加元素，添加到vector的尾端
* vector的情况和C反而相反，**当我们指定了具体的长度的时候，运行的效率反而会变慢**
* **如果循环体内包含了对于vector的添加元素的语句，不能使用C++11新标准定义的简单的for循环(for (declare:expression))，因为for循环内部定义了具体的end()如果添加了之后，会破坏掉**

---

* 我们可以使用for (auto &i:v)来改变具体的值。（和string一样）
* 对于具体的相等，大于小于，和string一样，但是要注意的是，当内部的值可以被比较的时候，才可以比较。
* **vector不允许用下标去添加元素，只能使用push_back** 只能对于已知存在的元素进行下标操作。

>练习3.18 不合法，可以修改初始化方式 vector<int> ivec{0}
>练习3.19 vector<int> i = (10, 42) vector<int> i = {42,42,42,42,42,42,42,42,42,42} 使用 十次push_back

---

* 类似于string或者vector或者这种对象，可以使用迭代器来进行访问。类似于指针一样，迭代器也是一个一个的去指向。
* 迭代器类似于指针的指向，使用Begin返回第一个元素的指向，使用end返回最后一个元素的后一个位置的指向
*  **我们需要注意的是，当我们进行迭代器的时候，只有string以及vector有下标操作，其他的一些都没有，并且迭代器一般都没有大于小于操作，所以我们在使用的时候，最好同意一下，就是用==或者!=进行判断**
*  迭代器真正的类型，如果对于vector<int>的话就是 vector<int>::iterator it;当然也有const_iterator当是const的时候，类似于指针，我们只能读，不能写，类似的，当vector本身为const的时候，那么只可以读取，而不可以修改
*  在C++11当中，我们可以使用cbegin()获取到具体的const_iterator
*  对于具体的迭代器内部，我们可以使用圆括号加上\*来进行具体对象的调用 (*it)
*  为了简化上面的操作，我们使用了 -> 箭头运算符号，来把解引用符号，以及成员访问放在一起。
**只要使用了迭代器的循环体，就不要在迭代器所属的容器内部添加元素**
**在迭代器中，类似于指针，一个iterator代表了指向元素里面的一个“指针”，我们也可以使用(*it).member或者it->member来访问具体的内部的变量**

----

* 对于迭代器我们可以进行相关的操作，我们可以让他们相减，得到他们的距离，得到的是different_type 也就是带符号的整数。

> 练习3.26 因为不是从最开始的1/2里面搜索，是从我们确定的区间里面搜索。


---

###数组

* 数组和迭代器不一样的地方就是，数组是固定长度的，而迭代器不是。因为这样，所以数组运行效能更好。
* 定义数组的时候必须指定数组的类型，不允许auto来进行类型的推断
* 注意数组的指定的长度必须为const，但是在使用列表初始化的时候，我们可以忽略长度。
*  **数组不允许进行拷贝以及赋值（这里的赋值是指，不允许把一个数组直接赋值给另外一个数组）**
*  对于数组阅读的时候，最好从内向外来阅读

>练习 3.27 （c）非法，必须要是const类型 (d)非法 长度对不上
>练习3.28 sa 与 ia都被默认初始化为长度为10的空字符串以及0 sa2是空字符串数组  ia2 未被初始化。
>练习3.29 数组长度固定，不允许被赋值拷贝。而且速度块。

---

* 数组的下标是size_t类型，可以存放任意对象的大小，在cstddef里面定义了相关的类型。
* 数组可以使用unsigned来访问数组，注意不要超过具体的长度

>练习3.30 ix不应该小于等于 array_size 这样会导致溢出。
>练习3.33 什么也不会发生。程序不会出错，就是数组是未定义的。

---

* **在很多表达式当中，其实我们经常是对数组的指针进行操作，比如auto a(a1);如果a1是一个数组的话，那么返回的是只想a1第一个元素的指针**
*  但是我们使用decltype(a1)的话，我们还是可以得到正常的数组。
*  我们可以使用指针来访问数组，此时，所有迭代器支持的操作，数组指针全部都支持
*  在C++11当中，我们可以使用begin()以及end()操作，来获取相应的数组指针（因为直接用下标很容易出错）
*  两个指向数组的指针相减为一个**ptrdiff_t**的类型 它是一种带符号类型的。

>练习3.34 这里面p1指针并没有发生变化（也可以说发生了变化，但是只是p2指的对象给了p1），当两个指针指向不同类型的数组，就会出错，但是不同数组相同类型的也不会报错。

---

* **尽量不要使用C风格的字符串，会产生很多错误，C++的string操作方便，并且速度块**

>练习 3.37 输出每一个字符

>练习 3.38指针相加没有任何意义，因为指针存储的是地址，所以在进行相减的时候有意义，相加没有任何意义

---

* 针对于以前的程序（标准库还没出现之前）我们可以使用 string.c_str() c_str返回一个只想const char*来把一个string的变量转换成char[]变量。但是，当我们改变原先的string的时候，会改变char[]，所以真的要使用，先拷贝一份再说
* 我们可以使用数组来初始化vector 具体可以使用 vector<int> ivec(begin(int_arr),end(int_arr))

---

### 多维数组

* C++其实没有多维数组，所谓的多维数组其实是数组的数组。
* 习惯上,int a[3][4]我们把第一个成为行，第二个称为列。我们可以直接给出十二个元素来进行初始化。我们可以使用{{3},{3},{3}}仅仅初始化每一行的第一个元素。 我们也可以使用{1,2,3,4}来初始化第一行的四个元素。
* 我们使用下标进行访问的时候，我们可以使用与维度一样多的下标访问来获取具体的元素，如果不是，获取到的是具体的数组。比如我们可以使用 int (&row)[4]  = a[1]获得第二个数组的引用。
*  **(FBI warning!)在具体使用数组的时候，我们可以使用C++11新定义的范围for语句来遍历具体的数组，但是加入二维数组的时候，第一个需要定义为引用，也就是for(auto &row :a){for(auto col: row)}除了最里面一层，其他都要用引用，因为数组会自动转换成指针**
*  


