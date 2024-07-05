### Tips

#### o2·o3优化

```c
#pragma GCC optimize(1)
#pragma GCC optimize(2)
#pragma GCC optimize(3,"Ofast","inline")
```



#### 对拍

#### typing

#### c++ 官方文档

`https://zh.cppreference.com/w`



#### 二维矩阵旋转坐标变换

```c++
原坐标 a[i][j];
顺时针 90 度 a[j][n - i + 1];
顺时针 180 度 a[n - i + 1][n - j + 1];
顺时针 270 度 a[n - j + 1][i]
```



#### 结构体重载

```c++
#include<bits/stdc++.h>
using namespace std;
struct Node{
	int a,b;
	bool operator<(const Node & n)const{//Node相当于下面cmp的a  相当于cmp的b； 
		return a<n.a;//重新定义了小于号  如果a<n.a 那么小于号就是‘<’ 
	}
};
bool cmp(Node a,Node b){ 
	return a.a<b.a;//sort排序出来之后这是升序	a.a<b.a则是小于  
	return a.a>b.a//a.a>b.a是小于   也就是说  <是这里的'>' 
}
int main(){
	Node a[10];
	a[0].a=5;a[1].a=6,a[2].a=7;
	Node e;e.a=6;
	cout<<(*(lower_bound(a,a+3,e))).a;//lower_bound()的结构体实现 
	cout<<(*(upper_bound(a,a+3,e))).a;//upper_bound()的结构体实现 
	sort(a,a+2);
	cout<<a[0].a<<" "<<a[1].a;
	
} 
```



```c++
struct newtype{
    int a,b;
    bool operator <(const newtype & tmp)const{
        if (tmp.a!=a) return a<tmp.a;
        return b>tmp.b;
    } // a作为第一关键词升序（从小到大），b作为第二关键词降序
}x[100];
```



>一般地，赋值运算符重载的参数是结构体const的引用，加const是因为：
>
>①我们不希望在这个函数中对用来进行赋值的“原版”做任何修改。
>
>②加上const，对于const的和非const的实参，函数就能接受；如果不加，就只能接受非const的实参。
>
>用引用是因为：这样可以避免在函数调用时对实参的一次拷贝，提高了效率。
>
>## 注意：
>
>上面的规定都不是强制的，可以不加const，也可以没有引用，甚至参数可以不是函数所在的对象。

####  map容器按值（value）排序

```c++
bool cmp(const PAIR& x, const PAIR& y)
{
	return x.second > y.second //降序 
}
typedef pair<string, int> PAIR
map<string, int> mp;

vector<PAIR> v(mp.begin() ,mp.end() );
sort(v.begin(), v.end(), cmp);

```

#### map遍历

```c++
//迭代器版本
auto i = my_map.begin();
while(i != my_map.end()){
    cout << i->first << ":" << i->second << endl;
    i++;
}
//另一种写法
for (auto i = my_map.begin(); i != my_map.end(); ++i)
    cout << i->first << ":" << i->second << endl;
//C++11新特性
for(auto i:my_map)
　　cout << i.first << ":" << i.second <<endl;
for(auto [u, v] : mp)
	std::cout << u << ' ' << v << '\n';

```



#### 内联函数

#####  next_permutation

```

```

##### __builtin_popcount

```

```



#### 函数封装

##### 1\. 定义

函数模板不是一个实在的函数，编译器不能为其生成可执行代码。定义函数模板后只是一个对函数功能框架的描述，当它具体执行时，将根据传递的实际参数决定其功能。

##### 2\. 用法

C++函数模板提高了程序的可重用性，我的粗浅的理解就是写一个功能相似的模具，比如写了一个做杯子的方法，材料在将来可以选择塑料、玻璃、等等。

2.1 变量交换函数模板

假如不使用模板函数，那么如果定义一个交换两个整型变量的值的函数，代码如下：

```cpp
void Swap(int &x, int &y){
    int temp = x;
    x = y;
    y = temp;
}
```

如果是浮点类型的变量的值交换，则替换int 为double 即可。

```cpp
void Swap(double &x, double &y){
    double temp = x;
    x = y;
    y = temp;
}
```

但是如果需要更多类型之间进行交换时，显然就会做很多重复性的工作，这个时候，模板函数应运而生。

在C++中，模板分为函数模板和类模板两种：

-   函数模板是用于生成函数
-   类模板则是用于生成类的

###### 2.2 函数模板的声明和模板函数的生成

1）函数模板的声明

```objective-c++
templete <class 类型参数1， class 类型参数2, ...>
返回值类型 模板名(形参表) {
    函数体
};
```

说明：

-   templete是定义模板函数的关键字
-   templete后面的 <>不能省略;
-   class 可以用typename代替，是声明数据类型参数标识符的关键字，用以说明它后面的标识符是数据类型标识。

交换函数的模板函数可以写成：

```cpp
templete <class T>
void Swap(T &x, T &y) {
    T temp = x;
    x = y;
    y = temp;
}
/*其实就是把数据类型变量换成 T */
```

注意：

-   在templete语句与函数模板定义语句<返回类型> 之间不允许有别的语句，以下是错误示范：

```text
templete<class T>
int I;
void Swap(T &x, T &y){

}
```

-   函数模板允许使用多个类型参数，但在templete定义部分的每个形参前必须有关键字typename或class

```cpp
template <class T1, class T2>
T2 MyFun(T1 arg1, T2 arg2)
{
    cout<< arg1 << " "<< arg2<<endl;
    return arg2;
}
```

2）如何调用定义好的函数模板

```cpp
int main()
{
    int n = 1,m = 2;
    Swap(n,m); //编译器自动生成 void Swap(int & ,int & )函数

    double f = 1.2,g = 2.3;
    Swap(f,g); //编译器自动生成 void Swap(double & ,double & )函数

    return 0;
}
```

编译器由模板自动生成函数的过程叫做 模板的实例化。由模板实例化而得到的函数称为 模板函数。在某些编译器中，模板只有在被实例化时，编译器才会检查其语法的正确性，如果程序中写了一个模板却没有用到，那么编译器不会报告这个模板中的语法错误。

模板调用语句也可以明确指明要把类型参数实例化哪种类型。例如：

```cpp
int main()
{
    int n = 1,m = 2;
    Swap<int>(n,m);     // 指定模板函数的变量类型为int

    double f = 1.2,g = 2.3;
    Swap<double>(f,g); // 指定模板函数的变量类型为double

    return 0;
}
```

###### 2.3 函数模板的重载

首先说明函数模板和函数重载区别：

函数重载时：每个函数体可以执行不同的动作，但同一个函数模板实例化后的函数都必须执行相同的动作，只是类型不同，就是都是做同一款杯子，虽然材料不同，但是工序相同。

函数模板也可以重载，只要他们的 形参表 或 类型参数表 不同即可。

```cpp
//模板函数1
templete<class T1, class T2>
void print(T1 arg1, T2 arg2) {
    cout<<arg1<<" "<<arg2<<endl;
}
//模板函数2
templete<class T>
void print(T arg1, T arg2) {
    cout<<arg1<<" "<<arg2<<endl;
}
// 模板函数 3
template<class T,class T2>
void print(T arg1, T arg2) 
{
    cout<< arg1 << " "<< arg2<<endl;
}
```

可以看到：

①模板函数1 和模板函数2 不仅参数数量不同，参数类型也不同

②模板函数1和模板函数2 的参数类型是不同的

**编译器在处理函数调用语句时的顺序：**

1.  参数完全匹配的普通函数
2.  参数完全匹配的模板函数
3.  实参数经过自动类型转换后能够匹配的普通函数
4.  上面的都找不到，报错

```cpp
// 模板函数 - 1个参数类型
template <class T>
T Max(T a, T b) 
{
    cout << "TemplateMax" <<endl; return 0;
}

// 模板函数 - 2个参数类型
template <class T, class T2>
T Max(T a, T2 b) 
{
    cout << "TemplateMax2" <<endl; return 0;
}

// 普通函数
double Max(double a, double b)
{
    cout << "MyMax" << endl;
    return 0;
}

int main() 
{
    int i=4, j=5;

    // 输出MyMax - 匹配普通函数
    Max( 1.2, 3.4 ); 

   //输出TemplateMax - 匹配参数一样的模板函
    Max( i, j );

    //输出TemplateMax2 - 匹配参数类型不同的模板函数
    Max( 1.2, 3 );   

    return 0;
}
```

##### 3\. 类模板

###### 3.1 定义

```text
templete <class Type1, class Type2, ... > //类型参数列表
class TClass {
    //TClass 的成员函数
    private:
        Type1 DataMember;
        Type2 DataMemeber2;
    //...
};
```

注意类属参数至少在类说明中出现一次

用类模板定义对象的写法:

```text
类模板名<真实类型参数表>对象名(构造函数实参表)
TClass<int,int> a(100,50)
```

1）单个类模板语法

```cpp
 //类的类型参数化 抽象的类
 //单个类模板
 template<typename T>
 class A 
 {
 public:
     A(T t)
     {
         this->t = t;
     }
 
     T &getT()
     {
         return t;
     }
 protected:
 public:
    T t;
 };
void main()
 {
   //模板了中如果使用了构造函数,则遵守以前的类的构造函数的调用规则
     A<int>  a(100); 
     a.getT();
     printAA(a);
     return ;
}
```

2）Pair类模板例子

```cpp
// 类模板
template <class T1, class T2>
class Pair
{
public:
    Pair(T1 k, T2 v):m_key(k),m_value(v) {};
    bool operator < (const Pair<T1,T2> & p) const;
private:
    T1 m_key;
    T2 m_value;
};

// 类模板里成员函数的写法
template <class T1, class T2>
bool Pair<T1,T2>::operator < (const Pair<T1,T2> &p) const
{
    return m_value < p.m_value;
}

int main()
{
    Pair<string,int> Astudent("Jay",20); 
    Pair<string,int> Bstudent("Tom",21);

    cout << (Astudent < Bstudent) << endl;

    return 0;
}
```

输出结果

```text
1
```

**注意：**

-   **类模板里成员函数的写法**

**templete <class Type1, class Type2>**

**返回值类型 类模板名<Type1,Type2>::函数名(形参列表){}**

-   **同一个类模板的两个模板类是不兼容的**

```cpp
Pair<string,int> *p;
Pair<string,double> a;
p = & a; //错误！！
```

###### 3.2 函数模板作为类模板成员

没有什么特别的地方，只是把函数模板的声明写在了类的成员函数而已，其模板参数类型并不需要出现在类模板的参数类型里。

```cpp
// 类模板
template <class T>
class A
{
public:
    template<class T2>
    void Func(T2 t) { cout << t; } // 成员函数模板
};

int main()
{
    A<int> a;
    a.Func('K');     //成员函数模板 Func被实例化
    a.Func("hello"); //成员函数模板 Func再次被实例化

    return 0;
}
```

###### 3.3 类模板与非类型参数

类模板的<类型参数表>中可以出现非类型参数:

```cpp
template <class T, int size>
class CArray
{
public:
    void Print( )
    {
        for( int i = 0;i < size; ++i)
        cout << array[i] << endl;
    }
private:
    T array[size];
};

CArray<double,40> a2;
CArray<int,50> a3; //a2和a3属于不同的类
```

个人理解：在类的实例化时，这个类型参数要传入，其实相当于强制要求传入一个int 类型量。当实例化时，传入了size，也就自动定义了array数组的大小。

  

这里多亏了前辈的总结，我这里只是学习前辈门总结的资料，做了一些笔记而已。附上链接：

[小林coding：C++ 模板常见特性（函数模板、类模板）](https://zhuanlan.zhihu.com/p/101898043)

[C++模板：函数模板和模板函数\_HavenZhao的专栏-CSDN博客\_函数模板和模板函数](https://blog.csdn.net/BeyondHaven/article/details/4204345?ops_request_misc=&request_id=&biz_id=&utm_medium=distribute.pc_search_result.none-task-blog-2~all~es_rank~default-4-4204345.es_vector_control_group&utm_term=C%2B%2B+%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0&spm=1018.2226.3001.4187)

[C++函数模板（模板函数）详解\_low5252的博客-CSDN博客\_模板函数](https://blog.csdn.net/low5252/article/details/94622335?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522164707730716780264051009%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=164707730716780264051009&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-2-94622335.es_vector_control_group&utm_term=C%2B%2B+%E6%A8%A1%E6%9D%BF%E5%87%BD%E6%95%B0&spm=1018.2226.3001.4187)

未完待续....

* * *

#### Lamda 函数

##### 语法分析

>[函数对象参数] ([操作符重载](https://so.csdn.net/so/search?q=操作符重载&spm=1001.2101.3001.7020)函数参数) mutable 或 exception 声明 -> 返回值类型 {函数体}。可以看到，Lambda 主要分为五个部分：[函数对象参数]、(操作符重载函数参数)、mutable 或 exception 声明、-> 返回值类型、{函数体}.

(1) [capture][函数对象参数]：标识一个 Lambda 表达式的开始，这部分必须存在，不能省略。函数对象参数是传递给编译器自动生成的函数对象类的构造函数的。函数对象参数只能使用那些到定义 Lambda 为止时 Lambda 所在作用范围内可见的局部变量(包括 Lambda 所在类的 this，通俗：主函数的局部变量等)。函数对象参数有以下形式：

>1.  []。没有任何函数对象参数。
>2.  [=]。函数体内可以使用 Lambda 所在范围内所有可见的局部变量（包括 Lambda 所在类的 this），并且是值传递方式（相当于编译器自动为我们按值传递了所有局部变量）。
>3.  [&]。函数体内可以使用 Lambda 所在范围内所有可见的局部变量（包括 Lambda 所在类的 this），并且是引用传递方式（相当于是编译器自动为我们按引用传递了所有局部变量）。
>4.  [this]。函数体内可以使用 Lambda 所在类中的成员变量。
>5.  [a]。将 a 按值进行传递。按值进行传递时，函数体内不能修改传递进来的 a 的拷贝，因为默认情况下函数是 const 的，要修改传递进来的拷贝，可以添加 mutable 修饰符。
>6.  [&a]。将 a 按引用进行传递。
>7.  [a，&b]。将 a 按值传递，b 按引用进行传递。
>8.  [=，&a，&b]。除 a 和 b 按引用进行传递外，其他参数都按值进行传递。
>9.  [&，a，b]。除 a 和 b 按值进行传递外，其他参数都按引用进行传递。
>    **注意：值传递，在lambda函数定义时就确定了，不会随lambda引用改变。**

(2) (parameters)(操作符重载函数参数)：标识重载的 () 操作符的参数，没有参数时，这部分可以省略。参数可以通过按值（如: (a, b)）和按引用 (如: (&a, &b)) 两种方式进行传递。

(3) mutable 或 exception 声明：这部分可以省略。按值传递函数对象参数时，加上 mutable 修饰符后，可以修改传递进来的拷贝（注意是能修改拷贝，而不是值本身）。exception 声明用于指定函数抛出的异常，如抛出整数类型的异常，可以使用 throw(int)。

(4) ->return-type-> 返回值类型：标识函数返回值的类型，当返回值为 void，或者函数体中只有一处 return 的地方（此时编译器可以自动推断出返回值类型）时，这部分可以省略。

(5) {statement}{函数体}：标识函数的实现，这部分不能省略，但函数体可以为空。





##### 递归写法

```c++
#include <iostream>
#include <functional>

int main()
{
    std::function<int(int)> f = [&f](int n) {
        if (n == 0 || n == 1) {
            return 1;
        }

        return n * f(n - 1);
    }

    std::cout << f(5) << std::endl;
}
```

>   这种写法避免了使用 `auto f = [&f](int n)` 。如果使用 auto 会造成 f 的类型推导不出来，因为 f 的类型依赖于后面的 Lambda 表达式，而编译器在编译 Lambda 表达式时无法确定 f 的类型。借助 std::function 就可以避免推导 f 的类型。这种写法看似奇特，其实是合法的，原理与 C 语言的 [`void *p = &p;`](https://stackoverflow.com/questions/48369190/is-void-p-p-legal-in-c) 类似。

###### 0x01使用std::function

```c++
const auto& sum1 = [](const int& n) {
	std::function<int(const int&)>s;
	s = [&](const int& n) {
		return n == 1 ? 1 : n + s(n - 1);
	};
	return s(n);
};
```

```c++
int a = 1;
int b = 2;
function<void(int, int)> dfs = [&](int index, int steps) 
dfs(a,b);

```



###### # 0x02将lambda作为参数

```c++
const auto& sum2 = [](const int& n) {
	const auto& s = [&](auto&& self, const int& x) -> int{
		return x == 1 ? 1 : x + self(self, x - 1);
	};
	return s(s,n);
};
```

###### # 0x03使用Y组合子

```c++
const auto& y = [](const auto& f) {
	return [&](const auto& x) {
		return x(x);
	}([&](const auto& x) -> std::function<int(int)> {
		return f([&](const int& n) {
			return x(x)(n);
		});
	});
};
```

###### 0x04测试

```c++
int main() {
	std::cout << sum1(100);//print 5050
	std::cout << sum2(100);//print 5050
	std::cout << y(sum3)(100);//print 5050
}
```

#### accumulate 求和

```c++
#include <iostream>
#include <vector>
#include <numeric>

using namespace std;

template<typename T>
T SumVector(vector<T>& vec)
{
    T res = 0;
    for (size_t i=0; i<vec.size(); i++)
    {
        res += vec[i];
    }
    return res;
}

int main()
{
    vector<int> v = { 1, 2, 3, 4, 5 };
    cout << "sum1: " << SumVector(v) << endl;
    cout << "sum2: " << accumulate(v.begin(), v.end(), 0) << endl;
    cout << "sum3: " << accumulate(v.begin(), v.end(), 5) << endl;
    return 0;
}

```



#### 上取整

```c++
a = (a + n - 1) / n;
```

#### 去除前导零

```c
while (C.size() > 1 && C.back() == 0)
	C.pop_back();
```

#### bitset     &       vector<bool> 

>随机访问时，bitset更快；连续访问时，bool更快。所以多测如果要清空时，建议选bool数组，选bitset此时可能会TLE。

####c++ 各种读入总结， cin, getline, sstream

##### 1. cin

cin 是从缓冲区读入，会把空格回车等不可见字符当做分割，跳过。并且最后读入后，后面会剩余未读入的部分，比如空格，回车等。

######2. getline

getline 配合 cin. 格式getline(cin,s) ,s 是个字符串类型。缓冲区的第一行，以回车作为分割符，放入字符串s，回车不会放入。如果缓冲区只有一个回车，那个执行后，缓冲区的回车被取走，s为空串。

#####3. sstream 中的 stringstream

格式 ' stringstream ssin; ssin << s; ' s 是个字符串，通常用getlien(cin, s);获得。
指向后， ssin 相当于一个缓冲区，保存了字符串里面的所有字符。
然后通过 ssin >> a; 把字符串赋给a，a可以是各种类型，会跳过空格。和cin类似。

##### 4.sscanf ssprintf



>   注意：
>
>   普通的读入可以用cin
>   当出现要读入一个数组，当时不知道元素个数的时候，用 stringstream

```####c++
#include<sstream>//stringstream 的头文件
#include <iostream>
using namespace std;
int num[100];
int num2[100];
int main()
{
    int a, b;
    cin >> a >> b;//a b 保存 1 2
    string s;
    getline(cin, s);//读入cin剩下的回车
    getline(cin, s);//读入第二行， 不会剩下回车，回车不会给s
    stringstream ssin;
    ssin << s;//将s 放入 ssin
    int cnt = 0;
    int x;
    while (ssin >> x) num[cnt++] = x;//以空格为分割，一个个拿出给x，  3 4 5 保存到了num
    getline(cin, s);//读入第三行， 不会剩下回车，回车不会给s
    stringstream ssin1;//一个对象只能用一次，再次使用需要新的
    ssin1 << s;
     cnt = 0;

    while (ssin1 >> x) num2[cnt++] = x;//6 7 8 保存到了 num2

}
```

#### cout 前导零

```c++
#include<iomanip>  //  必须加上这个头文件
#include<iostream>
using namespace std;
//  用printf 是直接这样即可解决前导0，printf("%02d",a);
int main()
{
   int a=5;
   cout<<<setw(2) <<setfill('0')<<a<<endl;  //  这样写就有前导零了，输出 05
   //printf("%02d",a);
   return 0;
}
```



#### cout 输出小数

```c++
int main( void ) { 
    const double value = 12.3456789;
    cout << value << endl; // 默认以6精度，所以输出为 12.3457 
    cout << setprecision(4) << value << endl; // 改成4精度，所以输出为12.35 
    cout << setprecision(8) << value << endl; // 改成8精度，所以输出为12.345679 
    cout << fixed << setprecision(4) << value << endl; // 加了fixed意味着是固定点方式显示，所以这里的精度指的是小数位，输出为12.3457 
    cout << value << endl; // fixed和setprecision的作用还在，依然显示12.3457 cout.unsetf( ios::fixed ); 
    // 去掉了fixed，所以精度恢复成整个数值的有效位数，显示为12.35 
    cout << value << endl; cout.precision( 6 ); 
    // 恢复成原来的样子，输出为12.3457
    cout << value << endl; 
}
```

#### 升序·降序

```c++
sort(arr.begin(), arr.end(), greater<int>()); // 降序
sort(arr.begin(), arr.end(), less<int>()); // 升序
```

#### lower_bound / upper_bound

```c++
vector<int> nums; // 需要先进行排序

// 查找 nums 中是否有等于 target 的数
binary_search(nums.begin(), nums.end(), target);

// 返回 nums 中第一个大于或等于 target 元素位置的迭代器
lower_bound(nums.begin(), nums.end(), target);
// 返回 nums 中第一个大于 target 元素位置的迭代器
upper_bound(nums.begin(), nums.end(), target);

// 返回 nums 中第一个小于或等于 target 元素位置的迭代器
lower_bound(nums.begin(), nums.end(), target, greater<int>());
// 返回 nums 中第一个小于 target 元素位置的迭代器
upper_bound(nums.begin(), nums.end(), target, greater<int>());

// 通过这种方式可得到下标
int index = lower_bound(nums.begin(), nums.end(), target) - nums.begin();
```

#### 区间赋值

fill

```c++
fill(dp.begin(), dp.end(), -1);
```

iota

```c++
// 第三个参数为第一个元素的值，之后元素的值以此 +1 递增
iota(fa.begin(), fa.end(), 0);

int val = 0;
for (int i = 0; i < fa.size(); i++) {
	fa[i] = val;
	val++;
}
```

#### 逆向遍历

```c++
	std::cout << mp.size() << '\n';
	for (auto it = mp.rbegin(); it != mp.rend(); it++)
		std::cout << it->second << " " << it->first << '\n';
```

#### setw()函数

>设置输出的域宽，n表示字段宽度。它**只对紧接着的输出有效**，紧接着的输出结束后又变回默认的域宽。当后面紧跟着的输出字段长度小于n的时候，在该字段前面用空格补齐；当输出字段长度大于n时，全部整体输出。

```c++
#include <iostream>
using namespace std;
 
#include <iomanip>
using std::setw;
 
int main()
{
    cout << 123456789 << endl;
    cout << setw(4) << 123 << setw(7) << 456789 << endl;
    return 0;
}
```

