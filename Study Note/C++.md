# C++
### const修饰
##### const修饰函数参数
1. const只修饰输入参数。修饰输出参数则失去输出功能，const修饰为了保护输入参数不被修改，比如：
```C++
void CopyString(char *p_target, const char *p_source)
```
const修饰p_source，如果函数体内试图修改p_source的内容，则编译器会指出错误。

2. const只修饰"引用传递"的参数。
若使用"值传递"，函数会自动产生临时变量来复制该参数，本就无须保护，比如不要写以下代码：
```C++
void function(int x) --> void function(const int x) //错误
void function(AAA a) --> void function(const AAA a) //错误
```
可以写成：提高效率，保护输入参数a
```C++
void function(AAA a) --> void function(const AAA &a) //正确
```
这时候再解释一下"引用传递"的作用：一是想使用同一个变量，仅改一下别名；二是，对于非内部类型的变量而言，"值传递"一次需要有构造、赋值、析构的操作，这对性能都有一点的消耗，所有使用"引用传递加速"。但对于内部类型无此消耗，所以不要写以下代码：不能提高效率、const修饰使其不能修改达不到修改同一变量的目标、理解性下降。
```C++
void function(int a) --> void function(const int &a) //错误
```
3. 总结：const修饰需要保护的输入参数：
对非内部类型变量："值传递"->"const引用传递"。
对内部类型变量：const和引用不要一起用。

##### const修饰函数的返回值
##### const修饰成员函数