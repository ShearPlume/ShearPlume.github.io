---
title: 10.24 S&N course
date: 2022-11-06 18:37:22
tags:
- S&N
- course
---

## 控制结构



### HLL中的控制结构如何转换为汇编？

#### goto：

JUMP指令：相当于HLL里的goto语句

![image-20221106184601249](10-24-S-N-course/image-20221106184601249.png)

JUMP里的label不是对变量而是表示语句

JUMPT和JUMPF指令进行条件跳转。要做到这一点，它们需要一个额外的操作数，这个操作数被保存在一个选定的寄存器中。一般和比较类指令同用（if() goto）

##### 例子：if(x=y) then goto L1

![image-20221106190419292](10-24-S-N-course/image-20221106190419292.png)

#### 死循环：

HLL:

`while(true){statements}`

汇编方法：无条件JUMP

![image-20221106190739123](10-24-S-N-course/image-20221106190739123.png)

#### if()then:

HLL：

![image-20221106190903699](10-24-S-N-course/image-20221106190903699.png)

汇编方法：

![image-20221106191202286](10-24-S-N-course/image-20221106191202286.png)

语句2无论如何会被执行

#### ifelse:

HLL:

![image-20221106195847415](10-24-S-N-course/image-20221106195847415.png)

![image-20221106200139607](10-24-S-N-course/image-20221106200139607.png)

汇编方法：（短路结构）

![image-20221106195904975](10-24-S-N-course/image-20221106195904975.png)

![image-20221106200155466](10-24-S-N-course/image-20221106200155466.png)

#### While 和for循环

HLL:

![image-20221107014643792](10-24-S-N-course/image-20221107014643792.png)![image-20221107015003773](10-24-S-N-course/image-20221107015003773.png)

先转换为goto：

![image-20221107014909829](10-24-S-N-course/image-20221107014909829.png)![image-20221107015032966](10-24-S-N-course/image-20221107015032966.png)

#### 练习：

![image-20221107015217483](10-24-S-N-course/image-20221107015217483.png)
