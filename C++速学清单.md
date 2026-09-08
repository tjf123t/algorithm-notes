# C++ 速学清单（刷题够用版 · 1页起）

> 用途：给"学过 C、没学 C++"的人，只学刷题/蓝桥/机试够用的那点 C++。
> 范围：输入输出 + 常用 STL 容器 + sort 等算法函数。**不学**类/继承/多态/模板高级用法。
> 用法：每样先看"常用操作"，再抄一遍"最小示例"；学一个就在《蓝桥杯代码模板本》T01–T03 默写一遍。

## 0. 万能开头（每题先写这两行）

```cpp
#include <bits/stdc++.h>   // 一次包含所有标准库（OJ/蓝桥可用）
using namespace std;

int main() {
    ios::sync_with_stdio(false);  // 关同步：cin/cout 变快
    cin.tie(nullptr);             // 解绑，进一步提速
    // ...你的代码
    return 0;
}
```

> 注意：用了 `cin/cout` 就**别再混用 scanf/printf**（会乱序/超时）。

## 1. 输入输出

```cpp
int n; string s;
cin >> n;              // 读整数（自动跳过空格/换行）
cin >> s;              // 读字符串（遇空格停）
getline(cin, s);       // 读一整行（含空格）
cout << n << " " << s << "\n";   // 输出，\n 比 endl 快
// 多组输入：while (cin >> n) { ... }
```

## 2. vector（可变长数组，最常用）

```cpp
vector<int> a;              // 空数组
vector<int> b(n, 0);        // n 个 0
a.push_back(x);             // 尾部加 x
int sz = a.size();          // 元素个数
cout << a[i];               // 按下标访问
sort(a.begin(), a.end());   // 排序（升序）
```

## 3. string（字符串，比 char[] 好用）

```cpp
string s = "hello";
int len = s.size();              // 长度
s += '!';                        // 拼接
s.substr(pos, len);              // 取子串（从 pos 起 len 个）
s.find("ll");                    // 查找，找不到返回 string::npos
if (s.find('x') == string::npos) { /* 没找到 */ }
sort(s.begin(), s.end());        // 字符串也能排序
```

## 4. stack（栈）

```cpp
stack<int> st;
st.push(x);      // 入栈
int t = st.top(); // 看栈顶
st.pop();        // 出栈
bool empty = st.empty();  // 判空（stack 没有 clear，判空用 while(!st.empty())）
```

## 5. queue（队列）

```cpp
queue<int> q;
q.push(x);       // 入队
int f = q.front(); // 看队首
q.pop();         // 出队
q.empty();       // 判空
// 注意：queue 没有 clear()；清空用 while(!q.empty()) q.pop();
```

## 6. priority_queue（优先队列 / 堆）

```cpp
priority_queue<int> pq;                          // 默认大顶堆（取最大）
priority_queue<int, vector<int>, greater<int>> pq2;  // 小顶堆（取最小）
pq.push(x);
int t = pq.top();   // 取堆顶（最大/最小）
pq.pop();
// 用途：每次取当前最大/最小（贪心、Dijkstra）
```

## 7. map（键值对 / 字典）

```cpp
map<string, int> mp;   // key->value
mp["apple"]++;         // 不存在会自动创建为 0
mp.count("apple");     // 判断 key 是否存在（0/1）
mp["apple"];           // 取值
for (auto &p : mp) { cout << p.first << " " << p.second; }  // 遍历（按键排序）
```

## 8. set（集合，自动去重 + 排序）

```cpp
set<int> s;
s.insert(x);     // 插入
s.count(x);      // 是否存在（0/1）
s.erase(x);      // 删除
// 遍历即从小到大
```

## 9. sort + 自定义排序（蓝桥排序题核心）

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Node { int score; string name; };

bool cmp(const Node &a, const Node &b) {
    if (a.score != b.score) return a.score > b.score;  // 分数降序
    return a.name < b.name;                            // 同分按名字升序
}

int main() {
    vector<Node> v;
    sort(v.begin(), v.end(), cmp);   // 按 cmp 排序
    return 0;
}
```

## 10. 其他常用小函数

```cpp
int a = max(x, y), b = min(x, y);
swap(x, y);
reverse(v.begin(), v.end());     // 反转
// 数学：__gcd(x, y) 可以直接用（C++17）
```

---

## 检查清单（学完自测）

- [ ] 能默写万能开头（含关同步两行）
- [ ] 会用 cin/cout 读入输出、getline 读整行
- [ ] 会用 vector：push_back / size / 下标 / sort
- [ ] 会用 string：size / 拼接 / substr / find
- [ ] 会用 stack / queue：push / top·front / pop / empty
- [ ] 会建大小顶堆 priority_queue
- [ ] 会用 map 计数（mp[key]++）和 count 判断存在
- [ ] 会用 set 去重
- [ ] 会用结构体 + sort 自定义排序（cmp）

> 验收：每项都能不看上面、自己写出来 = 学会。然后去《蓝桥杯代码模板本》T01–T03 默写。