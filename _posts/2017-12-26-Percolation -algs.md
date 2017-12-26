---
layout: post
title: algs提交成功的第一个作业
date: 2017-12-26
categories: blog
tags: [language,c++,java,algorithm,coursera,debug]
description: wtf。
---
老爷子给的测试数据真严苛，方法里带个for就通不过timing测试，QWQ 
​    忙活了大半个月终于把algs4的第一周作业搞定了，关键是之前没摸过java，所以浪费了很多时间，好在基本语句长得差不多，就是多了类这些面向对象的概念。
​    除了语言熟悉花的时间，其他的时间其实是比较浪费的。思路大概是看完课程3-4天就完全了，调试bug调了大半个星期，不过终于也有了些经验上的收获。敲字也更快了（误
##debug
​    debug的过程还是CS50刚开始的那一套，不断给自己提问题，不断输入边角数据进行测试，查看每一步变量的变化，逐步缩小范围，找到bug，修正。但我每次都不能够逻辑严密地思考，总是一团乱遭。举例子来说，在这次作业里Percolation 有一个isopen方法和open方法：
 ```java
 public    void open(int row, int col) {
			   if(isOpen(row,col))
				   opensites--;
			   if(row<=0||row>size||col<=0||col>size) {
 				   throw new java.lang.IllegalArgumentException();
			   }
			      sites[col+(row-1)*size]=true;
			      
			      opensites++;
			      if(col>1 && isOpen(row,col-1)) {
			    	  uf.union(trans(row,col-1),trans(row,col));
			      }
			      if(row>1 && isOpen(row-1,col)) {
			    	 uf.union(trans(row-1,col),trans(row,col)); 
			      }
			      if(row<size && isOpen(row+1,col)) {
			    	  uf.union(trans(row+1,col),trans(row,col));
			      }
			      if(col<size && isOpen(row,col+1)) {
			    	  uf.union(trans(row,col+1),trans(row,col));
			      }
			      if(row==1) {
			    	  uf.union(trans(row,col), 0);
			      }
			      if(row==size) {
			    	  uf.union(trans(row,col), size*size+1);
			      }
}
public boolean isOpen(int row, int col) {
			   if(row<=0||col<=0||row>size||col>size){				  
				   throw new java.lang.IllegalArgumentException(); 
			   }                   
				return sites[trans(row,col)];
		   }// is site (row, col) open?
 ```

​    刚开始的时候，open里的if条件是

```
if(isOpen(row-1,col)&&row>1)
```

一测试就狂抛异常，到最后终于找到了是参数传着传着就改变了的原因，不是加1就是减一，而且只有当参数等于1或等于size的时候改变。明明能对row col改变的方法只有open里的那一堆if们，居然费了我一个小时才找到bug在哪。

 总结下这次作业的经验吧

- 要注意 条件判断的先后 如果条件中涉及参数传递的 确定要传的参数在范围内  

- 尽量把常用的运算用个方法包起来，更可读，也有利于debug

- 测试数据要尽量多，完整。在造数据，造读数据方法 多花一点时间，debug就少花一堆时间。

- 实在理不清顺序时，一步一步 写下来过程

  作业代码存在库里了https://github.com/stdxfs/algs-

