---
internallayout: post
title: 学习OOP之前
date: 2017-12-02
categories: blog
tags: [programming,c++]
description:学习OOP之前（c++）
---
# keyword break and continue
   两者均用来跳过循环体中的语句执行，在细节也很容易搞懂，break用来跳出整个循环体（只有里break最近的一层），continue用来跳过一次循环中的剩下的语句，跳转到下一次循环的条件判断。
```c++
for(int i=0;i<9;i++){
  
  if(i>5){
    cout<<"i>5";
    break;//当i>5时，输出字符串一次，然后跳出循环，执行循环之后的语句
    }
  else{
    continue;//当i<=5时，会跳过下面的语句，跳到下次循环的开始
  }
  cout<<"i <= 5";
}
········
```

# scope and storage duration, linkage 

   一个变量根据其声明的位置和方式，具有不同的scope（作用域）和storage duration（存储时间）

| storages                     | storage   | duration | scope   | linkage          | declaration                              |
| :--------------------------- | :-------- | :------- | :------ | ---------------- | ---------------------------------------- |
| automatic                    | automatic | block    | block   | none             | in a block                               |
| static with no linkage       | static    | block    | block   | no linkage       | within a function                        |
| static with internal linkage | static    | file     | file    | internal linkage | out of all functions and using keyword static |
| static with external linkage | static    | file     | project | external linkage | out of all functions                     |

全局与局部其实就是scope是file还是block的区别，其他的情况（除了register）都在表里列出。
## using declaration and directive 
using declaration，正如其名是声明，namespace里的各种名称都有block的scope，在不同的block中可以被hide。
```c++
namespace john{
  int x;
  int j;
  char w;
}
using namespace john;
int x;//正确 隐藏了namespace里的x
```
using dirctive  可以说是对namespace中的声明拿到调用的位置。
```c++
namespace john{
  int x;
  int j;
  char w;
}
using john::x;
int x;//错误，本地已经有一个int x存在
```
未完待续。
