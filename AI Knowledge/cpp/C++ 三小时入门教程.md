# C++ 三小时入门教程（Day 1）

> **适用对象**：零 C++ 基础，有 C 和 Python 经验  
> **学习时间**：约 3 小时（含练习）  
> **学习目标**：掌握 C++ 基本语法、输入输出、引用、函数重载、类的基础，以及 vector 容器  

---

## 📋 学习路线总览

| 时间段 | 内容 | 核心知识点 |
|--------|------|-----------|
| 第 1 小时 | C++ 初体验 | `cout`/`cin`、`string`、`namespace`、`auto` |
| 第 2 小时 | 引用与函数 | 引用 `&`、函数重载、类入门 |
| 第 3 小时 | 容器与实战 | `vector`、范围 for、简单文件 IO、综合练习 |

---

# 🕐 第 1 小时：C++ 初体验（60 分钟）

## 1.1 C++ 和 C 有什么不同？（5 分钟阅读）

你已经学过 C 语言，好消息是 C++ 几乎完全兼容 C！你之前写的所有 C 代码基本都能在 C++ 编译器下运行。C++ 在 C 的基础上增加了：

- **面向对象**：类（class）、对象
- **更安全方便的数据类型**：`string`、`vector`、智能指针
- **更简洁的语法**：`auto`、范围 `for`、`namespace`
- **标准模板库（STL）**：一大堆现成的数据结构和算法

"*C++ 就是 C 语言的超级进化版*" —— 这么理解就够了。

---

## 1.2 第一个 C++ 程序（10 分钟）

### 📝 要求：输出 "Hello, C++ World!"

```cpp
#include <iostream>   // C++ 标准输入输出头文件（不是 stdio.h！）

int main() {
    std::cout << "Hello, C++ World!" << std::endl;
    return 0;
}
```

### 🔍 讲解

| 代码 | 解释 |
|------|------|
| `#include <iostream>` | C++ 的输入输出头文件，相当于 C 的 `<stdio.h>` |
| `std::cout` | **标准输出流**，相当于 C 的 `printf` |
| `<<` | **流插入运算符**，把数据"送进"输出流 |
| `std::endl` | 换行并刷新缓冲区，等价于 `"\n"` + `fflush` |
| `std::` | **命名空间前缀**，C++ 标准库的东西都在 `std` 里面 |

### 💡 对比 C 语言

```c
// C 写法
#include <stdio.h>
int main() {
    printf("Hello, C++ World!\n");
    return 0;
}
```

```cpp
// C++ 写法
#include <iostream>
int main() {
    std::cout << "Hello, C++ World!" << std::endl;
    return 0;
}
```

**重点**：`cout` 很聪明，自动识别数据类型，不需要 `%d`、`%s` 这些格式控制符。

---

## 1.3 使用 `namespace std` 偷懒（5 分钟）

每次写 `std::` 很麻烦？可以用 `using namespace std;`：

```cpp
#include <iostream>
using namespace std;  // 声明使用 std 命名空间

int main() {
    cout << "不用写 std:: 了！" << endl;
    return 0;
}
```

> ⚠️ **注意**：大型项目中不推荐 `using namespace std;`，容易发生命名冲突。目前学习阶段可以使用。

---

## 1.4 输入：`cin`（10 分钟）

### 📝 要求：输入你的名字和年龄，然后输出

```cpp
#include <iostream>
#include <string>      // C++ 的字符串类型
using namespace std;

int main() {
    string name;       // C++ 字符串，比 char[] 好用得多！
    int age;

    cout << "请输入你的名字: ";
    cin >> name;       // 输入，等价于 C 的 scanf("%s", ...)

    cout << "请输入你的年龄: ";
    cin >> age;

    cout << "你好, " << name << "! 你今年 " << age << " 岁了。" << endl;

    return 0;
}
```

### 🔍 讲解

- **`string`** 是 C++ 内置的字符串类型，不需要手动管理内存，自动扩容，比 C 的 `char name[100]` 安全得多。
- **`cin`** 是标准输入流，`>>` 是流提取运算符。
- **链式调用**：`cout << a << b << c;` 可以连续输出多个值。

### 💡 对比 C 语言

```c
// C: 又臭又长
char name[100];
int age;
printf("请输入你的名字: ");
scanf("%s", name);
printf("请输入你的年龄: ");
scanf("%d", &age);
printf("你好, %s! 你今年 %d 岁了。\n", name, age);
```

```cpp
// C++: 简洁优雅
string name;
int age;
cout << "请输入你的名字: ";
cin >> name;
cout << "请输入你的年龄: ";
cin >> age;
cout << "你好, " << name << "! 你今年 " << age << " 岁了。" << endl;
```

**注意**：`cin >>` 读取字符串时遇到空格会停止。如果要读取一行带空格的文字：

```cpp
string fullName;
getline(cin, fullName);  // 读取一整行，包括空格
```

---

## 1.5 `auto` 关键字：让编译器猜类型（5 分钟）

C++11 开始支持 `auto`，让编译器自动推导变量类型（类似于 Python 的动态类型但本质是静态的）：

```cpp
auto x = 10;           // x 是 int
auto y = 3.14;         // y 是 double
auto z = "hello";      // z 是 const char*
auto s = string("hi"); // s 是 string
auto it = s.begin();   // it 是 string::iterator（以后再学迭代器）
```

> **原则**：类型很明显的时候可以用 `auto` 偷懒，但不要滥用，保持代码可读性。

---

## 📝 第 1 小时练习（15 分钟）

### 练习 1：计算器

**要求**：输入两个整数，输出它们的和、差、积、商。

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cout << "请输入两个整数: ";
    cin >> a >> b;  // 可以连续输入！

    cout << "和: " << a + b << endl;
    cout << "差: " << a - b << endl;
    cout << "积: " << a * b << endl;
    
    if (b != 0) {
        cout << "商: " << (double)a / b << endl;  // 强转避免整除
    } else {
        cout << "除数不能为 0！" << endl;
    }

    return 0;
}
```

</details>

### 练习 2：字符串拼接

**要求**：输入名和姓（两个单词），拼接成全名输出。

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string firstName, lastName;
    
    cout << "请输入你的名: ";
    cin >> firstName;
    cout << "请输入你的姓: ";
    cin >> lastName;

    string fullName = lastName + " " + firstName;  // 字符串用 + 拼接！
    cout << "你的全名是: " << fullName << endl;

    return 0;
}
```

</details>

**值得注意**：C++ 的 `string` 直接支持 `+` 拼接，比 C 的 `strcat` 安全多了！

---

# 🕑 第 2 小时：引用与函数（60 分钟）

## 2.1 引用 `&`：C++ 的秘密武器（20 分钟）

### 📝 这是什么？

**引用**（Reference）就是给一个变量起"别名"。操作引用就等于操作原变量。

```cpp
int x = 10;
int& ref = x;  // ref 是 x 的引用（别名）

ref = 20;      // 修改 ref 就是修改 x
cout << x;     // 输出 20
```

### 🔍 引用 vs 指针（结合你的 C 经验）

```cpp
// C 语言：用指针交换两个数
void swap_c(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
// 调用：swap_c(&x, &y);  ← 麻烦，要取地址

// C++ 语言：用引用交换两个数
void swap_cpp(int& a, int& b) {  // a 和 b 是实参的引用  ^C++YINYONG
    int temp = a;
    a = b;
    b = temp;
}
// 调用：swap_cpp(x, y);  ← 简洁！直接传变量名
```

^71d48a

### 💡 引用的三个核心特点

1. **必须初始化**：`int& ref;` ❌ 编译错误！必须 `int& ref = x;`
2. **不能重新绑定**：一旦引用绑定到 x，就永远指向 x
3. **没有空引用**：不存在 "null 引用"，比指针更安全

### 📝 要求：写一个函数，用引用将两个数都变成 0

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
using namespace std;

void setZero(int& a, int& b) {
    a = 0;
    b = 0;
}

int main() {
    int x = 42, y = 99;
    cout << "修改前: x = " << x << ", y = " << y << endl;
    
    setZero(x, y);  // 直接传变量，不用 &
    
    cout << "修改后: x = " << x << ", y = " << y << endl;
    return 0;
}
```

</details>

### const 引用：只读不写

如果一个函数不想修改参数，但参数又很大（比如大字符串、大对象），就用 `const` 引用：

```cpp
void printInfo(const string& name, const int& age) {
    // name = "xxx";  ❌ 编译错误！const 引用不能修改
    cout << "姓名: " << name << ", 年龄: " << age << endl;
}
```

**好处**：避免了拷贝的开销，又保证了数据不会被修改。

---

## 2.2 函数重载（15 分钟）

### 📝 这是什么？

C++ 允许**同名函数**，只要参数类型或数量不同即可。编译器会根据调用时的参数自动匹配。

```cpp
#include <iostream>
using namespace std;

// 同名函数，参数不同
int add(int a, int b) {
    return a + b;
}

double add(double a, double b) {
    return a + b;
}

int add(int a, int b, int c) {  // 参数数量不同
    return a + b + c;
}

int main() {
    cout << add(1, 2) << endl;        // 调用 int 版本 → 3
    cout << add(1.5, 2.5) << endl;    // 调用 double 版本 → 4.0
    cout << add(1, 2, 3) << endl;     // 调用三参数版本 → 6
    return 0;
}
```

### 💡 和 C 的对比

C 语言中不能有同名函数，必须写成 `add_int()`、`add_double()` 等。C++ 的函数重载让代码更优雅。

### 📝 要求：重载 `print` 函数，分别打印 int、double 和 string

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

void print(int x) {
    cout << "整数: " << x << endl;
}

void print(double x) {
    cout << "浮点数: " << x << endl;
}

void print(const string& s) {
    cout << "字符串: " << s << endl;
}

int main() {
    print(42);
    print(3.14159);
    print(string("Hello"));
    return 0;
}
```

</details>

---

## 2.3 类与对象入门（25 分钟）

### 📝 类的概念

你已经从 Python 了解过类和对象。C++ 的类写法不同，但思想一样：**把数据和操作数据的方法打包在一起**。

### 最简单的人类（Person）

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
public:                   // 公有成员（外部可访问）
    string name;
    int age;

    void introduce() {    // 成员函数（方法），直接写在类里
        cout << "大家好，我叫" << name << "，今年" << age << "岁。" << endl;
    }
};

int main() {
    Person p1;            // 创建对象（栈上分配，和 C 的结构体一样）
    p1.name = "小明";
    p1.age = 20;
    p1.introduce();       // 调用成员函数

    Person p2;
    p2.name = "小红";
    p2.age = 18;
    p2.introduce();

    return 0;
}
```

### 🔍 讲解

| 概念 | C++ | C（结构体） | Python |
|------|-----|-----------|--------|
| 定义 | `class Person { ... };` | `struct Person { ... };` | `class Person:` |
| 公有 | `public:` | 默认全部公有 | 默认公有 |
| 访问成员 | `p1.name` | `p1.name` | `p1.name` |
| 方法 | 写在类里面 | 不存在 | `def method(self):` |
| 分号 | 类定义后**必须**有 `;` | 结构体定义后**必须**有 `;` | 不需要 |

> ⚠️ **C++ 的 class 和 struct 几乎一样**，唯一区别：class 默认 private，struct 默认 public。

### 构造函数：自动初始化

```cpp
class Person {
private:                 // 私有成员（外部不可访问）
    string name;
    int age;

public:
    // 构造函数：创建对象时自动调用
    Person(string n, int a) {
        name = n;
        age = a;
    }

    void introduce() {
        cout << "我叫" << name << "，今年" << age << "岁。" << endl;
    }
};

int main() {
    Person p1("小明", 20);  // 创建对象时直接初始化
    Person p2("小红", 18);
    p1.introduce();
    p2.introduce();
    return 0;
}
```

### 💡 和 Python 对比

| | C++ | Python |
|------|-----|--------|
| 构造函数 | `Person(string n, int a)` | `def __init__(self, n, a):` |
| 创建对象 | `Person p1("小明", 20);` | `p1 = Person("小明", 20)` |
| self | 不需要写（隐式） | 必须显式写 |

---

## 📝 第 2 小时练习（用于巩固，建议 10 分钟）

### 练习：定义一个 Rectangle 类

**要求**：
1. 有 `width` 和 `height` 两个私有成员
2. 有构造函数初始化它们
3. 有 `area()` 方法返回面积
4. 有 `perimeter()` 方法返回周长
5. 在 `main` 中创建一个矩形并打印其面积和周长

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
using namespace std;

class Rectangle {
private:
    double width;
    double height;

public:
    Rectangle(double w, double h) {
        width = w;
        height = h;
    }

    double area() {
        return width * height;
    }

    double perimeter() {
        return 2 * (width + height);
    }
};

int main() {
    Rectangle rect(5.0, 3.0);
    cout << "面积: " << rect.area() << endl;
    cout << "周长: " << rect.perimeter() << endl;
    return 0;
}
```

</details>

---

# 🕒 第 3 小时：容器与实战（60 分钟）

## 3.1 `vector`：C++ 的动态数组（20 分钟）

### 📝 这是什么？

`vector` 是 C++ 标准库中的**动态数组**，可以自动扩容，类似于 Python 的 `list`。它比 C 的 `malloc`/`realloc` 安全一万倍。

```cpp
#include <iostream>
#include <vector>     // 使用 vector 必须包含此头文件
using namespace std;

int main() {
    vector<int> v;    // 创建一个空的 int 动态数组

    // 添加元素
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);

    // 访问元素（和数组一样用 []）
    cout << "第一个元素: " << v[0] << endl;
    cout << "第二个元素: " << v[1] << endl;

    // 获取大小
    cout << "数组大小: " << v.size() << endl;

    // 修改元素
    v[0] = 100;

    // 删除最后一个元素
    v.pop_back();

    cout << "删除后大小: " << v.size() << endl;

    return 0;
}
```

### 🔍 vector 常用操作速查表

| 操作 | 代码 | 说明 |
|------|------|------|
| 创建 | `vector<int> v;` | 空数组 |
| 创建指定大小 | `vector<int> v(10);` | 10 个元素，默认值为 0 |
| 创建并初始化 | `vector<int> v = {1,2,3};` | 包含 1,2,3 |
| 添加 | `v.push_back(x);` | 在末尾添加 |
| 删除末尾 | `v.pop_back();` | 删除最后一个 |
| 大小 | `v.size()` | 返回元素个数 |
| 访问 | `v[i]` | 第 i 个元素（从 0 开始） |
| 清空 | `v.clear();` | 删除所有元素 |
| 判空 | `v.empty()` | 是否为空 |

### 📝 要求：从键盘输入 5 个数字存到 vector，然后打印它们

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;

    cout << "请输入 5 个整数：" << endl;
    for (int i = 0; i < 5; i++) {
        int x;
        cin >> x;
        v.push_back(x);
    }

    cout << "你输入的数字是：" << endl;
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;

    return 0;
}
```

</details>

---

## 3.2 范围 for 循环：更优雅的遍历（10 分钟）

C++11 引入了**范围 for**（Range-based for loop），让遍历容器变得极其简单：

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};

    // 传统 for（你已熟悉）
    cout << "传统方式: ";
    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;

    // 范围 for（C++11 新特性）
    cout << "范围 for: ";
    for (int x : v) {      // 读作：对于 v 中的每个元素 x
        cout << x << " ";
    }
    cout << endl;

    // 使用 auto 更简洁
    cout << "auto 版本: ";
    for (auto x : v) {
        cout << x << " ";
    }
    cout << endl;

    // 想修改元素？用引用
    for (int& x : v) {
        x *= 2;  // 每个元素翻倍
    }
    cout << "翻倍后: ";
    for (auto x : v) {
        cout << x << " ";
    }
    cout << endl;

    return 0;
}
```

### 💡 对比 Python

```python
# Python
for x in my_list:
    print(x)
```

```cpp
// C++ 范围 for
for (int x : v) {
    cout << x << " ";
}
```

非常相似！C++ 也可以写得很简洁。

---

## 3.3 简单文件输入输出（15 分钟）

C++ 的文件操作继承自 `cout`/`cin` 的思路，使用 `fstream` 头文件。

### 写入文件

```cpp
#include <iostream>
#include <fstream>      // 文件操作头文件
#include <string>
using namespace std;

int main() {
    // 创建输出文件流对象
    ofstream outFile("output.txt");

    if (!outFile) {     // 检查文件是否打开成功
        cout << "文件打开失败！" << endl;
        return 1;
    }

    // 就像写 cout 一样写文件！
    outFile << "Hello, File!" << endl;
    outFile << "这是第二行" << endl;
    outFile << "数字: " << 42 << endl;

    outFile.close();    // 关闭文件（也可不写，析构函数自动关）
    cout << "文件写入成功！" << endl;

    return 0;
}
```

### 读取文件

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    ifstream inFile("output.txt");

    if (!inFile) {
        cout << "文件打开失败！" << endl;
        return 1;
    }

    string line;
    while (getline(inFile, line)) {  // 逐行读取
        cout << "读到: " << line << endl;
    }

    inFile.close();
    return 0;
}
```

### 🔍 三个关键类

| 类 | 用途 | 类比 |
|----|------|------|
| `ofstream` | Output File Stream | 写文件（类似于 `cout`） |
| `ifstream` | Input File Stream | 读文件（类似于 `cin`）|
| `fstream` | File Stream | 读写文件 |

---

## 3.4 综合练习：学生成绩管理系统（15 分钟）

这是今天学习的综合检验，把学到的知识全部用上。

### 📝 要求

创建一个简易的成绩管理系统：

1. 定义一个 `Student` 类，包含姓名（`string`）和成绩（`int`）
2. 用 `vector<Student>` 存储多个学生
3. 实现以下功能：
   - 添加学生
   - 显示所有学生信息
   - 计算平均成绩
4. 在 `main` 中演示所有功能

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <iomanip>    // 用于格式化输出
using namespace std;

// 学生类
class Student {
private:
    string name;
    int score;

public:
    // 构造函数
    Student(const string& n, int s) {
        name = n;
        score = s;
    }

    // 获取姓名
    string getName() const {
        return name;
    }

    // 获取成绩
    int getScore() const {
        return score;
    }

    // 显示学生信息
    void display() const {
        cout << "姓名: " << name << " | 成绩: " << score << endl;
    }
};

// 成绩管理系统
class ScoreManager {
private:
    vector<Student> students;

public:
    // 添加学生
    void addStudent(const string& name, int score) {
        students.push_back(Student(name, score));
        cout << "已添加学生: " << name << endl;
    }

    // 显示所有学生
    void showAll() const {
        if (students.empty()) {
            cout << "暂无学生数据！" << endl;
            return;
        }
        cout << "\n====== 学生成绩列表 ======" << endl;
        for (const auto& s : students) {
            s.display();
        }
    }

    // 计算平均成绩
    double getAverage() const {
        if (students.empty()) {
            return 0.0;
        }
        int total = 0;
        for (const auto& s : students) {
            total += s.getScore();
        }
        return (double)total / students.size();
    }

    // 显示统计信息
    void showStats() const {
        if (students.empty()) {
            cout << "暂无学生数据！" << endl;
            return;
        }
        cout << "\n====== 成绩统计 ======" << endl;
        cout << "学生总数: " << students.size() << endl;
        cout << "平均成绩: " << fixed << setprecision(2) << getAverage() << endl;
    }
};

int main() {
    ScoreManager manager;

    // 添加一些学生
    manager.addStudent("张三", 85);
    manager.addStudent("李四", 92);
    manager.addStudent("王五", 78);
    manager.addStudent("赵六", 88);

    // 显示所有学生
    manager.showAll();

    // 显示统计信息
    manager.showStats();

    return 0;
}
```

</details>

### 💡 代码中的知识点回顾

| 知识点 | 对应代码 |
|--------|----------|
| 类与对象 | `class Student`, `class ScoreManager` |
| `vector` | `vector<Student> students` |
| `const` 引用 | `const string& n` |
| `const` 成员函数 | `getName() const` |
| 范围 for | `for (const auto& s : students)` |
| `auto` | `const auto& s` |
| 构造函数 | `Student(const string& n, int s)` |

---

## 🎯 今日总结

| 你学到的 | 重要性 | 
|----------|--------|
| `cout` / `cin` 输入输出 | ⭐⭐⭐⭐⭐ |
| `string` 字符串类型 | ⭐⭐⭐⭐⭐ |
| `namespace std` | ⭐⭐⭐ |
| `auto` 类型推导 | ⭐⭐⭐ |
| 引用 `&` | ⭐⭐⭐⭐⭐ |
| 函数重载 | ⭐⭐⭐⭐ |
| `class` 类与对象 | ⭐⭐⭐⭐⭐ |
| `vector` 动态数组 | ⭐⭐⭐⭐⭐ |
| 范围 `for` 循环 | ⭐⭐⭐⭐ |
| 简单文件 IO | ⭐⭐⭐ |

---

## 📚 课后任务（选做，巩固今天的内容）

1. **修改成绩管理系统**：增加"删除学生"和"查找学生"的功能
2. **文件持久化**：将学生数据写入文件，程序启动时从文件读取
3. **复习对比**：把今天的每个 C++ 特性和你熟悉的 C/Python 写法做对比，加深理解

---

> 🎉 **恭喜你完成了第一天的 C++ 学习！**  
> 明天我们将继续学习：指针与动态内存、`new`/`delete`、this 指针、析构函数、拷贝构造等进阶内容。  
> 记得今天多敲代码，光看不练等于白学！明天见～