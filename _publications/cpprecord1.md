---
title: "C++ Fundation: Annotation, I/OS, Variables and Data Types"
collection: publications
permalink: /cpp/record1
excerpt: 'This is the 1st record of my C++ study.'
date: 2023-05-08
venue: 'May 8'
---
<!-- paperurl: 'http://academicpages.github.io/files/paper1.pdf' -->
<!-- citation: 'Your Name, You. (2009). &quot;Paper Title Number 1.&quot; <i>Journal 1</i>. 1(1).'-->

### Code notes:
```cpp
#include <iostream>
using namespace std;
#include <string>

/* [3]常量2种定义方法
 * 3.1 #define 宏常量
 * 3.2 const修饰的变量
 */
#define Day 7 // 3.1, 预处理语句后 不加 ；不加 ；不加 ；

int main() {
    std::cout << "hello, world" << endl;// [1]single line 
/* 
 * [1]multiple line
 *
 * [2]变量： 方便管理内存空间
 * [2]创建于法： 数据类型 变量名称 = 初始值；
 * 
 */
    int a = 10;
    std::cout << a << endl;
    std::cout << Day << endl; // 3.1
    const int month = 12; // 3.2
    std::cout << month << endl; // 3.2

/* -------------------------------------------------------
 * ----------------------- 数据类型 -----------------------
 * -------------------------------------------------------
 * 
 * [4]整形
 * 4.1 short 2 bytes -> (-2^15,2^15-1) = (-32768,32767)
 * 4.2 int 4 bytes
 * 4.3 long 4 bytes at Windows 8 at Linux 2^31
 * 4.4 long long 8 bytes 2^63
 * 
 * [5] sizeof(数据类型/变量) 
 */
    std::cout << sizeof(short) << endl; // 4.1
    std::cout << sizeof(int) << endl; // 4.2
    std::cout << sizeof(long) << endl; // 4.3
    std::cout << sizeof(long long) << endl; // 4.4
    
/* [6]浮点型
 * 6.1 单精度 float 4 bytes 7位有效数字
 * 6.2 双精度 double  8 bytes 15～16位有效数字
 * 默认情况输出6位有效数字
 */
    float pi = 3.14f; // 6.1, 后加'f',否则默认双精度
    double pii = 3.1415; // 6.2
    std::cout << pi << ", 更精确：" << pii << endl; 
    std::cout << sizeof(float) << endl; 
    std::cout << sizeof(double) << endl; 

    // 科学计数法
    float test = 3e2;
    float minTest = 3e-2;
    std::cout << test << endl; 
    std::cout << minTest << endl; 

/* [7]字符型
 *    储蓄ASCII编码
 */
    char charTest_a = 'a'; // 只能用单引号
    char charTest_A = 'A'; // 只能输入一位字符
    std::cout << charTest_a << endl; 
    std::cout << charTest_A << endl; 
    std::cout << int(charTest_a) << endl; // ASCII编码唯一 a: 97
    std::cout << int(charTest_A) << endl; // A: 65
    std::cout << sizeof(char) << endl; // 占位 1 byte
    char charTest_d = 100;
    std::cout << charTest_d << endl; // 可以直接用ASCII编码给字符型变量赋值

/* [8]转义字符： 不能显示出来的ASCII字符
 *      \n 换行
 *      \t 水平制表
 *      \v 垂直制表
 *      \\ \
 *      \a 警报
 *      \b 退格
 *      \f 换页
 *      \r 回车
 */

/* [9]字符串型
 * 9.1 C 风格
 * 9.2 C++ 风格
 */

    char str_1[] = "C风格字符串"; // 9.1 a. 加[]; b. 要用双引号
    string str_2 = "C++风格字符串"; // 9.2 需要 #include <string>
    std::cout << str_1 << endl; // 9.1
    std::cout << str_2 << endl; // 9.2
    std::cout << sizeof(str_1) << endl; // 24 bytes
    std::cout << sizeof(string) << endl; // 24 bytes

/* [10]bool
 */
    bool flag = true;
    bool flag1 = false;
    std::cout << flag << endl; // true = 1
    std::cout << flag1 << endl; // flase = 0
    std::cout << sizeof(bool) << endl; // 1 bytes

/* [11]数据的输入
 * 语法：cin >>
 */

// 11.1 输入整型
    int int_a = 0;
    cout << "请给a赋值:" << endl;
    cin >> int_a;
    cout << "int_a的值为:" << int_a << endl;
    
    return 0;
} 
```

### [Course Video - 【黑马程序员匠心之作|C++教程从0到1入门编程,学习编程不再难】(1~15/314)](https://www.bilibili.com/video/BV1et411b73Z/?p=15&share_source=copy_web&vd_source=a50a021a72570cf19f8159ff96b36111)

<!-- Recommended citation: Your Name, You. (2009). "Paper Title Number 1." <i>Journal 1</i>. 1(1). -->
