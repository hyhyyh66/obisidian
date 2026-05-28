


---

## 📋 课程体系总览

```
：

第一阶段：C++ 基础入门（对应视频 P1-P140）
├── 第1章  C++ 初识
├── 第2章  数据类型
├── 第3章  运算符
├── 第4章  程序流程结构
├── 第5章  数组
├── 第6章  函数
├── 第7章  指针
└── 第8章  结构体

第二阶段：C++ 核心编程（对应视频 P141-P240）
├── 第1章  内存分区模型
├── 第2章  引用
├── 第3章  函数提高
├── 第4章  类与对象（封装/继承/多态）
└── 第5章  文件操作

第三阶段：C++ 提高编程（对应视频 P241-P380）
├── 第1章  模板
├── 第2章  STL 初识
├── 第3章  string 容器
├── 第4章  vector 容器
├── 第5章  deque 容器
├── 第6章  stack 容器
├── 第7章  queue 容器
├── 第8章  list 容器
├── 第9章  set/multiset 容器
├── 第10章 map/multimap 容器
├── 第11章 函数对象（仿函数）
└── 第12章 STL 常用算法
```

---

# 第一阶段：C++ 基础入门

---

## 第1章 C++ 初识

### 1.1 第一个 C++ 程序

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello World" << endl;
    system("pause");  // Windows 下暂停控制台
    return 0;
}
```

### 1.2 注释

```cpp
// 单行注释

/*
 * 多行注释
 */
```

### 1.3 变量与常量

```cpp
// 变量：值可以修改
int a = 10;
a = 20;  // ✅ 可以

// 常量：值不可修改
// 方式1：#define 宏常量
#define MAX 100

// 方式2：const 修饰
const int MIN = 0;
// MIN = 10;  ❌ 编译错误
```

### 1.4 关键字（C++ 特有）

| 关键字 | 作用 |
|--------|------|
| `bool` | 布尔类型 |
| `class` | 类 |
| `namespace` | 命名空间 |
| `new` / `delete` | 动态内存 |
| `try` / `catch` / `throw` | 异常处理 |
| `virtual` | 虚函数 |
| `template` | 模板 |

### 1.5 标识符命名规则

- 不能是关键字
- 由字母、数字、下划线组成
- 第一个字符必须是字母或下划线
- **区分大小写**

---

## 第2章 数据类型

### 2.1 整型

| 类型 | 占用空间 | 取值范围 |
|------|---------|----------|
| `short` | 2 字节 | -2^15 ~ 2^15-1 (-32768 ~ 32767) |
| `int` | 4 字节 | -2^31 ~ 2^31-1 |
| `long` | 4/8 字节 | 取决于平台 |
| `long long` | 8 字节 | -2^63 ~ 2^63-1 |

```cpp
short s = 32767;
int i = 2147483647;
long l = 2147483647;
long long ll = 9223372036854775807;

// 查看占用空间
cout << "short: " << sizeof(short) << " 字节" << endl;
cout << "int: " << sizeof(int) << " 字节" << endl;
```

### 2.2 sizeof 关键字

```cpp
// sizeof 是运算符，不是函数
cout << sizeof(int) << endl;       // 4
cout << sizeof(long long) << endl; // 8

int a = 10;
cout << sizeof(a) << endl;         // 4（也可以对变量使用）
```

### 2.3 实型（浮点型）

| 类型 | 占用空间 | 有效数字范围 |
|------|---------|-------------|
| `float` | 4 字节 | 7 位有效数字 |
| `double` | 8 字节 | 15-16 位有效数字 |

```cpp
float f1 = 3.1415926f;   // 加 f 表示 float
double d1 = 3.1415926;   // 默认是 double

// 科学计数法
float f2 = 3e2;   // 3 * 10^2 = 300
float f3 = 3e-2;  // 3 * 10^-2 = 0.03
```

### 2.4 字符型

```cpp
char ch = 'A';                  // 用单引号
cout << ch << endl;             // 输出: A
cout << (int)ch << endl;        // 输出: 65（ASCII 码）
cout << sizeof(char) << endl;   // 1 字节

// 常见 ASCII
// 'A' = 65, 'a' = 97, '0' = 48
// 'A' + 32 = 'a'（大小写转换技巧）

// 转义字符
cout << "Hello\nWorld" << endl;  // \n 换行
cout << "He said:\"Hi\"" << endl; // \" 双引号
cout << "Path: C:\\Users" << endl; // \\ 反斜杠
cout << "Tab\there" << endl;     // \t 制表符
```

### 2.5 字符串类型

```cpp
// C 风格字符串
char str1[] = "Hello";
cout << str1 << endl;

// C++ 风格字符串（推荐）
#include <string>
string str2 = "Hello World";
cout << str2 << endl;
cout << "长度: " << str2.length() << endl;
```

### 2.6 布尔类型 bool

```cpp
bool flag1 = true;   // 本质是 1
bool flag2 = false;  // 本质是 0
cout << flag1 << endl;  // 1
cout << flag2 << endl;  // 0
cout << sizeof(bool) << endl;  // 1 字节
```

### 2.7 数据的输入 cin

```cpp
int a;
cout << "请输入一个整数: ";
cin >> a;
cout << "你输入的是: " << a << endl;

// 连续输入
int x, y;
cin >> x >> y;

// 输入字符串（遇到空格会截断）
string name;
cin >> name;  // 输入 "Zhang San" → 只得到 "Zhang"

// 读取一行（包含空格）
getline(cin, name);  // 输入 "Zhang San" → 得到 "Zhang San"
```

---

## 第3章 运算符

### 3.1 算术运算符

```cpp
int a = 10, b = 3;
cout << a + b << endl;  // 13
cout << a - b << endl;  // 7
cout << a * b << endl;  // 30
cout << a / b << endl;  // 3（整数除法，舍弃小数）
cout << a % b << endl;  // 1（取模）

// 除法的特殊规则
double d = 10.0 / 3;  // 3.33333（有一个是浮点数即可）
```

### 3.2 赋值运算符

```cpp
int a = 10;
a += 3;   // a = a + 3 → 13
a -= 3;   // a = a - 3 → 10
a *= 2;   // a = a * 2 → 20
a /= 4;   // a = a / 4 → 5
a %= 3;   // a = a % 3 → 2
```

### 3.3 比较运算符

```cpp
int a = 10, b = 20;
cout << (a == b) << endl;  // 0 (false)
cout << (a != b) << endl;  // 1 (true)
cout << (a > b)  << endl;  // 0
cout << (a < b)  << endl;  // 1
cout << (a >= b) << endl;  // 0
cout << (a <= b) << endl;  // 1
```

### 3.4 逻辑运算符

```cpp
int a = 10, b = 0;
cout << (a && b) << endl;  // 0（逻辑与，全真才真）
cout << (a || b) << endl;  // 1（逻辑或，有真就真）
cout << (!a)     << endl;  // 0（逻辑非）

// 🔥 短路特性
int x = 0;
if (x != 0 && 10 / x > 0) {  // 左边为假，右边不执行，不会除以 0
    // ...
}
```

### 3.5 三目运算符（唯一的三目）

```cpp
int a = 10, b = 20;
int max = (a > b) ? a : b;  // max = 20

// C++ 中三目运算符返回的是变量，可以赋值
(a > b ? a : b) = 100;  // b = 100
```

---

## 第4章 程序流程结构

### 4.1 选择结构

#### if 语句

```cpp
// 单分支
if (score >= 60) {
    cout << "及格" << endl;
}

// 双分支
if (score >= 60) {
    cout << "及格" << endl;
} else {
    cout << "不及格" << endl;
}

// 多分支
if (score >= 90) {
    cout << "优秀" << endl;
} else if (score >= 80) {
    cout << "良好" << endl;
} else if (score >= 60) {
    cout << "及格" << endl;
} else {
    cout << "不及格" << endl;
}
```

#### switch 语句

```cpp
// ⚠️ switch 只能判断整型或字符型
switch (score / 10) {
    case 10:
    case 9:
        cout << "优秀" << endl;
        break;  // 必须加 break，否则会继续执行！
    case 8:
        cout << "良好" << endl;
        break;
    case 7:
    case 6:
        cout << "及格" << endl;
        break;
    default:
        cout << "不及格" << endl;
        break;
}
```

### 4.2 循环结构

```cpp
// while 循环
int i = 0;
while (i < 10) {
    cout << i << " ";
    i++;
}
// 输出: 0 1 2 3 4 5 6 7 8 9

// do...while（先执行一次再判断）
int j = 0;
do {
    cout << j << " ";
    j++;
} while (j < 10);

// for 循环
for (int k = 0; k < 10; k++) {
    cout << k << " ";
}
```

### 4.3 跳转语句

```cpp
// break：跳出循环
for (int i = 0; i < 10; i++) {
    if (i == 5) break;  // 到 5 就退出
    cout << i << " ";
}
// 输出: 0 1 2 3 4

// continue：跳过本次
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue;  // 偶数跳过
    cout << i << " ";           // 只输出奇数
}
// 输出: 1 3 5 7 9

// goto：跳转到标记（少用）
int i = 0;
LOOP:
    cout << i++ << " ";
    if (i < 5) goto LOOP;
```

### 4.4 经典案例：猜数字游戏

```cpp
#include <iostream>
#include <ctime>    // time()
#include <cstdlib>  // rand(), srand()
using namespace std;

int main() {
    srand((unsigned int)time(NULL));  // 随机种子
    int target = rand() % 100 + 1;    // 1-100 的随机数
    int guess = 0;
    
    cout << "猜数字游戏 (1-100)" << endl;
    
    while (true) {
        cout << "请输入你的猜测: ";
        cin >> guess;
        
        if (guess > target) {
            cout << "猜大了！" << endl;
        } else if (guess < target) {
            cout << "猜小了！" << endl;
        } else {
            cout << "恭喜你，猜对了！" << endl;
            break;
        }
    }
    return 0;
}
```

---

## 第5章 数组

### 5.1 一维数组

```cpp
// 定义方式 1
int arr1[5] = {10, 20, 30, 40, 50};

// 定义方式 2（自动推断长度）
int arr2[] = {10, 20, 30, 40, 50};

// 定义方式 3（先定义再赋值）
int arr3[5];
arr3[0] = 10;

// 访问
cout << arr1[0] << endl;  // 10

// 🔥 一维数组名 = 首地址
cout << arr1 << endl;       // 地址
cout << (int)&arr1[0] << endl;  // 和上面相同

// 获取数组长度
int len = sizeof(arr1) / sizeof(arr1[0]);
cout << "数组长度: " << len << endl;  // 5
```

### 5.2 冒泡排序

```cpp
int arr[] = {4, 2, 8, 0, 5, 7, 1, 3, 9, 6};
int len = sizeof(arr) / sizeof(arr[0]);

// 冒泡排序
for (int i = 0; i < len - 1; i++) {          // 外层：轮数
    for (int j = 0; j < len - 1 - i; j++) {  // 内层：每轮比较次数
        if (arr[j] > arr[j + 1]) {
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```

### 5.3 二维数组

```cpp
// 定义方式
int arr1[2][3] = {
    {1, 2, 3},
    {4, 5, 6}
};

int arr2[2][3] = {1, 2, 3, 4, 5, 6};  // 自动分组
int arr3[][3] = {1, 2, 3, 4, 5, 6};   // 行数可省，列数不可省

// 遍历
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        cout << arr1[i][j] << " ";
    }
    cout << endl;
}

// 二维数组名
cout << sizeof(arr1) << endl;          // 24 (2*3*4)
cout << sizeof(arr1[0]) << endl;       // 12 (一行的长度)
cout << sizeof(arr1[0][0]) << endl;    // 4
```

---

## 第6章 函数

### 6.1 函数定义与调用

```cpp
// 函数定义
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(10, 20);  // 函数调用
    cout << result << endl;     // 30
    return 0;
}
```

### 6.2 值传递

```cpp
// C++ 默认是值传递（传的是副本）
void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
    // 这里 a,b 交换了，但外面的不会变！
}

int main() {
    int x = 10, y = 20;
    swap(x, y);
    cout << x << " " << y << endl;  // 10 20（没有交换！）
    return 0;
}
```

### 6.3 函数的声明

```cpp
// 声明在前，定义在后（或放在头文件中）
int max(int a, int b);  // 函数声明（分号不能少）

int main() {
    cout << max(10, 20) << endl;
    return 0;
}

// 函数定义
int max(int a, int b) {
    return a > b ? a : b;
}
```

### 6.4 函数的分文件编写

```
// swap.h（头文件：声明）
#ifndef SWAP_H
#define SWAP_H

void swap(int& a, int& b);  // 声明

#endif
```

```cpp
// swap.cpp（源文件：定义）
#include "swap.h"

void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}
```

```cpp
// main.cpp
#include "swap.h"

int main() {
    int x = 10, y = 20;
    swap(x, y);  // x=20, y=10
    return 0;
}
```

---

## 第7章 指针

### 7.1 指针的定义与使用

```cpp
int a = 10;
int* p = &a;   // 定义指针，存储 a 的地址
*p = 20;       // 解引用，修改 a 的值

cout << "a = " << a << endl;        // 20
cout << "&a = " << &a << endl;      // a 的地址
cout << "p = " << p << endl;        // 也是 a 的地址
cout << "*p = " << *p << endl;      // 20
cout << "sizeof(p) = " << sizeof(p) << endl;  // 4（32位）或 8（64位）
```

### 7.2 空指针和野指针

```cpp
// 空指针：指向内存编号为 0 的空间
int* p1 = NULL;    // C 风格
int* p2 = nullptr; // C++11 风格（推荐）

// 空指针不可访问
// *p1 = 100;  ❌ 运行错误！0-255 是系统占用

// 野指针：指向非法内存的指针（未初始化）
// int* p3;     ❌ 危险！p3 指向随机地址
// *p3 = 100;   可能崩溃
```

### 7.3 const 修饰指针

```cpp
int a = 10, b = 20;

// 1. const int* p（常量指针）
//    指向的值不能改，指向可以改
const int* p1 = &a;
// *p1 = 20;  ❌ 不能修改值
p1 = &b;      // ✅ 可以改指向

// 2. int* const p（指针常量）
//    指向可以改？不行。指向的值可以改。
int* const p2 = &a;
*p2 = 20;     // ✅ 可以修改值
// p2 = &b;   ❌ 不能改指向

// 3. const int* const p（既不能改值也不能改指向）
const int* const p3 = &a;
// *p3 = 20;  ❌
// p3 = &b;   ❌
```

**记忆口诀**：`const` 在 `*` 左边 → 值不能改；`const` 在 `*` 右边 → 指向不能改

### 7.4 指针和数组

```cpp
int arr[] = {10, 20, 30, 40, 50};
int* p = arr;  // arr 就是首地址

cout << *p << endl;        // 10 (arr[0])
cout << *(p + 1) << endl;  // 20 (arr[1])
cout << *(p + 2) << endl;  // 30 (arr[2])

// 遍历
for (int i = 0; i < 5; i++) {
    cout << *(p + i) << " ";
}
```

### 7.5 指针和函数

```cpp
// 地址传递：函数内外操作同一块内存
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 10, y = 20;
    swap(&x, &y);  // 传地址
    cout << x << " " << y << endl;  // 20 10 ✅ 真正交换了
    return 0;
}
```

---

## 第8章 结构体

### 8.1 结构体定义与使用

```cpp
// 定义结构体
struct Student {
    string name;
    int age;
    int score;
};

int main() {
    // 创建方式 1：struct 关键字可省略
    Student s1;
    s1.name = "张三";
    s1.age = 18;
    s1.score = 90;
    
    // 创建方式 2：直接初始化
    Student s2 = {"李四", 19, 85};
    
    // 输出
    cout << s1.name << " " << s1.age << " " << s1.score << endl;
    return 0;
}
```

### 8.2 结构体数组

```cpp
Student students[3] = {
    {"张三", 18, 90},
    {"李四", 19, 85},
    {"王五", 20, 92}
};

// 遍历
for (int i = 0; i < 3; i++) {
    cout << students[i].name << ": " << students[i].score << endl;
}
```

### 8.3 结构体指针

```cpp
Student s = {"张三", 18, 90};
Student* p = &s;

// 通过指针访问成员：使用 ->
cout << p->name << endl;   // 张三
cout << p->age << endl;    // 18
cout << p->score << endl;  // 90
```

### 8.4 结构体嵌套

```cpp
struct Teacher {
    string name;
    Student students[5];  // 老师有 5 个学生
    int studentCount;
};

void printTeacher(const Teacher& t) {
    cout << "老师: " << t.name << endl;
    cout << "辅导学生:" << endl;
    for (int i = 0; i < t.studentCount; i++) {
        cout << "  " << t.students[i].name << ": " << t.students[i].score << endl;
    }
}
```

### 8.5 结构体做函数参数

```cpp
// 值传递（复制一份，不修改原数据）
void print1(Student s) {  // 会拷贝整个结构体，开销大
    cout << s.name << endl;
}

// 地址传递（可修改原数据，省内存）
void print2(const Student* s) {  // const 防止误修改
    cout << s->name << endl;
}

// 🔥 推荐用 const 引用（C++ 特有，又省内存又不能修改）
void print3(const Student& s) {
    cout << s.name << endl;
}
```

### 8.6 结构体案例：通讯录

```cpp
#include <iostream>
#include <string>
using namespace std;

#define MAX 1000

struct Person {
    string name;
    int sex;    // 1 男 2 女
    int age;
    string phone;
    string address;
};

struct AddressBook {
    Person personArray[MAX];
    int size;  // 当前通讯录人数
};

// 显示菜单
void showMenu() {
    cout << "************************" << endl;
    cout << "***** 1. 添加联系人 *****" << endl;
    cout << "***** 2. 显示联系人 *****" << endl;
    cout << "***** 3. 删除联系人 *****" << endl;
    cout << "***** 4. 查找联系人 *****" << endl;
    cout << "***** 5. 修改联系人 *****" << endl;
    cout << "***** 6. 清空联系人 *****" << endl;
    cout << "***** 0. 退出通讯录 *****" << endl;
    cout << "************************" << endl;
}

// 添加联系人
void addPerson(AddressBook* abs) {
    if (abs->size == MAX) {
        cout << "通讯录已满！" << endl;
        return;
    }
    
    Person p;
    cout << "姓名: "; cin >> p.name;
    cout << "性别(1男2女): "; cin >> p.sex;
    cout << "年龄: "; cin >> p.age;
    cout << "电话: "; cin >> p.phone;
    cout << "住址: "; cin >> p.address;
    
    abs->personArray[abs->size] = p;
    abs->size++;
    cout << "添加成功！" << endl;
}

// 显示所有联系人
void showPerson(const AddressBook* abs) {
    if (abs->size == 0) {
        cout << "通讯录为空！" << endl;
        return;
    }
    for (int i = 0; i < abs->size; i++) {
        cout << "姓名: " << abs->personArray[i].name << "\t"
             << "性别: " << (abs->personArray[i].sex == 1 ? "男" : "女") << "\t"
             << "年龄: " << abs->personArray[i].age << "\t"
             << "电话: " << abs->personArray[i].phone << "\t"
             << "住址: " << abs->personArray[i].address << endl;
    }
}

int main() {
    AddressBook abs;
    abs.size = 0;
    
    int select = 0;
    while (true) {
        showMenu();
        cin >> select;
        switch (select) {
            case 1: addPerson(&abs); break;
            case 2: showPerson(&abs); break;
            case 0:
                cout << "再见！" << endl;
                return 0;
            default: break;
        }
    }
    return 0;
}
```

---

# 第二阶段：C++ 核心编程

---

## 第1章 内存分区模型

### 🔥 面试必考：C++ 程序内存四区

```
高地址
┌──────────────────┐
│     栈区 (Stack)   │  ← 编译器自动管理，存放局部变量、函数参数
├──────────────────┤    方向：高→低
│       ↓↓         │
│                  │
│       ↑↑         │
├──────────────────┤
│     堆区 (Heap)    │  ← 程序员手动管理 (new/delete)
├──────────────────┤    方向：低→高
│   全局区 (Static)  │  ← 全局变量、静态变量、常量
├──────────────────┤
│    代码区 (Text)   │  ← 存放 CPU 执行的机器指令（只读共享）
└──────────────────┘
低地址
```

### 1.1 代码区（程序运行前）

- 存放二进制代码（函数体）
- **共享**：内存中只有一份
- **只读**：防止程序修改自己的指令

### 1.2 全局区

```cpp
// 全局变量
int g_a = 10;
int g_b = 10;

// const 修饰的全局常量
const int c_g_a = 10;

int main() {
    // 局部变量（不在全局区）
    int a = 10;
    
    // 静态变量（在全局区）
    static int s_a = 10;
    
    // 字符串常量（在全局区）
    cout << "hello" << endl;
    
    // const 修饰的局部常量（不在全局区）
    const int c_a = 10;
    
    return 0;
}
```

### 1.3 栈区

```cpp
// 栈区：由编译器自动分配释放
// 不要返回局部变量的地址！

int* func() {
    int a = 10;   // 局部变量，在栈区
    return &a;    // ❌ 错误！a 在函数结束后就被释放了
}

int main() {
    int* p = func();
    cout << *p << endl;  // 第一次可能正常（编译器保留）
    cout << *p << endl;  // 第二次就乱了
    return 0;
}
```

### 1.4 堆区

```cpp
// 堆区：由程序员分配释放
// new 出来的数据在堆区，可以返回其地址

int* func() {
    int* p = new int(10);  // 在堆区创建
    return p;              // ✅ 可以！堆区的数据不会自动释放
}

int main() {
    int* p = func();
    cout << *p << endl;   // 10
    delete p;             // 手动释放
    return 0;
}
```

### 1.5 new 操作符

```cpp
// new 基本类型
int* p1 = new int(10);
delete p1;

// new 数组
int* arr = new int[10];
for (int i = 0; i < 10; i++) arr[i] = i;
delete[] arr;  // 注意是 delete[]

// new 对象
class Person {
public:
    Person() { cout << "构造" << endl; }
    ~Person() { cout << "析构" << endl; }
};

Person* p2 = new Person;  // 调用构造函数
delete p2;                // 调用析构函数
```

---

## 第2章 引用

### 2.1 引用的基本使用

```cpp
// 引用：给变量起别名
int a = 10;
int& b = a;  // b 是 a 的引用（别名）

b = 20;
cout << a << endl;  // 20（修改 b 就是修改 a）
cout << b << endl;  // 20
```

### 2.2 引用注意事项

```cpp
// 1. 引用必须初始化
int a = 10;
// int& b;  ❌ 错误！必须初始化
int& b = a;  // ✅

// 2. 引用一旦初始化就不能更改
int c = 20;
b = c;   // 这是赋值操作！不是更改引用！a 变成了 20
// 不能让 b 变成 c 的引用
```

### 2.3 引用做函数参数

```cpp
// 和指针一样，可以修改实参，但语法更简洁
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int x = 10, y = 20;
    swap(x, y);  // 传引用，不需要 &x
    cout << x << " " << y << endl;  // 20 10
    return 0;
}
```

### 2.4 引用做函数返回值

```cpp
// ⚠️ 不要返回局部变量的引用
int& func1() {
    int a = 10;
    return a;  // ❌ a 是局部变量，函数结束就释放了
}

// ✅ 可以返回静态变量的引用
int& func2() {
    static int a = 10;  // 静态变量，在全局区
    return a;
}

// 函数调用可以作为左值
int& func3() {
    static int a = 10;
    return a;
}

int main() {
    func3() = 100;  // 把 a 赋值为 100
    cout << func3() << endl;  // 100
    return 0;
}
```

### 2.5 引用的本质

```cpp
// 引用的本质是指针常量（C++ 内部实现）
// int& ref = a; 等价于 int* const ref = &a;

// 所以：
// - 引用必须初始化（指针常量的约束）
// - 引用不能改变指向
// - 使用 ref 时自动解引用
```

### 2.6 🆚 指针 vs 引用速查

| 维度 | 指针 | 引用 |
|------|------|------|
| 语法 | `int* p = &x; *p` | `int& r = x; r` |
| 可否为空 | `nullptr` | ❌ |
| 可否改变指向 | `p = &y` | ❌ |
| sizeof | 4/8 字节 | 等同于原变量 |
| 多级 | 可以（`int**`） | ❌ |

---

## 第3章 函数提高

### 3.1 函数默认参数

```cpp
// 有默认值的参数必须从右往左排列
int func(int a, int b = 10, int c = 20) {
    return a + b + c;
}

int main() {
    cout << func(1) << endl;        // 1+10+20 = 31
    cout << func(1, 2) << endl;     // 1+2+20 = 23
    cout << func(1, 2, 3) << endl;  // 1+2+3 = 6
    return 0;
}

// ⚠️ 注意
// 1. 声明和定义不能同时有默认参数（只能有一个地方有）
int func2(int a, int b = 10);     // 声明时有默认值
int func2(int a, int b) {         // 定义时不写
    return a + b;
}
```

### 3.2 函数占位参数

```cpp
// 占位参数：只有类型，没有名字
void func(int a, int) {
    cout << "a = " << a << endl;
}

// 占位参数也可以有默认值
void func2(int a, int = 10) {
    cout << "a = " << a << endl;
}

int main() {
    func(10, 20);   // 必须传参
    func2(10);      // 可以不传（有默认值）
    return 0;
}
```

### 3.3 函数重载（Overloading）

```cpp
// 函数名相同，参数不同 → 重载
void func() {
    cout << "func()" << endl;
}

void func(int a) {
    cout << "func(int): " << a << endl;
}

void func(double a) {
    cout << "func(double): " << a << endl;
}

void func(int a, int b) {
    cout << "func(int,int): " << a << ", " << b << endl;
}

int main() {
    func();          // func()
    func(10);        // func(int): 10
    func(3.14);      // func(double): 3.14
    func(10, 20);    // func(int,int): 10, 20
    return 0;
}

// ⚠️ 函数重载的条件：
// 1. 同一作用域
// 2. 函数名相同
// 3. 参数个数或类型或顺序不同
// 4. 仅返回值不同不能构成重载！
```

### 3.4 函数重载注意事项

```cpp
// 1. 引用作为重载条件
void func(int& a) {
    cout << "int&" << endl;
}
void func(const int& a) {
    cout << "const int&" << endl;
}

int main() {
    int a = 10;
    func(a);    // 调用 int&（a 是可修改的）
    func(10);   // 调用 const int&（字面量只能绑定到 const 引用）
    return 0;
}

// 2. 重载碰到默认参数 → 可能出现二义性
void func2(int a, int b = 10) {
    cout << "1" << endl;
}
void func2(int a) {
    cout << "2" << endl;
}
// func2(10);  ❌ 二义性！两个都能匹配
```

### 3.5 内联函数（inline）

```cpp
// 普通函数：调用时有开销（跳转、压栈等）
// 内联函数：在编译时将函数体直接展开到调用处，省去调用开销

inline int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(10, 20);  // 编译时展开为: int result = 10 + 20;
    return 0;
}

// ⚠️ 内联只是给编译器的建议，编译器可能忽略
// - 适合：短小、频繁调用的函数
// - 不适合：递归、函数体大的函数
// - 类中定义的成员函数默认就是内联的
```

---

## 第4章 类与对象

### 4.1 封装

#### 访问权限

```cpp
class Person {
public:        // 公共权限：类内类外都能访问
    string name;
    
private:       // 私有权限：只有类内可以访问
    int age;
    string idCard;
    
protected:     // 保护权限：类内和子类可以访问
    string phone;
    
public:
    // 通过公有方法访问私有属性（封装的核心思想）
    void setAge(int a) {
        if (a >= 0 && a <= 150) {  // 数据验证
            age = a;
        }
    }
    int getAge() {
        return age;
    }
};
```

#### struct 和 class 的区别

| | struct | class |
|------|--------|-------|
| 默认访问权限 | public | private |
| 继承默认 | public | private |

```cpp
struct S { int a; };  // a 是 public
class C { int a; };   // a 是 private
```

#### 成员属性设为私有

```cpp
// 好处：
// 1. 可以控制读写权限
// 2. 可以验证数据的有效性

class Person {
private:
    string name;   // 可读可写
    int age;       // 可读可写（但需验证范围）
    string lover;  // 只写

public:
    // 姓名：可读可写
    void setName(string n) { name = n; }
    string getName() { return name; }
    
    // 年龄：可读可写，0-150
    void setAge(int a) {
        if (a >= 0 && a <= 150) age = a;
    }
    int getAge() { return age; }
    
    // 情人：只写
    void setLover(string l) { lover = l; }
};
```

#### 构造函数和析构函数

```cpp
class Person {
public:
    // 构造函数：创建对象时自动调用
    // 语法：类名(){}，无返回值（void 也不写）
    Person() {
        cout << "构造函数调用" << endl;
    }
    
    // 析构函数：对象销毁前自动调用
    // 语法：~类名(){}，无返回值
    ~Person() {
        cout << "析构函数调用" << endl;
    }
};

// 构造函数的分类
class Person {
public:
    Person() {                          // 无参构造
        cout << "无参构造" << endl;
    }
    Person(int a) {                     // 有参构造
        age = a;
        cout << "有参构造" << endl;
    }
    Person(const Person& p) {           // 拷贝构造
        age = p.age;
        cout << "拷贝构造" << endl;
    }
    
    int age;
};

// 调用方式
void test() {
    // 1. 括号法
    Person p1;          // 无参（不要加括号！）
    Person p2(10);      // 有参
    Person p3(p2);      // 拷贝
    
    // 2. 显示法
    Person p1;          // 无参
    Person p2 = Person(10);  // 有参
    Person p3 = Person(p2);  // 拷贝
    
    // 3. 隐式转换法
    Person p4 = 10;     // 有参（Person p4 = Person(10)）
    Person p5 = p4;     // 拷贝
}

// ⚠️ 拷贝构造函数的调用时机
// 1. 用已有对象初始化新对象
// 2. 值传递传给函数参数
// 3. 值方式返回局部对象
```

#### 深拷贝与浅拷贝（面试重点）

```cpp
class Person {
public:
    int* height;
    
    Person(int h) {
        height = new int(h);
    }
    
    // 默认拷贝构造是浅拷贝！
    // Person p2(p1); → p1.height 和 p2.height 指向同一块内存
    // 析构时同一块内存被释放两次 → 💥 崩溃！
    
    // 深拷贝：自己实现
    Person(const Person& p) {
        height = new int(*p.height);  // 重新分配内存
    }
    
    ~Person() {
        if (height != nullptr) {
            delete height;
            height = nullptr;
        }
    }
};
```

#### 初始化列表

```cpp
class Person {
public:
    int a;
    int b;
    int c;
    
    // 传统方式
    // Person(int a1, int b1, int c1) {
    //     a = a1; b = b1; c = c1;
    // }
    
    // 初始化列表方式（推荐，效率更高）
    Person(int a1, int b1, int c1) 
        : a(a1), b(b1), c(c1) {
        // 构造函数体（可为空或做其他事）
    }
};
```

#### 类对象作为成员

```cpp
// 构造顺序：先构造成员对象，再构造自己
// 析构顺序：先析构自己，再析构成员（与构造相反！）

class Phone {
public:
    string brand;
    Phone(string b) : brand(b) {
        cout << "Phone 构造" << endl;
    }
    ~Phone() { cout << "Phone 析构" << endl; }
};

class Person {
public:
    Phone phone;  // 类对象作为成员
    
    Person(string name, string phoneBrand)
        : phone(phoneBrand) {  // 初始化列表调用 Phone 构造
        cout << "Person 构造" << endl;
    }
    ~Person() { cout << "Person 析构" << endl; }
};

// 输出顺序：
// Phone 构造
// Person 构造
// Person 析构
// Phone 析构
```

#### 静态成员

```cpp
class Person {
public:
    // 静态成员变量：所有对象共享同一份数据
    static int count;
    
    Person() { count++; }
    ~Person() { count--; }
    
    // 静态成员函数：只能访问静态成员变量
    static void showCount() {
        cout << "当前人数: " << count << endl;
        // cout << name;  ❌ 不能访问非静态成员
    }
};

// 静态成员变量必须类外初始化
int Person::count = 0;

int main() {
    Person p1, p2;
    cout << Person::count << endl;  // 2（通过类名访问）
    
    // 静态成员函数调用
    Person::showCount();  // 通过类名
    p1.showCount();       // 通过对象
    return 0;
}
```

### 4.2 继承

#### 继承的基本语法

```cpp
// 基本语法
class 子类 : 继承方式 父类 {
    // ...
};

class Base {
public:
    int a;
protected:
    int b;
private:
    int c;  // 子类永远无法访问
};

// public 继承
class Son1 : public Base {
    void test() {
        a = 10;  // ✅ public → public
        b = 20;  // ✅ protected → protected
        // c = 30;  ❌ private 不可访问
    }
};

// protected 继承
class Son2 : protected Base {
    void test() {
        a = 10;  // ✅ public → protected
        b = 20;  // ✅ protected → protected
    }
};

// private 继承
class Son3 : private Base {
    void test() {
        a = 10;  // ✅ public → private
        b = 20;  // ✅ protected → private
    }
};
```

#### 继承中的对象模型

```cpp
// 父类中所有非静态成员都会被子类继承
// private 成员也被继承，只是被编译器隐藏了

class Base {
public:    int a;
protected: int b;
private:   int c;
};

class Son : public Base {
public:    int d;
};

// sizeof(Son) = 16（a+b+c+d = 4*4 = 16）
// 说明 c 也被继承了！
```

#### 继承中的构造和析构

```cpp
class Base {
public:
    Base() { cout << "Base 构造" << endl; }
    ~Base() { cout << "Base 析构" << endl; }
};

class Son : public Base {
public:
    Son() { cout << "Son 构造" << endl; }
    ~Son() { cout << "Son 析构" << endl; }
};

// 输出：
// Base 构造  ← 先构造父类
// Son 构造   ← 再构造子类
// Son 析构   ← 先析构子类
// Base 析构  ← 再析构父类
```

#### 继承中同名成员的处理

```cpp
class Base {
public:
    int a = 100;
    void func() { cout << "Base::func" << endl; }
};

class Son : public Base {
public:
    int a = 200;
    void func() { cout << "Son::func" << endl; }
};

int main() {
    Son s;
    cout << s.a << endl;           // 200（子类自己的）
    cout << s.Base::a << endl;     // 100（通过作用域访问父类）
    
    s.func();          // Son::func
    s.Base::func();    // Base::func
    return 0;
}
```

#### 多继承

```cpp
class A { public: int a; };
class B { public: int a; };

// C++ 支持多继承
class C : public A, public B {
public:
    int c;
};

int main() {
    C obj;
    // obj.a;  ❌ 二义性！A::a 还是 B::a？
    obj.A::a = 10;  // 使用作用域指定
    obj.B::a = 20;
    return 0;
}
```

#### 菱形继承问题

```
        Animal（基类）
       /     \
   Sheep     Camel
       \     /
       Alpaca（羊驼）
```

```cpp
class Animal {
public:
    int age;
};

// 虚继承解决菱形继承问题！
class Sheep : virtual public Animal {};   // virtual 关键字
class Camel : virtual public Animal {};   // virtual 关键字

class Alpaca : public Sheep, public Camel {};

int main() {
    Alpaca a;
    a.age = 10;  // 没有二义性！只有一个 age 了
    // 原理：虚基类指针 vbptr → 虚基类表 → 找到同一个 Animal 偏移量
    return 0;
}
```

### 4.3 多态

#### 多态的基本概念

```cpp
// 多态条件：
// 1. 有继承关系
// 2. 子类重写父类虚函数
// 3. 父类指针或引用指向子类对象

class Animal {
public:
    virtual void speak() {        // 虚函数
        cout << "动物在说话" << endl;
    }
    virtual ~Animal() {}          // 基类析构函数必须 virtual
};

class Cat : public Animal {
public:
    void speak() override {       // 重写（推荐加 override 做检查）
        cout << "小猫在说话" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {
        cout << "小狗在说话" << endl;
    }
};

// 实现多态
void doSpeak(Animal& animal) {
    animal.speak();  // 运行时多态：根据实际类型调用
}

int main() {
    Cat cat;
    Dog dog;
    doSpeak(cat);  // 小猫在说话
    doSpeak(dog);  // 小狗在说话
    return 0;
}
```

#### 多态原理（vtable）

```cpp
// 没有虚函数时：sizeof(Animal) = 1
// 有虚函数时：sizeof(Animal) = 4（32位）或 8（64位）

// 多出的空间就是 vfptr（虚函数表指针）
// vfptr → vftable（虚函数表）→ 实际函数地址
```

#### 纯虚函数与抽象类

```cpp
// 纯虚函数：virtual 返回类型 函数名() = 0;
// 有纯虚函数的类 = 抽象类（不能实例化）

class Base {
public:
    virtual void func() = 0;  // 纯虚函数
};

// Base b;  ❌ 抽象类不能实例化

class Son : public Base {
public:
    void func() override {
        cout << "子类实现了纯虚函数" << endl;
    }
};

Son s;  // ✅ 可以
```

#### 虚析构与纯虚析构

```cpp
// 问题：父类指针释放子类对象时，不会调用子类析构 → 内存泄漏！

class Base {
public:
    // virtual ~Base() {}  // 虚析构 ✅
    virtual ~Base() = 0;    // 纯虚析构
};

Base::~Base() {}  // 纯虚析构也需要实现（因为父类析构也要被调用）

class Son : public Base {
public:
    int* data;
    Son() { data = new int(10); }
    ~Son() {
        delete data;
        cout << "Son 析构" << endl;
    }
};

int main() {
    Base* p = new Son;
    delete p;  // ✅ 先调 Son 析构，再调 Base 析构
    return 0;
}
```

---

## 第5章 文件操作

### 5.1 文本文件

```cpp
#include <fstream>
#include <iostream>
#include <string>
using namespace std;

// 写文件
void writeFile() {
    ofstream ofs;
    ofs.open("test.txt", ios::out);
    // 或：ofstream ofs("test.txt", ios::out);
    
    ofs << "姓名：张三" << endl;
    ofs << "年龄：18" << endl;
    ofs << "成绩：90" << endl;
    
    ofs.close();
}

// 读文件（三种方式）
void readFile() {
    // 方式 1：逐词读取
    ifstream ifs("test.txt", ios::in);
    if (!ifs.is_open()) {
        cout << "文件打开失败" << endl;
        return;
    }
    
    char buf1[1024] = {0};
    while (ifs >> buf1) {  // 遇到空格/换行就停
        cout << buf1 << endl;
    }
    ifs.close();
    
    // 方式 2：逐行读取
    ifstream ifs2("test.txt", ios::in);
    char buf2[1024] = {0};
    while (ifs2.getline(buf2, sizeof(buf2))) {
        cout << buf2 << endl;
    }
    ifs2.close();
    
    // 方式 3：用 string 逐行读取（推荐）
    ifstream ifs3("test.txt", ios::in);
    string line;
    while (getline(ifs3, line)) {
        cout << line << endl;
    }
    ifs3.close();
}
```

### 5.2 二进制文件

```cpp
// 写二进制文件
class Person {
public:
    char name[64];
    int age;
};

void binaryWrite() {
    Person p = {"张三", 18};
    ofstream ofs("person.dat", ios::out | ios::binary);
    ofs.write((const char*)&p, sizeof(p));
    ofs.close();
}

// 读二进制文件
void binaryRead() {
    Person p;
    ifstream ifs("person.dat", ios::in | ios::binary);
    ifs.read((char*)&p, sizeof(p));
    cout << p.name << " " << p.age << endl;
    ifs.close();
}
```

### 5.3 文件打开方式

| 模式 | 说明 |
|------|------|
| `ios::in` | 读文件 |
| `ios::out` | 写文件（覆盖） |
| `ios::app` | 追加写 |
| `ios::ate` | 打开时定位到文件末尾 |
| `ios::trunc` | 如果文件存在，先删除再创建 |
| `ios::binary` | 二进制方式 |

组合使用：`ios::out | ios::binary`

---

# 第三阶段：C++ 提高编程

---

## 第1章 模板（Template）

### 1.1 函数模板

```cpp
// 不用模板：每个类型写一个函数
void swapInt(int& a, int& b) { int t = a; a = b; b = t; }
void swapDouble(double& a, double& b) { double t = a; a = b; b = t; }

// 用模板：一个搞定所有
template<typename T>      // 或 template<class T>
void mySwap(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

int main() {
    int a = 10, b = 20;
    mySwap(a, b);               // 自动类型推导
    
    double c = 1.1, d = 2.2;
    mySwap<double>(c, d);       // 显式指定类型
    
    return 0;
}
```

### 1.2 函数模板注意事项

```cpp
// 1. 自动类型推导必须推导出一致的数据类型 T 才能使用
template<typename T>
void func(T a, T b) {}

// func(10, 3.14);  ❌ T 推导出 int 还是 double？不一致！

// 2. 模板必须确定出 T 的数据类型才可以使用
template<typename T>
void func2() { T a; }

// func2();  ❌ 无法推导 T 的类型
func2<int>();  // ✅ 显式指定
```

### 1.3 普通函数与函数模板的区别

```cpp
// 普通函数可以发生隐式类型转换
// 函数模板用自动类型推导时不可隐式转换（显式指定可以）

int myAdd(int a, int b) { return a + b; }

template<typename T>
T myAddTemplate(T a, T b) { return a + b; }

int main() {
    int a = 10;
    char c = 'A';  // 'A' = 65
    
    cout << myAdd(a, c) << endl;        // 75（char → int 隐式转换）
    // cout << myAddTemplate(a, c);  ❌ 自动推导：int vs char 不一致
    cout << myAddTemplate<int>(a, c) << endl;  // 75（显式指定 int）
    return 0;
}
```

### 1.4 普通函数与函数模板的调用规则

```
1. 优先调用普通函数
2. 可通过空模板参数列表强制调模板：func<>(a, b)
3. 函数模板也能重载
4. 如果函数模板能产生更好的匹配，优先调模板
```

### 1.5 类模板

```cpp
template<class NameType, class AgeType = int>  // 可以指定默认类型
class Person {
public:
    NameType name;
    AgeType age;
    
    Person(NameType n, AgeType a) : name(n), age(a) {}
    
    void show() {
        cout << name << " " << age << endl;
    }
};

int main() {
    Person<string, int> p1("张三", 18);  // 类模板必须显式指定类型
    Person<string> p2("李四", 20);        // 使用默认类型 int
    
    p1.show();
    p2.show();
    return 0;
}
```

### 1.6 类模板做函数参数

```cpp
// 方式1：指定传入类型（最常用）
void printPerson1(Person<string, int>& p) {
    p.show();
}

// 方式2：参数模板化
template<class T1, class T2>
void printPerson2(Person<T1, T2>& p) {
    p.show();
    cout << "T1: " << typeid(T1).name() << endl;
}

// 方式3：整个类模板化
template<class T>
void printPerson3(T& p) {
    p.show();
    cout << "T: " << typeid(T).name() << endl;
}
```

### 1.7 类模板与继承

```cpp
template<class T>
class Base {
public:
    T value;
};

// 子类继承模板类时必须指定父类的模板类型
// class Son : public Base { ❌ 错误！必须知道 T 的类型 }
class Son1 : public Base<int> {};  // ✅ 指定为 int

// 或者子类也做成模板
template<class T>
class Son2 : public Base<T> {
    T value2;
};
```

### 1.8 类模板成员函数类外实现

```cpp
template<class T1, class T2>
class Person {
public:
    T1 name;
    T2 age;
    Person(T1 n, T2 a);
    void show();
};

// 类外实现构造函数
template<class T1, class T2>
Person<T1, T2>::Person(T1 n, T2 a) : name(n), age(a) {}

// 类外实现成员函数
template<class T1, class T2>
void Person<T1, T2>::show() {
    cout << "姓名：" << name << " 年龄：" << age << endl;
}
```

### 1.9 类模板分文件编写

```
⚠️ 类模板的声明和实现不要分开到 .h 和 .cpp！

原因：模板在编译时实例化，编译器需要看到完整定义。
解决：
1. 直接放到一个 .hpp 文件中（推荐）
2. 或在使用时 #include "xxx.cpp"
```

### 1.10 模板案例：通用数组类

```cpp
#include <iostream>
using namespace std;

template<class T>
class MyArray {
private:
    T* pAddress;    // 数组指针
    int capacity;   // 容量
    int size;       // 当前大小

public:
    MyArray(int cap) {
        capacity = cap;
        size = 0;
        pAddress = new T[capacity];
    }

    // 拷贝构造（深拷贝）
    MyArray(const MyArray& arr) {
        capacity = arr.capacity;
        size = arr.size;
        pAddress = new T[capacity];
        for (int i = 0; i < size; i++) {
            pAddress[i] = arr.pAddress[i];
        }
    }

    // 赋值运算符（深拷贝）
    MyArray& operator=(const MyArray& arr) {
        if (this == &arr) return *this;
        if (pAddress != nullptr) {
            delete[] pAddress;
            pAddress = nullptr;
        }
        capacity = arr.capacity;
        size = arr.size;
        pAddress = new T[capacity];
        for (int i = 0; i < size; i++) {
            pAddress[i] = arr.pAddress[i];
        }
        return *this;
    }

    // 尾插
    void pushBack(const T& val) {
        if (size == capacity) return;
        pAddress[size++] = val;
    }

    // 尾删
    void popBack() {
        if (size == 0) return;
        size--;
    }

    // 通过下标访问（可修改）
    T& operator[](int index) {
        return pAddress[index];
    }

    // 通过下标访问（只读）
    const T& operator[](int index) const {
        return pAddress[index];
    }

    int getSize() const { return size; }
    int getCapacity() const { return capacity; }

    ~MyArray() {
        if (pAddress != nullptr) {
            delete[] pAddress;
            pAddress = nullptr;
        }
    }
};
```

---

## 第2章 STL 初识

### 2.1 STL 六大组件

```
1. 容器（Containers）      各种数据结构：vector、list、map...
2. 算法（Algorithms）      常用算法：sort、find、copy...
3. 迭代器（Iterators）     容器和算法之间的粘合剂
4. 仿函数（Functors）      行为类似函数的对象
5. 适配器（Adapters）      修饰容器/仿函数/迭代器接口
6. 空间配置器（Allocators） 负责内存管理
```

### 2.2 三大常用容器

```cpp
#include <vector>
#include <algorithm>

void print(int val) { cout << val << " "; }

int main() {
    vector<int> v;  // 创建容器
    
    // 插入数据
    v.push_back(10);
    v.push_back(20);
    v.push_back(30);
    
    // 通过迭代器遍历
    // 方式 1
    for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
        cout << *it << " ";
    }
    cout << endl;
    
    // 方式 2（C++11 范围 for）
    for (int val : v) cout << val << " ";
    cout << endl;
    
    // 方式 3：for_each 算法 + 仿函数
    for_each(v.begin(), v.end(), print);
    cout << endl;
    
    return 0;
}
```

### 2.3 vector 中存放自定义类型

```cpp
class Person {
public:
    string name;
    int age;
    Person(string n, int a) : name(n), age(a) {}
};

int main() {
    vector<Person> v;
    
    // 直接放对象
    v.push_back(Person("张三", 18));
    v.push_back(Person("李四", 20));
    
    // 放指针（常用）
    vector<Person*> vp;
    vp.push_back(new Person("王五", 22));
    
    // 遍历
    for (vector<Person>::iterator it = v.begin(); it != v.end(); it++) {
        cout << (*it).name << " " << (*it).age << endl;
        // 或 it->name << " " << it->age
    }
    
    // 记得释放指针！
    for (auto p : vp) delete p;
    
    return 0;
}
```

### 2.4 vector 容器嵌套

```cpp
// 二维数组
vector<vector<int>> v;

// 创建小容器
vector<int> v1 = {1, 2, 3};
vector<int> v2 = {4, 5, 6};
vector<int> v3 = {7, 8, 9};

// 大容器装入小容器
v.push_back(v1);
v.push_back(v2);
v.push_back(v3);

// 遍历
for (auto& sub : v) {
    for (int val : sub) {
        cout << val << " ";
    }
    cout << endl;
}
```

---

## 第3章 string 容器

### 3.1 string 构造函数

```cpp
string s1;                    // 默认构造
string s2("Hello");           // C 字符串初始化
string s3(s2);                // 拷贝构造
string s4(10, 'a');           // "aaaaaaaaaa"
```

### 3.2 string 赋值操作

```cpp
string s;
s = "Hello";                    // = 赋值
s.assign("World");              // assign
s.assign("Hello World", 5);     // 前 5 个字符 "Hello"
s.assign("Hello World", 6, 5);  // 从下标6开始取5个 "World"
s.assign(10, 'X');              // "XXXXXXXXXX"
```

### 3.3 string 拼接

```cpp
string s = "Hello";
s += " World";                   // +=
s += '!';                        // += char
s.append(" C++");                // append
s.append("is great", 2);         // 前2个字符 "is"
s.append("ABCDE", 1, 3);         // 从下标1取3个 "BCD"
```

### 3.4 string 查找和替换

```cpp
string s = "abcdefgabc";

// 查找（找不到返回 string::npos，即 -1）
int pos1 = s.find("de");         // 3（从 0 开始，默认从头找）
int pos2 = s.find("abc", 1);     // 7（从下标1开始找）
int pos3 = s.rfind("abc");       // 7（从右往左找）

// 替换
s.replace(1, 3, "1111");         // 从下标1开始，替换3个字符为 "1111"
// "abcdefgabc" → "a1111efgabc"
```

### 3.5 string 比较

```cpp
string s1 = "abc";
string s2 = "abd";

int ret = s1.compare(s2);
// ret = 0: 相等
// ret < 0: s1 < s2（逐个字符 ASCII 比较）
// ret > 0: s1 > s2

// 常用于判断大小写无关的排序
```

### 3.6 string 字符存取

```cpp
string s = "Hello";

// 方式 1：[]（不检查越界）
cout << s[0] << endl;  // 'H'
s[0] = 'h';             // "hello"

// 方式 2：at()（检查越界，越界抛异常）
cout << s.at(0) << endl;
s.at(0) = 'H';
```

### 3.7 string 插入和删除

```cpp
string s = "Hello";
s.insert(1, "xxx");    // "Hxxxello"（在下标1处插入）
s.erase(1, 3);         // "Hello"（从下标1开始删除3个）
```

### 3.8 string 子串

```cpp
string s = "Hello World";
string sub = s.substr(6, 5);  // 从下标6开始取5个 → "World"

// 实用：提取邮箱用户名
string email = "zhangsan@qq.com";
int pos = email.find('@');
string username = email.substr(0, pos);  // "zhangsan"
```

---

## 第4章 vector 容器

### 4.1 vector 基本概念

```
vector 是单端动态数组
- 尾部插入/删除：O(1)
- 头部插入/删除：O(n)（需要移动所有元素）
- 支持随机访问：v[i]（O(1)）
```

### 4.2 vector 常用 API

```cpp
#include <vector>

// 构造函数
vector<int> v1;                           // 默认
vector<int> v2(10, 100);                  // 10 个 100
vector<int> v3(v2.begin(), v2.end());     // 区间拷贝
vector<int> v4(v3);                       // 拷贝构造

// 赋值
v1.assign(v2.begin(), v2.end());
v1.assign(10, 100);                       // 10 个 100
v1 = v3;

// 容量和大小
v.empty();          // 是否为空
v.size();           // 元素个数
v.capacity();       // 容量（>= size）
v.resize(15);       // 重新指定大小（变长默认填充 0，变短删除超出）
v.resize(15, 100);  // 重新指定大小（填充 100）

// 插入和删除
v.push_back(10);    // 尾部插入
v.pop_back();       // 尾部删除
v.insert(v.begin(), 100);         // 在迭代器位置插入 100
v.insert(v.begin(), 2, 100);      // 插入 2 个 100
v.erase(v.begin());               // 删除迭代器位置元素
v.erase(v.begin(), v.end());      // 删除区间
v.clear();                        // 清空

// 数据存取
v[i];          // 不检查越界
v.at(i);       // 检查越界
v.front();     // 第一个元素
v.back();      // 最后一个元素

// 互换容器（收缩内存）
vector<int>(v).swap(v);  // 匿名对象交换后立刻销毁，释放多余容量
```

### 4.3 vector 预留空间

```cpp
vector<int> v;
v.reserve(100000);  // 预留空间，减少动态扩容次数

// 适用场景：已知大概要存多少数据，提前 reserve 可以大幅提升性能
```

---

## 第5章 deque 容器

### 5.1 deque 基本概念

```
deque 是双端数组
- 头部和尾部插入/删除：O(1)
- 中间插入/删除：O(n)
- 支持随机访问：d[i]（比 vector 稍慢）
- 内部使用分段连续空间（中控器 + 多个缓冲区）
```

### 5.2 deque 常用 API

```cpp
#include <deque>

deque<int> d;

// 两端操作
d.push_back(10);     // 尾插
d.push_front(5);     // 头插
d.pop_back();        // 尾删
d.pop_front();       // 头删

// 其他和 vector 一样
d.size(); d.empty(); d.resize(); 
d.insert(); d.erase(); d.clear();
d[i]; d.at(i); d.front(); d.back();
```

### 5.3 案例：评委打分

```cpp
#include <iostream>
#include <vector>
#include <deque>
#include <algorithm>
#include <ctime>
using namespace std;

class Player {
public:
    string name;
    double score;
};

// 模拟：5 个选手，10 个评委打分，去掉最高最低后取平均
void contest(vector<Player>& players) {
    for (auto& p : players) {
        deque<int> scores;
        
        // 10 个评委打分
        for (int i = 0; i < 10; i++) {
            int score = rand() % 41 + 60;  // 60-100
            scores.push_back(score);
        }
        
        sort(scores.begin(), scores.end());
        
        scores.pop_front();  // 去掉最低
        scores.pop_back();   // 去掉最高
        
        int sum = 0;
        for (int s : scores) sum += s;
        p.score = (double)sum / scores.size();
    }
}
```

---

## 第6章 stack 容器

### 6.1 stack 基本概念

```
stack 是栈（先进后出 FILO）
- 只有顶端能进出
- 不允许遍历（没有迭代器）
- 底层可以是 deque（默认）或 vector
```

### 6.2 stack 常用 API

```cpp
#include <stack>

stack<int> s;

s.push(10);     // 入栈
s.push(20);
s.push(30);
s.pop();        // 出栈（删除栈顶）
s.top();        // 查看栈顶元素（不删除）
s.empty();      // 是否为空
s.size();       // 大小
```

---

## 第7章 queue 容器

### 7.1 queue 基本概念

```
queue 是队列（先进先出 FIFO）
- 队尾进，队头出
- 不允许遍历（没有迭代器）
- 底层默认是 deque
```

### 7.2 queue 常用 API

```cpp
#include <queue>

queue<int> q;

q.push(10);     // 入队（队尾）
q.push(20);
q.push(30);
q.pop();        // 出队（队头删除）
q.front();      // 队头元素
q.back();       // 队尾元素
q.empty();
q.size();
```

---

## 第8章 list 容器

### 8.1 list 基本概念

```
list 是双向循环链表
- 任何位置插入/删除：O(1)
- 不支持随机访问：没有 v[i]（需要遍历）
- 额外有指针开销
- 有专属的 sort、reverse 方法
```

### 8.2 list 常用 API

```cpp
#include <list>

list<int> l;
l.push_back(10);       // 尾插
l.push_front(5);       // 头插
l.pop_back();          // 尾删
l.pop_front();         // 头删

// 插入和删除
l.insert(++l.begin(), 100);   // 在第二个位置插入
l.erase(l.begin());           // 删除第一个
l.remove(100);                // 删除所有值为 100 的

// 专属操作
l.reverse();          // 反转
l.sort();             // 排序（list 的成员方法，不是算法库的）
l.unique();           // 去重（需要先排序）

// ⚠️ list 不支持 v[i] 随机访问！只能用迭代器遍历
for (list<int>::iterator it = l.begin(); it != l.end(); it++) {
    cout << *it << " ";
}
```

---

## 第9章 set/multiset 容器

### 9.1 set 基本概念

```
set 是关联式容器，底层是红黑树
- 所有元素自动排序（默认升序）
- 不允许重复元素
- 插入/删除/查找：O(log n)
```

### 9.2 set 常用 API

```cpp
#include <set>

// 构造
set<int> s1;
set<int> s2(s1);
set<int> s3 = {5, 3, 1, 4, 2};  // 自动排序为 1,2,3,4,5

// 插入
s1.insert(10);
s1.insert(10);  // ❌ set 不允许重复，第二次插入无效
s1.insert(20);

// 大小和交换
s1.size(); s1.empty(); s1.swap(s2);

// 删除
s1.erase(10);              // 按值删除
s1.erase(s1.begin());      // 按迭代器删除
s1.clear();                // 清空

// 查找和统计
set<int>::iterator pos = s1.find(10);  // 找到返回迭代器，否则返回 s1.end()
int count = s1.count(10);              // 统计个数（set 只会是 0 或 1）

// 插入结果（pair）
pair<set<int>::iterator, bool> ret = s1.insert(10);
if (ret.second) {
    cout << "插入成功" << endl;
} else {
    cout << "插入失败（重复元素）" << endl;
}
```

### 9.3 set 排序规则

```cpp
// 方式 1：自定义仿函数
class MyCompare {
public:
    bool operator()(int v1, int v2) const {
        return v1 > v2;  // 降序
    }
};

set<int, MyCompare> s;
s.insert(10); s.insert(30); s.insert(20);
// 存储顺序：30, 20, 10

// 方式 2：自定义类型的排序
class Person {
public:
    string name;
    int age;
};

class ComparePerson {
public:
    bool operator()(const Person& p1, const Person& p2) const {
        return p1.age < p2.age;  // 按年龄升序
    }
};

set<Person, ComparePerson> persons;
```

### 9.4 multiset

```cpp
// multiset 和 set 几乎一样，唯一区别：允许重复元素！
multiset<int> ms;
ms.insert(10);
ms.insert(10);  // ✅ 可以插入重复值
cout << ms.count(10) << endl;  // 2
```

---

## 第10章 map/multimap 容器

### 10.1 map 基本概念

```
map 是关联式容器，底层是红黑树
- 存储 pair<key, value>
- key 唯一且自动排序
- value 可以重复
- 插入/删除/查找：O(log n)
```

### 10.2 pair 对组

```cpp
// pair 将两个数据组合成一组
pair<string, int> p("张三", 18);

// 创建方式
pair<string, int> p1("张三", 18);
pair<string, int> p2 = make_pair("李四", 20);

// 访问
cout << p1.first << endl;   // 张三（key）
cout << p1.second << endl;  // 18（value）
```

### 10.3 map 常用 API

```cpp
#include <map>

map<string, int> m;

// 插入（四种方式）
m.insert(pair<string, int>("张三", 18));
m.insert(make_pair("李四", 20));
m.insert(map<string, int>::value_type("王五", 22));
m["赵六"] = 25;          // 最简洁，但 key 不存在时会创建默认值！

// 大小和交换
m.size(); m.empty(); m.swap(m2);

// 删除
m.erase("张三");          // 按 key 删除
m.erase(m.begin());       // 按迭代器删除
m.clear();

// 查找
map<string, int>::iterator pos = m.find("李四");
if (pos != m.end()) {
    cout << "找到了: " << pos->first << " " << pos->second << endl;
} else {
    cout << "没找到" << endl;
}

// 统计
cout << m.count("张三") << endl;  // 0 或 1（map 不允许重复 key）

// 遍历
for (auto& p : m) {
    cout << p.first << ": " << p.second << endl;
}
```

### 10.4 map 排序

```cpp
// 默认按 key 升序
// 自定义排序：需要仿函数
class MyCompare {
public:
    bool operator()(int v1, int v2) const {
        return v1 > v2;  // 降序
    }
};

map<int, int, MyCompare> m;
m.insert(make_pair(1, 10));
m.insert(make_pair(3, 30));
m.insert(make_pair(2, 20));
// 遍历顺序：3, 2, 1
```

### 10.5 multimap

```cpp
// multimap 和 map 几乎一样，区别：
// 1. key 可以重复
// 2. multimap 不支持 m[key] 访问（因为 key 不唯一！）

multimap<string, int> mm;
mm.insert(make_pair("张三", 18));
mm.insert(make_pair("张三", 85));  // ✅ 可以重复 key

cout << mm.count("张三") << endl;  // 2
```

---

## 第11章 函数对象（仿函数）

### 11.1 什么是函数对象？

```cpp
// 重载了 operator() 的类对象 = 函数对象（仿函数）

class MyAdd {
public:
    int operator()(int v1, int v2) {
        return v1 + v2;
    }
};

int main() {
    MyAdd myAdd;
    cout << myAdd(10, 20) << endl;  // 30（像函数一样调用对象！）
    cout << MyAdd()(10, 20) << endl;  // 30（匿名对象）
    return 0;
}
```

### 11.2 一元谓词

```cpp
// 谓词：返回值为 bool 的仿函数
// 一元谓词：一个参数

class GreaterThanFive {
public:
    bool operator()(int val) {
        return val > 5;
    }
};

int main() {
    vector<int> v = {1, 3, 5, 7, 9};
    
    // find_if 使用谓词
    vector<int>::iterator it = find_if(v.begin(), v.end(), GreaterThanFive());
    if (it != v.end()) {
        cout << "第一个大于5的数: " << *it << endl;  // 7
    }
    
    return 0;
}
```

### 11.3 二元谓词

```cpp
// 二元谓词：两个参数

class MyCompare {
public:
    bool operator()(int v1, int v2) {
        return v1 > v2;  // 降序
    }
};

int main() {
    vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6};
    
    // sort 使用二元谓词自定义排序
    sort(v.begin(), v.end(), MyCompare());
    // v: 9, 6, 5, 4, 3, 2, 1, 1
    
    return 0;
}
```

### 11.4 内建函数对象

```cpp
#include <functional>

// 算术仿函数
negate<int> n;               // 取反
cout << n(10) << endl;       // -10

plus<int> p;                 // 加法
cout << p(10, 20) << endl;   // 30

// 关系仿函数（常用于排序）
sort(v.begin(), v.end(), greater<int>());  // 降序

// 逻辑仿函数
logical_not<bool> l;
cout << l(true) << endl;     // false
```

---

## 第12章 STL 常用算法

### 12.1 遍历算法

```cpp
#include <algorithm>

vector<int> v = {1, 2, 3, 4, 5};

// for_each：遍历
void print(int val) { cout << val << " "; }
for_each(v.begin(), v.end(), print);

// transform：搬运（可以给另一个容器）
vector<int> v2;
v2.resize(v.size());
transform(v.begin(), v.end(), v2.begin(), [](int val) {
    return val * 10;
});
// v2: 10, 20, 30, 40, 50
```

### 12.2 查找算法

```cpp
// find：查找值
vector<int>::iterator it = find(v.begin(), v.end(), 3);
if (it != v.end()) cout << "找到了: " << *it << endl;

// find_if：按条件查找
it = find_if(v.begin(), v.end(), [](int val) { return val > 3; });

// adjacent_find：查找相邻重复元素
vector<int> v2 = {1, 2, 2, 3, 4, 4, 5};
it = adjacent_find(v2.begin(), v2.end());
// 找到第一个 2（和下一个相同）

// binary_search：二分查找（必须有序！）
bool found = binary_search(v.begin(), v.end(), 3);

// count：统计个数
int cnt = count(v.begin(), v.end(), 4);  // 值为 4 的有几个

// count_if：按条件统计
int cnt2 = count_if(v.begin(), v.end(), [](int val) { return val > 3; });
```

### 12.3 排序算法

```cpp
// sort：排序（默认升序）
sort(v.begin(), v.end());
sort(v.begin(), v.end(), greater<int>());  // 降序

// random_shuffle：随机打乱
#include <ctime>
srand((unsigned)time(NULL));
random_shuffle(v.begin(), v.end());

// merge：合并两个有序序列到第三个（结果仍然有序）
vector<int> v1 = {1, 3, 5};
vector<int> v2 = {2, 4, 6};
vector<int> v3(6);
merge(v1.begin(), v1.end(), v2.begin(), v2.end(), v3.begin());
// v3: 1, 2, 3, 4, 5, 6

// reverse：反转
reverse(v.begin(), v.end());
```

### 12.4 拷贝和替换算法

```cpp
// copy：拷贝
vector<int> v2;
v2.resize(v.size());
copy(v.begin(), v.end(), v2.begin());

// replace：替换
replace(v.begin(), v.end(), 5, 500);  // 把所有 5 替换成 500

// replace_if：按条件替换
replace_if(v.begin(), v.end(), [](int val) { return val > 3; }, 100);

// swap：交换两个容器（同类型）
swap(v1, v2);
```

### 12.5 算术生成算法

```cpp
#include <numeric>  // 注意！不是 algorithm

// accumulate：累加
int sum = accumulate(v.begin(), v.end(), 0);  // 0 是起始累加值

// fill：填充
fill(v.begin(), v.end(), 100);  // 全部填充为 100
```

### 12.6 集合算法

```cpp
// 两个集合必须是有序的！
vector<int> v1 = {1, 2, 3, 4, 5};
vector<int> v2 = {3, 4, 5, 6, 7};
vector<int> result(10);

// set_intersection：交集 → 3, 4, 5
auto it = set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());
result.resize(it - result.begin());

// set_union：并集 → 1, 2, 3, 4, 5, 6, 7
it = set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());
result.resize(it - result.begin());

// set_difference：差集 (v1 中不在 v2 的) → 1, 2
it = set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());
result.resize(it - result.begin());
```

### 12.7 综合案例：员工分组

```cpp
#include <iostream>
#include <vector>
#include <map>
#include <string>
#include <algorithm>
#include <ctime>
using namespace std;

// 部门编号
enum Department { CEHUA = 0, MEISHU = 1, YANFA = 2 };

class Worker {
public:
    string name;
    int salary;
};

void createWorkers(vector<Worker>& v) {
    string nameSeed = "ABCDEFGHIJ";
    for (int i = 0; i < 10; i++) {
        Worker w;
        w.name = "员工";
        w.name += nameSeed[i];
        w.salary = rand() % 10001 + 10000;  // 10000-20000
        v.push_back(w);
    }
}

void setGroup(const vector<Worker>& v, multimap<int, Worker>& m) {
    for (auto& w : v) {
        int deptId = rand() % 3;
        m.insert(make_pair(deptId, w));
    }
}

void showWorkers(const multimap<int, Worker>& m) {
    cout << "策划部门：" << endl;
    auto range = m.equal_range(CEHUA);
    for (auto it = range.first; it != range.second; it++) {
        cout << it->second.name << " 薪资: " << it->second.salary << endl;
    }
    
    cout << "美术部门：" << endl;
    range = m.equal_range(MEISHU);
    for (auto it = range.first; it != range.second; it++) {
        cout << it->second.name << " 薪资: " << it->second.salary << endl;
    }
    
    cout << "研发部门：" << endl;
    range = m.equal_range(YANFA);
    for (auto it = range.first; it != range.second; it++) {
        cout << it->second.name << " 薪资: " << it->second.salary << endl;
    }
}

int main() {
    srand((unsigned)time(NULL));
    
    vector<Worker> workers;
    createWorkers(workers);
    
    multimap<int, Worker> groups;
    setGroup(workers, groups);
    
    showWorkers(groups);
    
    return 0;
}
```

---

## 🎯 全课程核心知识点速查表

| 章节 | 必知必会 | 面试频率 |
|------|---------|---------|
| 数据类型 | sizeof、ASCII、字符串类型 | ⭐⭐⭐ |
| 程序流程 | if/switch/for/while/break/continue | ⭐⭐⭐⭐ |
| 数组 | 一维/二维定义、冒泡排序 | ⭐⭐⭐ |
| 函数 | 声明/定义/分文件、值传递 | ⭐⭐⭐⭐ |
| 指针 | 定义、const 指针、指针与数组/函数 | ⭐⭐⭐⭐⭐ |
| 结构体 | 定义、数组、指针、嵌套 | ⭐⭐⭐ |
| 内存分区 | 四区模型、栈 vs 堆、new/delete | ⭐⭐⭐⭐⭐ |
| 引用 | 本质（指针常量）、传参、返回值 | ⭐⭐⭐⭐⭐ |
| 函数提高 | 默认参数、占位参数、重载 | ⭐⭐⭐⭐ |
| 类与对象 | 封装/继承/多态、构造析构、深浅拷贝 | ⭐⭐⭐⭐⭐ |
| 文件操作 | 文本/二进制读写 | ⭐⭐ |
| 模板 | 函数模板、类模板、分文件问题 | ⭐⭐⭐⭐ |
| STL 容器 | vector/deque/stack/queue/list/set/map | ⭐⭐⭐⭐⭐ |
| 函数对象 | 谓词、内建仿函数 | ⭐⭐⭐ |
| STL 算法 | sort/find/for_each/count/merge | ⭐⭐⭐⭐ |

---

> 📚 **学习建议**  
> 1. 第一阶段重点：函数、指针、结构体（C 基础过渡到 C++）  
> 2. 第二阶段重点：内存模型、引用、类与对象（面向对象核心）  
> 3. 第三阶段重点：模板、STL 容器和算法（实际开发最常用）  
> 
> 每个代码示例都至少手敲一遍！只看不练 = 没学。