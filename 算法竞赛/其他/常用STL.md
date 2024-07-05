#! https://zhuanlan.zhihu.com/p/635986757
## 常用STL容器

### vector

变长数组，倍增思想

```c
std::vector<int> a(n); // 定义一个长度为n的vector容器, 初始值为0
a.size();
a.empty();
a.clear();
a.front() = a[0] / a.back() = a[n - 1];
a.push_back() / a.pop_back(); // 尾插，头弹出
a.begin()/a.end();
```

>需要注意的是 std::vector<bool> 不是stl容器

```c++
std::vector<int>;
std::vector<std::string>
std::vector<std::pair<int, int>>;
std::vector<std::vector<int>> a(n, std::vector<int> (n)) // n * n 二维数组
== std::vector a(n, std::vector<int>(n)); // 部分c++低版本不支持
```



### string

```c++
substr()    c_str()
size()/length();
empty();
clear();
find();
````

### queue

```c++
size();
empty();
push();// 向队尾插入一个元素
front();// 返回队首元素
back();// 返回队尾元素
pop();// 弹出队头元素
```

###priority_queue

优先队列，默认是大根堆
```c++
std::priority_queue<int,vector<int>,greater<int>>q;
std::priority_queue<int,vector<int>,less<int>>q;
// int 也可换成 std::pair<int, int>
```

```c++
push();// 插入一个元素
top();// 返回堆顶元素
pop();// 弹出堆顶元素
```

### deque

### stack

````c++
size();
empty();
push();
top();
pop();
````

### pair<int,int>

-   first第一个元素
-   second第二个元素	
-   支持比较运算，以first为第一关键字，second为第二关键字（字典序）

```c++
std::pair<int, string>;
.......
```



set, map, multiset, multimap

```c++
size();
empty();
clear();
begin()/end();
```

### set/multiset;

set 元素单调且不重复，multiset元素可重复

```c++
insert();
find();
count();
erase();
	(1)输入是一个数x，删除所有x O(k + log n)
	(2)输入一个迭代器，删除这个迭代器
lower_bound()/upper_bound();
	lower_bound(x)  返回大于等于x的最小迭代器
	upper_bound(x)  返回大于x的最小的数的迭代器
```

###  map/muiltimap

map表示一种映射关系

```C++
std::map<int, int>;
std::map<int, vector<int>>;
std::map<int, bool>;
```



```c++
insert();   插入pair 
erase();  输入pair 或者 迭代器
find();  O(log n)
lower_bound()/upper_bound();
```

unordered_map,
unordered_set,
unordered_multimap,
unordered_multiset

### bitset

压位	        

```c++
bitset<10000>s;
~,&,|,^
>> << 
==    != 
count()返回多少个1

any()判断是否至少一个1
none() 判断是否全为零

set();把所有位置成一
set(k,v) 将第k位变成v
reset() 所有位变成0
flip() 等价于~
flip(k) 第k位取反
```