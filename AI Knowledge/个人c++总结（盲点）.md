- cpp 要包含的头文件是 iostream  不是stdio
- std::cout  写法是std：： 后面接上函数名称，就可以调用
- 使用 using namespace std  可以省略std：：
- cout可以链式调用  cout<<name << age
- `cin >>` 读取字符串时遇到空格会停止。如果要读取一行带空格的文字：getline(cin, name);  
- auto关键字可以再变量定义的时候使用，自适应是整型 浮点或者字符串类型，auto age = 19；
- cin>>a,b 等价于(cin >> a), b;  正确写法应该是cin>>a>>b
- [ ] void setZero(int a, int b)  setZero(x, y); 函数里修改的是副本，原变量 `x`/`y` 不变
      void setZero(int& a, int& b) setZero(x, y); 函数里修改的是原变量的别名，`x`/`y` 会被修改
- [ ] CPP允许同名函数，只要函数里面参数量或者参数类型不同即可，运行时编译器会自适应的进行匹配。
- 类 private只能在类的内部访问，public可以在外部访问。
- [ ] vector  需要先包含头文件，vector<int>a; 创建整型a，此刻是空向量，a[1]=1；这是错的，属于越界访问。应该用a.push_back(1);pushback只支持函数来调用。
-  [ ]  // 范围 for（C++11 新特性）
    for (int x : v) {      // 读作：对于 v 中的每个元素 x
        cout << x << " ";
    }  这个有点类似于python的for循环 for x in list：
									 print x
- [ ]  文件写入操作方式
      - 首先需要包含头文件  fstream
      - ofstream  test1（”test.txt“）  这里相当于用test1代表了和test.txt的链接通道
      - if（！test1）即可用来判断test.txt文件是否被打开了
      - 接下来在文件中写内容跟cout用法相似，test <<"first line"<<endl; 注意这里是用链接通道test代替的cout。
- [ ]  读文件操作
      ```cpp   
      用ifstream关键字来链接读文件操作    ifstream test("test.txt")
      getline（test，a）即可把读取到的字符串信息放到a里面。
