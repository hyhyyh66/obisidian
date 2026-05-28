# C++ 三小时进阶教程（Day 2）

> **前置知识**：Day 1 内容（cout/cin、string、引用、函数重载、class 基础、vector）  
> **适用对象**：有 C 指针基础、Day 1 C++ 入门  
> **学习时间**：约 3 小时（含练习）  
> **学习目标**：掌握 C++ 动态内存、析构函数、拷贝控制、继承、多态、智能指针  

---

## 📋 学习路线总览

| 时间段 | 内容 | 核心知识点 |
|--------|------|-----------|
| 第 1 小时 | 指针与动态内存 | `new`/`delete`、`malloc` 对比、空指针、`this` 指针 |
| 第 2 小时 | 析构与拷贝控制 | 析构函数、拷贝构造、赋值运算符、Rule of Three |
| 第 3 小时 | 继承与多态 | 继承语法、虚函数 `virtual`、纯虚函数、智能指针 |

---

# 🕐 第 1 小时：指针与动态内存（60 分钟）

## 1.1 C 指针快速回顾（5 分钟）

你已经熟悉 C 的指针，简单过一下：

```cpp
int x = 10;
int* p = &x;       // p 存储 x 的地址
*p = 20;           // 解引用，修改 x 的值
cout << x;         // 20
```

- `&` 取地址（你已熟悉）
- `*` 解引用（你已熟悉）

**和 Day 1 学的引用的区别**：

| | 指针 (Pointer) | 引用 (Reference) |
|------|---------------|-----------------|
| 语法 | `int* p = &x;` | `int& ref = x;` |
| 解引用 | 需要 `*p` | 直接 `ref` |
| 可以为空 | `nullptr` | ❌ 不存在空引用 |
| 可重新指向 | `p = &y;` | ❌ 不能重新绑定 |
| 需要取地址调用 | `func(&x)` | `func(x)` 直接传 |

---

## 1.2 `new` 和 `delete`：C++ 的动态内存（15 分钟）

### 📝 C 语言回忆

```c
// C 语言
int* p = (int*)malloc(sizeof(int));   // 分配
*p = 42;
free(p);                              // 释放
```

### C++ 方式：`new` 和 `delete`

```cpp
// C++ 语言（更简洁更安全）
int* p = new int;      // 分配一个 int
*p = 42;
delete p;              // 释放

// 分配并初始化
int* p2 = new int(42);  // 直接初始化为 42
delete p2;

// 分配数组
int* arr = new int[10];  // 分配 10 个 int 的数组
for (int i = 0; i < 10; i++) {
    arr[i] = i;
}
delete[] arr;             // 释放数组！注意是 delete[] 不是 delete
```

### 🔍 `new`/`delete` vs `malloc`/`free` 核心区别

| | `malloc`/`free` | `new`/`delete` |
|------|---------------|----------------|
| 是什么 | **函数** | **运算符**（C++ 关键字） |
| 返回类型 | `void*`（需要强转） | 正确类型指针（不需要强转） |
| 调用构造函数 | ❌ 不调用 | ✅ 自动调用 |
| 调用析构函数 | ❌ 不调用 | ✅ 自动调用 |
| 分配失败 | 返回 `NULL` | 抛出 `std::bad_alloc` 异常 |
| 大小计算 | 需要 `sizeof` | 编译器自动算 |

### 💡 最重要的区别：构造函数和析构函数

```cpp
class Person {
public:
    string name;
    Person(const string& n) {
        name = n;
        cout << "Person " << name << " 被创建" << endl;
    }
    ~Person() {  // 析构函数，后面会详细讲
        cout << "Person " << name << " 被销毁" << endl;
    }
};

// malloc/free：不调用构造/析构函数
Person* p1 = (Person*)malloc(sizeof(Person));  // 构造没被调用！
free(p1);                                       // 析构没被调用！→ 危险！

// new/delete：正确调用构造/析构函数
Person* p2 = new Person("小明");  // 输出: Person 小明 被创建
delete p2;                        // 输出: Person 小明 被销毁
```

> ⚠️ **黄金法则**：在 C++ 中永远用 `new`/`delete`，不要用 `malloc`/`free`，除非你有特殊理由（比如要和 C 代码交互）。

### 📝 要求：用 `new` 创建一个 Rectangle 数组并打印其面积

回忆 Day1 的 Rectangle 类（有 width、height、area()），用 new 在堆上创建两个 Rectangle 对象。

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
using namespace std;

class Rectangle {
private:
    double width, height;
public:
    Rectangle(double w, double h) : width(w), height(h) {}
    double area() { return width * height; }
};

int main() {
    // 在堆上创建单个对象
    Rectangle* r1 = new Rectangle(5.0, 3.0);
    cout << "r1 面积: " << r1->area() << endl;  // 指针用 -> 访问成员
    delete r1;

    // 在堆上创建对象数组
    Rectangle* rects = new Rectangle[2]{
        Rectangle(4.0, 2.0),
        Rectangle(3.0, 3.0)
    };
    
    for (int i = 0; i < 2; i++) {
        cout << "rects[" << i << "] 面积: " << rects[i].area() << endl;
    }
    delete[] rects;  // 数组必须用 delete[]

    return 0;
}
```

</details>

---

## 1.3 空指针：`nullptr`（5 分钟）

C 语言用 `NULL`（本质是 `0`），C++11 引入了专用的 `nullptr`：

```cpp
// C 风格（不推荐）
int* p1 = NULL;
int* p2 = 0;

// C++11 风格（推荐）
int* p3 = nullptr;
```

**为什么 `nullptr` 更好？**

```cpp
void func(int x) {
    cout << "func(int) 被调用" << endl;
}

void func(int* p) {
    cout << "func(int*) 被调用" << endl;
}

int main() {
    func(NULL);     // 调用 func(int)！因为 NULL 就是 0！
    func(nullptr);  // 调用 func(int*)！nullptr 有指针类型！
    return 0;
}
```

> **结论**：在 C++ 中，始终用 `nullptr`。

---

## 1.4 `this` 指针（10 分钟）

### 📝 这是什么？

每个成员函数内部都有一个隐式的 `this` 指针，指向**调用该函数的对象**。

```cpp
class Person {
private:
    string name;
    int age;
public:
    Person(const string& name, int age) {
        // 参数名和成员名相同怎么办？
        // this->name 是成员变量，name 是参数
        this->name = name;
        this->age = age;
    }

    // 返回 *this 可以实现链式调用
    Person& setAge(int age) {
        this->age = age;
        return *this;   // 返回自己
    }

    Person& setName(const string& name) {
        this->name = name;
        return *this;
    }

    void print() {
        cout << "我叫" << this->name << ", 今年" << this->age << "岁" << endl;
        // 也可以省略 this->
        // cout << "我叫" << name << ", 今年" << age << "岁" << endl;
    }
};

int main() {
    Person p("张三", 20);
    p.print();  // 此时 this 指向 p

    // 链式调用：因为 setAge 返回 *this
    p.setName("李四").setAge(25).print();
    // 输出：我叫李四, 今年25岁

    return 0;
}
```

### 💡 和 Python 对比

| C++ | Python |
|-----|--------|
| `this` 是隐式指针 | `self` 必须显式写在参数列表 |
| `this->name` | `self.name` |
| 不写 `this->` 也能访问成员 | 必须写 `self.` |

---

## 📝 第 1 小时练习（10 分钟）

### 练习：动态学生数组

**要求**：
1. 用 Day1 中的 Student 类（name, score）
2. 用户先输入学生数量 n
3. 用 `new` 创建 n 个 Student 的数组
4. 逐个输入姓名和成绩
5. 输出所有学生信息并计算平均分
6. 用 `delete[]` 释放内存

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Student {
private:
    string name;
    int score;
public:
    Student() {}  // 默认构造函数（new 数组需要）
    
    void input() {
        cout << "姓名: ";
        cin >> name;
        cout << "成绩: ";
        cin >> score;
    }
    
    void print() {
        cout << name << ": " << score << "分" << endl;
    }
    
    int getScore() { return score; }
};

int main() {
    int n;
    cout << "请输入学生数量: ";
    cin >> n;
    
    Student* students = new Student[n];  // 堆上创建数组
    
    for (int i = 0; i < n; i++) {
        cout << "学生 " << (i + 1) << " - ";
        students[i].input();
    }
    
    cout << "\n===== 成绩单 =====" << endl;
    int sum = 0;
    for (int i = 0; i < n; i++) {
        students[i].print();
        sum += students[i].getScore();
    }
    cout << "平均分: " << (double)sum / n << endl;
    
    delete[] students;  // 释放！
    return 0;
}
```

</details>

---

# 🕑 第 2 小时：析构函数与拷贝控制（60 分钟）

## 2.1 析构函数（Destructor）（15 分钟）

### 📝 这是什么？

析构函数在对象**生命周期结束时**自动调用，用于清理资源（释放内存、关闭文件等）。

```cpp
class FileWriter {
private:
    ofstream* file;  // 文件流指针
    string filename;
    
public:
    // 构造函数：打开文件
    FileWriter(const string& fname) : filename(fname) {
        file = new ofstream(fname);
        if (!file->is_open()) {
            cout << "文件 " << filename << " 打开失败！" << endl;
        } else {
            cout << "文件 " << filename << " 已打开" << endl;
        }
    }
    
    void write(const string& content) {
        *file << content << endl;
    }
    
    // 析构函数：关闭文件，释放资源
    // 写法：~类名()，无参数，无返回值
    ~FileWriter() {
        if (file) {
            file->close();
            delete file;        // 释放 new 出来的文件对象
            file = nullptr;
            cout << "文件 " << filename << " 已关闭并释放" << endl;
        }
    }
};

int main() {
    {
        FileWriter fw("test.txt");  // 构造：打开文件
        fw.write("Hello, C++!");
        fw.write("这是第二行");
    }  // fw 离开作用域 → 析构函数自动调用 → 文件自动关闭！
    
    cout << "fw 已经被销毁，文件已安全关闭" << endl;
    return 0;
}
```

### 🔍 析构函数的三个关键点

1. **语法**：`~ClassName()`，无参数，无返回值
2. **自动调用**：栈对象离开作用域自动调用 / `delete` 堆对象时调用
3. **不可重载**：每个类只有一个析构函数

### 💡 和 Python 对比

| C++ | Python |
|-----|--------|
| `~ClassName()` | `__del__(self)` |
| 确定性调用（离开作用域 / delete） | 非确定性（GC 回收时，不确定何时） |
| 常用来释放资源 | 不常用（因为 GC） |

### ⚠️ 什么时候必须写析构函数？

当你的类在构造函数中 `new` 了资源（内存、文件、网络连接等），就必须写析构函数去释放它们。否则 → **内存泄漏**！

---

## 2.2 拷贝构造函数（Copy Constructor）（20 分钟）

### 📝 什么是拷贝？什么时候发生拷贝？

```cpp
Person p1("小明", 20);   // 普通构造
Person p2 = p1;          // 拷贝构造！用 p1 创建 p2
Person p3(p1);           // 也是拷贝构造
```

### 🔥 核心问题：浅拷贝 vs 深拷贝（面试必考！）

**默认拷贝是浅拷贝**（逐成员复制），对于指针成员，只复制指针本身，不复制指向的内容！

```cpp
class ShallowCopy {
public:
    int* data;
    
    ShallowCopy(int value) {
        data = new int(value);  // 堆上分配
    }
    
    ~ShallowCopy() {
        delete data;  // 释放内存
    }
    // 没有自定义拷贝构造 → 编译器生成默认拷贝（浅拷贝）
};

int main() {
    ShallowCopy obj1(42);
    ShallowCopy obj2 = obj1;  // 浅拷贝！obj2.data 和 obj1.data 指向同一块内存！
    
    // obj1 和 obj2 都指向同一块内存
    // 当它们被销毁时，同一块内存被 delete 两次 → 💥 崩溃！
    return 0;
}
```

### 💡 深拷贝：创建自己的拷贝构造函数

```cpp
class DeepCopy {
public:
    int* data;
    
    DeepCopy(int value) {
        data = new int(value);
        cout << "构造: *data = " << *data << endl;
    }
    
    // 拷贝构造函数：深拷贝！
    DeepCopy(const DeepCopy& other) {
        data = new int(*other.data);  // 分配新内存，复制值
        cout << "拷贝构造: *data = " << *data << endl;
    }
    
    ~DeepCopy() {
        cout << "析构: *data = " << *data << endl;
        delete data;
    }
};

int main() {
    DeepCopy obj1(42);
    DeepCopy obj2 = obj1;  // 深拷贝：obj2.data 指向全新的内存
    
    *obj2.data = 100;      // 只修改 obj2，不影响 obj1
    
    cout << "obj1.data = " << *obj1.data << endl;  // 42
    cout << "obj2.data = " << *obj2.data << endl;  // 100
    
    return 0;  // 两个对象各自释放自己的内存，安全！
}
```

### 🔍 拷贝构造函数语法

```cpp
ClassName(const ClassName& other);  // 必须传 const 引用
```

**为什么必须是引用？** 如果传值，会触发另一个拷贝构造 → 无限递归！

### 📝 拷贝发生的三种情况

```cpp
// 1. 直接初始化
Person p2 = p1;

// 2. 函数传参（传值）
void func(Person p) { ... }  // p 是拷贝出来的
func(p1);  // 触发拷贝构造

// 3. 函数返回（返回值优化前）
Person createPerson() {
    Person p("tmp", 0);
    return p;  // 可能触发拷贝（现代编译器有 RVO 优化，不一定触发）
}
```

---

## 2.3 赋值运算符（Assignment Operator）（10 分钟）

### 📝 拷贝构造 vs 赋值

```cpp
Person p1("小明", 20);
Person p2 = p1;   // 拷贝构造：创建新对象时
Person p3("xxx", 0);
p3 = p1;          // 赋值运算符：两个对象都已经存在
```

### 自定义赋值运算符

```cpp
class DeepCopy {
public:
    int* data;
    
    DeepCopy(int value) {
        data = new int(value);
    }
    
    // 拷贝构造
    DeepCopy(const DeepCopy& other) {
        data = new int(*other.data);
    }
    
    // 赋值运算符
    DeepCopy& operator=(const DeepCopy& other) {
        if (this == &other) {       // 防止自赋值
            return *this;
        }
        delete data;                // 先释放旧资源
        data = new int(*other.data);  // 再分配新资源并复制
        return *this;               // 返回 *this 支持连续赋值
    }
    
    ~DeepCopy() {
        delete data;
    }
};

int main() {
    DeepCopy obj1(42);
    DeepCopy obj2(100);
    obj2 = obj1;  // 赋值
    return 0;
}
```

---

## 2.4 Rule of Three（三法则）（5 分钟）

### 🔥 面试必考：Rule of Three 是什么？

> **如果你需要自定义析构函数、拷贝构造函数、赋值运算符中的任何一个，那么你很可能需要全部三个。**

```cpp
class MyClass {
public:
    ~MyClass();                          // 1. 析构函数
    MyClass(const MyClass&);             // 2. 拷贝构造函数
    MyClass& operator=(const MyClass&);  // 3. 赋值运算符
};
```

**原因**：三个函数都涉及资源管理。你需要析构函数 → 说明你有自己管理的资源 → 默认拷贝会导致浅拷贝 → 需要自定义拷贝构造和赋值运算符。

> 💡 C++11 后又扩展为 **Rule of Five**（加上移动构造和移动赋值），明天 Day 3 会讲。

---

## 📝 第 2 小时练习（10 分钟）

### 练习：实现 String 类的深拷贝

**要求**：
1. 实现一个简单的 `MyString` 类
2. 构造函数接受 `const char*`
3. 实现析构函数（释放内存）
4. 实现拷贝构造函数（深拷贝）
5. 实现赋值运算符
6. 在 main 中测试拷贝和赋值

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <cstring>
using namespace std;

class MyString {
private:
    char* str;
    size_t len;
    
public:
    // 构造函数
    MyString(const char* s = "") {
        len = strlen(s);
        str = new char[len + 1];
        strcpy(str, s);
    }
    
    // 拷贝构造（深拷贝）
    MyString(const MyString& other) {
        len = other.len;
        str = new char[len + 1];
        strcpy(str, other.str);
        cout << "拷贝构造被调用" << endl;
    }
    
    // 赋值运算符
    MyString& operator=(const MyString& other) {
        if (this == &other) return *this;  // 防止自赋值
        delete[] str;                       // 释放旧内存
        len = other.len;
        str = new char[len + 1];
        strcpy(str, other.str);
        cout << "赋值运算符被调用" << endl;
        return *this;
    }
    
    // 析构函数
    ~MyString() {
        delete[] str;
    }
    
    void print() const {
        cout << str << endl;
    }
};

int main() {
    MyString s1("Hello");
    MyString s2 = s1;    // 拷贝构造
    MyString s3("World");
    s3 = s1;             // 赋值运算符
    
    s1.print();
    s2.print();
    s3.print();
    return 0;
}
```

</details>

---

# 🕒 第 3 小时：继承与多态（60 分钟）

## 3.1 继承（Inheritance）（15 分钟）

### 📝 这是什么？

继承让你基于现有类创建新类，复用代码。

```cpp
// 基类（父类）
class Animal {
protected:          // protected：子类可访问，外部不可访问
    string name;
    
public:
    Animal(const string& n) : name(n) {}
    
    void eat() {
        cout << name << " 在吃东西" << endl;
    }
};

// 派生类（子类）：class 子类 : public 父类
class Dog : public Animal {
public:
    Dog(const string& n) : Animal(n) {}  // 调用父类构造函数
    
    void bark() {
        cout << name << " 汪汪叫！" << endl;
    }
};

int main() {
    Dog dog("旺财");
    dog.eat();   // 继承自 Animal
    dog.bark();  // Dog 自己的方法
    return 0;
}
```

### 🔍 访问控制

| 基类成员 | public 继承 | protected 继承 | private 继承 |
|----------|------------|---------------|-------------|
| `public:` | public | protected | private |
| `protected:` | protected | protected | private |
| `private:` | 不可访问 | 不可访问 | 不可访问 |

> **90% 的情况用 `public` 继承就行。**

---

## 3.2 多态与虚函数（Polymorphism & Virtual）（25 分钟）

### 🔥 面试必考：什么是多态？为什么需要虚函数？

**多态**：同一个接口，不同对象有不同的行为。

### 问题：没有虚函数时

```cpp
class Animal {
public:
    void speak() {
        cout << "动物叫了一声" << endl;
    }
};

class Dog : public Animal {
public:
    void speak() {
        cout << "汪汪！" << endl;
    }
};

int main() {
    Animal* ptr;
    Dog dog;
    ptr = &dog;
    
    ptr->speak();  // 输出：动物叫了一声  ← 不对！明明指向 Dog！
    // 这是因为没有声明虚函数，编译器根据指针的静态类型（Animal）调用
    
    return 0;
}
```

### 💡 解决办法：虚函数 `virtual`

```cpp
class Animal {
public:
    virtual void speak() {     // ← 加上 virtual！
        cout << "动物叫了一声" << endl;
    }
    virtual ~Animal() {}       // 基类析构函数必须也是 virtual！
};                             // 否则 delete 基类指针时不会调子类析构函数！

class Dog : public Animal {
public:
    void speak() override {    // ← override 关键字（C++11），编译器会检查是否真的重写了
        cout << "汪汪！" << endl;
    }
};

class Cat : public Animal {
public:
    void speak() override {
        cout << "喵喵！" << endl;
    }
};

int main() {
    Animal* animals[2];
    animals[0] = new Dog();
    animals[1] = new Cat();
    
    for (int i = 0; i < 2; i++) {
        animals[i]->speak();  // 输出：汪汪！  喵喵！
        delete animals[i];    // 正确调用各自的析构函数（因为 ~Animal 是 virtual）
    }
    // 汪汪！
    // 喵喵！
    
    return 0;
}
```

### 🔍 虚函数原理（面试必问）

每个有虚函数的类都有一个**虚函数表（vtable）**，对象里有一个**虚指针（vptr）**指向它：

```
Animal 对象：
┌──────────┐
│  vptr    │──→ Animal vtable ┌──────────────┐
│  name    │                  │ &Animal::speak │
└──────────┘                  └──────────────┘

Dog 对象：
┌──────────┐
│  vptr    │──→ Dog vtable ┌──────────────┐
│  name    │               │ &Dog::speak   │
└──────────┘               └──────────────┘
```

调用 `ptr->speak()` 时，程序通过 `vptr` → `vtable` 找到实际的函数地址 → **运行时多态**！

### 🔥 纯虚函数和抽象类

```cpp
class Animal {  // 抽象类（不能直接创建对象）
public:
    virtual void speak() = 0;  // 纯虚函数（= 0）
    virtual ~Animal() {}
};

class Dog : public Animal {
public:
    void speak() override {
        cout << "汪汪！" << endl;
    }
};

int main() {
    // Animal a;  ❌ 编译错误！抽象类不能实例化
    Animal* ptr = new Dog();  // ✅ 可以通过指针/引用使用
    ptr->speak();
    delete ptr;
    return 0;
}
```

### 💡 和 Python 对比

```python
# Python 抽象类
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass
```

```cpp
// C++ 抽象类
class Animal {
public:
    virtual void speak() = 0;  // 纯虚函数
};
```

---

## 3.3 智能指针初探（15 分钟）

### 📝 为什么要智能指针？

手动 `new`/`delete` 太容易出错了（忘记 delete、异常导致跳过 delete、重复 delete）。

**C++11 引入了智能指针**，自动管理内存：

```cpp
#include <memory>  // 智能指针头文件

// unique_ptr：独占所有权（不能拷贝，只能移动）
void uniquePtrDemo() {
    unique_ptr<int> p1 = make_unique<int>(42);  // C++14 推荐写法
    // unique_ptr<int> p2 = p1;  ❌ 编译错误！不能拷贝
    unique_ptr<int> p2 = move(p1);  // ✅ 可以移动，移动后 p1 = nullptr
    
    cout << *p2 << endl;  // 42
    // 离开作用域自动 delete！
}

// shared_ptr：共享所有权（引用计数）
void sharedPtrDemo() {
    shared_ptr<int> sp1 = make_shared<int>(100);
    {
        shared_ptr<int> sp2 = sp1;  // 引用计数 +1
        cout << "引用计数: " << sp1.use_count() << endl;  // 2
    }  // sp2 离开作用域，引用计数 -1
    cout << "引用计数: " << sp1.use_count() << endl;  // 1
    // 引用计数为 0 时才 delete
}
```

### 🔍 三种智能指针速查

| 智能指针 | 特点 | 使用场景 |
|----------|------|----------|
| `unique_ptr` | 独占，不能拷贝，可移动 | 默认首选，单一所有者 |
| `shared_ptr` | 共享，引用计数 | 多个所有者 |
| `weak_ptr` | 不增加引用计数 | 避免循环引用（观察者） |

### 📝 实际例子：代替原始指针

```cpp
#include <iostream>
#include <memory>
#include <vector>
using namespace std;

class Student {
private:
    string name;
    int score;
public:
    Student(const string& n, int s) : name(n), score(s) {}
    void print() const {
        cout << name << ": " << score << "分" << endl;
    }
};

int main() {
    // 旧写法：手动管理内存（容易出错）
    vector<Student*> oldStudents;
    oldStudents.push_back(new Student("张三", 85));
    oldStudents.push_back(new Student("李四", 92));
    // ... 如果中间抛异常，内存泄漏！
    for (auto* s : oldStudents) delete s;  // 手动释放，可能漏掉

    // 新写法：智能指针自动管理
    vector<unique_ptr<Student>> students;
    students.push_back(make_unique<Student>("张三", 85));
    students.push_back(make_unique<Student>("李四", 92));
    
    for (const auto& s : students) {
        s->print();
    }
    // 离开作用域自动释放！不用手动 delete！
    
    return 0;
}
```

> **现代 C++ 原则**：尽量不用裸 `new`/`delete`，用智能指针！

---

## 📝 第 3 小时练习：动物园系统（15 分钟）

### 📝 要求

综合运用继承、多态，创建一个动物园系统：

1. 抽象基类 `Animal`，有纯虚函数 `speak()` 和 `getType()`
2. 派生类 `Dog`、`Cat`、`Cow`，各自实现 `speak()`
3. 用 `vector<unique_ptr<Animal>>` 存储动物
4. 遍历所有动物并让它们说话

<details>
<summary>✅ 点击查看答案</summary>

```cpp
#include <iostream>
#include <vector>
#include <memory>
using namespace std;

// 抽象基类
class Animal {
public:
    virtual void speak() const = 0;       // 纯虚函数
    virtual string getType() const = 0;   // 纯虚函数
    virtual ~Animal() = default;          // 虚析构（default 表示用编译器默认生成的）
};

// Dog 类
class Dog : public Animal {
public:
    void speak() const override {
        cout << "🐶 汪汪！汪汪汪！" << endl;
    }
    string getType() const override {
        return "狗";
    }
};

// Cat 类
class Cat : public Animal {
public:
    void speak() const override {
        cout << "🐱 喵喵～" << endl;
    }
    string getType() const override {
        return "猫";
    }
};

// Cow 类
class Cow : public Animal {
public:
    void speak() const override {
        cout << "🐄 哞～～" << endl;
    }
    string getType() const override {
        return "牛";
    }
};

int main() {
    vector<unique_ptr<Animal>> zoo;
    
    // 添加动物
    zoo.push_back(make_unique<Dog>());
    zoo.push_back(make_unique<Cat>());
    zoo.push_back(make_unique<Cow>());
    zoo.push_back(make_unique<Dog>());
    
    // 让所有动物说话
    cout << "===== 🎪 动物园表演时间 =====" << endl;
    for (const auto& animal : zoo) {
        cout << animal->getType() << ": ";
        animal->speak();
    }
    
    cout << "\n===== 表演结束，动物们回家 =====" << endl;
    // 自动清理，无需手动 delete！
    
    return 0;
}
```

</details>

---

## 🎯 Day 2 总结

| 你学到的 | 重要性 |
|----------|--------|
| `new`/`delete` vs `malloc`/`free` | ⭐⭐⭐⭐⭐ |
| `nullptr` | ⭐⭐⭐ |
| `this` 指针 | ⭐⭐⭐⭐ |
| 析构函数 `~ClassName()` | ⭐⭐⭐⭐⭐ |
| 浅拷贝 vs 深拷贝 | ⭐⭐⭐⭐⭐ |
| 拷贝构造 / 赋值运算符 | ⭐⭐⭐⭐⭐ |
| Rule of Three | ⭐⭐⭐⭐⭐ |
| 继承 `class A : public B` | ⭐⭐⭐⭐⭐ |
| 虚函数 `virtual` / `override` | ⭐⭐⭐⭐⭐ |
| 纯虚函数 `= 0` / 抽象类 | ⭐⭐⭐⭐ |
| `unique_ptr` / `shared_ptr` | ⭐⭐⭐⭐⭐ |

---

## 📚 课后任务

1. **实现完整的 MyString 类**：加上 `length()`、`c_str()`、`operator==` 等方法
2. **扩展动物园**：增加更多动物类型，添加 `feed()` 虚函数
3. **练习智能指针**：把你 Day 1 写的代码中的裸指针替换为智能指针
4. **思考题**：为什么基类的析构函数必须是 `virtual`？如果不写会怎样？

---

> 🎉 **Day 2 完成！你现在已经掌握了 C++ 的核心面向对象机制！**  
> 明天 Day 3 我们将学习：移动语义（Move）、模板（Template）、运算符重载、Lambda 表达式等现代 C++ 特性。  
> 今天的内容比较硬核（特别是拷贝控制和多态），建议多敲代码加深理解！明天见～