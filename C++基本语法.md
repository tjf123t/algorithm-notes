# C++ 基本语法（面向蓝桥杯 · 从 C 过渡）

> 适合：已经学过 C、准备用 C++ 刷题/参赛的人
> 定位：只讲蓝桥杯真正用得到的 C++，不学面向对象那套
> 配套：《C++速学清单.md》（速查版）——本文件是"教学详细版"，那份是"考场速查版"

---

## 0. 先理解 C++ 和 C 的关系

- **C++ 是 C 的超集**：C 里的 `int / char / for / while / 数组 / 函数 / scanf / printf` 在 C++ 里**全部能用**，不需要重学。
- 蓝桥 C/C++ 组用 `g++` 编译，提交文件后缀是 `.cpp`。
- 学 C++ 不是"推倒重来"，而是**在 C 基础上加工具**。

---

## 1. 万能开头（每道题先写这三样）

```cpp
#include <bits/stdc++.h>   // 一次包含所有标准库，蓝桥/洛谷都能用
using namespace std;       // 省得每次写 std::cin、std::cout

int main() {
    ios::sync_with_stdio(false);  // 让 cin/cout 变快
    cin.tie(nullptr);
    // 你的代码
    return 0;
}
```

---

## 2. 输入输出：cin / cout

| 功能 | 写法 |
| --- | --- |
| 读一个整数 | `cin >> n;` |
| 读一个字符串（遇空格停） | `cin >> s;` |
| 读一整行（含空格） | `getline(cin, s);` |
| 输出 | `cout << n << " " << s << "\n";` |
| 多组输入（读不到就停） | `while (cin >> n) { ... }` |

**对比 C**：
- `cin >> n` ≈ `scanf("%d", &n)`
- `cout << n` ≈ `printf("%d", n)`

**两条铁律**：
1. 用了 `cin/cout` 就**别混用 scanf/printf**；
2. 前面用 `cin` 读过数、后面要 `getline` 读整行时，中间加 `cin.ignore();` 吃掉残留换行符。

---

## 3. 多出来的常用类型

```cpp
bool flag = true;          // C++ 的真·布尔类型（C 里通常用 int 0/1）
long long x;               // 大整数，蓝桥必用
string s = "hello";        // 字符串（比 char[] 好用得多）
```

---

## 4. 引用 &（C++ 最重要的新概念之一）

`&` 表示"同一个东西的别名"，不复制。

```cpp
int a = 10;
int &b = a;   // b 是 a 的别名
b = 20;       // a 也变成 20
```

**刷题里最常见的一个用法——遍历字符串并原地修改**：

```cpp
for (char &c : s) {   // ★ 用 &，c 就是 s 里的那个字符本身
    c = toupper(c);   // 能真正改到 s
}
// 如果不写 &，改成 char c，那只是副本，改了没效果
```

---

## 5. 范围 for 循环（遍历整个数组/字符串/容器）

```cpp
vector<int> v = {1,2,3};
for (int x : v) cout << x << " ";   // 依次输出每个元素

string s = "abc";
for (char c : s) cout << c;         // 依次输出每个字符
```

---

## 6. string（字符串）常用操作

```cpp
string s = "hello";
int len = s.size();          // 长度
s += '!';                    // 拼接
string sub = s.substr(0, 3); // 取子串（从 0 起 3 个）
if (s.find("ll") != string::npos) { /* 找到了 */ }
s == "hello";                // 直接比较（C 里要 strcmp）
reverse(s.begin(), s.end()); // 反转
sort(s.begin(), s.end());    // 排序
```

---

## 7. vector（可变长数组）

```cpp
vector<int> a;              // 空数组
vector<int> b(10, 0);       // 10 个元素，都是 0
a.push_back(x);             // 尾部加一个
int sz = a.size();          // 元素个数
cout << a[i];               // 按下标访问
sort(a.begin(), a.end());   // 排序
```

---

## 8. 其他容器速览（背操作名即可）

```cpp
stack<int> st;   st.push(x); st.top(); st.pop(); st.empty();
queue<int> q;    q.push(x);  q.front(); q.pop(); q.empty();
// 小顶堆（每次取最小）
priority_queue<int, vector<int>, greater<int>> pq;
map<string,int> mp;  mp["a"]++;  mp.count("a");  // 键值对/计数
set<int> s;          s.insert(x); s.count(x);    // 自动去重+排序
```

---

## 9. sort + 自定义排序（蓝桥排序题核心）

```cpp
struct Node { int score; string name; };

bool cmp(const Node &a, const Node &b) {
    if (a.score != b.score) return a.score > b.score;  // 分数降序
    return a.name < b.name;                            // 同分按名字升序
}

vector<Node> v;
sort(v.begin(), v.end(), cmp);
```

**心法**：`return a < b` 是升序（a 排在 b 前面）；`return a > b` 是降序。

---

## 10. 常用小函数

```cpp
int a = max(x, y), b = min(x, y);
swap(x, y);
reverse(v.begin(), v.end());
__gcd(x, y);   // 最大公约数（C++17 可直接用）
toupper(c); tolower(c); isdigit(c); isalpha(c);
```

---

## 上手路线（结合你的情况）

1. **第 1 天**：只练"万能开头 + cin/cout + string"三样，用 C++ 重写一道做过的字符串题（如 B2115 密码翻译）；
2. **第 2–3 天**：加 vector 和 sort，重写一道排序/数组题；
3. **第 4–5 天**：加 map/set，重写去重/计数题（B2098、B2110）；
4. **第 6–7 天**：把《蓝桥笔记整合版》第二部分的 C++ 套路（分词、逐字符变换、子串/回文）全部用 C++ 默写一遍。

## 别学的东西（蓝桥用不上，先跳过）

类、继承、多态、模板、异常、智能指针、lambda 高级用法。